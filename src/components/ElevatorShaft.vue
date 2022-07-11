<template>
  <div class="wrapper">
    <div class="elevator-shaft">
  <div v-bind:class="this.wait+' elevator-doors elevator-doors'+this.currFloor">
    <p><strong>{{currFloor}} {{direction}}</strong></p>
  </div>
    </div>
    <div class="floors">
      <div class="floor">
        <input type="button" class="btn" v-on:click="setFloor(5)" value="5"/>
      </div>
      <div class="floor">
        <input type="button" class="btn" v-on:click="setFloor(4)"  value="4"/>
      </div>
      <div class="floor">
        <input type="button" class="btn" v-on:click="setFloor(3)"  value="3"/>
      </div>
      <div class="floor">
        <input type="button" class="btn" v-on:click="setFloor(2)"  value="2"/>
      </div>
      <div class="floor">
        <input type="button" class="btn" v-on:click="setFloor(1)"  value="1"/>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ElevatorShaft',
  data() {
    return {
      direction: null,
      timer: null,
      floor: [],
      followingFloor: 1,
      currFloor : 1,
      wait: "",
    }
  },
  methods: {
    start() {
      if (this.timer) {
        return;
      }
      this.timer = setTimeout(() => {
      setInterval(() => {
        if (this.currFloor === this.followingFloor) {
          setTimeout(() => {
            this.nextFloor();
          },3000)
          this.wait = "wait"
          this.direction = ""
        }}, 4000);
      setInterval(() => {
        if (this.currFloor < this.followingFloor) {
          this.upfloor();
          this.wait = ""
          this.direction = "↑"
          }
        if (this.currFloor > this.followingFloor) {
          this.downfloor();
          this.wait = ""
          this.direction = "↓"
          }
      }, 1000)
    }, 1000);
  },
    setFloor(num) {
      this.floor.push(num);
      this.start();
    },
    nextFloor() {
      if (this.floor.length) {
        this.followingFloor = this.floor.shift();
        console.log ("Движемся на " + this.followingFloor + " этаж");
      }
    },
    upfloor() {
      if (this.currFloor < this.followingFloor) {
        this.currFloor += 1;
        console.log(this.currFloor)
      }
    },
    downfloor() {
      if (this.currFloor > this.followingFloor) {
        this.currFloor -= 1;
        console.log(this.currFloor)
      }
    },
  }
  }
</script>

<style scoped>
.wrapper {
  display: flex;
  flex-direction: row
}

.btn{
  display:block;
  height: 20px;
  width: 20px;
  border-radius: 50%;
  padding: 0;
}

.floors {
  width: 100vh;
  display: flex;
  flex-direction: column;
}
.floor {
  width: 100vh;
  height: 100px;
  border: 0.5px solid rgb(158, 158, 158);
  display: flex;
  flex-wrap: wrap;
  align-content: center;
}
.floor input {
  margin-left: 20px;
}

.elevator-doors {
  width: 100px;
  height: 100px;
  background: #cdcbcd;
  border: 0.5px solid rgb(158, 158, 158);
  position: sticky;
  transition-duration: 1s;
  text-align: center;
}

.elevator-doors1 {
transform: translate(0,406px);
}

.elevator-doors2 {
transform: translate(0,305px);
}

.elevator-doors3 {
transform: translate(0,203px);
}

.elevator-doors4 {
transform: translate(0,101px);
}

.elevator-doors5 {
transform: translate(0,0px);
}
.elevator-shaft {
  border: 0.5px solid rgb(158, 158, 158);
}

.wait {
  animation-name: blink;
  animation-timing-function: linear;
  animation-duration: 1.5s;
  animation-iteration-count: infinite;
}

@keyframes blink {
  50% {
    opacity: 50%;
    background-color: greenyellow;
  }
}
</style>
