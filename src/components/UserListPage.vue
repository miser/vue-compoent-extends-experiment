<script type="text/javascript">
import ListPageAbstract from './ListPageAbstract.vue'
import Button from './ButtonPop.vue'
// 模拟ajax请求
// 仅做了名字的模糊查询，其他参数忽略
function search (opt) {
  return new Promise((resolve) => {
    let list = [
      { name: 'User Peter', phone: '313141414', status: 'status1', date: '2018-10-10' },
      { name: 'User Marry', phone: '123931873', status: 'status2', date: '2018-11-11' },
      { name: 'User Sue', phone: '342391873', status: 'status1', date: '2018-01-01' },
      { name: 'User Join', phone: '143391873', status: 'status1', date: '2018-12-12' }
    ]
    if (opt.name) {
      list = list.filter(item => item.name.match(opt.name))
    }
    setTimeout(() => {
      resolve(list)
    }, 1000)
  })
}
export default {
  extends: ListPageAbstract,
  components: { Button },
  data: function () { return {} },
  mounted: function () {
    this.title = '用户列表'
  },
  methods: {
    createConfig () {
      // 用户名、创建时间、手机号、状态
      let config = ListPageAbstract.methods.createConfig.call(this)
      config.filter.conditions.splice(1, 0, 'phone')

      let table = config.table
      table.column.push({ key: 'date', label: '时间' })
      table.action = {
        headerLabel: '操作',
        label: '删除',
        click: this.deleteRow
      }
      return config
    },
    async fetchData () {
      let list = await search(this.filterForm)
      this.list = list
    },
    deleteRow (item) {
      return new Promise((resolve, reject) => {
        console.log(`delete date: ${item.name}`)
        setTimeout(() => {
          this.list.splice(this.list.indexOf(item), 1)
          resolve()
        }, 1000)
      })
    }
  }
}
</script>
<style type="text/css">
.title {
  margin-bottom: 50px;
  color: blue;
}
</style>
