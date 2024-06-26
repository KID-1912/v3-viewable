# v3-viewable

<h3 align="center">
    vue3图片内容查看——useViewable；
    vue3 image content viewer - useViewable.
</h3>

<br/>

![](https://raw.githubusercontent.com/KID-1912/Github-PicGo-Images/master/2024/06/26/20240626104957.png)

---

<p align="center">
  <a href="https://www.npmjs.com/package/v3-viewable">
    <img
     alt="NPM URL"
     src="https://img.shields.io/badge/npm-v3Viewable?logo=npm">
  </a>
  <img
     alt="version"
     src="https://img.shields.io/badge/version-1.0.0-blue">
</p>

## Install

```shell
npm install v3-viewable -S
```

## Usage

```vue
<script setup>
import { useViewable } from "v3-viewable";

const viewableRef = ref(null);
const { style, scale } = useViewable(viewableRef, {
  initialSizePercentage: 0.8,
});
</script>

<template>
  <div class="h-100vh relative overflow-hidden">
    <!-- viewable content -->
    <img
      ref="viewableRef"
      :style="style"
      class="absolute"
      src="@/assets/images/post-bg-tree.jpg"
      draggable="false"
    />
    <!-- control-bar -->
    <div class="control-bar">
      <button class="px-4px" @click="scale -= 0.05">-</button>
      <div class="px-4px w-50px">{{ `${parseInt(scale * 100)}%` }}</div>
      <button class="px-4px" @click="scale += 0.05">+</button>
    </div>
  </div>
</template>
```

### Options

- `initialSizePercentage` - The initial size of the content viewer, default is `1`.

- `containerElement` - The container element of the content viewer, default is `viewableRef.value.parentNode`.

- `scaleStep` - The scale step of the content viewer, default is `0.02`.

- `onDrag({x, y})` - The drag event handler of the content viewer.

- `onScale(mouseWheelEvent)` - The scale event handler of the content viewer.

### Return

- `style` - The style object of the content viewer.

- `scale` - The scale of the content viewer.

- `width/height` - The width/height of the content viewer.

- `position` - The position(x, y) of the content viewer.

- `setScale(num)` - The method to set the scale of the content viewer(hold center position).

- `calcScaleBySizePercentage(num)` - A method that calculates the scale by size percentage and returns it.

### Component Usage

```vue
<script setup>
import { UseViewable } from "v3-viewable/component";

const viewableRef = ref(null);
const options = { ... }; // options
const handleSetScale = (num) => viewableRef.value.setScale(num); // by viewableRef.value
</script>

<template>
  <div class="h-100vh relative overflow-hidden">
    <UseViewable
      ref="viewableRef"
      class="absolute"
      v-bind="options"
      v-slot="{ style... }"
    >
      <img src="@/assets/images/post-bg-tree.jpg" draggable="false" />
    </UseViewable>
  </div>
</template>
```
