<template>
  <v-container fluid>
    <v-app-bar fluid>
      <v-toolbar-title>
        RegEx
      </v-toolbar-title>
      <v-spacer>
      </v-spacer>
    </v-app-bar>
        <v-toolbar
          dark
          color="blue darken-3"
          class="mb-1"
        >
          <span class="title">/</span>
          <v-text-field
            v-model="pattern"
            clearable
            flat
            solo-inverted
            hide-details
            @input="findPattern"
            @click:clear="findPattern"
          ></v-text-field>
            <span class="title">/</span>
            <v-spacer></v-spacer>
            <v-select
              v-model="typeBy"
              flat
              hide-details
              :items="types"
              @change="changeType"
            ></v-select>
        </v-toolbar>
    <v-card-text>
      <v-textarea v-model="text" :auto-grow="autoGrow" @input="fillText"></v-textarea>
    </v-card-text>
    <v-card-actions>
      <v-spacer></v-spacer>
    </v-card-actions>
    <pre v-html="resultHtml"></pre>
</v-container>
</template>

<script>
export default {
  name: 'RegExCheckEditor',
  data: () => ({
    text: '',
    pattern: '',
    autoGrow: true,
    resultHtml: '',
    errorDisplay: false,
    typeBy: 'g',
    types: [
      'g',
      'i',
      'm',
      's',
      'u',
      'y'
    ]
  }),
  methods: {
    changePattern () {
      var re = new RegExp(this.pattern, this.typeBy)
      var matchArray
      var resultString = ''
      var first = 0
      var last = 0
      var data = this.text

      // 각각의 일치하는 부분 검색
      while ((matchArray = re.exec(data)) != null) {
        last = matchArray.index

        // 일치하는 모든 문자열을 연결
        resultString += data.substring(first, last)

        // 일치하는 부분에 강조 스타일이 지정된 class 추가
        resultString += '<span class="lime accent-2">' + matchArray[0] + '</span>'
        first = re.lastIndex
        // RegExp객체의 lastIndex속성을 이용해 검색 결과의 마지막인덱스 접근 가능
      }

      // 문자열 종료
      resultString += data.substring(first, data.length)
      this.resultHtml = resultString
    },
    findPattern (data) {
      this.pattern = data
      if (this.pattern.length > 0 && this.text.length > 0) {
        this.changePattern()
      } else {
        this.resultHtml = this.text
      }
    },
    changeType (data) {
      this.typeBy = data
    },
    fillText (data) {
      this.text = data
      this.resultHtml = data

      if (this.pattern.length > 0 && this.text.length > 0) {
        this.changePattern()
      }
    }
  }
}
</script>
