<template>
  <b-row>
    <b-col cols="12" class="flex justify-content-center align-items-center flex-column">
      <h1>Invox</h1>
      <b-icon icon="clock" font-scale="8"></b-icon>
      <div class="mt-4">
        <b-button @click="create" class="m-2" variant="success">Create</b-button>
        <b-button @click="upload" class="m-2" variant="primary">
          Import
          <input
              type="file"
              style="display: none"
              ref="fileInput"
              accept="application/json"
              @change="parseFile"/>
        </b-button>
      </div>
    </b-col>
  </b-row>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      data: null
    }
  },
  methods: {
    create() {
      this.$emit('create')
    },
    upload() {
      this.$refs.fileInput.click()
    },
    parseFile(event) {
      let file = event.target.files[0]
      let fileReader = new FileReader()

      fileReader.onload = evt => this.$emit('file-loaded', JSON.parse(evt.target.result))
      fileReader.readAsText(file)
    }
  }
}
</script>

<style scoped>

</style>
