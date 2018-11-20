<template>
  <div>
    <el-button size="small" plain type="primary"
      @click.stop="dialogVisible = true">{{ label }}</el-button>
    <el-dialog
      title="提示"
      :visible.sync="dialogVisible"
      width="30%">
      <span>确认删除数据吗？</span>
      <span slot="footer" class="dialog-footer">
      <el-button @click="dialogVisible = false">取 消</el-button>
      <el-button type="primary" @click="deleteInfo">确 定</el-button>
      </span>
    </el-dialog>
  </div>
</template>
<script type="text/javascript">
export default {
  props: ['click', 'label', 'opt'],
  data () {
    return {
      dialogVisible: false
    }
  },
  mounted () {
    console.log('ButtonPop mounted')
  },
  methods: {
    async deleteInfo () {
      await this.click()
      this.dialogVisible = false
    }
  }
}
</script>
