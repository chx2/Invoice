<template>
  <b-form v-on:submit.prevent="submit">
    <b-card>
      <b-card-header>
        <b-row>
          <b-col cols="12" class="flex justify-content-center align-items-center flex-column">
            <h1>Create Invoice</h1>
          </b-col>
        </b-row>
      </b-card-header>
      <b-card-body>
        <b-row>
          <b-col cols="12" md="4">
            <b-form-group label="Company Name">
              <b-input placeholder="Enter an company name" v-model="form.company"></b-input>
            </b-form-group>
          </b-col>
          <b-col cols="12" md="8">
            <b-form-group label="Company Address">
              <b-input placeholder="Enter an address" v-model="form.address"></b-input>
            </b-form-group>
          </b-col>
        </b-row>
        <b-row>
          <b-col cols="12" md="4">
            <b-form-group label="Company City">
              <b-input placeholder="Enter a city" v-model="form.city"></b-input>
            </b-form-group>
          </b-col>
          <b-col cols="12" md="4">
            <b-form-group label="Company State">
              <b-input placeholder="Enter a State" v-model="form.state"></b-input>
            </b-form-group>
          </b-col>
          <b-col cols="12" md="4">
            <b-form-group label="Company Country">
              <b-input placeholder="Enter a Country" v-model="form.country"></b-input>
            </b-form-group>
          </b-col>
        </b-row>
        <b-row>
          <b-col cols="12" md="4">
            <b-form-group label="Company Phone">
              <b-input placeholder="Enter a phone number" v-model="form.phone"></b-input>
            </b-form-group>
          </b-col>
          <b-col cols="12" md="4">
            <b-form-group label="Company Fax">
              <b-input placeholder="Enter a Fax number" v-model="form.country"></b-input>
            </b-form-group>
          </b-col>
          <b-col cols="12" md="4">
            <b-form-group label="Company E-Mail">
              <b-input placeholder="Enter a E-Mail" v-model="form.email"></b-input>
            </b-form-group>
          </b-col>
        </b-row>
        <b-row>
          <b-col cols="12" md="6">
            <b-form-group label="Start Date">
              <b-form-datepicker v-model="form.start" locale="en"></b-form-datepicker>
            </b-form-group>
          </b-col>
          <b-col cols="12" md="6">
            <b-form-group label="End Date">
              <b-form-datepicker v-model="form.end" locale="en"></b-form-datepicker>
            </b-form-group>
          </b-col>
        </b-row>
      </b-card-body>
      <b-card-footer>
        <b-button type="submit" block variant="primary">Continue</b-button>
      </b-card-footer>
    </b-card>
  </b-form>
</template>

<script>
  export default {
    name: "Setup",
    data() {
      return {
        form : {
          company: null,
          address: null,
          city: null,
          country: null,
          state: null,
          phone: null,
          email: null,
          fax: null,
          start: null,
          end: null,
          entries: [{
            'name': 'Example Task',
            'time': 0,
            'disabled': false
          }]
        }
      }
    },
    methods: {
      submit() {
        this.$emit('submit', this.form)
      }
    }
  }
</script>

<style scoped>

</style>
