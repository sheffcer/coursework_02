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
      :error="errors.name"
      :errorLength="errors.length"
      ></app-text-area>
      <app-button color="primary" type="submit">{{added}}</app-button>
    </form>
    <div class="card card-w70">
      <component
      v-for="block in blocks"
      :key="block"
      :is="block.componentName"
      :message="block.componentText"
      ></component>
      <!-- <app-title></app-title> -->
      <!-- <app-avatar></app-avatar> -->
      <!-- <app-subtitle :title="Опыт"></app-subtitle> -->
      <!-- <app-text></app-text> -->
      <h3 v-if="blocks.length === 0">Добавьте первый блок, чтобы увидеть результат</h3>
    </div>
  </div>
  <div class="container">
    <p>
      <app-button color="primary" type="submit" @click="getComments">{{download}}</app-button>
    </p>
    <div class="card">
      <app-comments :comments="comments"></app-comments>
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
import axios from 'axios'
export default {
  data () {
    return {
      selected: 'title',
      message: '',
      loading: false,
      blocks: [],
      comments: [],
      names: ['AppTitle', 'AppSubtitle', 'AppAvatar', 'AppText'],
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
      download: 'Загрузить комментарии',
      errors: {
        name: ''
      }
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
      if (this.formIsValid()) {
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
        this.selected = 'title'
        this.message = ''
      }
    },
    getComments () {
      this.loading = true
      setTimeout(() => {
        const url = 'https://jsonplaceholder.typicode.com/comments?_limit=42'
        // this.loading = true
        axios.get(url)
          .then((response) => {
            // console.log(response)
            const data = response.data
            this.comments = Object.keys(data).map(key => {
              return {
                id: data[key].id,
                email: data[key].email,
                body: data[key].body
              }
            })
          }, (error) => {
            console.log(error)
          })
      }, 1500)
    },
    formIsValid () {
      let isValid = true
      if (this.message.length <= 2) {
        this.errors.name = 'Поле не может быть пустым и меньше 3-х символов'
        this.errors.length = this.message.length
        console.log(this.error)
        isValid = false
      } else {
        this.errors.name = null
      }
      return isValid
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
