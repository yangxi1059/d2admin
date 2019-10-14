<template>
    <commonOffers :tableData="tableData"
    ></commonOffers>
</template>

<script>
import commonOffers from '../../../../components/commonOffers/commonOffers'
export default {
  name: 'Offers1',
  data () {
    return {
      // input1: '',
      // input2: '',
      tableData: [
        {
          Mentee: 'Mentee C',
          EducationBackground: 'Top 10 US National University',
          OfferReceived: 'McKinsey',
          Division: 'Analytics',
          ImgSrc: 'XXX',
          id: 1
        }, {
          Mentee: 'Mentee X',
          EducationBackground: 'Top 5 Mainland China University',
          OfferReceived: 'CICC',
          Division: 'IBD',
          ImgSrc: 'XXX',
          id: 2
        }, {
          Mentee: 'Mentee Z',
          EducationBackground: 'Top 50 US National University',
          OfferReceived: 'Goldman Sachs',
          Division: 'GIR',
          ImgSrc: 'XXX',
          id: 3
        }, {
          Mentee: 'Mentee L',
          EducationBackground: 'Top 30 US National University',
          OfferReceived: 'Bain',
          Division: 'Consulting',
          ImgSrc: 'XXX',
          id: 4
        }, {
          Mentee: 'Mentee J',
          EducationBackground: 'Top 40 US National University',
          OfferReceived: 'Duff&Phelps',
          Division: 'Portfolio Valuation',
          ImgSrc: 'XXX',
          id: 5
        }
      ]
      // currentPage: 1, // 默认显示第一页
      // pageSize: 1 // 默认每页显示1条
    }
  },
  // methods: {
  //   onSubmit () {
  //     // console.log('submit!');
  //   },
  //   handleClick (row) {
  //     // console.log(row);
  //   },
  //   handleSizeChange (val) {
  //     this.pageSize = val // 动态改变每页 ${val} 条
  //   },
  //   handleCurrentChange (val) {
  //     this.currentPage = val // 动态改变当前页数: ${val}
  //   }
  // },
  // created () {
  //   this.total = this.tableData.length
  // },
  components: {
    commonOffers
  }
}
</script>
