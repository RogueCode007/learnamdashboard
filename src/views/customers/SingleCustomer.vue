<template>
  <div>
    <CRow>
      <CCol sm='12' md='6'>
        <CCard>
          <CCardHeader>
            About Customer
          </CCardHeader>
          <CCardBody>
            <div>
              <strong>Name</strong>
              <p>{{customer.name}}</p>
            </div>
            <div>
              <strong>Phone number</strong>
              <p>{{customer.phone_number}}</p>
            </div>
            <div>
              <strong>Address</strong>
              <p>{{customer.address}}</p>
            </div>
            <div>
              <strong>Email Address</strong>
              <p>{{customer.email}}</p>
            </div>
            <div>
              <strong>BVN Number</strong>
              <p>{{customer.bvn}}</p>
            </div>
            <div>
              <strong>NIN Number</strong>
              <p>{{customer.nin}}</p>
            </div>
            <div>
              <strong>Date Joined</strong>
              <p>{{customer.date_joined}}</p>
            </div>
          </CCardBody>
        </CCard>
      </CCol>
      <CCol sm='12' md='6'>
        <CCard>
          <CCardHeader>Loans</CCardHeader>
          <CCardBody>
            <CListGroup accent>
              <CListGroupItem color="secondary" 
              v-for="loan in customer.loans" 
              :key="loan.id"
              :accent="getAccent(loan.status)"
              class="my-1"
              >
              <div style="display: flex; justify-content: space-between">
                <div>
                  <p>Request Date: {{loan.date}}</p>
                  <p><strong>Loan Amount: #{{loan.amount}}</strong></p>
                  <strong class="mr-2">Approval Status:</strong>{{loan.status}}
                </div>
                <div v-if="loan.status == 'Approved' ">
                  <div v-if="loan.repaid">
                    <strong class="mr-2">Repayment Status:</strong>
                    <CBadge :color="getRepaidBadge(loan.repaid)" style="padding: 8px;">
                      Repaid
                    </CBadge>
                  </div>
                  <div v-else>
                    <strong class="mr-2">Repayment Status:</strong>
                    <CBadge :color="getRepaidBadge(loan.repaid)" style="padding: 8px;" >
                      Not Repaid
                    </CBadge>
                  </div>
                    <CDropdown 
                        style="display: block; margin-top: 20px; float: right"
                        size="sm"
                        toggler-text="Change Repayment Status"
                        color="info"
                      >
                      <CDropdownItem @click="changePaymentStatus(loan, 'repaid')">Fully Repaid</CDropdownItem>
                      <CDropdownItem @click="changePaymentStatus(loan, 'pending')">Incomplete</CDropdownItem>
                    </CDropdown>
                </div>
                <div v-else>
                  <CButton size="sm" color="primary" class="ml-3" @click="showApproveModal(loan)">
                    Approve Loan
                  </CButton>
                </div>
              </div>
              </CListGroupItem>
            </CListGroup>
          </CCardBody>
        </CCard>
      </CCol>
    </CRow>
    <CModal
      color="warning"
      title="Are you sure"
      :show.sync="approveModal"
    > 
      <h2>Approve this loan?</h2>
      <template #footer>
        <CButton @click="approveModal = false" color="secondary">Cancel</CButton>
        <CButton  @click="approval()" color="success">Proceed</CButton>
      </template>
    </CModal>
  </div>
</template>

<script>
const servicemen = [
  'Jide', 'Taiwo', "Gbenga", 'George'
]

export default {
  data(){
    return{
      servicemen: servicemen,
      customer: {
        name: 'Avon Barksdale',
        phone_number: '08036738733',
        address: 'Plot 256, Arike Ade Street, Downtown',
        email: 'obiwan@gmail.com',
        date_joined: '2019/12/25',
        nin: 12324342232,
        bvn: 12330404933,
        loans: [
          {'id':1, 'date': '2020/1/3','order_number': 234,  'status': 'Approved', 'amount': 50000, repaid: true },
          {'id':2, 'date': '2020/1/3','order_number': 234,  'status': 'Approved', 'amount': 50000, repaid: false},
          {'id':3, 'date': '2020/1/3','order_number': 234,  'status': 'Pending Approval', 'amount': 50000,  },
        ],
      },
      approveModal: false,
       loan: {},
    }
  },
  methods:{
    getBadge(str){
      switch(str){
        case 'Approved':
        return 'success'
        default: return 'warning'
      }
    },
    getRepaidBadge(str){
      switch(str){
        case true:
        return 'success';
        case false :
        return 'danger';
        default: return 'danger'
      }
    },
    getAccent(str){
      switch(str){
        case 'Approved':
        return 'success'
        default: return 'warning'
      }
    },
    changePaymentStatus(param1, param2){
      console.log(param1)
      this.loan = param1

      if(param2 == 'repaid'){
          param1.repaid = true
      }else{
        param1.repaid = false
      }
    },
    showApproveModal(param){
      this.loan = param
      console.log(this.loan)
      this.approveModal = true
    },
    approval(){
      this.loan.status = "Approved"
      this.loan.repaid = false
      console.log(this.customer.loans)
      this.approveModal = false
    }
  }
}
</script>

<style>

</style>