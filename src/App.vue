<template>
  <div class="container column">
    <form class="card card-w30" @submit.prevent="submitHeandler">
      <app-select
      v-model="selected"
      :options="options"
      :selected="selected"
      @change:selected="selected = $event"
      >{{selected}}</app-select>

      <app-text-area
      v-model.trim="message"
      title="Значение"
      placeholder="введите сюда что-нибудь"
      ></app-text-area>

      <app-button color="primary" type="submit">{{added}}</app-button>
    </form>

    <div class="card card-w70">
      <!-- <h1>Резюме Nickname</h1> -->
      <app-title></app-title>
      <!-- <div class="avatar">
        <img src="https://cdn.dribbble.com/users/5592443/screenshots/14279501/drbl_pop_r_m_rick_4x.png">
      </div> -->
      <app-avatar></app-avatar>
      <app-subtitle :title="Опыт"></app-subtitle>
      <!-- <p>
        главный герой американского мультсериала «Рик и Морти», гениальный учёный, изобретатель, атеист (хотя в некоторых сериях он даже молится Богу, однако, каждый раз после чудесного спасения ссылается на удачу и вновь отвергает его существование), алкоголик, социопат, дедушка Морти. На момент начала третьего сезона ему 70 лет[1]. Рик боится пиратов, а его главной слабостью является некий - "Санчезиум". Исходя из того, что существует неограниченное количество вселенных, существует неограниченное количество Риков, герой сериала предположительно принадлежит к измерению С-137. В серии комикcов Рик относится к измерению C-132, а в игре «Pocket Mortys» — к измерению C-123[2]. Прототипом Рика Санчеза является Эмметт Браун, герой кинотрилогии «Назад в будущее»[3].
      </p> -->
      <app-text></app-text>
      <h3 v-if="blocks.length !==0">Добавьте первый блок, чтобы увидеть результат</h3>
    </div>
  </div>
  <div class="container">
    <p>
      <!-- <button class="btn primary">Загрузить комментарии</button> -->
      <app-button color="primary" type="submit">{{download}}</app-button>
    </p>
    <div class="card">
      <!-- <h2>Комментарии</h2> -->
      <app-comments></app-comments>
      <!-- <ul class="list">
        <li class="list-item">
          <div>
            <p><strong>test@microsoft.com</strong></p>
            <small>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Eligendi, reiciendis.</small>
          </div>
        </li>
      </ul> -->
    </div>
    <!-- <div class="loader"></div> -->
    <app-loader v-if="loading"></app-loader>
  </div>
</template>

<script>
import AppSelect from './components/AppSelect'
import AppTextArea from './components/AppTextAria.vue'
import AppButton from './components/AppButton.vue'
import AppTitle from './components/AppTitle.vue'
import AppSubtitle from './components/AppSubtitle.vue'
import AppAvatar from './components/AppAvatar.vue'
import AppText from './components/AppText.vue'
import AppComments from './components/AppComments.vue'
import AppLoader from './components/AppLoader.vue'
export default {
  data () {
    return {
      selected: 'title',
      message: '',
      loading: false,
      blocks: [],
      options: [
        {
          value: 'title',
          tag: 'Заголовок'
        },
        {
          value: 'subtitle',
          tag: 'Подзаголовок'
        },
        {
          value: 'avatar',
          tag: 'Аватар'
        },
        {
          value: 'text',
          tag: 'Текст'
        }
      ],
      submit: 'Отправить',
      added: 'Добавить',
      download: 'Загрузить комментарии'
    }
  },
  components: {
    AppSelect,
    AppTextArea,
    AppButton,
    AppTitle,
    AppSubtitle,
    AppText,
    AppAvatar,
    AppComments,
    AppLoader
  },
  methods: {
    submitHeandler () {
      console.group('Form Data')
      console.log('Согласен: ', this.selected)
      console.log('Текст: ', this.message)
      console.groupEnd()
      this.selected = 'title'
      this.message = ''
    }
  }
}
</script>

<style>
  .avatar {
    display: flex;
    justify-content: center;
  }

  .avatar img {
    width: 150px;
    height: auto;
    border-radius: 50%;
  }
</style>
