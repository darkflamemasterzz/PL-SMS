<template>
  <div id="app">
    <Header></Header>
    <OutcomeList></OutcomeList>
  </div>
</template>

<script>
import OutcomeList from './components/outcome/outcomeList'
import Header from './components/header'

export default {
  name: 'App',
  components: {
    OutcomeList,
    Header
  }
}
</script>

<style>

</style>
