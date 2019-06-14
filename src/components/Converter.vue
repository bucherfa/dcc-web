<template>
  <div class="converter">
    <div class="converter__content">
      <div class="converter__item">
        <div class="converter__header">input</div>
        <div class="converter__textarea-wrapper">
          <textarea class="converter__textarea" :placeholder="placeholder" v-model="input"></textarea>
        </div>
      </div>
      <div class="converter__item">
        <div class="converter__header">
          <div>docker-compose.yml</div>
          <div>
            <span class="header__download" @click="copy">Copy</span>
            <span class="header__download" @click="download">Download</span>
          </div>
        </div>
        <div class="converter__textarea-wrapper">
          <textarea class="converter__textarea js-converter__textarea--output" readonly v-model="output"></textarea>
        </div>
      </div>
    </div>
    <a class="download"></a>
  </div>
</template>

<script>
import dcc from 'docker-compose-converter'

export default {
  name: 'Converter',
  data () {
    return {
      input: '',
      placeholder: `docker run -d \\
  -v nextcloud:/var/www/html \\
  nextcloud
docker run -d \\
  -v db:/var/lib/mysql \\
  mariadb`
    }
  },
  computed: {
    output () {
      if (this.input) {
        return dcc(this.input)
      }
      return dcc(this.placeholder)
    }
  },
  methods: {
    copy () {
      const copyTextarea = document.querySelector('.js-converter__textarea--output')
      copyTextarea.focus()
      copyTextarea.select()
      try {
        document.execCommand('copy')
      } catch (err) {
        console.log('Copy failed.')
      }
    },
    download () {
      const data = 'data:text/yml;charset=utf-8,' + encodeURIComponent(this.output)
      const element = document.querySelector('.download')
      element.setAttribute('href', data)
      element.setAttribute('download', 'docker-compose.yml')
      element.click()
    }
  }
}
</script>

<style scoped>
.converter {
  margin: 0.5rem auto;
  max-width: 40rem;
}

.converter__content {
  margin: 0 0.5rem;
}

.converter__item {
  border-radius: 2px;
  box-shadow: 0 0.25rem 0.5rem rgba(0,0,0,0.16), 0 0.25rem 0.5rem rgba(0,0,0,0.23);
  margin-top: 1rem;
}

.converter__header {
  background: #006494;
  color: #ffffff;
  display: flex;
  justify-content: space-between;
  padding: 0.5rem;
}

.header__download {
  background: #ffffff;
  color: #006494;
  cursor: pointer;
  padding: 0.35rem;
  border-radius: 0.3rem;
  margin-left: 0.4rem;
}

.converter__textarea-wrapper {
  padding: 0.5rem;
}

.converter__textarea {
  background: white;
  border: 0;
  display: block;
  height: 20rem;
  margin: 0;
  padding: 0;
  width: 100%;
  resize: none;
}

.download {
  display: none;
}
</style>
