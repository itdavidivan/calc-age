<template>
  <div class="main">
    <div class="container">
      <div class="inputs">
        <input v-model="day" type="number" placeholder="day" min="1" max="31" />
        <input
          v-model="month"
          type="number"
          placeholder="month"
          min="1"
          max="12"
        />
        <input
          v-model="year"
          type="number"
          placeholder="year"
          min="1900"
          max="2100"
        />
        <button @click="calculateAge">Calculate</button>
      </div>
      <div class="dates">
        <p class="results" v-if="numberIsNotValid">Something is wrong!</p>
        <div v-else class="results">
          <h2>
            <span>{{ age.years > 0 ? age.years : " -- " }}</span> years
          </h2>
          <h2>
            <span>{{ age.months > 0 ? age.months : " -- " }}</span> month
          </h2>
          <h2>
            <span>{{ age.days > 0 ? age.days : " -- " }}</span> days
          </h2>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      numberIsNotValid: false,
      day: "",
      month: "",
      year: "",
      age: {
        years: 0,
        months: 0,
        days: 0,
      },
    };
  },

  methods: {
    calculateAge() {
      if (this.day < 32 && this.month < 13 && this.year < 2026) {
        const birthDate = new Date(this.year, this.month, this.day);
        const currentDate = new Date();

        let years = currentDate.getFullYear() - birthDate.getFullYear();
        let months = currentDate.getMonth() - birthDate.getMonth();
        let days = currentDate.getDate() - birthDate.getDate();

        if (months < 0 || (months === 0 && days < 0)) {
          years--;
          months += 12;
        }

        if (days < 0) {
          const lastMonth = new Date(
            currentDate.getFullYear(),
            currentDate.getMonth(),
            0
          );
          days += lastMonth.getDate();

          this.age.years = years;
          this.age.months = months;
          this.age.days = days;
        }
      } else {
        this.numberIsNotValid = true;
      }
    },
  },
};
</script>

<style scoped>
.main {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  margin: 0;
}
.container {
  background-color: rgb(255, 255, 255);
  height: 500px;
  width: 800px;
  display: flex;
  flex-direction: column;
  border-radius: 10px 10px 90px 10px;
  box-shadow: 2px 2px 2px black;
}
.inputs {
  border-bottom: 4px black solid;
  height: 100px;
  margin-top: 40px;
  padding-bottom: 30px;
}
input {
  margin: 0 15px;
  padding: 20px 30px;
  text-align: left;
  border-radius: 20px;
  font-family: "Cursive", sans-serif;
  font-weight: bold;
  font-size: 18px;
  border: 2px solid #ffffff;
  outline: none;
  transition: all 0.3s ease-in-out;
  box-shadow: 2px 4px 8px rgba(0, 0, 0, 0.1);
}

input:focus {
  border-color: #00c4cc;
  box-shadow: 0 0 10px rgba(0, 196, 204, 0.5);
}

input::placeholder {
  color: #8c8c8c;
  font-style: italic;
}
.dates {
  display: flex;
  justify-content: start;
  margin-left: 200px;
}
.results {
  font-size: 35px;
  color: black;
  font-weight: 900;
  font-family: cursive;
}
span {
  color: blueviolet;
}
input[type="number"] {
  -moz-appearance: textfield;
  -webkit-appearance: none;
  appearance: none;
}

input[type="number"]::-webkit-outer-spin-button,
input[type="number"]::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}
button {
  background: linear-gradient(45deg, #e3e3e3, #4e73df);
  color: white;
  font-size: 18px;
  font-weight: bold;
  padding: 15px 30px;
  border: none;
  border-radius: 30px;
  cursor: pointer;
  transition: all 0.3s ease-in-out;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  margin-left: 10px;
}

button:hover {
  background: linear-gradient(45deg, #808080, #aeaeae);
  transform: translateY(-3px);
}

button:focus {
  outline: none;
}

button:active {
  transform: translateY(2px);
}
</style>
