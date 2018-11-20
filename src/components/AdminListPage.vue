<!-- <template>
  <Page>
    <div slot="filter-slot">
      other input filter
    </div>
  </Page>
</template> -->
<script type="text/javascript">
import ListPageAbstract from './ListPageAbstract'
// 模拟ajax请求
// 仅做了名字的模糊查询，其他参数忽略
function search (opt) {
  return new Promise((resolve) => {
    let list = [
      { name: 'Admin Peter', phone: '313141414', status: 'status1', date: '2018-10-10' },
      { name: 'Admin Marry', phone: '123931873', status: 'status2', date: '2018-11-11' },
      { name: 'Admin Sue', phone: '342391873', status: 'status1', date: '2018-01-01' },
      { name: 'Admin Join', phone: '143391873', status: 'status1', date: '2018-12-12' }
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
  // components: {
  //   Page: ListPageAbstract,
  // },
  data () {
    return {
      title: '管理员列表'
    }
  },
  methods: {
    fetchOptions () {
      ListPageAbstract.methods.fetchOptions.call(this)
      console.log('to do other thing')
    },
    async fetchData () {
      let list = await search(this.filterForm)
      this.list = list
    }
  }
}
</script>
