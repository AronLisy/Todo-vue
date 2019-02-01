<template>
  <div id="content">
    <h3>Alarms</h3>
    <button
      v-on:click="addAlarm"
      class="primaryBtn"
      id="addAlarmBtn"
    >Add alarm</button>
    <div
      id="wrapper"
      class="row justify-content-center"
    >
      <div
        class="alarm col-12 col-sm-10"
        v-for="(alarm, index) in alarms"
        v-bind:key="alarm.id"
      >
        <div class="row justify-content-center">

          <!-- PASIVE STATE -->
          <span
            class="alarmTimeBox col-auto col-md-3 col-xl-2"
            v-show="!alarm.changing"
          >{{ displayHour(index) }}:{{ displayMinute(index)}}:{{ displaySecond(index) }}</span>
          <span
            class="note col-auto col-md-4 col-xl-6"
            v-show="!alarm.changing"
          >{{ alarm.text }}</span>
          <div
            class="col-auto col-md-5 col-xl-4"
            v-show="!alarm.changing"
          >
            <button
              type="button"
              class="changeBtn"
              v-on:click="alarm.changing = true"
            >change</button>
            <button
            type="button"
            class="deleteBtn"
            v-on:click="removeAlarm(index)"
            >delete</button>
          </div>

          <!-- ACTIVE STATE -->
          <div
            class="timeOptions col-auto col-sm-6 col-md-5 col-lg-auto"
            v-show="alarm.changing"
          >
              <select
                class="hour"
                v-model="alarm.hour"
              >
                <option v-for="u in time.hours">{{ u }}</option>
              </select>
              <select
                class="minute"
                v-model="alarm.minute"
              >
                <option v-for="u in time.minutes">{{ u }}</option>
              </select>
              <select
                class="second"
                v-model="alarm.second"
              >
                <option v-for="u in time.seconds">{{ u }}</option>
              </select>
          </div>
          <div
            class="col-12 col-sm-6 col-md-7 col-lg-auto"
            v-show="alarm.changing"
          >
            <input
              type="text"
              class="noteInput"
              placeholder="Note..."
              v-model="alarm.text"
            >
          </div>
          <div
            class="col-auto"
            v-show="alarm.changing"
          >
            <button
              type="button"
              class="saveBtn"
              v-on:click="alarm.changing = false"
            >save</button>
          </div>
        </div>
      </div>
    </div>
    <button class="primaryBtn" v-on:click="showInfo=!showInfo">info</button>
    <div v-show="showInfo">
      <p>This is an alarm list. By default there are no alarms.</p>
      <p>By clicking ADD NEW ALARM button, you can add as many alarms you like. After creating new alarm, set hours, minutes and seconds. You can also add a message into input field. For example: "Take a break!" or "Get back to work!"</p>
      <p>When the time is up, you will recieve message you wrote previously in a window and alarm sound will ring.</p>
    </div>
  </div>
</template>

<script>

export default {
  data() {
    return {
      alarms: [
        {
          id: 1,
          hour: 0,
          minute: 0,
          second: 0,
          text: "",
          changing: true
        }
      ],

      nextAlarmId: 2,

      showInfo: false,

      time: {
        hours: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23],
        minutes: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59],
        seconds: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59]
      }
    }
  },

  props: [
    'hours',
    'minutes',
    'seconds'
  ],

  methods: {
    displayHour: function(i) {
        if (this.alarms[i].hour < 10){
          return "0" + this.alarms[i].hour;
        }
        else {
          return this.alarms[i].hour;
        }
    },
    displayMinute: function(i) {
      if (this.alarms[i].minute < 10){
        return "0" + this.alarms[i].minute;
      }
        else {
          return this.alarms[i].minute;
        }
    },
    displaySecond: function(i) {
      if (this.alarms[i].second < 10){
        return "0" + this.alarms[i].second;
      }
        else {
          return this.alarms[i].second;
        }
    },

    addAlarm: function() {
      this.alarms.push({
        id: this.nextAlarmId++,
        hour: 0,
        minute: 0,
        second: 0,
        text: "",
        changing: true
      })
    },

    removeAlarm: function(i) {
      this.alarms.splice(i, 1);
    }
  },

  created() {
    setInterval(() => {
      for (var i in this.alarms) {
        if (
          this.hours == this.alarms[i].hour &&
          this.minutes == this.alarms[i].minute &&
          this.seconds == this.alarms[i].second
        ) {
          this.$emit('ringAlarm', this.alarms[i].text);
        }
      }
    }, 1000)
  }
}
</script>

<style scoped>
#addAlarmBtn {
  height: 35px;
  width: 160px;
  font-size: 14px;
  margin-top: 0px;
  margin-bottom: 30px;
}

.alarm {
  padding: 6px 5% 6px 5%;
  border: solid #594A54 2px;
  border-radius: 21px;
  background-color: #C2CEC6;
  min-height: 42px;
  margin-bottom: 8px;
  overflow: hidden;
}

.alarmTimeBox {
  font-weight: bold;
  text-align: center;
}

.note {
  /* text-align: center; */
}

.timeOptions select {
  height: 26px;
  border-radius: 5px;
  background-color: #F5F3F2;
  margin: 2px 0px;
}

.noteInput {
  border: solid 1px;
  border-color:rgb(169, 169, 169);
  border-radius: 5px;
  background-color: #F5F3F2;
  height: 27px;
  width: 100%;
  padding: 6px;
  margin: 2px;
}

.alarm button {
  background-color: #C2CEC6;
  border: 0px;
  border-radius: 5px;
  height: 26px;
  padding: 0px 5px;
  margin: 2px;
  color: #594A54;
  text-transform: uppercase;
  font-weight: 600;
  font-size: 14px;
}
.alarm button:hover {
  background-color: #6FA198;
  transition: linear 0.2s;
  cursor: pointer;
}
.alarm button:focus {
  outline: none;
}

.alarm .deleteBtn:hover {
  background-color: #C46666;
}
</style>
