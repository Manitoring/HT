


<template>
  <div class="app-wrapper">

    <div class="main-card">

      <h1 class="title">
        Habit Tracker
      </h1>

      <p class="subtitle">
        Оцени свой день
      </p>

      <!-- ФОРМА -->

      <div class="form-block">

        <div class="input-group-custom">

          <label>
            Часы сна
          </label>

          <input
            v-model="sleep"
            type="number"
            class="form-control custom-input"
          />
        </div>


        <div class="input-group-custom">

          <label>
            Часы работы
          </label>

          <input
            v-model="work"
            type="number"
            class="form-control custom-input"
          />
        </div>

        <div class="input-group-custom">

          <label>
            Часы игр
          </label>

          <input
            v-model="games"
            type="number"
            class="form-control custom-input"
          />
        </div>

        <!-- CHECKBOX -->

        <div class="checkbox-group">

          <label class="check-item">
            <input type="checkbox" v-model="read" />
            Читал
          </label>

          <label class="check-item">
            <input type="checkbox" v-model="sport" />
            Спорт
          </label>

          <label class="check-item">
            <input type="checkbox" v-model="smoke" />
            Курил
          </label>

        </div>

        <button
          @click="addDay"
          class="btn add-btn"
        >
          Добавить день
        </button>

      </div>

      <!-- СРЕДНИЙ ПРОЦЕНТ -->

      <div
        v-if="days.length > 0"
        class="average-box"
      >
        Средний результат:
        <span>{{ averageScore }}%</span>
      </div>

      <!-- КАРТОЧКИ -->

      <div class="days-grid">

        <div
          class="day-card"
          :class="getCardColor(day.score)"
          v-for="(day, index) in days"
          :key="index"
        >

          <h3>
            День {{ index + 1 }}
          </h3>

          <p>Сон: {{ day.sleep }} ч</p>

          <p>Работа: {{ day.work }} ч</p>

          <p>Игры: {{ day.games }} ч</p>

          <p>
            Читал:
            {{ day.read ? 'Да' : 'Нет' }}
          </p>

          <p>
            Спорт:
            {{ day.sport ? 'Да' : 'Нет' }}
          </p>

          <p>
            Курил:
            {{ day.smoke ? 'Да' : 'Нет' }}
          </p>

          <div class="score">
            {{ day.score }}%
          </div>

          <button
            @click="deleteDay(index)"
            class="btn delete-btn"
          >
            Удалить
          </button>

        </div>

      </div>

    </div>

  </div>
</template>


<style>
body {
  margin: 0;
  padding: 0;
  background: #f4f6f8;
  font-family: Arial, sans-serif;
}

.app-wrapper {
  min-height: 100vh;

  display: flex;
  justify-content: center;
  align-items: center;

  padding: 40px 20px;
}

.main-card {

  width: 100%;
  max-width: 900px;

  background: white;

  border-radius: 25px;

  padding: 40px;

  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.08);

  animation: fadeIn 0.6s ease;

}

.title {

  text-align: center;

  font-size: 42px;

  margin-bottom: 10px;

  color: #222;

}

.subtitle {

  text-align: center;

  color: #777;

  margin-bottom: 30px;

}

.form-block {

  display: flex;
  flex-direction: column;

  gap: 15px;

}

.custom-input {

  border-radius: 14px;

  border: 1px solid #ddd;

  padding: 14px;

  transition: 0.3s;

}

.custom-input:focus {

  border-color: #6c63ff;

  box-shadow: 0 0 10px rgba(108, 99, 255, 0.2);

}

.checkbox-group {

  display: flex;

  gap: 20px;

  flex-wrap: wrap;

  margin-top: 10px;

}

.check-item {

  color: #444;

  font-size: 15px;

}

.add-btn {

  margin-top: 10px;

  background: #6c63ff;

  border: none;

  border-radius: 14px;

  padding: 14px;

  color: white;

  font-weight: bold;

  transition: 0.3s;

}

.add-btn:hover {

  background: #5a52e0;

  transform: translateY(-2px);

}

.average-box {

  margin-top: 30px;

  padding: 18px;

  border-radius: 14px;

  background: #f0f4ff;

  text-align: center;

  font-size: 20px;

  animation: fadeIn 0.5s ease;

}

.average-box span {

  font-weight: bold;

  color: #6c63ff;

}

.days-grid {

  margin-top: 30px;

  display: grid;

  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));

  gap: 20px;

}

.day-card {

  padding: 25px;

  border-radius: 20px;

  transition: 0.3s;

  animation: fadeInUp 0.4s ease;

}

.day-card:hover {

  transform: translateY(-5px);

}

.good-day {

  background: #e8f8ee;

}

.normal-day {

  background: #fff8e7;

}

.bad-day {

  background: #ffeaea;

}

.score {

  font-size: 32px;

  font-weight: bold;

  margin-top: 15px;

  margin-bottom: 15px;

}

.delete-btn {

  width: 100%;

  border-radius: 12px;

  border: none;

  background: #ff5c5c;

  color: white;

  padding: 12px;

  transition: 0.3s;

}

.delete-btn:hover {

  background: #e04848;

}

.input-group-custom {

  display: flex;

  flex-direction: column;

  gap: 8px;
}

.input-group-custom label {

  font-size: 14px;

  font-weight: 600;

  color: #555;

  padding-left: 4px;
}

@keyframes fadeIn {

  from {
    opacity: 0;
    transform: translateY(10px);
  }

  to {
    opacity: 1;
    transform: translateY(0);
  }

}

@keyframes fadeInUp {

  from {
    opacity: 0;
    transform: translateY(20px);
  }

  to {
    opacity: 1;
    transform: translateY(0);
  }

}
</style>
<script>
export default {

  data() {

    return {

      sleep: '',
      work: '',
      games: '',

      read: false,
      sport: false,
      smoke: false,

      days: []

    };

  },

  computed: {

    averageScore() {

      if (this.days.length === 0) {
        return 0;
      }

      let total = 0;

      this.days.forEach(day => {
        total += day.score;
      });

      return Math.round(total / this.days.length);

    }

  },

  methods: {

    addDay() {

      let score = 50;

      // СОН

      if (this.sleep >= 7) {
        score += 20;
      }

      // РАБОТА

      if (this.work >= 4) {
        score += 15;
      }

      // ИГРЫ

      if (this.games <= 2) {
        score += 10;
      }
      if (this.games > 6){
        score -= 10;
      }

      // ПРИВЫЧКИ

      if (this.read) {
        score += 10;
      }

      if (this.sport) {
        score += 10;
      }

      if (this.smoke) {
        score -= 20;
      }

      // LIMIT

      if (score > 100) {
        score = 100;
      }

      if (score < 0) {
        score = 0;
      }

      // PUSH

      this.days.push({

        sleep: this.sleep,
        work: this.work,
        games: this.games,

        read: this.read,
        sport: this.sport,
        smoke: this.smoke,

        score: score

      });

    },

    deleteDay(index) {

      this.days.splice(index, 1);

    },

    getCardColor(score) {

      if (score >= 80) {
        return 'good-day';
      }

      if (score >= 50) {
        return 'normal-day';
      }

      return 'bad-day';

    }

  }

};
</script>

//http://localhost:5173/
