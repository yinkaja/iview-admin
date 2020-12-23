<template>
  <div>
    <Card>
      <tables ref="tables" editable searchable search-place="top" v-model="tableData" :columns="columns" @on-delete="handleDelete"/>
      <Button style="margin: 10px 0;" type="primary" @click="exportExcel">导出为Csv文件</Button>
    </Card>
  </div>
</template>

<script>
import Tables from '_c/tables'
import { getTableData } from '@/api/data'
export default {
  name: 'tables_page',
  components: {
    Tables
  },
  data () {
    return {
      columns: [
        { title: '设备id', key: 'name', sortable: true },
        { title: '设备名称', key: 'email', editable: true },
        { title: '设备状态', key: 'createTime' },
        {
          title: '相关操作',
          key: 'handle',
          options: ['delete'],
          button: [
            (h, params, vm) => {
              return h('Poptip', {
                props: {
                  confirm: true,
                  title: '你确定要删除吗?'
                },
                on: {
                  'on-ok': () => {
                    vm.$emit('on-delete', params)
                    vm.$emit('input', params.tableData.filter((item, index) => index !== params.row.initRowIndex))
                  }
                }
              }, [
                h('Button', '设备详情')
              ])
            }
          ]
        }
        // {
        //
        //   title: '相关操作',
        //   key: 'handle',
        //   width: 150,
        //   align: 'center',
        //   render: (h, params) => {
        //     return h('div', [
        //       h('Button', {
        //         props: {
        //           type: 'primary',
        //           size: 'small'
        //         },
        //         style: {
        //           marginRight: '5px'
        //         },
        //         on: {
        //           click: () => {
        //             this.show(params.index)
        //           }
        //         }
        //       }, 'View'),
        //       h('Button', {
        //         props: {
        //           type: 'error',
        //           size: 'small'
        //         },
        //         on: {
        //           click: () => {
        //             this.remove(params.index)
        //           }
        //         }
        //       }, 'Delete')
        //     ]);
        //    }
        // }

      ],
      tableData: []
    }
  },
  methods: {
    handleDelete (params) {
      console.log(params)
    },
    exportExcel () {
      this.$refs.tables.exportCsv({
        filename: `table-${(new Date()).valueOf()}.csv`
      })
    }
    // show (index) {
    //   this.$Modal.info({
    //     title: 'User Info',
    //     content: `Name：${this.tableData[index].name}<br>Age：${this.tableData[index].email}<br>Address：${this.data6[index].address}`
    //   })
    // },
    // remove (index) {
    //   this.tableData.splice(index, 1);
    // }
  },
  mounted () {
    getTableData().then(res => {
      this.tableData = res.data
    })
  }
}
</script>

<style>

</style>
