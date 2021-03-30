<template>
  <div class="wrapper">
    <div class="details">
      <h2>Person Details</h2>
      <p>Name: {{person.name}}</p>
      <p>Age: {{person.age}}</p>
      <p>Siblings:</p>
      <ul v-if="person.siblings.length">
        <li v-bind:key="sibling" v-for="sibling in person.siblings">{{sibling}}</li>
      </ul>
      <p>Status: {{ person.active ? 'Yes' : 'No'}}</p>
    </div>

    <strong class="msg">Person schema check passed!</strong>
  </div>
  
</template>

<script>

export default {
  name: 'PersonDetails',
  props: {
    person: Object,
  }, 
  methods: {
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .wrapper {
    padding: 10px;
    border: 1px solid #ddd;
    width: 300px;
    margin: 0 auto;
  }
  .details { 
    margin-bottom: 30px;
    border-bottom: 1px solid #ddd;
  }
  .msg {
    color: green;
  }
</style>
