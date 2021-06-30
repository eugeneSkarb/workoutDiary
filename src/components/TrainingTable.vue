<template>
  <div class="wrapper">
    <table class="table" v-if="data && data.length > 0">
      <thead>
      <tr>
        <th>Номер</th>
        <th>Упражнение</th>
        <th>Подходы</th>
        <th>Повторения</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="(row, rowIndex) in data" :key="row.id">
        <td v-for="(columnKey, columnIndex) in Object.keys(row)"
            v-on:click="onCellClick(rowIndex, columnKey)"
            :key="columnIndex">{{ row[columnKey] }}</td>
      </tr>
      </tbody>
    </table>
    <div class="addForm">
      <input placeholder="Упражнение" v-model="exerciseValue" type="text">
      <input placeholder="Подходы" v-model="setValue" type="text">
      <input placeholder="Повторения" v-model="repValue" type="text">
      <button class="submit" v-on:click="onAddRow(exerciseValue, setValue, repValue)">Добавить</button>
    </div>
    <p class="text" v-if="!data" >Заполните данные.</p>
  </div>
</template>

<script>
export default {
  name: 'TrainingTable',
  props: {
    data: Array,
    onAddRow: Function,
    onCellChange: Function
  },
  data: () => ({
    exerciseValue: '',
    setValue: '',
    repValue: ''
  }),
  methods: {
    onCellClick: function (rowIndex, columnKey) {
      if (columnKey === 'id') {
        return;
      }

      const userInput = window.prompt('Введите новое значение');
      if (!userInput) {
        return;
      }

      this.onCellChange(rowIndex, columnKey, userInput);
    }
  }
};
</script>

<style scoped lang="scss">
$border-size: 2px;

.wrapper {
  margin-top: 30px;
  width: 90%;
  text-align: center;
}
.table {
  border: $border-size solid black;
  border-spacing: 0;
  border-bottom: 0;
  border-radius: 15px;
  width: 100%;
  overflow: hidden;

  tbody {
    background-image: linear-gradient(0deg, rgba(55, 43, 36, 0.8), rgba(55, 43, 36, 0.8)), url("https://cdn.iz.ru/sites/default/files/styles/1920x1080/public/article-2020-07/Depositphotos_151084986_xl-2015.jpg?itok=vAh_S1v5");
    background-position: center;
    background-size: cover;
  }

  th, td {
    text-align: center;
    border-bottom: $border-size solid black;
    padding: 10px 5px;
  }

  th {
    font-size: 24px;
    background-color: lightgray;
  }

  td {
    font-size: 18px;
    color: white;

    &:not(:first-child) {
      cursor: pointer;
    }
  }

  th:not(:last-child), td:not(:last-child) {
      border-right: $border-size solid black;
  }
}
.text {
  margin: 15px;
  color: black;
  font-size: 30px;
  font-weight: 400;
}
.addForm {
  display: flex;
  margin-top: 15px;
  justify-content: center;
}
input {
  padding: 10px 15px;
  margin-left: 5px;
  text-align: center;
  border: 2px solid green;
  font-size: 16px;
  background-color: honeydew;
}
.submit {
  border: 2px solid green;
  background-color: green;
  color: white;
  border-radius: 10px;
  padding: 7px 12px;
  width: 140px;
  height: 40px;
  font-size: 18px;
  margin-left: 15px;
  cursor: pointer;
  &:hover {
    background-color: darkgreen;
  }
}
</style>
