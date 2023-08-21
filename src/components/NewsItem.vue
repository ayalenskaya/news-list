<template>
  <div class="news-item">
    <img v-if="item.image" :src="item.image" :alt="item.name">
    <div class="news-format">
      <div class="format">
        <p class="format-date">{{ formatDate(item.date) }}</p>
        <div class="format-month-y">
          <p>{{ formatMonth(item.date) }}</p>
          <p>{{ formatYear(item.date) }}</p>
        </div>
      </div>
      <h2 class="item-name">{{ item.name }}</h2>
      <p class="item-description">{{ item.previewText }}</p>
    </div>
    <div class="type">{{ item.type.value }}</div>
  </div>
</template>
<script>
import { ref, onMounted } from 'vue';
import moment from 'moment';
export default {
  name: 'NewsItem',
  props: {
    item: Object,
  },

  setup() {
    const currentDate = ref('');
    const currentMonth = ref('');
    const currentYear = ref('');
    const formatDate = (date) => {
      return moment(date).format('DD');
    };
    const formatMonth = (date) => {
      return moment(date).format('MMMM');
    };
    const formatYear = (date) => {
      return moment(date).format('YYYY');
    };
    onMounted(() => {
      currentDate.value = moment().format('DD');
      currentDate.value = moment().format('MMMM');
      currentDate.value = moment().format('YYYY');
    });

    return {
      currentDate,
      currentMonth,
      currentYear,
      formatDate,
      formatMonth,
      formatYear
    };
  }
}
</script>

<style scoped>
.news-format {
  padding: 32px 32px 0 32px;
}

.format {
  display: flex;
  color: #A1A7B5;
}

.format-month-y p {
  margin: 0;
}

.format-date {
  font-size: 36px;
  margin: 0 5px 0 0;
}

.item-name {
  font-size: 22px;
  line-height: 26px;
  font-weight: 400;
  color: #0C5BEF;
}

.item-description {
  font-size: 20px;
  line-height: 26px;
  font-weight: 400;
  color: #222327;
}

.news-item {
  width: calc(33.33% - 100px);
  border-radius: 16px;
  height: auto;
  border: 1px solid #0F62FE;
  display: flex;
  flex-direction: column;
}

.news-item img {
  width: 100%;
  height: auto;
  border-radius: 16px;
}

.type {
  margin: auto 32px 32px;
  width: 132px;
  padding: 32px;
  border-radius: 16px;
  font-size: 14px;
  padding: 4px 16px;
  background-color: #F0F6FE;
  color: #00133A;
  white-space: nowrap;
  text-align: center;
}
</style>