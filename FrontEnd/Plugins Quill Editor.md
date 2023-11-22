-   使用 url 链接代替 base64 字符

```vue
<template>
	<div class="app-container">
		<div class="editor" ref="editor" style="height: 800px"></div>
	</div>
</template>
<script>
import Quill from 'quill';
import 'quill/dist/quill.core.css';
import 'quill/dist/quill.snow.css';
import fileUploadAliOSS from '@/utils/upload';

export default {
	name: 'Editor',
	mounted() {
		this.init();
	},
	data() {
		return {
			Quill: null,
			currentValue: '',
			options: {
				theme: 'snow',
				bounds: document.body,
				debug: 'warn',
				modules: {
					// 工具栏配置
					toolbar: {
						container: [
							['bold', 'italic', 'underline', 'strike'],
							['blockquote', 'code-block'],
							[{ list: 'ordered' }, { list: 'bullet' }],
							[{ indent: '-1' }, { indent: '+1' }],
							[{ size: ['small', false, 'large', 'huge'] }],
							[{ header: [1, 2, 3, 4, 5, 6, false] }],
							[{ color: [] }, { background: [] }],
							[{ align: [] }],
							['clean'],
							['link', 'image', 'video'],
						],
						handlers: {
							image: function () {
								const input = document.createElement('input');
								input.setAttribute('type', 'file');
								input.setAttribute('accept', 'image/*');
								input.click();
								input.onchange = async () => {
									const file = input.files[0];
									const range = this.quill.getSelection(true);
									const res = await fileUploadAliOSS(file);
									this.quill.deleteText(range.index, 1);
									this.quill.insertEmbed(range.index, 'image', res.url);
								};
							},
						},
					},
				},
				placeholder: '请输入内容',
				readOnly: this.readOnly,
			},
		};
	},

	created() {
		const html = `<p>时事新闻</p>`;
		this.currentValue = html;
	},
	methods: {
		init() {
			const editor = this.$refs.editor;
			this.Quill = new Quill(editor, this.options);

			this.Quill.pasteHTML(this.currentValue);

			this.Quill.on('text-change', (delta, oldDelta, source) => {
				const html = this.$refs.editor.children[0].innerHTML;
				const text = this.Quill.getText();
				const quill = this.Quill;
				this.currentValue = html;
				this.$emit('input', html);
				this.$emit('on-change', { html, text, quill });
			});

			this.Quill.on('text-change', (delta, oldDelta, source) => {
				this.$emit('on-text-change', delta, oldDelta, source);
			});

			this.Quill.on('selection-change', (range, oldRange, source) => {
				this.$emit('on-selection-change', range, oldRange, source);
			});

			this.Quill.on('editor-change', (eventName, ...args) => {
				this.$emit('on-editor-change', eventName, ...args);
			});
		},
	},
};
</script>
```
