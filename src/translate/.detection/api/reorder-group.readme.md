# ion-reorder-group

The reorder group is a wrapper component for items with the `ion-reorder` component, Check [Reorder documentation](../reorder/) for further information about the anchor component that is used to drag items within the `ion-reorder-group` list.

Once the user drags an item and drops it in a new position, the `ionItemReorder` event is dispatched. A handler for it must be implemented by the developer to commit changes.

```js
reorderGroup.addEventListener('ionItemReorder', (ev) => {
  console.log(`Moving item from ${ev.detail.from} to ${ev.detail.to}`);

  this.dataList = reorderArray(this.dataList, ev.detail.from, ev.detail.to);
  ev.detail.complete();
});
```

The event's detail includes all the relevant information about the reorder operation, including the `from` and `to` indexes. In the context of reordering, an item moves `from` index X `to` index Y.

For example, in this list we move the item at index `0` to the index `3`:

```
BEFORE | AFTER
  0    |   1
  1    |   2
  2    |   3
  3    |   0
  4    |   4
```

```
detail: {
  from: 0
  to: 3
}
```

Once the data structure has been updated to reflect the reorder change, the `complete()` method must be called.
This method finishes the reorder operation and resets all the CSS transforms applied by the `ion-reorder-group` component.

Fortunately this `complete()` method can optionally accept an array as input and it will return a reordered copy, based in `detail.from` and `detail.to`.

```ts
this.dataList = reorderGroup.complete(this.dataList);
```
