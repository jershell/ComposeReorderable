# Lazy reorder list
![Sample](readme/sample.gif)

A sample reorderable list built with Jetpack Compose.


Create your LazyColumn or LazyRow:

```
val listState: LazyListState = rememberLazyListState()
val state: ReorderableState = rememberReorderState(listState)
LazyColumn(
    state = listState,
    modifier = Modifier.reorderable(state, items))
```

Apply the offset to your item layout :

```
itemsIndexed(items) { idx, item ->
    val offset by remember {
        derivedStateOf { state.indexWithOffset?.takeIf { it.first == idx }?.second }
    }

    Column(
        modifier = Modifier.draggedItem(offset)
    ) {
        ...
    }
}
```
Use `draggedItem` for a default dragged effect or create your own.

Unfortunately this solution has some known limitations.

* You can`t use keyed items cause in this case the LazyList will [keep the scroll position based on the key](https://developer.android.com/reference/kotlin/androidx/compose/foundation/lazy/package-summary#(androidx.compose.foundation.lazy.LazyListScope).items(kotlin.collections.List,kotlin.Function1,kotlin.Function2))
* Every item must be a drag target
* Equal item size in drag direction




## License
```
Copyright 2021 André Claßen

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    https://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```