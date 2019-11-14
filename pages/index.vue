<template>
  <section class="section">
    <div class="is-mobile">

      <div class="selectWrap">
        <b-field label="放映年">
          <b-select placeholder="年数を選択してください。" v-model="selectYear">
            <option>2017</option>
            <option>2018</option>
            <option>2019</option>
          </b-select>
        </b-field>

        <b-field label="クール">
          <b-select placeholder="クール数を選択してください。" v-model="selectSeason">
            <option>1</option>
            <option>2</option>
            <option>3</option>
            <option>4</option>
          </b-select>
        </b-field>

        <section>
          <b-button type="is-primary" outlined @click="getApi">{{ selectYear }}年の{{ selectSeason }}クールを検索する</b-button>
        </section>
      </div>

      <div class="tile is-ancestor">
        <div class="tile is-parent is-vertical">

          <div class="tile is-child box" v-for="data in json.data">
            <p class="tileTtl">
              {{ data.title }}
            </p>
            <div class="tileBox">
              <dl>
                <dt>公式サイト：</dt>
                <dd><a :href="data.public_url" target="_blank">{{ data.public_url }}</a></dd>
              </dl>
              <dl>
                <dt>制作会社：</dt>
                <dd>{{ data.product_companies }}</dd>
              </dl>
            </div>
        </div>

        </div>
      </div>

    </div>
  </section>
</template>

<script>
import Card from '~/components/Card'
import axios from 'axios'

export default {
  name: 'HomePage',

  data: function() {
    return {
      selectYear: '2019',
      selectSeason: '4',
      json: {}
    }
  },

  methods: {
    getApi: function() {
      axios.get('https://api.moemoe.tokyo/anime/v1/master/' + this.selectYear + '/' + this.selectSeason)
      .then((res) => {
        this.json = res;
      });
    }
  }
}
</script>

<style lang="scss">
html,body {
  height: 100%;
}
body {
  background-color: #eee;
}
.selectWrap {
  margin-bottom: 3rem;
}
.tileTtl {
  font-weight: bold;
}
.tileBox {
  margin-top: 0.5rem;
  dl {
    margin-top: 0.5rem;
  }
  dt {
    font-size: 0.8rem;
  }
}
</style>
