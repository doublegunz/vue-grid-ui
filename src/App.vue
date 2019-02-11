<template>
  <div id="app">
    <Grid :style="{height: '450px' }"
          :data-items="result"
          :columns="columns"
          :pageable="true"
          :skip="skip"
          :take="take"
          :total="total"
          @pagechange="pageChange">
    </Grid>

  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'app',
  data () {
    return {
      dataItems:[],
      skip: 0,
      take: 10,
      columns: [
        { field: 'name'},
        { field: 'surname'},
        { field: 'gender'},
        { field: 'region'}
      ],

    };
  },
  computed: {
    result () {
      return this.dataItems.slice(this.skip, this.take + this.skip)
    },
    total () {
      return this.dataItems.length
    }
  },
  mounted () {
    axios
      .get('https://uinames.com/api/?amount=25')
      .then(response => {
        this.dataItems = response.data
      })
  },
  methods: {
    pageChange(event) {
      this.skip = event.page.skip;
      this.take = event.page.take;
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
