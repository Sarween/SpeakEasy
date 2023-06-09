<template lang="pug">
v-row.tool-table.justify-center.mx-auto
  v-card.pa-4.rounded-xl(outlined)
    v-card-title
      p.mb-0 Tool Status
      v-spacer
    hr.mx-2

    //- Datatable
    v-data-table(
      :headers="headers"
      :items="desserts"
      :search="search"
    )
      template(v-slot:item.status="{ item }")
        v-chip(
          :color="getColor(item.status)"
          outlined
          pill
        )
          p.mb-0 {{ item.status }}
          v-icon.ml-2(v-if="item.status === 'Need Maintenance'" small) mdi-wrench
          v-icon.ml-2(v-if="item.status === 'Normal'" small) mdi-check-circle
          v-icon.ml-2(v-if="item.status === 'Checking'" small) mdi-clock-time-eight

      template(v-slot:item.action="{ item }")
        v-btn(
          icon
          :color="$vuetify.theme.themes.light.primary"
          :to="'/tooldetails'"
        )
          v-icon mdi-magnify

      template(v-slot:body.prepend)
          tr
            td.py-4
              v-text-field(v-model="toolid" type="text" label="Tool ID" hide-details="auto" dense outlined)
            td.py-4
              v-text-field(v-model="toolname" type="text" label="Tool Name" hide-details="auto" dense outlined)
            td.py-4
              v-text-field(v-model="time" type="text" label="Date & Time" hide-details="auto" dense outlined)
            td.py-4
              v-select.select-category(:items="statusList" label="Select a status" v-model="status" hide-details="auto" multiple chips dense outlined)
                template(v-slot:selection="{ item, index }")
                  v-chip(:color="getColor(item)" outlined)
                    span {{ item }}
            td.py-4.text-center
              v-icon.white--text mdi-magnify
</template>

<script>
export default {
  name: 'ToolTable',
  data () {
    return {
      search: '',
      toolid: '',
      toolname: '',
      time: '',
      status: '',
      statusList: ['Normal', 'Need Maintenance', 'Checking'],
      headers: [
        {
          text: 'Tools ID',
          align: 'start',
          sortable: false,
          value: 'id'
        },
        { text: 'Tools Name', value: 'name' },
        { text: 'Date & Time', value: 'dt' },
        {
          text: 'Status',
          align: 'center',
          value: 'status',
          filter: (value) => {
            if (this.status.length === 0) { return true }
            return this.status.includes(value)
          }
        },
        { text: 'Action', value: 'action', sortable: false }
      ],
      desserts: [
        {
          id: 'T10-12118A',
          name: 'SF 4-A22 CORDLESS DRILL DRIVER',
          dt: '12:57 PM, 11/5/2023',
          status: 'Need Maintenance',
          action: ''
        },
        {
          id: 'T10-12119A',
          name: 'TE 2-A22 CORDLESS ROTARY HAMMER',
          dt: '06:48 PM, 24/1/2023',
          status: 'Normal',
          action: ''
        },
        {
          id: 'T10-13418A',
          name: 'SID 4-A22 CORDLESS IMPACT DRIVER',
          dt: '06:48 PM, 24/1/2023',
          status: 'Checking',
          action: ''
        },
        {
          id: 'T10-12328A',
          name: 'BX 3 02 FASTENING TOOL',
          dt: '06:48 PM, 24/1/2023',
          status: 'Normal',
          action: ''
        },
        {
          id: 'T10-32342A',
          name: 'BX 3-BT (02) CORDLESS FASTENING TOOL',
          dt: '06:48 PM, 24/1/2023',
          status: 'Normal',
          action: ''
        },
        {
          id: 'T12-12111A',
          name: 'HDE 500-A22 CORDLESS',
          dt: '06:48 PM, 24/1/2023',
          status: 'Checking',
          action: ''
        },
        {
          id: 'T13-11238A',
          name: 'TE 2-A22 CORDLESS ROTARY HAMMER',
          dt: '06:48 PM, 24/1/2023',
          status: 'Need Maintenance',
          action: ''
        },
        {
          id: 'T20-75868A',
          name: 'HDE 500-A22 CORDLESS',
          dt: '06:48 PM, 24/1/2023',
          status: 'Normal',
          action: ''
        },
        {
          id: 'T22-12118B',
          name: 'TE 2-A22 CORDLESS ROTARY HAMMER',
          dt: '06:48 PM, 24/1/2023',
          status: 'Normal',
          action: ''
        },
        {
          id: 'T30-12118B',
          name: 'TE 2-A22 CORDLESS ROTARY HAMMER',
          dt: '06:48 PM, 24/1/2023',
          status: 'Checking',
          action: ''
        },
        {
          id: 'T10-12118A',
          name: 'SID 4-A22 CORDLESS IMPACT DRIVER',
          dt: '06:48 PM, 24/1/2023',
          status: 'Normal',
          action: ''
        }
      ]
    }
  },
  computed: {

  },
  methods: {
    getColor (status) {
      if (status === 'Normal') {
        return this.$vuetify.theme.themes.light.green
      } else if (status === 'Checking') {
        return this.$vuetify.theme.themes.light.blue
      } else {
        return this.$vuetify.theme.themes.light.primary
      }
    }
  }
}
</script>

<style scoped>
.width-80 {
  width: 90% !important;
}

:deep(.select-category .v-chip .v-chip__content) {
  font-size: 12px !important;
}

:deep(.select-category .v-chip.v-size--default) {
  height: 20px;
}

</style>
