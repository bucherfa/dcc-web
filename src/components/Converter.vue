<template>
  <div class="converter">
    <div class="converter__content">
      <div class="converter__item">
        <span class="converter__header">input</span>
        <textarea class="converter__textarea" :placeholder="placeholder" v-model="input"></textarea>
      </div>
      <div class="converter__item converter__item--output">
        <span class="converter__header">docker-compose.yml</span>
        <textarea class="converter__textarea js-converter__textarea--output" readonly v-model="output"></textarea>
      </div>
    </div>
    <div class="converter__download">
      <div class="download__button" @click="copy">Copy</div>
      <div class="download__button" @click="download">Download</div>
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
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
}

.converter__item--output {
  margin-top: 1rem;
}

.converter__header {
  margin: 0 0.5rem;
}

.converter__textarea {
  background: white;
  border: 0;
  border-radius: 2px;
  box-shadow: 0 3px 6px rgba(0,0,0,0.16), 0 3px 6px rgba(0,0,0,0.23);
  display: block;
  height: 20rem;
  margin: 0.25rem auto;
  padding: 0.5rem;
  width: 90%;
  resize: none;
}

.converter__download {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  margin-top: 0.5rem;
}

.download__button {
  background: #099cec;
  border-radius: 0.25rem;
  color: #ffffff;
  cursor: pointer;
  padding: 0.5rem;
  margin-right: 0.5rem;
}

.download {
  display: none;
}
</style>
