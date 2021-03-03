<template>
  <div style="margin:25mm;font-size:12pt">
    <h1 style="text-align:center">Invoice</h1>
    <ul style="text-align:left;list-style:none;margin-left:-2rem">
      <li>{{ items.company }}</li>
      <li>{{ items.address }}</li>
      <li v-if="items.city || items.state || items.country">{{ items.city }}, {{ items.state }}, {{ items.country }}</li>
      <li>{{ items.phone }}</li>
      <li>{{ items.fax }}</li>
      <li>{{ items.email }}</li>
    </ul>
    <div style="text-align:center">
      <p>{{ humanDate(items.start) }} - {{ humanDate(items.end) }}</p>
    </div>
    <hr/>
    <table style="width:100%">
      <thead>
        <tr>
          <th style="width:80%;text-align:left">Name</th>
          <th style="width:20%;text-align:right">Time(In Hours)</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in items.entries" :key="index">
          <td style="text-align:left">{{ item.name }}</td>
          <td style="text-align:right">{{ item.time }}</td>
        </tr>
      </tbody>
      <tfoot>
        <tr>
          <td></td>
          <td style="text-align:right">
            <hr/>
            <strong>{{ total }}</strong>
          </td>
        </tr>
      </tfoot>
    </table>
  </div>
</template>

<script>
import dayjs from 'dayjs'
export default {
  name: "Export",
  methods: {
    toCommaNumber(number) {
      return number.toFixed(2).toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",")
    },
    humanDate(timestamp) {
      return dayjs(timestamp).format('MMMM D, YYYY')
    }
  },
  props: {
    items: Object
  },
  computed: {
    total() {
      let total = 0
      for (let item of this.items.entries) {
        total = total + parseFloat(item.time)
      }
      return this.toCommaNumber(total)
    }
  }
}
</script>

<style scoped>

</style>
