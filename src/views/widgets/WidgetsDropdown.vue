<template>
  <CRow>
    <CCol sm="6" lg="4">
      <CWidgetDropdown color="gradient-primary" header="250" text="No of Enrollees" style="min-height: 150px"> 
        <template #default>
          
        </template>
        <template #footer>
          <CChartLineSimple
            pointed
            class="mt-3 mx-3"
            style="height:70px"
            :data-points="[65, 59, 84, 84, 51, 55, 40]"
            point-hover-background-color="primary"
            label="Enrollees"
            labels="months"
          />
        </template>
      </CWidgetDropdown>
    </CCol>
    <CCol sm="6" lg="4">
        <CWidgetDropdown color="gradient-info" header="200" text="No of Loans" style="min-height: 150px"> 
          <template #default>
            
          </template>
          <template #footer>
            <CChartLineSimple
              pointed
              class="mt-3 mx-3"
              style="height:70px"
              :data-points="[1, 18, 9, 17, 34, 22, 11]"
              point-hover-background-color="info"
              :options="{ elements: { line: { tension: 0.00001 }}}"
              label="Loans"
              labels="months"
            />
          </template>
        </CWidgetDropdown>
    </CCol>
    <CCol sm="6" lg="4">
      <CWidgetDropdown color="gradient-warning" header="#120,000" text="Value of Loans" style="min-height: 150px"> 
        <template #default>
          
        </template>
        <template #footer>
          <CChartLineSimple
            class="mt-3"
            style="height:70px"
            background-color="rgba(255,255,255,.2)"
            :data-points="[78, 81, 80, 45, 34, 12, 40]"
            :options="{ elements: { line: { borderWidth: 2.5 }}}"
            point-hover-background-color="warning"
            label="Value"
            labels="months"
          />
        </template>
      </CWidgetDropdown>
    </CCol>
    <CCol sm="6" lg="4">
      <CWidgetDropdown color="gradient-success" header="50" text="No of Loan Defaults" style="min-height: 150px"> 
        <template #default>
          
        </template>
        <template #footer>
          <CChartLineSimple
            class="mt-3"
            style="height:70px"
            background-color="rgba(255,255,255,.2)"
            :data-points="[78, 81, 80, 45, 34, 12, 40]"
            :options="{ elements: { line: { borderWidth: 2.5 }}}"
            point-hover-background-color="success"
            label="Defaults"
            labels="months"
          />
        </template>
      </CWidgetDropdown>
    </CCol>
    <CCol sm="6" lg="4">
      <CWidgetDropdown color="gradient-danger" header="#50,000" text="Value of Loan Defaults" style="min-height: 150px">
        <template #default>
          
        </template>
        <template #footer>
          <CChartLineSimple
            class="mt-3"
            style="height:70px"
            background-color="rgba(255,255,255,.2)"
            :data-points="[78, 81, 80, 45, 34, 12, 40]"
            :options="{ elements: { line: { borderWidth: 2.5 }}}"
            point-hover-background-color="danger"
            label="Value"
            labels="months"
          />
        </template>
      </CWidgetDropdown>
    </CCol>
    <CCol sm="6" lg="4">
      <CWidgetDropdown color="gradient-warning" header="100" text="Pending Loan Requests" style="min-height: 150px">
        <template #default>
          
        </template>
        <template #footer>
          <CChartLineSimple
            class="mt-3"
            style="height:70px"
            background-color="rgba(255,255,255,.2)"
            :data-points="[78, 81, 80, 45, 34, 12, 40]"
            :options="{ elements: { line: { borderWidth: 2.5 }}}"
            point-hover-background-color="warning"
            label="Pending Requests"
            labels="months"
          />
        </template>
      </CWidgetDropdown>
    </CCol>
  </CRow>
</template>

<script>
import { CChartLineSimple, CChartBarSimple } from '../charts/index.js'

export default {
  name: 'WidgetsDropdown',
  components: { CChartLineSimple, CChartBarSimple },
  data(){
    return {
      
    }
  }
}
</script>
