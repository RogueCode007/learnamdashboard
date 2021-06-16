<template>
  <CCardBody>
    <CDataTable
      :items="customersData"
      :fields="fields"
      items-per-page-select
      :items-per-page="10"
      hover
      sorter
      pagination
      table-filter
      cleaner
    >
    
    <template #fullname="{item}">
      <td>
        <router-link :to="{ name: 'customer', params: { id: item.id }}">{{item.fullname}}</router-link>
      </td>
    </template>
    <template #is_approved="{item}">
      <td v-if="item.is_approved">
        <CBadge :color="getBadge(item.is_approved)" style="padding: 8px">
          Approved
        </CBadge>
      </td>
      <td v-else>
        <CBadge :color="getBadge(item.is_approved)" style="padding: 8px">
          Unapproved
        </CBadge>
      </td>
    </template>
    <template #Action="{item}">
      <td class="py-2">
        <CButton size="sm" color="info" class="" @click="showLoanModal(item)" >
          View
        </CButton>
      </td>
    </template>
    </CDataTable>
    <CModal
      color="info"
      title="Loan Details"
      :show.sync="loanModal"
    > 
      <div>
        <strong>Loan Value</strong>
        <p>{{loan.amount}}</p>
      </div>
      <div>
        <strong>Customer Name</strong>
        <p>{{loan.fullname}}</p>
      </div>
      <div>
        <strong>Customer Phone</strong>
        <p>{{loan.phone}}</p>
      </div>
      <div>
        <strong>Customer Email</strong>
        <p>{{loan.email}}</p>
      </div>
      <div>
        <strong>Approval Status</strong>
        <p v-if="loan.is_approved">Approved</p>
        <p v-else>Unapproved</p>
      </div>
      <div>
        <strong>Request Date</strong>
        <p>{{loan.date}}</p>
      </div>
      <template #footer>
        <CButton @click="approveModal = false" color="secondary">Cancel</CButton>
        <CButton  @click="approval()" color="success">Proceed</CButton>
      </template>
    </CModal>
  </CCardBody>
</template>

<script>
// import axios from 'axios'
// import url from '@/main'

const fields = [
  { key: 'fullname', _style:'min-width:30%', label: 'Customer Name' },
  {key:'amount', label: 'Loan Value'},
  { key: 'phone', label: 'Phone number', _style:'min-width:20%;' },
  'email',
  // 'no_of_orders',
  
  { key: 'date', _style:'min-width:10%;', label: 'Request Date' },
  {key:'is_approved', label: 'Status'},
  'Action'
  
]

export default {
  data () {
    return {
      fields,
      details: [],
      collapseDuration: 0,
      loanModal: false,
      loan: {},
      customersData: [
        {id: 1, amount: "#50,000", fullname: "Avon Barksdale", phone: "080939091090", email: "a.avici@gmail.com", date:"2020/03/05",  is_approved: false},
        {id: 2, amount: "#150,000", fullname: "Avon Barksdale", phone: "080939091090", email: "a.avici@gmail.com", date:"2020/03/05",  is_approved: true},
        {id: 3, amount: "#120,000", fullname: "Avon Barksdale", phone: "080939091090", email: "a.avici@gmail.com", date:"2020/03/05",  is_approved: false},
        {id: 4, amount: "#70,000", fullname: "Avon Barksdale", phone: "080939091090", email: "a.avici@gmail.com", date:"2020/03/05",  is_approved: false},
        {id: 5, amount: "#200,000", fullname: "Avon Barksdale", phone: "080939091090", email: "a.avici@gmail.com", date:"2020/03/05",  is_approved: true},
        {id: 6, amount: "#300,000", fullname: "Avon Barksdale", phone: "080939091090", email: "a.avici@gmail.com", date:"2020/03/05",  is_approved: false},
        
      ]
    }
  },
  filters:{
    formateDate(str){
      var date = new Date(str);
      var day = date.getDate();
      var year = date.getFullYear();
      var month = date.getMonth()+1;
      var dateStr = year+"/"+month+"/"+day;
      return dateStr
    }
  },
  methods: {
    getBadge (status) {
      switch (status) {
        case true: return 'success'
        case false: return 'warning'
      }
    },
    showLoanModal(item){
      this.loan = item;
      this.loanModal = true
    }
  },
  // beforeCreate(){
  //   this.$store.state.loading = true;
  //   axios.get(`${url}/users/allUsers`)
  //   .then(res=>{
  //     this.customersData = res.data
  //     this.$store.state.loading = false
  //   })
  // }
}
</script>