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
      <app-text></app-text>
      <h3 v-if="blocks.length !==0">Добавьте первый блок, чтобы увидеть результат</h3>
    </div>
  </div>
  <div class="container">
    <p>
      <app-button color="primary" type="submit">{{download}}</app-button>
    </p>
    <div class="card">
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
    capitalizeFirstLetter (string) {
      return string.charAt(0).toUpperCase() + string.slice(1)
    },
    submitHeandler () {
      console.group('Form Data')
      console.log('Согласен: ', this.selected)
      console.log('Текст: ', this.message)
      console.groupEnd()
      const component = {
        componentName: 'App' + this.capitalizeFirstLetter(this.selected),
        componentText: this.message
      }
      this.blocks.push(component)
      console.log(this.blocks)

      // this.selected = 'title'
      // this.message = ''
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
