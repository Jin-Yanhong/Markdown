## 关键字

```typescript
type User = {
	name: string;
	age: number;
};
```

### keyof

### xxxxxxxxxx97 1<template>2    <div class="app-container">3        <div class="editor" ref="editor" style="height: 800px"></div>4    </div>5</template>6<script>7import Quill from 'quill';8import 'quill/dist/quill.core.css';9import 'quill/dist/quill.snow.css';10import fileUploadAliOSS from '@/utils/upload';11​12export default {13    name: 'Editor',14    mounted() {15        this.init();16    },17    data() {18        return {19            Quill: null,20            currentValue: '',21            options: {22                theme: 'snow',23                bounds: document.body,24                debug: 'warn',25                modules: {26                    // 工具栏配置27                    toolbar: {28                        container: [29                            ['bold', 'italic', 'underline', 'strike'],30                            ['blockquote', 'code-block'],31                            [{ list: 'ordered' }, { list: 'bullet' }],32                            [{ indent: '-1' }, { indent: '+1' }],33                            [{ size: ['small', false, 'large', 'huge'] }],34                            [{ header: [1, 2, 3, 4, 5, 6, false] }],35                            [{ color: [] }, { background: [] }],36                            [{ align: [] }],37                            ['clean'],38                            ['link', 'image', 'video'],39                        ],40                        handlers: {41                            image: function () {42                                const input = document.createElement('input');43                                input.setAttribute('type', 'file');44                                input.setAttribute('accept', 'image/*');45                                input.click();46                                input.onchange = async () => {47                                    const file = input.files[0];48                                    const range = this.quill.getSelection(true);49                                    const res = await fileUploadAliOSS(file);50                                    this.quill.deleteText(range.index, 1);51                                    this.quill.insertEmbed(range.index, 'image', res.url);52                                };53                            },54                        },55                    },56                },57                placeholder: '请输入内容',58                readOnly: this.readOnly,59            },60        };61    },62​63    created() {64        const html = `<p>时事新闻</p>`;65        this.currentValue = html;66    },67    methods: {68        init() {69            const editor = this.$refs.editor;70            this.Quill = new Quill(editor, this.options);71​72            this.Quill.pasteHTML(this.currentValue);73​74            this.Quill.on('text-change', (delta, oldDelta, source) => {75                const html = this.$refs.editor.children[0].innerHTML;76                const text = this.Quill.getText();77                const quill = this.Quill;78                this.currentValue = html;79                this.$emit('input', html);80                this.$emit('on-change', { html, text, quill });81            });82​83            this.Quill.on('text-change', (delta, oldDelta, source) => {84                this.$emit('on-text-change', delta, oldDelta, source);85            });86​87            this.Quill.on('selection-change', (range, oldRange, source) => {88                this.$emit('on-selection-change', range, oldRange, source);89            });90​91            this.Quill.on('editor-change', (eventName, ...args) => {92                this.$emit('on-editor-change', eventName, ...args);93            });94        },95    },96};97</script>vue

### extends

### infer

## 工具类型

### `Partial<T>`、`Required<T>`、`Readonly<T>`、`Mutable<T>`

### `Record<K, T>`、`Pick<T, K>`
