<template>
  <div id="app">
    <h1>Дневник тренировок</h1>
    <div class="buttonsWrapper">
      <Button v-for="(day, index) in days" :title="day" :key="index" :isActive="index === activeButton" :onClick="() => onButtonClick(index)" />
    </div>
    <TrainingTable :data="tableData[activeButton]" :onAddRow="onAddRow" :onCellChange="onCellChange"/>
  </div>
</template>

<script>
import '@/assets/styles/global.scss';
import Button from './components/Button';
import TrainingTable from './components/TrainingTable';

export default {
  name: 'App',
  data: () => ({
    days: ['Понедельник', 'Вторник', 'Среда', 'Четверг', 'Пятница', 'Суббота', 'Воскресенье'],
    activeButton: 0,
    tableData: JSON.parse(window.localStorage.getItem('data'))
  }),
  methods: {
    onButtonClick: function (index) { this.activeButton = index; },
    onAddRow: function (exercise, set, rep) {
      if (!this.tableData[this.activeButton]) {
        this.tableData[this.activeButton] = [];
      }
      this.tableData = {
        ...this.tableData,
        [this.activeButton]: [...this.tableData[this.activeButton], {
          id: this.tableData[this.activeButton].length + 1, exercise, set, rep
        }]
      };

      this.saveData();
    },
    onCellChange: function (rowNumber, cellValue, value) {
      const newDayData = [...this.tableData[this.activeButton]];
      newDayData[rowNumber][cellValue] = value;

      this.tableData = {
        ...this.tableData,
        [this.activeButton]: newDayData
      };

      this.saveData();
    },
    saveData: function () {
      window.localStorage.setItem('data', JSON.stringify(this.tableData));
    }
  },
  components: {
    Button,
    TrainingTable
  }
};
</script>

<style lang="scss">
#app {
  min-height: 100vh;
  background-size: 400px 500px;
  background-repeat: no-repeat;
  background-position: center 50vh;
  display: flex;
  width: 100%;
  align-items: center;
  flex-direction: column;
  font-family: "Roboto", sans-serif;
  background-image: url("https://st2.depositphotos.com/7717264/10526/v/950/depositphotos_105260826-stock-illustration-bodybuilder-big-biceps-vector-logo.jpg");

  .buttonsWrapper {
    display: flex;
    justify-content: space-between;
    width: 90%;
    margin-top: 12px;
  }
}
</style>
