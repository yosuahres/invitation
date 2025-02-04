<template>
  <div class="game-container">
    <div v-if="showWelcomePage">
      <div class="welcome-page">
        <h1>BUKA DI LAPTOP KARENA TIDAK RESPONSIF</h1>
        <button @click="goToGamePage">PENCET BOS</button>
      </div>
    </div>
    <div v-else>
      <div class="explosion" v-if="showExplosion" :style="explosionStyle"></div>
      <div v-if="!showBirthdayMessage">
        <div class="game-area">
          <div class="character" :style="characterStyle">
            <div class="head"></div>
            <div class="body"></div>
            <div class="left-arm"></div>
            <div class="right-arm"></div>
            <div class="left-leg"></div>
            <div class="right-leg"></div>
          </div>
          <div class="door" :style="doorStyle"></div>
          <div class="sign" :style="signStyle">MASUK SINI</div>
          <div class="house" style="left: 100px; top: 100px;">
            <div class="house-roof"></div>
            <div class="house-body">
              <div class="house-window left"></div>
              <div class="house-window right"></div>
              <div class="house-door"></div>
            </div>
          </div>
          <div class="house" style="left: 300px; top: 100px;">
            <div class="house-roof"></div>
            <div class="house-body">
              <div class="house-window left"></div>
              <div class="house-window right"></div>
              <div class="house-door"></div>
            </div>
          </div>
          <div class="house" style="left: 500px; top: 100px;">
            <div class="house-roof"></div>
            <div class="house-body">
              <div class="house-window left"></div>
              <div class="house-window right"></div>
              <div class="house-door"></div>
            </div>
          </div>
          <div class="house" style="left: 700px; top: 100px;">
            <div class="house-roof"></div>
            <div class="house-body">
              <div class="house-window left"></div>
              <div class="house-window right"></div>
              <div class="house-door"></div>
            </div>
          </div>
          <div class="house" style="left: 900px; top: 100px;">
            <div class="house-roof"></div>
            <div class="house-body">
              <div class="house-window left"></div>
              <div class="house-window right"></div>
              <div class="house-door"></div>
            </div>
          </div>
          <div class="house" style="left: 1100px; top: 100px;">
            <div class="house-roof"></div>
            <div class="house-body">
              <div class="house-window left"></div>
              <div class="house-window right"></div>
              <div class="house-door"></div>
            </div>
          </div>
          <div class="house" style="left: 1300px; top: 100px;">
            <div class="house-roof"></div>
            <div class="house-body">
              <div class="house-window left"></div>
              <div class="house-window right"></div>
              <div class="house-door"></div>
            </div>
          </div>
          <div class="tree" style="left: 150px; top: 200px;"></div>
          <div class="tree" style="left: 350px; top: 200px;"></div>
          <div class="tree" style="left: 550px; top: 200px;"></div>
          <div class="tree" style="left: 750px; top: 200px;"></div>
          <div class="tree" style="left: 950px; top: 200px;"></div>
          <div class="tree" style="left: 1150px; top: 200px;"></div>
          <div class="tree" style="left: 1350px; top: 200px;"></div>
          <div class="river"></div>
          <div class="fence" style="left: 495px; top: 295px;"></div>
          <div class="instructions">PAKAI ARROW BUAT GERAK || TEKAN A MELEDAK</div>
        </div>
      </div>
      <div v-else>
        <div v-if="showInvitationMessage" class="invitation-card">
          <h1>Would you go out with me on 14th February to celebrate your birthdayyyy?</h1>
          <p>Place: Societte</p>
          <p>Time: 19.00</p>
          <button @click="handleYesClick">Yes</button>
          <button v-if="showNoButton" @click="handleNoClick" :class="{ 'crack-animation': !showNoButton }">No</button>
        </div>
        <div v-else class="invitation-card">
          <h1>I'll pick you up! Love you</h1>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'GameAnimation',
  data() {
    return {
      showWelcomePage: true,
      characterPosition: { x: 50, y: 50 },
      doorPosition: { x: 1300, y: 600 },
      characterSize: { width: 40, height: 80 },
      doorSize: { width: 60, height: 80 },
      showBirthdayMessage: false,
      showExplosion: false,
      explosionPosition: { x: 0, y: 0 },
      explosionSize: { width: 100, height: 100 },
      showInvitationMessage: true,
      showNoButton: true
    };
  },
  computed: {
    characterStyle() {
      return {
        left: `${this.characterPosition.x}px`,
        top: `${this.characterPosition.y}px`,
        width: `${this.characterSize.width}px`,
        height: `${this.characterSize.height}px`,
        position: 'absolute'
      };
    },
    doorStyle() {
      return {
        left: `${this.doorPosition.x}px`,
        top: `${this.doorPosition.y}px`,
        width: `${this.doorSize.width}px`,
        height: `${this.doorSize.height}px`
      };
    },
    explosionStyle() {
      return {
        left: `${this.explosionPosition.x}px`,
        top: `${this.explosionPosition.y}px`,
        width: `${this.explosionSize.width}px`,
        height: `${this.explosionSize.height}px`,
        position: 'absolute',
        backgroundColor: 'red',
        borderRadius: '50%',
        opacity: 0.8
      };
    },
    signStyle() {
      return {
        left: `${this.doorPosition.x + this.doorSize.width / 2 - 50}px`,
        top: `${this.doorPosition.y - 30}px`,
        width: '100px',
        height: '30px',
        textAlign: 'center',
        lineHeight: '30px',
        backgroundColor: 'yellow',
        border: '1px solid black',
        position: 'absolute'
      };
    }
  },
  mounted() {
    window.addEventListener('keydown', this.handleKeyDown);
  },
  beforeUnmount() {
    window.removeEventListener('keydown', this.handleKeyDown);
  },
  methods: {
    goToGamePage() {
      this.showWelcomePage = false;
    },
    handleKeyDown(event) {
      const step = 10;
      switch (event.key) {
        case 'ArrowUp':
          this.characterPosition.y -= step;
          break;
        case 'ArrowDown':
          this.characterPosition.y += step;
          break;
        case 'ArrowLeft':
          this.characterPosition.x -= step;
          break;
        case 'ArrowRight':
          this.characterPosition.x += step;
          break;
        case 'a':
        case 'A':
          this.triggerExplosion();
          break;
      }
      this.checkCollision();
    },
    triggerExplosion() {
      this.explosionPosition = { ...this.characterPosition };
      this.showExplosion = true;
      setTimeout(() => {
        this.showExplosion = false;
      }, 500); // Explosion lasts for 500ms
    },
    checkCollision() {
      const char = this.characterPosition;
      const door = this.doorPosition;
      if (
        char.x < door.x + this.doorSize.width &&
        char.x + this.characterSize.width > door.x &&
        char.y < door.y + this.doorSize.height &&
        char.y + this.characterSize.height > door.y
      ) {
        this.showBirthdayMessage = true;
      }
    },
    handleYesClick() {
      this.showInvitationMessage = false;
    },
    handleNoClick() {
      this.showNoButton = false;
    }
  }
};
</script>

