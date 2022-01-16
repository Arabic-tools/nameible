<template>
  <div class="custom-container">
    <div class="mt-3">
      <div class="banner-section">
        <div class="right-section">
          <!-- <div class="mb-4 display-block">
            <h2 style="color: #ff6437" class="heading">Nameible.com</h2>
          </div> -->
          <div class="mb-4 display-block">
            <div class="mb-2 display-block">
              <p class="description">
                Nameible helps you generate catchy names for your business,
                startup, or any side project you work on using the following
                methods:
              </p>
            </div>
          </div>
          <div class="mb-2 display-block">
            <p
              v-for="(example, index) in examples"
              :key="index"
              class="sub-description"
            >
              {{ example }}
              (<a class="sub-description link" @click="makeExample(index + 1)">
                Example here</a
              >)
            </p>
          </div>
        </div>
      </div>
    </div>

    <v-container fluid>
      <v-row>
        <v-col cols="12" sm="4">
          <v-textarea
            label="Enter some words here (optional)"
            outlined
            rows="4"
            row-height="50"
            v-model="firstText"
            height="210"
          ></v-textarea>
        </v-col>
        <v-col cols="12" sm="4">
          <v-textarea
            label="Enter some words here (optional)"
            height="210"
            outlined
            rows="4"
            row-height="50"
            v-model="secondText"
          ></v-textarea>
        </v-col>
        <v-col cols="12" sm="4">
          <v-textarea
            label="Enter some words here (optional)"
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
      <!-- <p class="option-tag" @click="showOption = !showOption">
        + Extra Options
      </p> -->
      <v-btn class="ml-5" color="primary" rounded @click="reset"
        >Reset Field</v-btn
      >
    </div>
    <div>
      <div class="featured-section mt-3">
        <v-container fluid>
          <v-row align="center">
            Add a list of :
            <v-col class="d-flex" cols="12" sm="6" md="4">
              <v-select
                :items="items"
                label="Select Prefixes, Suffixes etc"
                outlined
                v-model="selectOption"
              ></v-select>
            </v-col>
            <v-col class="d-flex" cols="12" sm="6" md="3">
              <v-select
                :items="fields"
                label="Select Fields"
                outlined
                v-model="selectField"
                v-show="selectOption"
              ></v-select>
            </v-col>
            <v-col class="d-flex" cols="12" sm="6" md="3">
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
      </div>
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
        >Copy & Open GoDaddy</v-btn
      >
    </div>
  </div>
</template>
<script>
import {
  domainSuffix,
  domainPrefix,
  suffix,
  prefix,
  letters,
} from './data.json'

export default {
  data() {
    return {
      showOption: false,
      showCustomField: false,
      firstText: '',
      secondText: '',
      thirdText: '',
      combineText: '',
      separate: '',
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
      prefix,
      domainPrefix,
      letters,
      domainSuffix,
      examples: [
        '1- Add all English prefixes to your prefered word or term. ',
        '2- Add all English suffixes to your prefered word or term. ',
        '3- Add all popular domain prefixes to your prefered word or term. ',
        '4- Add all popular domain suffixes to your prefered word or term. ',
        '5- Replace a letter of your preferred word/term with another letter. Consider this play on the word "Coffeeshop". ',
        '6- Merge your preferred words/terms together, and check their domain availability. ',
      ],
    }
  },
  watch: {
    firstText() {
      this.firstTextArr = this.firstText.split('\n')
      this.firstTextArr = this.firstTextArr.map((val) => val.replace(' ', ''))
    },
    secondText() {
      this.secondTextArr = this.secondText.split('\n')
      this.secondTextArr = this.secondTextArr.map((val) => val.replace(' ', ''))
    },
    thirdText() {
      this.thirdTextArr = this.thirdText.split('\n')
      this.thirdTextArr = this.thirdTextArr.map((val) => val.replace(' ', ''))
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
    makeExample(example) {
      if (example === 1) {
        // english prefixes
        this.secondText = 'TestName1\n' + 'TestName2\n'
        this.firstText = this.prefix.join('\n')
      } else if (example === 2) {
        // english suffixes
        this.firstText = 'TestName1\n' + 'TestName2\n'
        this.secondText = this.suffix.join('\n')
      } else if (example === 3) {
        // domain prefixes
        this.secondText = 'TestName1\n' + 'TestName2\n'
        this.firstText = this.domainPrefix.join('\n')
        this.thirdText = '.com\n' + '.net\n' + '.org'
      } else if (example === 4) {
        // domain suffixes
        this.firstText = 'TestName1\n' + 'TestName2\n'
        this.secondText = this.domainSuffix.join('\n')
        this.thirdText = '.com\n' + '.net\n' + '.org'
      } else if (example === 5) {
        this.firstText = 'coffee'
        this.secondText = this.letters.join('\n')
        this.thirdText = 'op\n'
      } else if (example === 6) {
        this.firstText = 'Red\n' + 'Blue\n' + 'Yellow\n'
        this.secondText = 'CoffeeShop\n' + 'coffee\n'
      }
      setTimeout(() => {
        this.mergeText()
      }, 500)
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
        window.open('https://www.godaddy.com/domains/bulk-domain-search')
    },
  },
}
</script>
