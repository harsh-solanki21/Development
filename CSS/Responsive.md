# Think Responsively

### CSS units:

1. Absolute units - `px`

2. Relative units
   Two types of relative units:

   - Relative to font-size - `em` and `rem`
   - Relative to the viewport - `vw`, `vh`, `vmin`, `vmax`

3. Percentage - `%`
   Percentages are mainly used for widths. They are always relative to their parent.

<br />

- In case of image, we just need to specify the width in %, height will be automatically set to auto.

- `min-width` and `max-width`

<br />

- Relative units are always relative either to a font-size, or the size of the viewport.
- The em and rem are considered relative, because they are relative to the font-size of other elements.

- em are relative to their parent's font-size.
- font-size is an inherited property, so if you don't declare it anywhere, it's getting it from the body (or the default, which is normally 16px)

<br />

- Problem with `em`:
  When we use them for the font-size of an element though, it can create a cascading effect.

- The solution of this problem is using rem instad of em.
  The rem unit is short for root em.
  That means it's always relative to the 'root' of our document.
  The root of an HTML page is always the html element.

**THE USAGE:**

- font-size = rem
- padding and margin = em
- width = em or %

## Media Queries

- **Basic syntax**
  @media media-type and (media-features) { ... }

<br />

- **The media types lets us target different types of media like,**
  Screen - @media screen { ... }
  Print - @media print { ... }
  Speech - @media speech { ... }

<br />

- **The media condition lets us target specific conditions within that media type**
  Widths - @media (min-width: 600px) { ... }
  Orientation - @media (orientation: landscape) { ... }
  Specific features - @media (hover) { ... }

<br />

> **Responsive layout with flex-direction**
> On the desktop scrren size we use flex-direction: row to display content effectively, but when we go desktop screen to phone scrren that same layout become a mess. So in that case, we can do flex-direction: column in the media query to make it effective even on the phone screen.

<br />

## HTML Semantics:

```html
<body>
  <header>
    <nav></nav>
  </header>
  <main>
    <section>
      <article>
        <p></p>
      </article>
      <article>
        <h2></h2>
      </article>
    </section>
    <section>
      <article>
        <h3></h3>
        <p></p>
      </article>
      <article>
        <h3></h3>
        <p></p>
      </article>
    </section>
  </main>
  <footer>
    <p></p>
  </footer>
</body>
```
