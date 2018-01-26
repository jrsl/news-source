<template>
  <div class="source-selection">
    <div class="jumbotron">
      <h2><span class="glyphicon glyphicon-list-alt"></span> News list</h2>
      <h3>Select News source</h3>
      <select class="form-control" v-on:change="sourceChanged">
        <option v-bind:value="source.id" v-for="source in sources">{{source.name}}</option>
      </select>
      <div v-if="source">
        <p>{{source.description}}</p>
        <a v-bin:href="source.url" class="btn btn-primary" target="_blank">Go to {{source.name}} Website</a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SourceSelection',
  data () {
    return {
      sources: [],
      source: ''
    }
  },
  methods: {
    sourceChanged: function (e) {
      for(var i=0; i < this.sources.length; i++){
        if(this.sources[i].id == e.target.value){
          this.source = this.sources[i]
        }
      }
      this.$emit('sourceChanged', e.target.value)
    }
  },
  created () {
    this.$http.get('https://newsapi.org/v1/sources?language=en')
      .then(response => {
        this.sources = response.data.sources
      })
  }
}
</script>

<style scoped>
</style>
