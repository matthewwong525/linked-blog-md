By default, an unbreakable string like a very long word, will overflow and extend past the container.
CSS will display overflow in this way to prevent data loss.
Therefore, the default value of overflow is always `visible` so we can see the overflowing text. 

``````col
borderWidth=0
textAlign=start
===
`````col-md
flexGrow=1
===
```html file="html"
<div class="box">
  Llanfairpwllgwyngyllgogerychwyrndrobwllllantysiliogogogoch
</div>
```

```css
.box {
  border: 4px solid #f76707;
  border-radius: 5px;
  padding: 10px;
  inline-size: 150px;
}
```

`````

`````col-md
flexGrow=1
===
<div style="border: 4px solid #f76707; border-radius: 5px; padding: 10px; inline-size: 150px;"> Llanfairpwllgwyngyllgogerychwyrndrobwllllantysiliogogogoch </div>
`````
``````



- `word-break` changes how a word breaks onto the next line
- `white-space`


Setting the container's `width` or `inline-size` to `min-content` will find the minimum size of the box that will contain its content with **no overflows**.

## adding hyphens
To add hyphens when words are broken, use the `hypens` property:

```
.box {
  width: 150px;
  overflow-wrap: break-word;
  hyphens: auto;
}
```
