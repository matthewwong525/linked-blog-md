---
cssclasses: []
---

https://minimal.guide/cards

## Cards
With Minimal you can transform [Dataview](https://minimal.guide/plugins/dataview) tables or bullet lists into cards. To use cards add one of the following [helper class](https://minimal.guide/features/helper-classes) to the `cssclasses` property:

- `cards` to turn all Dataview tables in your note into cards
- `list-cards` to turn all bullet lists in your note into cards


## Progress bars
```html
<progress value="50" max="100"></progress>
```

Dataview query showing progress bar and % number:

```
= "<progress value='" + (length(filter(this.file.tasks.completed, (t) => t = true)) / length(this.file.tasks)) * 100 + "' max='100'></progress>" + "<br>" + round((length(filter(this.file.tasks.completed, (t) => t = true)) / length(this.file.tasks)) * 100) + "% completed"
```

![minimal-progress-bars.png#interface](https://publish-01.obsidian.md/access/342b33803baa5ad0055c9141648edad3/Images/minimal-progress-bars.png)