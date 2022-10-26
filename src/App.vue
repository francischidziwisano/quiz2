<template>
        <div class="flex w-full h-screen justify-center items-center" id="app">
            <div class="w-full max-w-xl">
              <img alt="Vue logo" class="m-10 mx-auto w-44" src="./assets/logo.png" />
                <h1 class="font-bold text-3xl text-center text-indigo-700">
                    Malawi Simple Quiz
                </h1>
                <div class="bg-white p-4 text-left rounded-lg shadow-lg w-full mt-8">
                    <div v-if="index < questions.length">
                        <p class="text-2xl font-bold">
                            {{ questions[index]['question'] }}
                        </p>      
                        <label
                            :for="key"
                            class="block mt-4 border border-gray-300 rounded-lg py-2 px-6 text-lg"
                            v-for="(answer, key) in questions[index]['answers']" :key="answer.question"
                            :class="[
                                selectedAnswer == key ? 'bg-red-200' : 'hover:bg-gray-100 cursor-pointer', 
                                key == questions[index]['correctAnswer'] && selectedAnswer != '' ? 'bg-green-200' : 'hover:bg-gray-100 cursor-pointer'

                            ]                
                        "

                        >
                            <input
                                type="radio"
                                :id="key"
                                class="hidden"
                                :value="key"
                                @change="answered($event)"
                                v-model="selectedAnswer"
                                :disabled="selectedAnswer != ''"
                            />
                            {{ answer }}
                        </label>
                
                        <div class="mt-6 flow-root">
                            <button
                                class="float-right px-5 py-2 bg-indigo-600 text-white text-sm font-bold tracking-wide rounded-full"
                                v-show="selectedAnswer != '' && index < (questions.length)-1"
                                @click="nextQuestion"
                            >
                                Next &gt;
                            </button>
                            <button
                                class="float-right px-5 py-2 bg-indigo-600 text-white text-sm font-bold tracking-wide rounded-full"
                                v-show="selectedAnswer != '' && index == (questions.length)-1"
                                @click="showResults"
                            >
                                Finish
                            </button>
                        </div>
                    </div>
                    <div v-else>
                        <h2 class="font-bold text-3xl">Results</h2>
                        <div class="flex justify-start space-x-4 mt-6">
                            <p>
                                Correct Answers:
                                <span class="text-2xl text-green-700 font-bold"
                                    >{{ correctAnswer }}</span
                                >
                            </p>
                            <p>
                                Wrong Answers:
                                <span class="text-2xl text-red-700 font-bold"
                                    >{{ wrongAnswer }}</span
                                >
                            </p>
                        </div>
                        <div class="mt-6 flow-root">
                            <button
                                class="float-right px-5 py-2 bg-indigo-600 text-white text-sm font-bold tracking-wide rounded-full"
                                @click="resetQuiz"
                            >
                                Play again
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import 'tw-elements'
import './index.css'

export default {
  name: 'App',
  components: {
    //HelloWorld
  },
  data() {
        return {
            index: 0,
            selectedAnswer: '',
            correctAnswer: 0,
            wrongAnswer: 0,
            
            questions: [
                {
                  question: "What is the real name for comedian - Manganya?",
                  answers: {
                  a: "Born Kalindo",
                  b: "Michael Usi",
                  c: "Eric Mabedi",
                  d: "John Nyanga"},
                  correctAnswer: "b",
                },
                {
                  question: "Who is the current president of Malawi?",
                  answers: {
                    a: "Chakwera",
                    b: "Chilima",
                    c: "Muluzi",
                    d: "Bingu"
                  },
                  correctAnswer: "a",
                },
                {
                  question: "How many districts are in Malawi?",
                  answers: {a: "31",
                  b: "28",
                  c: "30",
                  d: "32"},
                  correctAnswer: "b",
                },
                {
                  question: "How many regions are in Malawi?",
                  answers: {a: "Two",
                  b: "Five",
                  c: "Four",
                  d: "Three"},
                  correctAnswer: "d",
                },
                {
                  question: "Who composed and wrote Malawi's National Anthem?",
                  answers: {a: "Dr. Hastings Kamuzu Banda",
                  b: "Michael-Fredrick Paul Sauka",
                  c: "John Chilembwe",
                  d: "Aaron Gadama"},
                  correctAnswer: "b",
                },
                {
                  question: "What was the total population for Malawi at the time of census in 2018?",
                  answers: {a: "13,066,320",
                  b: "9,933,868",
                  c: "17,563,749",
                  d: "20,091,635"},
                  correctAnswer: "c",
                },  
                {
                  question: "How many districts are in Malawi's central region?",
                  answers: {a: "Eleven",
                  b: "Eight",
                  c: "Seven",
                  d: "Nine"},
                  correctAnswer: "c",
                },
                {
                  question: "What is the real name for the Musician - Piksy?",
                  answers: {a: "Evans Zangazanga",
                  b: "Zangazanga Chikhosi",
                  c: "Peter Zangazanga",
                  d: "Nicholus Mbonera"},
                  correctAnswer: "a",
                },
                {
                  question: "Professor Bingu wa Mutharika ruled Malawi in which years?",
                  answers: {a: "2005 to 2012",
                  b: "2004 to 2011",
                  c: "2004 to 2012",
                  d: "2004 to 2013"},
                  correctAnswer: "c",
                },
                {
                  question: "Shire river is in the following districts except?",
                  answers: {a: "Neno",
                  b: "Mangochi",
                  c: "Liwonde",
                  d: "Balaka"},
                  correctAnswer: "d",
                },
                {
                  question: "When did Dr. Hestings Kamuzu Died?",
                  answers: {a: "1996",
                  b: "1997",
                  c: "1998",
                  d: "1999"},
                  correctAnswer: "b",
                },
            ],
        }
    },
    methods: {
        answered(e) {
            this.selectedAnswer = e.target.value
            if(this.selectedAnswer == this.questions[this.index]['correctAnswer'])
                this.correctAnswer++
            else
                this.wrongAnswer++
        },
        nextQuestion() {
            this.index++
            this.selectedAnswer = ''
        },
        showResults() {
            this.index++
        },
        resetQuiz() {
            this.index = 0
            this.selectedAnswer = ''
            this.correctAnswer = 0
            this.wrongAnswer = 0
        }
    }
}

</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
  #body {
    background-color: #fff;
    background-image: linear-gradient(315deg, #b8c6db 0%, 3f5f7fa 74%);
    font-family: "Poppins", sans-serif;
    margin: 0;
    min-height: 100vh;
  }
  .logo{
    max-width: 200px;
    padding-bottom: 5px;
  }
  .quiz-container {
    text-align: center;
    margin: auto;
    background-color: #fff;
    border-radius: 10px;
    box-shadow: 0 0 10px 5px rgb(100, 100, 100, 0.1);
    width: 600px;
    max-width: 100%;
  }
  .quiz-header {
    padding: 4rem;
  }
  ul {
    list-style-type: none;
    padding: 0;
  }
  label{
    padding: 10px;
    cursor: pointer;
  }
  ul li {
    text-align: left;
    padding-left: 5px;
    margin: 1.2rem 0;
    font-size: 1.1rem;
  }
  h2 {
    margin: 0;
  }
  #question{
    text-align: left;
    padding-left: 5px;
  }
  button {
    background-color: purple;
    color: #fff;
    border: none;
    cursor: pointer;
    font-family: inherit;
    font-size: 1.1rem;
    display: block;
    width: 100%;
    padding: 1rem;
  }
  button:hover {
    background-color: grey;
  }
  
  </style>
