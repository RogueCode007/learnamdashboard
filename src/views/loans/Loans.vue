<template>
  <div>
    <CCard>
      <CCardHeader>
        <CIcon name="cil-grid"/> All Loans
      </CCardHeader>
      <LoansTable />
    </CCard> 
  </div>
</template>

<script>
import LoansTable from "@/components/LoansTable"
export default {
  components:{
    LoansTable
  }
}
</script>

<style>

</style>