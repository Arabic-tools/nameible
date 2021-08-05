<template>
  <div class="custom-container">
    <div class="mt-3">
      <div class="banner-section">
        <div class="right-section">
          <div class="mb-4 display-block">
            <h1 class="heading">WordsMerge.om</h1>
          </div>
          <div class="mb-4 display-block">
            <div class="mb-2 display-block">
              <p class="description">Merge and combine words fast and easy.</p>
            </div>
            <div class="mb-2 display-block">
              <p class="description">
                Use it for naming, domaining, Google Ads, PPC etc.
              </p>
            </div>
            <div class="mb-2 display-block">
              <p class="description">
                Or use it as a business & brand name generator.
              </p>
            </div>
          </div>
          <div class="mb-2 display-block">
            <p class="sub-description">
              Type your keywords in the 3 boxes and press
              <a class="sub-description link" tabindex="0" @click="mergeText"
                >Merge!</a
              >
            </p>
          </div>
          <p class="sub-description">
            Or load some sample data (<a
              class="sub-description link"
              @click="Domain"
              tabindex="0"
              >Domaining</a
            >,
            <a class="sub-description link" @click="link" tabindex="0"
              >Linkbuilding</a
            >,
            <a class="sub-description link" @click="adwords" tabindex="0"
              >Adwords</a
            >)
          </p>
        </div>
      </div>
    </div>

    <v-container fluid>
      <v-row>
        <v-col cols="12" sm="4">
          <v-textarea
            label="Enter some words here"
            outlined
            rows="4"
            row-height="50"
            v-model="firstText"
            height="210"
          ></v-textarea>
        </v-col>
        <v-col cols="12" sm="4">
          <v-textarea
            label="Enter some words here"
            height="210"
            outlined
            rows="4"
            row-height="50"
            v-model="secondText"
          ></v-textarea>
        </v-col>
        <v-col cols="12" sm="4">
          <v-textarea
            label="Enter some words here"
            outlined
            rows="4"
            row-height="50"
            v-model="thirdText"
            height="210"
          ></v-textarea>
        </v-col>
      </v-row>
    </v-container>
    <div class="featured-section">
      <p class="option-tag" @click="showOption = !showOption">
        + Extra Options
      </p>
      <v-btn class="ml-5" color="primary" rounded @click="reset"
        >Reset Field</v-btn
      >
    </div>
    <div v-show="showOption === true">
      <div class="featured-section mt-3">
        <div class="featured-section-left">
          <span class="featured-title">Separator:</span>
          <v-btn
            class="mb-2"
            @click="
              separate = ''
              showCustomField = false
              isActive = 'Nothing'
            "
            color="#dfe3e9"
            depressed
            :class="[isActive === 'Nothing' ? 'active' : '']"
            >Nothing</v-btn
          >
          <v-btn
            class="mb-2"
            @click="
              separate = ' '
              showCustomField = false
              isActive = 'Space'
            "
            color="#dfe3e9"
            depressed
            :class="[isActive === 'Space' ? 'active' : '']"
            >Space</v-btn
          >
          <v-btn
            class="mb-2"
            @click="
              separate = '-'
              showCustomField = false
              isActive = 'Minus'
            "
            color="#dfe3e9"
            depressed
            :class="[isActive === 'Minus' ? 'active' : '']"
            >Minus</v-btn
          >
          <v-btn
            class="mb-2"
            @click="
              separate = '+'
              showCustomField = false
              isActive = 'Plus'
            "
            color="#dfe3e9"
            depressed
            :class="[isActive === 'Plus' ? 'active' : '']"
            >Plus</v-btn
          >
          <v-btn
            class="mb-2"
            @click="
              showCustomField = true
              separate = ''
              isActive = 'Custom'
            "
            color="#dfe3e9"
            depressed
            :class="[isActive === 'Custom' ? 'active' : '']"
            >Custom
            <v-text-field
              class="custom-text-field"
              v-if="showCustomField"
              v-model="separate"
            ></v-text-field
          ></v-btn>
        </div>
        <div class="">
          <div class="">
            <span class="featured-title">Wrap in:</span>
            <v-btn
              @click="
                wrapStart = ''
                wrapEnd = ''
                activeWrap = 'Nothing'
              "
              color="#dfe3e9"
              depressed
              :class="[activeWrap === 'Nothing' ? 'active' : '']"
              >Nothing</v-btn
            >
            <v-btn
              @click="
                wrapping()
                activeWrap = ''
              "
              color="#dfe3e9"
              depressed
              :class="[activeWrap === '' ? 'active' : '']"
              >" "</v-btn
            >
            <v-btn
              @click="
                wrapStart = '['
                wrapEnd = ']'
                activeWrap = '[]'
              "
              color="#dfe3e9"
              depressed
              :class="[activeWrap === '[]' ? 'active' : '']"
              >[]</v-btn
            >
          </div>
        </div>
      </div>
      <v-container fluid>
        <v-row align="center">
          <v-col class="d-flex" cols="12" sm="6" md="4">
            <v-select
              :items="items"
              label="Select Prefixes, Suffixes etc"
              outlined
              v-model="selectOption"
            ></v-select>
          </v-col>
          <v-col class="d-flex" cols="12" sm="6" md="4">
            <v-select
              :items="fields"
              label="Select Fields"
              outlined
              v-model="selectField"
              v-show="selectOption"
            ></v-select>
          </v-col>
          <v-col class="d-flex" cols="12" sm="6" md="4">
            <v-btn
              class="mb-8"
              color="primary"
              @click="add"
              v-show="selectOption && selectField"
              rounded
              >Add</v-btn
            >
          </v-col>
        </v-row>
      </v-container>
    </div>
    <h2 class="text-center mt-5 combination-text" v-if="combine.length">
      {{ combine.length }} combinations possible
    </h2>
    <h2 class="text-center mt-5 combination-text" v-else>
      0 combinations possible
    </h2>
    <div class="text-center">
      <v-btn class="mt-5 mb-5" color="primary" @click="mergeText">Merge</v-btn>
    </div>
    <v-textarea
      outlined
      rows="4"
      row-height="50"
      id="myInput"
      v-model="combineText"
      height="250"
    ></v-textarea>
    <div class="featured-section">
      <v-btn color="primary" @click="copy(false)">Copy All</v-btn>
      <v-btn color="primary" class="ml-5" @click="copy(true)"
        >Copy $ Open GoDaddy</v-btn
      >
    </div>
  </div>
