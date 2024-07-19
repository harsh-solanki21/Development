# MongoDB Aggregation Pipeline

## Introduction

- Aggregation pipelines in MongoDB allow you to group, sort, perform calculations, analyze data, and much more. They consist of one or more stages, with each stage acting upon the results of the previous stage. The order of these stages is important.

**Note:** Aggregation pipelines are slower in execution. Avoid overusing them. If you need aggregation frequently, it may indicate poor database design.

<br />

## Common Aggregation Stages

### $group

- Groups documents by a unique expression.

```node
// Return distinct values from the property_type field
db.listingsAndReviews.aggregate([{ $group: { _id: "$property_type" } }]);

// Group documents by category and sum likes
db.posts.aggregate([
  { $match: { likes: { $gt: 1 } } },
  { $group: { _id: "$category", totalLikes: { $sum: "$likes" } } },
]);
```

### $limit

- Limits the number of documents passed to the next stage.

```node
// Return 1 movie from the collection
db.movies.aggregate([{ $limit: 1 }]);
```

### $project

- Passes only specified fields to the next stage.

```node
db.restaurants.aggregate([
  {
    $project: {
      name: 1,
      cuisine: 1,
      address: 1,
    },
  },
  { $limit: 5 },
]);
```

### $sort

- Sorts documents in the specified order.
- Below example returns the document sorted in descending order by the `accommodates` field.
- 1 is for ascending order sorting.
- -1 is descendingorder sorting.

```node
db.listingsAndReviews.aggregate([
  { $sort: { accommodates: -1 } },
  {
    $project: {
      name: 1,
      accommodates: 1,
    },
  },
  { $limit: 5 },
]);
```

### $match

- Filters documents that match the provided query.

```node
db.listingsAndReviews.aggregate([
  { $match: { property_type: "House" } },
  { $limit: 2 },
  {
    $project: {
      name: 1,
      bedrooms: 1,
      price: 1,
    },
  },
]);
```

### $addFields

- Adds new fields to documents.

```node
db.restaurants.aggregate([
  {
    $addFields: {
      avgGrade: { $avg: "$grades.score" },
    },
  },
  {
    $project: {
      name: 1,
      avgGrade: 1,
    },
  },
  { $limit: 5 },
]);
```

### $count

- Counts the total number of documents from the previous stage.

```node
db.restaurants.aggregate([
  { $match: { cuisine: "Chinese" } },
  { $count: "totalChinese" },
]);
```

### $lookup

- `$lookup`: it performs a left outer join to a collection in the same database
- `from`: The collection to use for lookup in the same database
- `localField`: The field in the primary collection that can be used as a unique identifier in the from collection.
- `foreignField`: The field in the from collection that can be used as a unique identifier in the primary collection.
- `as`: The name of the new field that will contain the matching documents from the from collection.

**Note:** create index on foreignField for faster query processing.

```node
db.comments.aggregate([
  {
    $lookup: {
      from: "movies",
      localField: "movie_id",
      foreignField: "_id",
      as: "movie_details",
    },
  },
  { $limit: 1 },
]);
```

### $out

- Writes the returned documents to a collection.

```node
db.listingsAndReviews.aggregate([
  {
    $group: {
      _id: "$property_type",
      properties: {
        $push: {
          name: "$name",
          accommodates: "$accommodates",
          price: "$price",
        },
      },
    },
  },
  { $out: "properties_by_type" },
]);
```

### $skip

- Skips a specified number of documents.

```node
db.article.aggregate([{ $skip: 5 }]);
```

### $unwind

- Used to deconstruct an array field from the input documents.

```node
db.inventory.insertOne({ _id: 1, item: "ABC1", sizes: ["S", "M", "L"] });
db.inventory.aggregate([{ $unwind: "$sizes" }]);

// Results:
// { "_id" : 1, "item" : "ABC1", "sizes" : "S" }
// { "_id" : 1, "item" : "ABC1", "sizes" : "M" }
// { "_id" : 1, "item" : "ABC1", "sizes" : "L" }

// Example with $group and $count
db.movies.aggregate([
  { $unwind: "$genres" },
  {
    $group: {
      _id: "$genres",
      genreCount: { $count: {} },
    },
  },
  { $sort: { genreCount: -1 } },
]);
```

### Additional Notes

- **Profiler:** You can set up a profiler to collect detailed information about Database Commands executed against a running mongod instance.

- Common Pipeline Optimizations:

  - `$sort + $limit`
  - `$project` as the final stage
  - Hinting: `db.collection.aggregate(pipeline, { hint: 'index_name' })`