<style scoped>
.explosion {
  position: absolute;
  background-color: red;
  border-radius: 50%;
  opacity: 0.8;
  transition: opacity 0.5s ease-out;
}

.game-container {
  position: relative;
  width: 100%;
  height: 100vh;
  overflow: hidden;
}

.welcome-page {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
  text-align: center;
}

.welcome-page h1 {
  font-size: 2em;
  margin-bottom: 20px;
}

.welcome-page button {
  padding: 10px 20px;
  font-size: 1em;
  cursor: pointer;
}

.game-area {
  position: relative;
  width: 100%;
  height: 100%;
}

.character {
  position: absolute;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.character .head {
  width: 20px;
  height: 20px;
  background-color: #ffcc99;
  border-radius: 50%;
}

.character .body {
  width: 10px;
  height: 30px;
  background-color: blue;
}

.character .left-arm,
.character .right-arm {
  width: 10px;
  height: 20px;
  background-color: blue;
  position: absolute;
  top: 20px;
}

.character .left-arm {
  left: -10px;
}

.character .right-arm {
  right: -10px;
}

.character .left-leg,
.character .right-leg {
  width: 10px;
  height: 20px;
  background-color: blue;
  position: absolute;
  top: 50px;
}

.character .left-leg {
  left: -5px;
}

.character .right-leg {
  right: -5px;
}

.door {
  position: absolute;
  background-color: brown;
}

.sign {
  position: absolute;
  background-color: yellow;
  border: 1px solid black;
  text-align: center;
  line-height: 30px;
}

.house {
  position: absolute;
  width: 100px;
  height: 100px;
}

.house-roof {
  position: absolute;
  width: 0;
  height: 0;
  border-left: 50px solid transparent;
  border-right: 50px solid transparent;
  border-bottom: 50px solid #8b4513;
  top: -50px;
  left: 0;
}

.house-body {
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: #8b4513; /* House color */
  border: 2px solid #654321;
}

.house-window {
  position: absolute;
  width: 20px;
  height: 20px;
  background-color: #ffffff;
  border: 2px solid #000000;
}

.house-window.left {
  left: 10px;
  top: 20px;
}

.house-window.right {
  right: 10px;
  top: 20px;
}

.house-door {
  position: absolute;
  width: 30px;
  height: 50px;
  background-color: #654321;
  border: 2px solid #000000;
  bottom: 0;
  left: 35px;
}

.tree {
  position: absolute;
  width: 40px;
  height: 60px;
  background-color: #228b22;
  border-radius: 20px 20px 0 0;
}

.tree::before {
  content: '';
  position: absolute;
  bottom: -20px;
  left: 15px;
  width: 10px;
  height: 20px;
  background-color: #8b4513;
}

.river {
  position: absolute;
  width: 100px;
  height: 100px;
  background-color: #1e90ff; /* River color */
  top: 300px;
  left: 500px;
}

.fence {
  position: absolute;
  width: 110px;
  height: 110px;
  border: 5px solid #8b4513; /* Fence color */
  top: 295px;
  left: 495px;
  box-sizing: border-box;
}

.invitation-card {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
  font-size: 2em;
  color: #42b983;
  text-align: center;
  background-color: #f0f8ff;
  border: 2px solid #42b983;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.invitation-card h1 {
  font-size: 2.5em;
  margin-bottom: 20px;
}

.invitation-card p {
  font-size: 1.5em;
  margin: 10px 0;
}

.invitation-card button {
  padding: 10px 20px;
  font-size: 1em;
  cursor: pointer;
  margin: 10px;
}

.crack-animation {
  animation: crack 0.5s forwards;
}

@keyframes crack {
  0% {
    transform: scale(1);
    opacity: 1;
  }
  50% {
    transform: scale(1.2) rotate(10deg);
    opacity: 0.5;
  }
  100% {
    transform: scale(0.5) rotate(-10deg);
    opacity: 0;
  }
}

.instructions {
  position: absolute;
  top: 10px;
  left: 10px;
  font-size: 1.5em;
  color: red;
}
</style>