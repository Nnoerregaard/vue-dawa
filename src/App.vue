<template>
  <div>
    <div id="main_container">
      <nav>
        <div class="nav-wrapper">
          <div class="container">
            <a
              href="#"
              class="brand-logo"
            >
              {{ moduleName }} v.{{ moduleVersion }}
              <sup>
                <a
                  href="https://travis-ci.org/AncaIO/vue-dawa"
                  target="_blank"
                >
                  <img
                    alt="travis report"
                    src="https://travis-ci.org/AncaIO/vue-dawa.svg?branch=master"
                  >
                </a>
              </sup>
            </a>
            <ul
              id="nav-mobile"
              class="right hide-on-med-and-down"
            >
              <li>
                <a
                  href="https://www.anca.io"
                  target="_blank"
                >
                  <i class="fas fa-home" />
                </a>
              </li>
              <li>
                <a
                  :href="repo"
                  target="_blank"
                >
                  <i class="fab fa-github" />
                </a>
              </li>
              <li>
                <a
                  :href="bugs"
                  target="_blank"
                >
                  <i class="fas fa-bug" />
                </a>
              </li>
              <li>
                <a
                  href="https://www.npmjs.com/package/@ancaio/vue-dawa"
                  target="_blank"
                >
                  <i class="fab fa-npm" />
                </a>
              </li>
              <li>
                <a
                  href="https://www.linkedin.com/in/ancaio"
                  target="_blank"
                >
                  <i class="fab fa-linkedin-in" />
                </a>
              </li>
            </ul>
          </div>
        </div>
      </nav>
      <div class="container field-container-no">
        <div class="row">
          <div class="col l4">
            <vue-dawa
              :val="firstAddress.oneLineAddress"
              :show-max="10"
              placeholder="Demo placeholder"
              container-id="container-0"
              field-id="field-0"
              field-name="field-0"
              field-classes="boo"
              container-classes="yah"
              :list-classes="{'banana': true}"
              :list-item-classes="{'papaya': true}"
              @select="selectItem($event, 'firstAddress')"
            >
              <label
                slot="label-top"
                for="field-0"
              >With an initial oneline address</label>
            </vue-dawa>
            <div class="clear" />
            <pre>
              <code>{{ firstAddress }}</code>
            </pre>
          </div>
          <div class="col l4">
            <vue-dawa
              :val="secondAddress.oneLineAddress"
              :address-id="secondAddress.id"
              :show-max="5"
              placeholder="Demo placeholder"
              container-id="container-1"
              field-id="field-1"
              field-name="field-1"
              @select="selectItem($event, 'secondAddress')"
            >
              <label
                slot="label-top"
                for="field-1"
              >Empty initial value, with DAWA address ID</label>
            </vue-dawa>
            <div class="clear" />
            <pre>
              <code>{{ secondAddress }}</code>
            </pre>
          </div>
          <div class="col l4">
            <vue-dawa
              :val="thirdAddress.oneLineAddress"
              :show-max="5"
              placeholder="Demo placeholder"
              container-id="container-2"
              field-id="field-2"
              field-name="field-2"
              @select="selectItem($event, 'thirdAddress')"
            >
              <label
                slot="label-top"
                for="field-2"
              >Empty oneline address</label>
            </vue-dawa>
            <div class="clear" />
            <pre>
              <code>{{ thirdAddress }}</code>
            </pre>
          </div>
        </div>
      </div>
      <footer class="page-footer">
        <p>
          © 2011 - {{ new Date(Date.now()).getFullYear() }}
          <a
            href="https://www.anca.io"
            target="_blank"
          >Anca I/O</a>
        </p>
      </footer>
    </div>
  </div>
</template>

<script type="text/javascript">
import VueDawa from './components/index'
const VERSION = JSON.stringify(require('../package.json').version).replace(
  /"/g,
  ''
)
const NAME = JSON.stringify(
  require('../package.json').config.prettyName
).replace(/"/g, '')
const REPO = JSON.stringify(require('../package.json').homepage).replace(
  /"/g,
  ''
)
const BUGS = JSON.stringify(require('../package.json').bugs.url).replace(
  /"/g,
  ''
)
export default {
  components: {
    VueDawa
  },
  data () {
    return {
      moduleName: NAME,
      moduleVersion: VERSION,
      repo: REPO,
      bugs: BUGS,
      firstAddress: {
        oneLineAddress: 'Tagensvej'
      },
      secondAddress: {
        id: '0a3f50a3-4152-32b8-e044-0003ba298018'
      },
      thirdAddress: {
        oneLineAddress: ''
      }
    }
  },
  methods: {
    selectItem (event, object) {
      this.$set(this, object, this.translateData(event))
    },
    translateData (address) {
      return {
        id: address.data.id,
        street: address.data.vejnavn,
        streetNumber: address.data.husnr,
        floor: address.data.etage,
        door: address.data.dør,
        zipCode: address.data.postnr,
        city: address.data.postnrnavn,
        oneLineAddress: address.tekst
      }
    }
  }
}
</script>
<style lang="css">
html,
body {
  min-height: 100vh;
  height: 100%;
  background-color: silver;
}
#main_container {
  min-height: 100vh;
}
.field-container {
  margin-top: 50px;
  max-height: 250px;
  overflow: hidden;
  background: white;
  padding: 40px 40px 40px 40px;
}
.field-container-no {
  margin-top: 75px;
  background: white;
  padding: 40px 40px 40px 40px;
}
h1 > small {
  font-size: 60%;
}
h1 code {
  font-size: 75%;
  background: silver;
  padding: 2px 10px;
  border-radius: 4px;
}
footer {
  position: fixed;
  width: 100%;
  bottom: 0;
}
.page-footer {
  padding: 0;
}
.page-footer p {
  text-align: center;
  width: 100%;
}
.page-footer a {
  color: white;
  font-weight: 500;
  margin-left: 15px;
}
</style>
