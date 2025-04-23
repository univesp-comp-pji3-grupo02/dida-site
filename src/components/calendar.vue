<template>
  <div class="calendar">
    <div class="header-calendar">
      <button @click="prevMonth">
        <i class="fa-solid fa-chevron-left"></i>
      </button>
      <div class="monthYear">{{ formattedMonthYear }}</div>
      <button @click="nextMonth">
        <i class="fa-solid fa-chevron-right"></i>
      </button>
    </div>

    <div class="weekDays">
      <div class="day" v-for="day in weekDayNames" :key="day">{{ day }}</div>
    </div>

    <div class="dates">
      <!-- Dias do mês anterior (sempre desabilitado) -->
      <button
        class="date"
        :class="{inactive: isPast(day.fullDate) || isSunday(day.fullDate) || !hasOpenTimeSlot(day.fullDate)}"
        disabled
        v-for="day in prevMonthDays"
        :key="`prev-${day.date}-${day.index}`"
      >
        {{ day.date }}
      </button>

      <!-- Dias do mês atual -->
      <button
        class="date"
        v-for="day in monthDays"
        :key="`current-${day.date}`"
        :class="{
          active: isToday(day.fullDate),
          noTimeSlot: !hasOpenTimeSlot(day.fullDate) && !isSunday(day.fullDate) && !isPast(day.fullDate),
          inactive: isPast(day.fullDate) || isSunday(day.fullDate) || !hasOpenTimeSlot(day.fullDate)
        }"
        :disabled="isPast(day.fullDate) || isSunday(day.fullDate) || !hasOpenTimeSlot(day.fullDate)"
      >
        {{ day.date }}
      </button>

      <!-- Dias do próximo mês (sempre desabilitado) -->
      <button
        class="date"
        disabled
        v-for="day in nextMonthDays"
        :key="`next-${day.date}-${day.index}`"
      >
        {{ day.date }}
      </button>
    </div>
  </div>
</template>

<script>
const WEEK_DAYS = ['dom', 'seg', 'ter', 'qua', 'qui', 'sex', 'sab']
// Exemplos de dias sem disponibilidade (strings no formato 'DD/MM/YYYY')
const notAvailableDays = ['01/05/2025', '02/05/2025', '03/05/2025', '04/05/2025', '05/05/2025']

export default {
  name: 'CalendarGrid',
  data () {
    return {
      weekDayNames: WEEK_DAYS,
      currentDate: new Date()
    }
  },
  computed: {
    formattedMonthYear () {
      return this.currentDate.toLocaleString('default', {
        month: 'long',
        year: 'numeric'
      })
    },
    monthDays () {
      const year = this.currentDate.getFullYear()
      const month = this.currentDate.getMonth()
      const lastDay = new Date(year, month + 1, 0).getDate()
      return Array.from({ length: lastDay }, (_, i) => ({
        date: i + 1,
        fullDate: new Date(year, month, i + 1)
      }))
    },
    prevMonthDays () {
      const year = this.currentDate.getFullYear()
      const month = this.currentDate.getMonth()
      const firstWeekDay = new Date(year, month, 1).getDay()
      return Array.from({ length: firstWeekDay }, (_, i) => {
        const dateObj = new Date(year, month, -i)
        return { date: dateObj.getDate(), fullDate: dateObj, index: i }
      }).reverse()
    },
    nextMonthDays () {
      const totalDisplayed = this.prevMonthDays.length + this.monthDays.length
      const daysToAdd = totalDisplayed % 7 === 0 ? 0 : 7 - (totalDisplayed % 7)
      const year = this.currentDate.getFullYear()
      const month = this.currentDate.getMonth()
      return Array.from({ length: daysToAdd }, (_, i) => {
        const dateObj = new Date(year, month + 1, i + 1)
        return { date: dateObj.getDate(), fullDate: dateObj, index: i }
      })
    }
  },
  methods: {
    prevMonth () {
      this.currentDate.setMonth(this.currentDate.getMonth() - 1)
      this.currentDate = new Date(this.currentDate)
    },
    nextMonth () {
      this.currentDate.setMonth(this.currentDate.getMonth() + 1)
      this.currentDate = new Date(this.currentDate)
    },
    isToday (date) {
      const today = new Date()
      return (
        date.getDate() === today.getDate() &&
        date.getMonth() === today.getMonth() &&
        date.getFullYear() === today.getFullYear()
      )
    },
    isPast (date) {
      const today = new Date()
      const dateOnly = new Date(date.getFullYear(), date.getMonth(), date.getDate())
      const todayOnly = new Date(today.getFullYear(), today.getMonth(), today.getDate())
      return dateOnly < todayOnly
    },
    isSunday (date) {
      return date.getDay() === 0
    },
    hasOpenTimeSlot (date) {
      const dateString = date instanceof Date
        ? date.toLocaleDateString('pt-BR')
        : date
      return !notAvailableDays.includes(dateString)
    }
  }
}
</script>

<style scoped>
.calendar {
  width: 380px;
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: #f0dfdf;
  padding: 10px;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
  gap: 10px;
}
.header-calendar {
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.header-calendar button {
  border: none;
  border-radius: 50%;
  background-color: #fff;
  cursor: pointer;
  width: 2.5rem;
  height: 2.5rem;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 0 4px rgba(0, 0, 0, 0.3);
}
.weekDays {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  width: 100%;
}
.day {
  text-align: center;
  padding: 5px;
  color: #999fa6;
}
.dates {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  width: 100%;
  gap: 5px;
}
.date {
  text-align: center;
  padding: 8px;
  border-radius: 4px;
  border: none;
  cursor: pointer;
}
.date.inactive {
  color: #ccc;
  background-color: #BA8B7B;
}
.date.active {
  background-color: #b15334;
  color: #fff;
}
.noTimeSlot {
  background-color: #ff0000;
  color: #fff;
}
button:disabled {
  pointer-events: none;
  opacity: 0.5;
  cursor: not-allowed;
}
</style>