</template>
<script>
import { domainSuffix, domainPrefix, suffix } from './data.json'

export default {
  data() {
    return {
      showOption: false,
      showCustomField: false,
      firstText: '',
      secondText: '',
      thirdText: '',
      combineText: '',
      separate: ' ',
      wrapStart: '',
      wrapEnd: '',
      isActive: 'Space',
      activeWrap: 'Nothing',
      firstTextArr: [],
      secondTextArr: [],
      thirdTextArr: [],
      selectOption: '',
      selectField: '',
      copyText: '',
      items: [
        {
          text: 'All English Prefixes (re-, dis-, un-, mis- ...)',
          value: 'prefix',
        },
        {
          text: 'All English Suffixes ( -able, -ness, -ify...)',
          value: 'suffix',
        },
        { text: 'Most Common Domain prefixes', value: 'domainPrefix' },
        { text: 'Most Common Domain Suffixes', value: 'domainSuffix' },
        { text: 'Add English letters A,B,C,....Z', value: 'letters' },
      ],

      fields: [
        { text: 'First Text Field', value: 'firstText' },
        { text: 'Second Text Field', value: 'secondText' },
        { text: 'Third Text Field', value: 'thirdText' },
      ],

      suffix,

      prefix: [
        'a-',
        'an-',
        'ante-',
        'anti-',
        'auto-',
        'circum-',
        'co-',
        'com-',
        'con-',
        'contra-',
        'contro-',
        'de-',
        'dis-',
        'en-',
        'ex-',
        'extra-',
        'hetero-',
        'homo-',
        'homeo-',
        'hyper-',
        'il-',
        'im-',
        'in-',
        'ir-',
        'inter-',
        'intra-',
        'intro-',
        'macro-',
        'micro-',
        'mono-',
        'non-',
        'omni-',
        'post-',
        'pre-',
        'pro-',
        'sub-',
        'sym-',
        'syn-',
        'tele-',
        'trans-',
        'tri-',
        'un-',
        'uni-',
        'up',
      ],

      domainPrefix,

      domainSuffix,

      letters: [
        'A',
        'B',
        'C',
        'D',
        'E',
        'F',
        'G',
        'H',
        'I',
        'J',
        'K',
        'L',
        'M',
        'N',
        'O',
        'P',
        'Q',
        'R',
        'S',
        'T',
        'U',
        'V',
        'W',
        'X',
        'Y',
        'Z',
      ],
    }
  },
  watch: {
    firstText() {
      this.firstTextArr = this.firstText.split('\n')
    },
    secondText() {
      this.secondTextArr = this.secondText.split('\n')
    },
    thirdText() {
      this.thirdTextArr = this.thirdText.split('\n')
    },
  },
  computed: {
    combine() {
      const combos = [] // or combos = new Array(2);
      // when all inputs have some data
      if (
        this.firstText.length > 0 &&
        this.secondTextArr.length > 0 &&
        this.thirdTextArr.length > 0
      ) {
        for (let i = 0; i < this.firstTextArr.length; i++) {
          for (let j = 0; j < this.secondTextArr.length; j++) {
            for (let k = 0; k < this.thirdTextArr.length; k++) {
              combos.push(
                this.firstTextArr[i] +
                  ',' +
                  this.secondTextArr[j] +
                  ',' +
                  this.thirdTextArr[k]
              )
            }
          }
        }
      }
      //  when first and second input fields have some data
      else if (this.firstText.length > 0 && this.secondTextArr.length > 0) {
        for (let i = 0; i < this.firstTextArr.length; i++) {
          for (let j = 0; j < this.secondTextArr.length; j++) {
            // you would access the element of the array as array1[i] and array2[j]
            // create and array with as many elements as the number of arrays you are to combine
            // add them in
            // you could have as many dimensions as you need
            combos.push(this.firstTextArr[i] + ',' + this.secondTextArr[j])
          }
        }
      }
      //  when first and third input fields have some data
      else if (this.firstText.length > 0 && this.thirdTextArr.length > 0) {
        for (let i = 0; i < this.firstTextArr.length; i++) {
          for (let k = 0; k < this.thirdTextArr.length; k++) {
            combos.push(this.firstTextArr[i] + ',' + this.thirdTextArr[k])
          }
        }
      }
      //  when first  input fields have some data
      else {
        for (let i = 0; i < this.firstTextArr.length; i++) {
          combos.push(this.firstTextArr[i])
        }
      }
      return combos
    },
  },
  beforeMount() {
    this.triggerConversion()
  },

  methods: {
    triggerConversion() {
      setTimeout(function () {
        //  gtag('config', 'AW-1006620676');
        //  gtag('event', 'conversion', {'send_to': 'AW-1006620676/2s0cCPLN-90CEISg_98D'});
      }, 120000)
    },
    mergeText() {
      const arr = []
      this.combine.forEach((data) => {
        const newArray = data.split(',')
        if (newArray.length > 2) {
          arr.push(
            (this.separate === '+' ? this.separate : '') +
              this.wrapStart +
              newArray[0] +
              this.separate +
              newArray[1] +
              this.separate +
              newArray[2] +
              this.wrapEnd
          )
        } else if (newArray.length > 1) {
          arr.push(
            (this.separate === '+' ? this.separate : '') +
              this.wrapStart +
              newArray[0] +
              this.separate +
              newArray[1] +
              this.wrapEnd
          )
        } else {
          arr.push(
            (this.separate === '+' ? this.separate : '') +
              this.wrapStart +
              newArray[0] +
              this.wrapEnd
          )
        }
      })
      this.combineText = arr.toString().replace(/,/g, '\n')
    },
    wrapping() {
      this.wrapStart = '"'
      this.wrapEnd = '"'
    },
    Domain() {
      this.firstText = ' iphone\n' + 'ipad\n' + 'ipod\n' + 'imac\n' + 'macbook'
      this.secondText =
        'world\n' +
        'life\n' +
        'web\n' +
        'planet\n' +
        'hub\n' +
        'center\n' +
        'club\n' +
        'central\n' +
        'spot\n' +
        'base\n' +
        'stuff'
      this.thirdText = '.com\n' + '.net\n' + '.org'
    },
    link() {
      this.firstText =
        'mountaineering\n' + 'climbing\n' + 'hiking\n' + 'trekking'
      this.secondText =
        'websites\n' + 'links\n' + '"add url"\n' + '"suggest a site"'
      this.thirdText =
        'intitle:list\n' +
        'inurl:resources\n' +
        'OR "suggest URL"\n' +
        'OR resources'
    },
    adwords() {
      this.firstText = 'ladies\n' + 'women\n' + 'designer\n' + 'fashion'
      this.secondText = 'shoes\n' + 'boots\n' + 'sandals\n' + 'stiletto heels'
      this.thirdText =
        'New York\n' + 'New Jersey\n' + 'Long Island City\n' + 'Manhattan'
    },
    add() {
      let options = []
      let field = ''
      const newArray = []
      switch (this.selectOption) {
        case 'prefix':
          options = this.prefix
          break
        case 'suffix':
          options = this.suffix
          break
        case 'domainPrefix':
          options = this.domainPrefix
          break
        case 'domainSuffix':
          options = this.domainSuffix
          break
        case 'letters':
          options = this.letters
          break
      }

      switch (this.selectField) {
        case 'firstText':
          field = this.firstTextArr
          break
        case 'secondText':
          field = this.secondTextArr
          break
        case 'thirdText':
          field = this.thirdTextArr
          break
      }
      if (field.length) {
        options.map((option) => {
          field.map((text) => {
            if (
              this.selectOption === 'suffix' ||
              this.selectOption === 'domainSuffix'
            ) {
              newArray.push(text + option)
            } else {
              newArray.push(option + text)
            }
          })
        })
        switch (this.selectField) {
          case 'firstText':
            this.firstText = newArray.toString().replace(/,/g, '\n')
            break
          case 'secondText':
            this.secondText = newArray.toString().replace(/,/g, '\n')
            break
          case 'thirdText':
            this.thirdText = newArray.toString().replace(/,/g, '\n')
            break
        }
      } else {
        switch (this.selectField) {
          case 'firstText':
            this.firstText = options.toString().replace(/,/g, '\n')
            break
          case 'secondText':
            this.secondText = options.toString().replace(/,/g, '\n')
            break
          case 'thirdText':
            this.thirdText = options.toString().replace(/,/g, '\n')
            break
        }
      }
    },
    reset() {
      this.firstText = ''
      this.secondText = ''
      this.thirdText = ''
      this.combineText = ''
    },
    copy(key) {
      const copyText = document.getElementById('myInput')
      copyText.select()
      copyText.setSelectionRange(0, 99999) /* For mobile devices */
      document.execCommand('copy')
      //  this.combineText = ''
      if (key === true)
        window.open('https:// www.godaddy.com/domains/bulk-domain-search')
    },
  },
}
</script>

