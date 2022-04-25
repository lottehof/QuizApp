<script setup>
import { ref, computed } from 'vue'
const questions = ref([
  {
	question: 'Wat voor frontend developer bent u?',
  answer: 0,
  answerVue: 1,
	options: [
		'Geen',
		'Junior',
		'Medior',
    'Senior'

	],
	selected: null
  },
  {
	question: 'Wat is uw ervaring met React?',
	answer: 0,
  answerVue: 1,
	options: [
		'Geen',
		'Weinig',
		'Gemiddeld',
    'Veel'
	],
	selected: null
  },
  {
	question: 'Wat is uw ervaring met Vue?',
  answer: 2,
  answerVue: 3,
	options: [
		'Geen',
		'Weinig',
		'Gemiddeld',
    'Veel'
	],
	selected: null
  },
  {
	question: 'Hoe lang is de ontwikkelingstijd?',
  answer: 0,
  answerVue: 0,
	options: [
		'< 2 maand',
		'3 - 4 maanden',
    '> 5 maanden'
	],
	selected: null
},
{
question: 'Hoe complex is de applicatie',
answer: 0,
answerVue: 0,
options: [
  'Simpel',
  'Medium',
  'Erg complex',
],
selected: null
}



])
const quizCompleted = ref(false)
const currentQuestion = ref(0)
const Vue = ref(false)

const score = computed(() => {
	let value = 0
  let Vuevalue = 0
	questions.value.map(q => {
		if (q.selected != null && q.answer == q.selected || q.selected != null && q.answerVue == q.selected ) {
			console.log('correct');
			value++
		}
	})
	return value
})

const getCurrentQuestion = computed(() => {
	let question = questions.value[currentQuestion.value]
	question.index = currentQuestion.value
	return question
})

const SetAnswer = (e) => {
	questions.value[currentQuestion.value].selected = e.target.value
	e.target.value = null
}
const NextQuestion = () => {
	if (currentQuestion.value < questions.value.length - 1) {
		currentQuestion.value++
    console.log(score.value);
    if (score.value >= 3){
      console.log("score hoger dan 5");
  		return Vue.value = true
  	}
		return
	}

	quizCompleted.value = true
}

</script>

