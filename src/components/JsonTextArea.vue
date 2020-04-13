<template>
  <v-container fluid>
    <v-app-bar fluid>
      <v-toolbar-title>
        JSON Lint
      </v-toolbar-title>
      <v-spacer>
      </v-spacer>
      <v-btn icon>
        <v-icon>mdi-eye</v-icon>
      </v-btn>
    </v-app-bar>
    <v-card-text>
      <v-textarea v-model="text" :auto-grow="autoGrow"></v-textarea>
    </v-card-text>
    <v-card-actions>
      <v-spacer></v-spacer>
      <v-btn @click="validate" >validate</v-btn>
    </v-card-actions>
    <v-alert type="error" :value="errorDisplay">
      {{errorText}}
    </v-alert>
</v-container>
</template>

<script>
export default {
  name: 'JsonTextArea',
  data: () => ({
    text: '',
    autoGrow: true,
    errorText: '',
    errorDisplay: false
  }),
  methods: {
    validate () {
      const jsonDataVal = this.text
      try {
        const jsonData = JSON.parse(jsonDataVal)
        this.text = JSON.stringify(jsonData, undefined, 4)
        this.errorDisplay = false
      } catch (e) {
        console.error(e)
        this.errorText = e
        this.errorDisplay = true
      }
    }
  }
}
</script>
