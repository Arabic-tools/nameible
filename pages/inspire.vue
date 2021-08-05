<template>
  <v-row>
    <v-col class="text-center">
      <img
        src="/v.png"
        alt="Vuetify.js"
        class="mb-5"
      >
      <blockquote class="blockquote">
        &#8220;First, solve the problem. Then, write the code.&#8221;
        <footer>
          <small>
            <em>&mdash;John Johnson</em>
          </small>
        </footer>
      </blockquote>
    </v-col>
  </v-row>
</template>
<style scoped>
.custom-container {
  max-width: 1000px;
  margin: 0 auto;
}
.banner-section {
  width: calc(100% + 32px);
  margin: -16px;
  align-items: center;
  display: flex;
  flex-wrap: wrap;
  box-sizing: border-box;
  padding: 16px;
}
@media (min-width: 768px) {
  .left-section {
    flex-grow: 0;
    max-width: 33.333333%;
    flex-basis: 33.333333%;
  }
}
.left-section {
  margin: 0;
  box-sizing: border-box;
}
@media (min-width: 768px) {
  .right-section {
    flex-grow: 0;
    max-width: 66.666667%;
    flex-basis: 66.666667%;
  }
}
.right-section {
  margin: 0;
  box-sizing: border-box;
  padding: 16px;
}

.VuetifyLogo {
  height: 180px;
  width: 180px;
  transform: rotateY(560deg);
  animation: turn 3.5s ease-out forwards 1s;
}

@keyframes turn {
  100% {
    transform: rotateY(0deg);
  }
}
.display-block {
  display: block;
}

.heading {
  color: #455065;
  font-size: 2.25rem;
  font-weight: 300;
  line-height: 1.25em;
  text-shadow: rgb(51, 51, 51) 0px 1px 1px;
}
.description {
  font-size: 1.25rem;
  line-height: 1.5em;
  font-weight: 400;
  color: #455065;
}
.sub-description {
  color: #455065;
  font-size: 1rem;
  line-height: 1.5em;
  font-weight: 400;
}
.link {
  color: #204ecf;
  cursor: pointer;
}

.featured-section {
  display: flex;
  flex-wrap: wrap;
  box-sizing: border-box;
  align-items: flex-start;
  width: calc(100% + 16px);
  margin: -8px;
}
@media (min-width: 992px) {
  .featured-section-left {
    flex-grow: 0;
    max-width: 66.666667%;
    flex-basis: 66.666667%;
  }
}
.featured-section-left {
  margin-bottom: 8px;
  box-sizing: border-box;
  display: inline-block;
}
.option-height {
  max-height: 200px;
}
.option-tag {
  color: #204ecf;
  padding-left: 16px;
  /*max-height: 0px;*/
  /*overflow: hidden;*/
  /*transition: max-height 0.4s ease-out 0s;*/
}
.option-tag:hover {
  text-decoration: underline;
  cursor: pointer;
}
.combination-text {
  color: #455065;
  font-size: 1.1428571428571428rem;
  font-weight: 400;
  line-height: 1.5;
}

.featured-title {
  display: inline-block;
  margin-right: 1rem;
  min-width: 4.5rem;
  padding-left: 16px;
}
/*.custom-text-field::v-deep .v-input__slot{*/
/*  width: 25%;*/
/*}*/
.custom-text-field::v-deep .v-input__control {
  width: 35px;
}
.active {
  background-color: #b6c0cd !important;
  /*color: blue;*/
}
.v-application .primary {
  background-color: #204ecf !important;
  border-color: #204ecf !important;
}
</style>
