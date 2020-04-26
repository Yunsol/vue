<template>
  <v-container fluid>
    <v-toolbar-title>
          자주 사용하는 정규식
    </v-toolbar-title>
  <v-row align="center">
    <v-expansion-panels
      :multiple="multiple"
      :focusable="focusable"
    >
      <v-expansion-panel v-for="item in items" :key="item">
        <v-expansion-panel-header>{{ item.header }}</v-expansion-panel-header>
        <v-expansion-panel-content>{{ item.value }}</v-expansion-panel-content>
      </v-expansion-panel>
    </v-expansion-panels>
  </v-row>
  </v-container>
</template>

<script>
export default {
  name: 'RegExListViewer',
  data: () => ({
    multiple: true,
    focusable: true,
    items: [
      { header: '이메일', value: '/^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,6}$/' },
      { header: '한국 전화번호', value: '/^[0-9]{3}[-]+[0-9]{4}[-]+[0-9]{4}$/' },
      { header: '핸드폰번호', value: '/^01([016789]?)-?([0-9]{3,4})-?([0-9]{4})$/' },
      { header: '숫자3자리 콤마', value: '/\\B(?=(\\d{3})+(?!\\d))/' }
    ]
  })
}
</script>
