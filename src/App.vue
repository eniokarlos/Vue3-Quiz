
<template>
	<div id="app">
		<h1>Super Quiz</h1>
	</div>
	<transition name="flip" mode="out-in">
		<Question :question="questions[questionIndex]" v-if="!isAnswered" @choiced="verifyAnswer"></Question>
		<Result @changeQuestion="toggleQuestion" v-else :correct="isCorrect"></Result>
	</transition>
</template>

<script>
/* eslint-disable */
import questions from './util/questions.js'
import Question from "./components/Question.vue";
import Result from './components/Result.vue'
export default {
	components: {Question, Result},
	data(){
		return{
			isCorrect: false,
			isAnswered: false,
			questionIndex: 0,
			questions 
		}
	},
	methods:{
		toggleQuestion(){
			this.questionIndex++
			this.isAnswered = false
		},
		verifyAnswer(answer){
			if(answer.correct){
				this.isCorrect = true
			}
			else{
				this.isCorrect = false
			}
			this.isAnswered = !this.isAnswered
		}
	}
}
</script>

<style>
body {
	background: linear-gradient(to right, rgb(0, 0, 70), rgb(28, 181, 224));
	font-family: 'Oswald', 'sans-serif';
	color: #FFF;
	height: 100vh;
}

#app {
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;

	display: flex;
	flex-direction: column;
	align-items: center;
}

#app h1 {
	font-weight: 200;
	font-size: 4rem;
}

@keyframes flip-out {
	from { transform: rotateY(0deg); }
	to { transform: rotateY(90deg); }
}

@keyframes flip-in {
	from { transform: rotateY(90deg); }
	to { transform: rotateY(0deg); }
}

.flip-enter-active {
	animation: flip-in 0.3s ease;
}

.flip-leave-active {
	animation: flip-out 0.3s ease;
}
</style>
