<template>
  <div>
    <div class="tc-pager">
      <el-pagination :small="small" :total="pager.totalCount" :current-page="pager.pageIndex" :page-sizes="pageSizeArray" :layout="layout" :page-size="pager.pageSize" v-bind="$attrs" background @current-change="pagerChange" @size-change="sizeChange" v-on="$listeners">
      </el-pagination>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TcPager',
  props: {
    pager: { type: Object, required: false, default: null },
    small: { type: Boolean, required: false, default: false },
    layout: { type: String, required: false, default: 'total, prev, pager, next, sizes' },
    pageSizes: { type: String, required: false, default: '10,30,50,100' }
  },
  data: () => ({
  }),
  computed: {
    pageSizeArray: function() {
      return this.pageSizes.split(',').map(item => parseInt(item, 10))
    }
  },
  methods: {
    pagerChange: function(val) {
      this.pager.pageIndex = val
      this.$emit('pagerChange', val, this.pager.pageSize)
    },
    sizeChange: function(val) {
      this.pager.pageSize = val
      this.$emit('pagerChange', this.pager.pageIndex, val)
      this.$emit('sizeChange', this.pager.pageIndex, val)
    }
  }
}
</script>
