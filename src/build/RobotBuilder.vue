<template>
      <div>
        <div class="top-row">
          <div class="top part">
            <div class="robot-name">
                {{ selectedRobot.head.title }}
                <span v-if="selectedRobot.head.onSale" class="sale">Sale!</span>

            </div>
            <img :src="selectedRobot.head.src" title="head"/>
            <button @click="selectPreviousHead()" class="prev-selector">&#9668;</button>
            <button @click="selectNextHead()" class="next-selector">&#9658;</button>
          </div>
        </div>
        <div class="middle-row">
          <div class="left part">
            <img :src="selectedRobot.leftArm.src" title="left arm"/>
            <button @click="selectNextLeftArm()" class="prev-selector">&#9650;</button>
            <button @click="selectPreviousLeftArm()" class="next-selector">&#9660;</button>
          </div>
          <div class="center part">
            <img :src="selectedRobot.torso.src" title="left arm"/>
            <button @click="selectNextTorsos()" class="prev-selector">&#9668;</button>
            <button @click="selectPreviousTorsos()" class="next-selector">&#9658;</button>
          </div>
          <div class="right part">
            <img :src="selectedRobot.rightArm.src" title="left arm"/>
            <button @click="selectNextRightArm()" class="prev-selector">&#9650;</button>
            <button @click="selectPreviousRightArm()" class="next-selector">&#9660;</button>
          </div>
        </div>
        <div class="bottom-row">
          <div class="bottom part">
            <img :src="selectedRobot.base.src" title="left arm"/>
            <button @click="selectNextBase()" class="prev-selector">&#9668;</button>
            <button @click="selectPreviousBase()" class="next-selector">&#9658;</button>
          </div>
        </div>
      </div>

</template>

<script>
import availableParts from '../data/parts';

function getPreviousValidIndex(index, length) {
  const deprecatedIndex = index - 1;
  return deprecatedIndex < 0 ? length - 1 : deprecatedIndex;
}
function getNextValidIndex(index, length) {
  const incrementedIndex = index + 1;
  return incrementedIndex > length - 1 ? 0 : incrementedIndex;
}

export default {
  name: 'RobotBuilder',
  data() {
    return {
      availableParts,
      selectedHeadIndex: 0,
      selectedArmIndex: 0,
      selectedTorsoIndex: 0,
      selectedRightArmIndex: 0,
      selectedBasesIndex: 0,
    };
  },
  computed: {
    selectedRobot() {
      return {
        head: availableParts.heads[this.selectedHeadIndex],
        leftArm: availableParts.arms[this.selectedArmIndex],
        torso: availableParts.torsos[this.selectedTorsoIndex],
        rightArm: availableParts.arms[this.selectedRightArmIndex],
        base: availableParts.bases[this.selectedBasesIndex],
      };
    },
  },
  methods: {
    selectNextHead() {
      this.selectedHeadIndex = getNextValidIndex(
        this.selectedHeadIndex,
        availableParts.heads.length,
      );
    },
    selectPreviousHead() {
      this.selectedHeadIndex = getPreviousValidIndex(
        this.selectedHeadIndex,
        availableParts.heads.length,
      );
    },
    selectNextLeftArm() {
      this.selectedArmIndex = getNextValidIndex(
        this.selectedArmIndex,
        availableParts.arms.length,
      );
    },
    selectPreviousLeftArm() {
      this.selectedArmIndex = getPreviousValidIndex(
        this.selectedArmIndex,
        availableParts.arms.length,
      );
    },
    selectNextTorsos() {
      this.selectedTorsoIndex = getNextValidIndex(
        this.selectedTorsoIndex,
        availableParts.torsos.length,
      );
    },
    selectPreviousTorsos() {
      this.selectedTorsoIndex = getPreviousValidIndex(
        this.selectedTorsoIndex,
        availableParts.torsos.length,
      );
    },
    selectNextRightArm() {
      this.selectedRightArmIndex = getNextValidIndex(
        this.selectedRightArmIndex,
        availableParts.arms.length,
      );
    },
    selectPreviousRightArm() {
      this.selectedRightArmIndex = getPreviousValidIndex(
        this.selectedRightArmIndex,
        availableParts.arms.length,
      );
    },
    selectNextBase() {
      this.selectedBasesIndex = getNextValidIndex(
        this.selectedBasesIndex,
        availableParts.bases.length,
      );
    },
    selectPreviousBase() {
      this.selectedBasesIndex = getPreviousValidIndex(
        this.selectedBasesIndex,
        availableParts.bases.length,
      );
    },
  },
};
</script>

<style>
.part {
  position: relative;
  width:165px;
  height:165px;
  border: 3px solid #aaa;
}
.part img {
  width:165px;
}
.top-row {
  display:flex;
  justify-content: space-around;
}
.middle-row {
  display:flex;
  justify-content: center;
}
.bottom-row {
  display:flex;
  justify-content: space-around;
  border-top: none;
}
.head {
  border-bottom: none;
}
.left {
  border-right: none;
}
.right {
  border-left: none;
}
.left img {
  transform: rotate(-90deg);
}
.right img {
  transform: rotate(90deg);
}
.bottom {
  border-top: none;
}
.prev-selector {
  position: absolute;
  z-index:1;
  top: -3px;
  left: -28px;
  width: 25px;
  height: 171px;
}
.next-selector {
  position: absolute;
  z-index:1;
  top: -3px;
  right: -28px;
  width: 25px;
  height: 171px;
}
.center .prev-selector, .center .next-selector {
  opacity:0.8;
}
.left .prev-selector {
  top: -28px;
  left: -3px;
  width: 144px;
  height: 25px;
}
.left .next-selector {
  top: auto;
  bottom: -28px;
  left: -3px;
  width: 144px;
  height: 25px;
}
.right .prev-selector {
  top: -28px;
  left: 24px;
  width: 144px;
  height: 25px;
}
.right .next-selector {
  top: auto;
  bottom: -28px;
  left: 24px;
  width: 144px;
  height: 25px;
}
.right .next-selector {
  right: -3px;
}
.robot-name {
position: absolute;
top: -25px;
text-align: center;
width: 100%;
}
.sale {
color: red;
}
</style>
