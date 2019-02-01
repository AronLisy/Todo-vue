<template>
  <div class="container">
    <div class="row justify-content-center">
      <div
        id="alarmModal"
        class="col-8 col-md-7 col-lg-6 col-xl-4"
        v-show="showModal"
      >
        <h4>Alarm</h4>
        <span id="message">{{ modalText }}</span><br>
        <button id="modalBtn" v-on:click="stopAlarm">ok</button>
      </div>
      <div class="col-12 col-md-10 col-lg-8">
        <app-header
          v-bind:hours="hours"
          v-bind:minutes="minutes"
          v-bind:seconds="seconds"
        ></app-header>
        <div id="navbar" class="row justify-content-center">
          <div
            class="col-3 col-lg-2 item"
            v-on:click="activePage = 'about'"
          >about</div>
          <div
            class="col-3 col-lg-2 item"
            v-on:click="activePage = 'tasks'"
          >tasks</div>
          <div
            class="col-3 col-lg-2 item"
            v-on:click="activePage = 'alarms'"
          >alarms</div>
        </div>
        <keep-alive>
          <component v-bind:is="activePage"
            v-bind:hours="hours"
            v-bind:minutes="minutes"
            v-bind:seconds="seconds"
            v-on:ringAlarm="ringAlarm"
            ></component>
        </keep-alive>
      </div>
    </div>
  </div>


</template>

<script>
import Header from './components/Header.vue';
import About from './components/About.vue';
import Tasks from './components/Tasks.vue';
import Alarms from './components/Alarms.vue';

var snd = new Audio('src/audio/coo-coo-clock-sound.mp3')

export default {
  components: {
    'app-header': Header,
    'about': About,
    'tasks': Tasks,
    'alarms': Alarms
  },

  data() {
    return {
      activePage: 'alarms',
      time: "",
      hours: "",
      minutes: "",
      seconds: "",
      showModal: false,
      modalText: ""
    }
  },

  methods: {
    ringAlarm: function(note) {
      this.modalText = note;
      this.showModal = true;
      snd.load();
      snd.play();
    },

    stopAlarm: function() {
      this.showModal = false;
      snd.pause();
    }
  },

  created() {
  	setInterval(() => {
  		this.time = new Date();
      if (this.time.getHours() < 10) {
        this.hours = "0" + this.time.getHours()
      }
        else {this.hours = this.time.getHours()}

      if (this.time.getMinutes() < 10) {
        this.minutes = "0" + this.time.getMinutes()
      }
        else {this.minutes = this.time.getMinutes()}

      if (this.time.getSeconds() < 10) {
        this.seconds = "0" + this.time.getSeconds()
      }
        else {this.seconds = this.time.getSeconds()}
  	}, 30)
  }
}
</script>

<style>
* {
  font-family: 'Muli';
  font-size: 18px;
}

#content {
  margin-top: 10px;
  margin-bottom: 20px;
  padding: 25px;
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
  margin: 0px;
}

#navbar .item {
  float: left;
  display: block;
  padding: 13px 0px;
  color: #F5F3F2;
  text-decoration: none;
  text-transform: uppercase;
  cursor: pointer;
  font-size: 16px;
  min-width: 60px;
}
#navbar .item:hover {
  background-color: #473B43;
}

h3 {
  font-size: 30px;
  margin-bottom: 50px;
}

h4 {
  font-size: 1rem;
  font-weight: 600;
  margin-bottom: 50px;
  margin-top: -30px;
}

p {
  text-align: left;
  font-size: 0.9rem;
}

.primaryBtn {
  background-color: #6FA198;
  border: solid 1.5px #594A54;
  border-radius: 5px;
  height: 30px;
  width: 120px;
  text-transform: uppercase;
  font-weight: 600;
  font-size: 12px;
  margin: 50px 0px 20px 0px;
  cursor: pointer;
}
.primaryBtn:focus {
  outline: none;
}

#alarmModal {
  position: fixed;
  z-index: 1;
  min-height: 200px;
  background-color: #C2CEC6;
  border: solid #594A54 1.5px;
  border-radius: 25px;
  text-align: center;
  padding: 2%;
  margin: 15% auto;
}

#alarmModal h4 {
  margin: 15px 0px 25px;
}

#message {
  font-size: 20px;
}

#modalBtn {
  background-color: #6FA198;
  border: 0px;
  border-radius: 5px;
  width: 20%;
  height: 35px;
  padding: 0px 0px;
  text-transform: uppercase;
  font-weight: 600;
  font-size: 14px;
  margin-top: 20px;
}

#modalBtn:hover {
  background-color: #5D877F;
  transition: linear 0.2s;
  cursor: pointer;
}

#modalBtn:focus {
  outline: none;
}
</style>
