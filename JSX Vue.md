```vue
// 子组件
<script>
export default {
	name: 'RenderFormEl',
	render(h) {
		let { elConfig, value = elConfig.props.value } = this;
		const vNode = (
			<div>
				<div class='flex'>
					<span style='flex:1'></span>
					<ElButton
						type='text'
						icon='el-icon-delete'
						onClick={() => {
							this.$emit('deleteEl', elConfig);
						}}>
						删除
					</ElButton>
				</div>

				{configToVNode.call(this, h, elConfig, value)}
			</div>
		);
		return vNode;
	},
};
</script>
```

```vue
// 父组件
<script>
export default {
	name: 'Editor',
	render(h) {
		let { elConfig, value = elConfig.props.value } = this;
		const vNode = (
			<ElForm form={this.form} size='small' labelPosition='top'>
				{elementList.map(el => {
					return (
						<ElFormItem class='ElFormItem' label={el.formProps.label} prop={el.formProps.prop} key={el.key}>
							<RenderFormEl elConfig={el} v-model={this.form[el.formProps.prop]} onDeleteEl={elConfig => onDeleteEl(elConfig)} />
						</ElFormItem>
					);
				})}
			</ElForm>
		);
		return vNode;
	},
};
</script>
```
