解决 select 下拉框漂浮的问题

```html
<template>
    <a-select
        style="width: 100%; position: relative"
        :getPopupContainer="trigger => trigger.parentNode"
        mode="multiple"
        :default-value="['a1', 'b2']"
        style="width: 100%"
        placeholder="Please select"
        @change="handleChange"
    >
        <a-select-option v-for="i in 25" :key="(i + 9).toString(36) + i">{{ (i + 9).toString(36) + i }}</a-select-option>
    </a-select>
</template>
<script>
    export default {
        methods: {
            handleChange(value) {
                console.log(`selected ${value}`);
            },
        },
    };
</script>
```
