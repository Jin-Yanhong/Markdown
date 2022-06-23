## Global API

### Application

### General

## Composition API

### setup()

### Reactivity: Utilities

### Lifecycle Hooks

### Reactivity: Core

### Reactivity: Advanced

### Dependency Injection

## Built-ins

### Directives

-   [v-pre](https://vuejs.org/api/built-in-directives.html#v-pre)
-   [v-once](https://vuejs.org/api/built-in-directives.html#v-once)
-   [v-memo](https://vuejs.org/api/built-in-directives.html#v-memo)

-   [v-cloak](https://vuejs.org/api/built-in-directives.html#v-cloak)

### Components

-   [teleport](https://vuejs.org/api/built-in-components.html#teleport)
-   [suspense](https://vuejs.org/api/built-in-components.html#suspense)

### Special Elements

-   [component](https://vuejs.org/api/built-in-special-elements.html#component)
-   [slot](https://vuejs.org/api/built-in-special-elements.html#slot)

### Special Attributes

-   [ref](https://vuejs.org/api/built-in-special-attributes.html#ref)
-   [is](https://vuejs.org/api/built-in-special-attributes.html#is)

## CSS

### css 选择器修饰符

#### :solted()

选择器只作用于插槽里面的内容

```vue
<style scoped>
:global(div) {
    color: red;
}
</style>
```

#### :deep()

组件库样式穿透

```vue
<style scoped>
:global(div) {
    color: red;
}
</style>
```

组件库样式穿透

#### :global()

全局生效

```vue
<style scoped>
:global(div) {
    color: red;
}
</style>
```

#### 动态 CSS

```vue
<template>
    <div class="div">动态CSS</div>
</template>

<script setup lang="ts">
import { ref } from "vue";
const style = ref("red");
</script>

<style scoped>
.div {
    color: v-bind(style);
}
</style>
```

### CSS Module

## 项目应用

动态引用静态资源

```typescript
const getAssetsFile = (url: string) => {
    return new URL(`../assets/${url}`, import.meta.url).href;
};
```
