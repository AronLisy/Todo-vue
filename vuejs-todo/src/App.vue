<template>
  <div class="container">
    <div class="row justify-content-center">
      <div class="col-12 col-md-10 col-lg-8">
        <app-header></app-header>
        <div id="navbar">
          <ul>
            <li v-for="(item, index) in items" v-on:click="changePage(index)">{{item}}</li>
          </ul>
        </div>
        <component v-bind:is="activePage"></component>
      </div>
    </div>
  </div>


</template>

<script>
import Header from './components/Header.vue';
import About from './components/About.vue';
import Tasks from './components/Tasks.vue';
import Alarms from './components/Alarms.vue';

export default {
  components: {
    'app-header': Header,
    'about': About,
    'tasks': Tasks,
    'alarms': Alarms
  },

  data() {
    return {
      activePage: 'tasks',
      items: ['about', 'tasks', 'alarms']
    }
  },

  methods: {
    changePage: function(index) {
      this.activePage = this.items[index]
    }
  }
}
</script>

<style>
* {
  font-family: 'Muli';
}

#content {
  margin-top: 10px;
  margin-bottom: 20px;
  padding: 60px;
  min-height: 700px;
  background-color: #E7E1E0;
  border-radius: 25px;
  text-align: center;
}

#navbar {
  background-color: #594A54;
  height: 50px;
  border-radius: 25px;
  text-align: center;
}

#navbar ul {
  list-style-type: none;
  margin: auto;
  display: inline-block;
  padding: 0px;
}
#navbar ul li {
  float: left;
  display: block;
  padding: 13px 40px;
  color: #F5F3F2;
  text-decoration: none;
  text-transform: uppercase;
  cursor: pointer;
}
#navbar ul li:hover {
  background-color: #473B43;
}
</style>
