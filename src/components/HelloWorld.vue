<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12">
        <h2 class="text-left">Test REST-API</h2>
      </v-col>
    </v-row>
    <v-row class="text-center">
      <v-col cols="6">
        <h4 class="text-left">Enter a URL</h4>
      </v-col>
      <v-col cols="6">
        <h4 class="text-left">Choose Request-Method</h4>
      </v-col>
    </v-row>
    <v-row class="text-center">
      <v-col cols="6">
        <v-text-field type="text" label="URL" v-model="url"/>
      </v-col>
      <v-col cols="6">
        <v-select :items="methods" v-model="method" label="Request-Method"/>
      </v-col>
    </v-row>
    <v-row class="text-center">
      <v-col cols="12">
        <h4 class="text-left">Enter JSON-Body</h4>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12">
        <v-textarea type="text" label="JSON" v-model="json"/>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12">
        <v-btn class="float-right" color="primary" type="submit" @click="doRequest">do request</v-btn>
      </v-col>
    </v-row>
    <v-row class="text-center">
      <v-col cols="12">
        <h4 class="text-left">Response</h4>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12">
        <span>{{response}}</span>
      </v-col>
    </v-row>
  </v-container>
</template>

<script lang="ts">
import Vue from 'vue'
import axios, { AxiosResponse } from 'axios'

export default Vue.extend({
  name: 'HelloWorld',

  data: () => ({
    url: '',
    json: '',
    method: '',
    methods: ['GET', 'POST', 'PUT', 'DELETE'],
    response: ''
  }),

  methods: {
    doRequest: function () {
      if (this.method === 'GET') {
        axios.get(this.url).then((response: AxiosResponse) => {
          this.response = response.data
        })
      } else if (this.method === 'POST') {
        axios.post(this.url, this.json, { headers: { 'Content-Type': 'application/json' } }).then((response: AxiosResponse) => {
          this.response = response.data
        })
      } else if (this.method === 'PUT') {
        axios.put(this.url, this.json, { headers: { 'Content-Type': 'application/json' } }).then((response: AxiosResponse) => {
          this.response = response.data
        })
      } else {
        axios.delete(this.url, { headers: { 'Content-Type': 'application/json' } }).then((response: AxiosResponse) => {
          this.response = response.data
        })
      }
    }
  }
})
</script>
