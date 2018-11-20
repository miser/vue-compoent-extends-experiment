<template>
<div>
	<el-button size="small" plain type="primary" @click.stop="click">
		{{ label }}
	</el-button>
</div>
</template>
<script type="text/javascript">
	export default {
		props: ['click', 'label', 'opt'],
		mounted () {
			console.log('ButtonClick mounted')
		}
	}
</script>