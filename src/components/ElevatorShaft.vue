<template>
  <div class="wrapper">
    <div class="elevator-shaft">
  <div v-bind:class="'elevator-doors elevator-doors'+this.currFloor">
  </div>
    </div>
    <div class="floors">
      <div class="floor">
        <input type="button" v-on:click="setFloor(5)" value="5"/>
      </div>
      <div class="floor">
        <input type="button" v-on:click="setFloor(4)"  value="4"/>
      </div>
      <div class="floor">
        <input type="button" v-on:click="setFloor(3)"  value="3"/>
      </div>
      <div class="floor">
        <input type="button" v-on:click="setFloor(2)"  value="2"/>
      </div>
      <div class="floor">
        <input type="button" v-on:click="setFloor(1)"  value="1"/>
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
          },2000)
        }}, 3000);
      setInterval(() => {
        if (this.currFloor < this.followingFloor) {
          this.upfloor();
          }
        if (this.currFloor > this.followingFloor) {
          this.downfloor();
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
</style>
