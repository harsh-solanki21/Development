# File System

```node
const fs = require("fs");

fs.stat("/Users/joe/test.txt", (err, stats) => {
  if (err) {
    console.error(err);
    return;
  }

  stats.isFile(); // true
  stats.isDirectory(); // false
  stats.isSymbolicLink(); // false
  stats.size; // 1024000 //= 1MB
});
```

<br />

## File descriptors

- Before you're able to interact with a file that sits in your filesystem, you must get a file descriptor.
- A file descriptor is a reference to an open file, a number (fd) returned by opening the file using the open() method offered by the fs module. This number (fd) uniquely identifies an open file in operating system:

```node
const fs = require("fs");
fs.open("/Users/joe/test.txt", "r", (err, fd) => {
  // fd is our file descriptor
});
```

<br />

- You can also open the file by using the fs.openSync method, which returns the file descriptor, instead of providing it in a callback:

```node
const fs = require("fs");
try {
  const fd = fs.openSync("/Users/joe/test.txt", "r");
} catch (err) {
  console.error(err);
}
```

<br />

- You can also open the file by using the promise-based fsPromises.open method offered by the fs/promises module.

```node
const fs = require("fs/promises");
async function example() {
  let filehandle;
  try {
    filehandle = await fs.open("/Users/joe/test.txt", "r");
    console.log(filehandle.fd);
    console.log(await filehandle.readFile({ encoding: "utf8" }));
  } finally {
    if (filehandle) await filehandle.close();
  }
}
example();
```

<br />

## Reading files

- The simplest way to read a file in Node.js is to use the fs.readFile() method, passing it the file path, encoding and a callback function that will be called with the file data (and the error):

```node
// Asynchronous Way
const fs = require("fs");
fs.readFile("/Users/joe/test.txt", "utf8", (err, data) => {
  if (err) {
    console.error(err);
    return;
  }
  console.log(data);
});

// Synchronous Way
const fs = require("fs");
try {
  const data = fs.readFileSync("/Users/joe/test.txt", "utf8");
  console.log(data);
} catch (err) {
  console.error(err);
}

// You can also use the promise-based fsPromises.readFile() method offered by the fs/promises module:
const fs = require("fs/promises");
async function example() {
  try {
    const data = await fs.readFile("/Users/joe/test.txt", { encoding: "utf8" });
    console.log(data);
  } catch (err) {
    console.log(err);
  }
}
example();

// OR

const fs = require("fs/promises");
let data = fs.readFile("file.txt", "utf-8");
data.then((data) => {
  console.log(data);
});
```

<br />

- All three of `fs.readFile()`, `fs.readFileSync()` and `fsPromises.readFile()` read the full content of the file in memory before returning the data.
- This means that big files are going to have a major impact on your memory consumption and speed of execution of the program.
- In this case, a better option is to read the file content using `streams`.

<br />

## Writing files

- The easiest way to write to files in Node.js is to use the fs.writeFile() API.

```node
// Asynchronous Way
const fs = require("fs");
const content = "Some content!";

fs.writeFile("/Users/joe/test.txt", content, (err) => {
  if (err) {
    console.error(err);
  }
  // file written successfully
});

// Synchronous Way
const fs = require("fs");
const content = "Some content!";

try {
  fs.writeFileSync("/Users/joe/test.txt", content);
  // file written successfully
} catch (err) {
  console.error(err);
}

// You can also use the promise-based fsPromises.writeFile() method offered by the fs/promises module:
const fs = require("fs/promises");
async function example() {
  try {
    const content = "Some content!";
    await fs.writeFile("/Users/joe/test.txt", content);
  } catch (err) {
    console.log(err);
  }
}

example();
```

<br />

- A handy method to append content to the end of a file is fs.appendFile() (and its fs.appendFileSync() counterpart):

```node
const fs = require("fs");
const content = "Some content!";

fs.appendFile("file.log", content, (err) => {
  if (err) {
    console.error(err);
  }
  // done!
});

// With Promise
const fs = require("fs/promises");
async function example() {
  try {
    const content = "Some content!";
    await fs.appendFile("/Users/joe/test.txt", content);
  } catch (err) {
    console.log(err);
  }
}
example();

// Deleting files
if (fs.existsSync("./docs/deleteme.txt")) {
  fs.unlink("./docs/deleteme.txt", (err) => {
    if (err) {
      console.log(err);
    }
    console.log("file deleted");
  });
}
```

<br />

## Streams and Buffer

- _Streams_ - Start using data, before it has finished loading

```node
const fs = require("fs");

const readStream = fs.createReadStream("./docs/blog3.txt", {
  encoding: "utf8",
}); //encoding will convert the buffer into the readable stream as the data comes in
const writeStream = fs.createWriteStream("./docs/blog4.txt");

readStream.on("data", (chunk) => {
  // console.log('---- NEW CHUNK ----');
  // console.log(chunk);
  writeStream.write("\nNEW CHUNK:\n");
  writeStream.write(chunk);
});

// piping
readStream.pipe(writeStream);
```

<br />

## Directories

```node
if (!fs.existsSync("./assets")) {
  fs.mkdir("./assets", (err) => {
    if (err) {
      console.log(err);
    }
    console.log("folder created");
  });
} else {
  fs.rmdir("./assets", (err) => {
    if (err) {
      console.log(err);
    }
    console.log("folder deleted");
  });
}
```

<br />

## OS Properties

```node
const os = require('os'); // os is in-built property
console.log(os); // it will return the object of os

// returns the information about the platform and home directory
console.log(os.platform(), os.homedir());
output: win32 c:\Users\Harsh
```