<template>
	<main class="app">
    <section class="container">
  		<h1>React vs Vue Quiz</h1>
      <section class="qi" v-if="!quizCompleted">


  		<section class="quiz" >
  			<div class="quiz-info">
  				<span class="question">{{ getCurrentQuestion.question }}</span>
  			</div>

  			<div class="options">
  				<label
  					v-for="(option, index) in getCurrentQuestion.options"
  					:for="'option' + index"
            :class="`option ${
  						getCurrentQuestion.selected == index

  					} ${
  						getCurrentQuestion.selected != null &&
  						index != getCurrentQuestion.selected
  							? 'disabled'
  							: ''
  					}`">
  					<input
  						type="radio"
  						:id="'option' + index"
  						:name="getCurrentQuestion.index"
  						:value="index"
  						v-model="getCurrentQuestion.selected"
  						@change="SetAnswer"
  					/>
  					<span>{{ option }}</span>
  				</label>
  			</div>

  			<button
  				@click="NextQuestion"
  				:disabled="!getCurrentQuestion.selected">
  				{{
  					getCurrentQuestion.index == questions.length - 1
  						? 'Finish'
  						: getCurrentQuestion.selected == null
  							? 'Maak een keuze'
  							: 'Volgende vraag'
  				}}
  			</button>
		</section>
  </section>
		<section v-else  class="">
      <div class="box" v-if="!Vue">
        <div class="winner-container">
          <div class="medal">
              <img class="medal-image" src="./assets/medal.png" alt="">
          </div>
          <div class="winner-text">
            <h2 class="style__H2">Framework Winner</h2>
            <p class="style__p">React</p>
          </div>
          <div class="medal">
              <img class="medal-image" src="./assets/medal.png" alt="">
          </div>
        </div>
        <div class="content">
          <div class="flex-delen">
              <div class="delen">
                <section class="section">
                  <h3 class="H2_delen">Voordelen</h3>
                  <ul class="list">
                    <li class="listitem"><b>Beschikbaarheid</b><br>React heeft een groter gemeenschap en ecosysteem dan Vue. Er is veel documentatie en kant-en-klare oplossingen beschikbaar. Hierdoor  is React geschikter voor grotere applicaties.</li>
                    <li class="listitem"><b>Efficiëntie</b><br>React is het meest efficiënt bij groter applicaties, mede door de kant-en klare oplossingen, maar ook door het brede ecosysteem wat ze hebben.</li>
                    <li class="listitem"><b>Snelheid</b><br>React is erg snel, dit komt omdat React met een Virtuele DOM werkt. Vue is net iets sneller dan React, echter is het verschil in snelheid zo klein dat een eindgebruiker dit niet merkt.</li>
                  </ul>
                </section>
              </div>
              <div class="delen">
                <section class="section">
                  <h3 class="H2_delen">Nadelen</h3>
                  <ul class="list">
                    <li class="listitem"><b>Gebruiksgemak</b><br>React is lastiger te leren dan Vue, maar indien een project een lange ontwikkelingstijd heeft en de applicatie is medium/erg complex is React wel geschikter dan Vue in verband met het ecoysteem van React.</li>
                    <li class="listitem">React heeft een groter gemeenschap dan Vue. Er is hierdoor veel documentatie en kant-en-klare oplossingen beschikbaar. </li>
                    <li class="listitem">De documentatie is slecht gestructureerd. </li>
                  </ul>
                </section>
              </div>
          </div>
        </div>
      </div>

      <div class="result" v-if="Vue">
        <div class="winner-container">
          <div class="medal">
              <img class="medal-image" src="./assets/medal.png" alt="">
          </div>
          <div class="winner-text">
            <h2 class="style__H2">Framework Winner</h2>
            <p class="style__p">Vue</p>
          </div>
          <div class="medal">
              <img class="medal-image" src="./assets/medal.png" alt="">
          </div>
        </div>
        <div class="content">
          <div class="flex-delen">
              <div class="delen">
                <section class="section">
                  <h3 class="H2_delen">Voordelen</h3>
                  <ul class="list">
                    <li class="listitem"><b>Gebruiksgemak</b><br>Vue heeft een minder stijle leercurve, en is daardoor makkelijker te leren.  </li>
                    <li><b>Efficiëntie</b><br>Vue is het meest efficiënt bij kleinschalige applicatiess, die snel opgeleverd moeten worden. Dit in verband met de minder stijle leercurve.</li>
                    <li class="listitem">De documentatie van Vue is erg gestructureerd.</li>
                    <li><b>Snelheid</b><br>Vue is erg snel, dit komt omdat Vue met een Virtuele DOM werkt. Vue is net iets sneller dan React, echter is het verschil in snelheid zo klein dat een eindgebruiker dit niet merkt.</li>
                  </ul>
                </section>
              </div>
              <div class="delen">
                <section class="section">
                  <h3 class="H2_delen">Nadelen</h3>
                  <ul class="list">
                    <li class="listitem"><b>Beschikbaarheid</b><br>Vue heeft een kleiner ecosyteem dan React, er zijn hierdoor minder kant-en-klare oplossingen beschikbaar. </li>
                    <li class="listitem">Vue is heel flexibel, maar het gevaar hiervan is dat het kan leiden tot spaghetti code.</li>
                  </ul>
                </section>
              </div>
          </div>
        </div>
      </div>
		  </section>
    </section>
	</main>

</template>

<style>
* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
	font-family: 'Montserrat', sans-serif;
}
h1 {
	font-size: 2rem;
  color: #FFF;
  text-align: center;
  margin-top: 2rem;
  padding: 1rem;
  /* padding: 2rem;
  font-size: 3rem
  margin-bottom: 3rem; */

}
h2 {
	margin-bottom: 2rem;
	text-align: center;
  font-family: 'Roboto';
  font-style: normal;
  font-weight: 400;
  font-size: 28px;
  line-height: 47px;
  display: flex;
  align-items: center;
  letter-spacing: 0.03em;
  color: #FFFFFF;
}
p {
  font-family: 'Roboto';
  font-style: normal;
  font-weight: 700;
  font-size: 60px;
  line-height: 70px;
  letter-spacing: 0.03em;
  color: #FFFFFF;
}

.app {
	display: flex;
	flex-direction: column;
	align-items: center;
	padding: 1rem;
	/* padding: 2rem; */
	min-height: 100vh;
  max-height: 200vh;

  background-color: #F6DDF2;
}
.container{
  border-radius: 30px;
  /* flex-grow: 1; */
  background: linear-gradient(0deg, rgba(23, 36, 63, 0.5), rgba(23, 36, 63, 0.5)), rgba(122, 203, 206, 0.57);
}
.qi{
  padding: 1rem;
  /* padding: 2rem; */
}
.quiz {
  background: #FFFFFF;
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
  border-radius: 30px;
	padding: 1rem;
	width: 100%;
	max-width: 640px;
}
.quiz-info {
	display: flex;
  align-items: center;
  justify-content: center;
	margin-bottom: 1.5rem;
  margin-top: 1.5rem;
  /* margin-bottom: 3rem; */
  /* margin-top: 3rem; */
}
.quiz-info .question {
  font-family: 'Inter';
  font-style: normal;
  font-weight: 500;
  /* font-size: 38px; */
  /* padding: 0 1rem; */
  line-height: 48px;
  display: flex;
  align-items: center;
  text-align: center;
  color: #000000;
  font-size: 28px;
}
.question{
  font-family: 'Inter';
  font-style: normal;
  font-weight: 500;
  font-size: 40px;
  line-height: 48px;
  display: flex;
  align-items: center;
  text-align: center;
  color: #000000;

}
.options {
	margin-bottom: 1rem;
}
.option {
	padding: 1rem;
	display: block;
	background: #F6DDF2;
	margin-bottom: 0.5rem;
	border-radius: 0.5rem;
	cursor: pointer;
}
.option:hover {
	background-color: rgba(28, 136, 147, 1);
}

.option.disabled {
	opacity: 0.5;
}
.option input {
	display: none;
}
button {
	appearance: none;
	outline: none;
	border: none;
	cursor: pointer;
	padding: 0.5rem 1rem;
	background-color: #2cce7d;
	color: #2d213f;
	font-weight: 700;
	text-transform: uppercase;
	font-size: 1.2rem;
	border-radius: 0.5rem;
}
button:disabled {
	opacity: 0.5;
}
.medal-image{
  width: 50px;
  height: 50px;
  /* width: 150px;
  height: 150px; */
}
.medal{
  margin-left: 20px;
  margin-right: 20px;
  /* width: 150px; */
}
.style__H2{
  font-size: 20px;
  margin-bottom: 0;
}
.style__p{
  font-size: 26px;
}
.winner-container{
  width: 100%;
  display: flex;
  padding-top: 3rem;
  margin: 0 auto;
}
.winner-text{
  text-align: center;
  margin: 0 auto;
}
.box{

}
.content{
  /* width: 90vw; */
  background: linear-gradient(0deg, rgba(234, 203, 180, 0.2), rgba(234, 203, 180, 0.2)), #1C8893;
  border-radius: 30px;
  margin-top: 3rem;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.H2_delen{
  margin-top: 1rem;
  /* font-size: 40px; */
  line-height: 47px;
  display: flex;
  align-items: center;
  color: #FFFFFF;
  font-size: 22px;

}
.flex-delen{
  flex-direction: column;
  margin: 0 auto;
  width: 90vw;

}

.delen{
  display: column;
  width: 100%;
  margin: 0 auto;
}

.section{
  width: 60%;
  vertical-align: center;
  margin-left: auto;
  margin-right: auto;
}

li{
  /* font-size: 24px; */
  line-height: 35px;
  margin-top: 1rem;
  margin-bottom: 1rem;
  color: #FDFDFD;
  font-size: 18px;
}
.list{
  /* padding-left: 2rem; */
  height: 100%;
}
@media (min-width: 820px) {
  h1{
    padding: 1.5rem;
    font-size: 2.5rem;
    margin-bottom: 1.5rem;
  }
  .app{
    padding: 1.5rem;

  }
  .style__H2{
    font-size: 28px;
  }
  .style__p{
    font-size: 32px;
  }
  .winner-container{
    width: 80%;
  }
  .medal-image{
    width: 100px;
    height: 100px;
    /* width: 150px;
    height: 150px; */
  }
  .flex-delen{
    display: table;
    margin: 0 auto;
    width: 90vw;
    min-height: 450px;
  }
  .delen{
    display: table-cell;
    width: 400px;
    margin: 0 auto;
  }
}

@media (min-width:1200px) {
.winner-container{
  width: 55%;
}
.winner-container{
  width: 55%;
}
.else-box{
  height: 100%;
}
.box{
  height: 100%;
}

}

</style>
