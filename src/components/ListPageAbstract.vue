<template>
  <div>
    <Title :title="title" />
    <div>
      <el-form v-if="config && config.filter" ref='form' :inline="true" :model="filterForm">
        <el-form-item v-if="config.filter.conditions.indexOf('name') >= 0" label="名字" prop="name">
          <el-input v-model="filterForm.name"></el-input>
        </el-form-item>
        <el-form-item v-if="config.filter.conditions.indexOf('phone') >= 0" label="手机" prop="date">
          <el-input v-model="filterForm.date"></el-input>
        </el-form-item>
        <el-form-item v-if="config.filter.conditions.indexOf('date') >= 0" label="时间" prop="date">
          <el-input v-model="filterForm.date"></el-input>
        </el-form-item>
        <el-form-item v-if="config.filter.conditions.indexOf('status') >= 0" label="状态" prop="status">
          <el-select v-model="filterForm.status" placeholder="请选择">
            <el-option v-for="option in statusOptions" :label="option.text" :value="option.value" :key="option.value"></el-option>
          </el-select>
        </el-form-item>
        <!-- <div>
          <slot name="filter-slot"></slot>
        </div> -->
        <el-form-item>
          <el-button type="primary" @click.stop="config.filter.action">提交</el-button>
        </el-form-item>
      </el-form>
    </div>
    <el-table v-if="config" :data="list" >
      <el-table-column v-for="(item, index) in config.table.column" :key="index"
      :prop="item.key" :label="item.label">
      </el-table-column>
      <el-table-column v-if="config.table.action" :label="config.table.action.headerLabel">
      <template slot-scope="scope">
      <Button :click="config.table.action.click.bind(null, scope.row)" :label="config.table.action.label" :opt="config.table.action" />
      </template>
      </el-table-column>
    </el-table>
  </div>
</template>
<script type="text/javascript">
import Button from './ButtonClick.vue'
import Title from './Title.vue'

export default {
  components: { Button, Title },
  data: function () {
    return {
      filterForm: { },
      statusOptions: [],
      list: [],
      title: null,
      config: null
    }
  },
  mounted: function () {
    this.config = this.createConfig()
    this.fetchOptions()
    this.fetchData()
    console.log('ListPageAbstract mounted')
  },
  methods: {
    createConfig () {
      let config = {}
      config.filter = {
        conditions: [ 'name', 'status' ],
        action: () => {
          this.fetchData(this.filterForm)
        }
      }
      config.table = {
        column: [
          { key: 'name', label: '用户名' },
          { key: 'phone', label: '手机号码' },
          { key: 'status', label: '状态' }
        ],
        action: {
          headerLabel: '操作',
          label: '修改',
          click: this.editRow
        }
      }
      return config
    },
    fetchOptions () {
      this.statusOptions = [
        { value: 1, text: 'status1' },
        { value: 2, text: 'status2' }
      ]
    },
    async fetchData () { },
    editRow (item) {
      console.log(`update data => ${item.name}`)
    }
  }
}
</script>
<style type="text/css">
.title {
  color: red;
  margin-bottom: 20px;
}
</style>
