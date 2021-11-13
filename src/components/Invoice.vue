<template>
    <div>
        <h1>Invoice For: {{ data.company }}</h1>
        <hr/>
        <b-row>
            <b-col cols="12">
                <b-button-group class="w-100">
                    <b-button @click="add" variant="success">
                        Add Entry
                        <b-icon-plus-square></b-icon-plus-square>
                    </b-button>
                    <b-button @click="download" variant="info" v-if="data.entries.length > 0">
                        Download Invoice
                        <b-icon-download></b-icon-download>
                    </b-button>
                    <b-button @click="exportJson" variant="warning" v-if="data.entries.length > 0">
                        Export Data
                        <b-icon-file-code></b-icon-file-code>
                    </b-button>
                </b-button-group>
                <hr/>
                <b-list-group v-if="data.entries.length > 0">
                    <b-list-group-item v-for="(entry, index) in data.entries" :key="index">
                        <b-row>
                            <b-col cols="12" md="4" class="mt-2">
                                <b-form-group label="Task Name">
                                    <b-input v-model="entry.name"></b-input>
                                </b-form-group>
                            </b-col>
                            <b-col cols="12" md="4" class="mt-2">
                                <b-form-group label="Hours">
                                    <b-input type="number" step="0.5" min="0" v-model="entry.time"
                                             :disabled="entry.disabled"></b-input>
                                </b-form-group>
                            </b-col>
                            <b-col cols="12" md="4">
                                <b-button variant="danger" class="m-2" @click="del(index)">
                                    <b-icon-trash></b-icon-trash>
                                </b-button>
                            </b-col>
                        </b-row>
                    </b-list-group-item>
                </b-list-group>
                <div v-else>
                    <h1>No Entries Found</h1>
                </div>
            </b-col>
        </b-row>
        <div v-show="false">
            <export id="content" :items="data"></export>
        </div>
    </div>
</template>

<script>
import html2pdf from 'html2pdf.js'
import Export from "@/components/Export"

export default {
    name: "InvoicePage",
    components: {Export},
    data() {
        return {
            invoiceData: {}
        }
    },
    created() {
        this.invoiceData = this.data
    },
    methods: {
        add() {
            this.invoiceData.entries.push({
                'name': 'Example Task',
                'time': 0,
            })
        },
        edit(index) {
            this.invoiceData.entries[index].disabled = false
        },
        disable(index) {
            this.invoiceData.entries[index].disabled = true
        },
        del(index) {
            this.invoiceData.entries.splice(index, 1)
        },
        exportJson() {
            let data = "data:text/json;charset=utf-8," + encodeURIComponent(JSON.stringify(this.data));
            let downloadAnchorNode = document.createElement('a');
            downloadAnchorNode.setAttribute("href", data);
            downloadAnchorNode.setAttribute("download", "invoice.json");
            document.body.appendChild(downloadAnchorNode); // required for firefox
            downloadAnchorNode.click();
            downloadAnchorNode.remove();
        },
        download() {
            let element = document.getElementById('content')
            html2pdf().from(element).save('invoice')
        }
    },
    props: {
        data: Object
    }
}
</script>
