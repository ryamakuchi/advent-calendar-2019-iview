<template>
  <div class="container">
    <h1>
      Nuxt.js Advent Calendar 2019
    </h1>

    <p class="comment">{{ comment }}</p>

    <Row>
      <Col
        v-for="dayName in dayNames"
        :key="dayName"
        class="day-name"
      >
        {{ dayName }}
      </Col>
    </Row>

    <Row>
      <Col
        v-for="day in days"
        :key="day.date"
      >
        <Card dis-hover>
          <div slot="title"
          >
            <Tag color="magenta">{{ day.date }}</Tag>

            <a
              :href="`https://qiita.com/${day.authorName}`"
              target="_blank"
              rel="noopener noreferrer"
              class="ellipsis"
            >
              {{ day.authorName }}
            </a>

            <Avatar
              :src="day.authorImageUrl"
              size="large"
            />
          </div>

          <a v-if="day.articleUrl !== null"
            :href="day.articleUrl"
            target="_blank"
            rel="noopener noreferrer"
          >
            {{ day.comment }}
          </a>

          <p v-else>
            {{ day.comment }}
          </p>
        </Card>
      </Col>

      <Col
        v-for="day in [26, 27, 28]"
        :key="day"
      >
        <Card dis-hover>
          <Tag color="default">{{ day }}</Tag>
        </Card>
      </Col>
    </Row>

    <p class="comment">
      ※ このページはレスポンシブ対応していません。デスクトップサイズの画面でご覧ください。
    </p>
  </div>
</template>

<script>
import { parse } from 'node-html-parser'

export default {
  async asyncData({ $axios }) {
    const { data } = await $axios.get('https://qiita.com/advent-calendar/2019/nuxt-js')
    const root = parse(data)
    return {
      comment: root.querySelector('.markdownContent').text,
      dayNames: root.querySelectorAll('.adventCalendarCalendar_dayName').map(dayName => dayName.text),
      days: root.querySelectorAll('.adventCalendarCalendar_day').map(day => {
        const articleUrl = day.querySelector('.adventCalendarCalendar_comment').querySelector('a') ?
          day.querySelector('.adventCalendarCalendar_comment').querySelector('a').attributes['href'] :
          null
        return {
          date: day.querySelector('.adventCalendarCalendar_date').text,
          authorName: day.querySelector('.adventCalendarCalendar_author').text.replace(/\s|&nbsp;/g, ''),
          authorImageUrl: day.querySelector('.adventCalendarCalendar_authorIcon').attributes['src'],
          comment: day.querySelector('.adventCalendarCalendar_comment').text,
          articleUrl: articleUrl
        }
      })
    }
  }
}
</script>

<style>
.container {
  padding: 20px 5%;
}

.comment {
  margin: 20px 0;
}

.ivu-row {
  display: flex;
  flex-wrap: wrap;
  border: 1px solid #e9e9e9;
}
.ivu-row > .ivu-col {
  width: calc(100% / 7);
  display: flex;
}

.day-name {
  padding: 10px;
  border-right: 1px solid #e9e9e9;
}
.day-name:last-child {
  border-right: none;
}

.ivu-card {
  border-radius: 0px;
  width: 100%;
}

.ivu-avatar {
  display: block;
  margin: 10px auto;
}

.ellipsis {
  display: inline-block;
  overflow: hidden;
  vertical-align: middle;
  white-space: nowrap;
  width: 80px;
  text-overflow: ellipsis;
}
</style>
