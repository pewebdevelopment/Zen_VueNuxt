<template class="antialiased text-gray-700 bg-gray-100">
    <div class="flex w-full h-screen justify-center items-center" id="app">
        <div class="w-full max-w-xl">
            <h1 class="font-bold text-5xl text-center text-indigo-700">
                Simple Quiz
            </h1>
            <div class="bg-white p-12 rounded-lg shadow-lg w-full mt-8">
                <div v-if="index < count">
                    <p class="text-2xl font-bold">
                        {{ questions[index]['question'] }}
                    </p>
                    <label :for="key" class="block mt-4 border border-gray-300 rounded-lg py-2 px-6 text-lg"
                        v-for="answer, key in questions[index]['answers']" 
                        :class="{ 'hover:bg-gray-100 cursor-pointer': selectedAnswer == '' },
                        {'bg-red-200': selectedAnswer == key },
                            {'bg-green-200' : key == questions[index]['correctAnswer'] && selectedAnswer != ''}">
                        <input type="radio" :id="key" class="hidden" :value="key" @change="answered($event)" v-model="selectedAnswer"
                            :disabled="selectedAnswer != ''" /> {{ answer }}
                    </label>
                    <div class="mt-6 flow-root">
                        <button
                            class="float-right px-5 py-2 bg-indigo-600 text-white text-sm font-bold tracking-wide rounded-full"
                            v-show="selectedAnswer != '' && index < count-1" @click="nextQuestion">Next
                            &gt</button>
                        <button
                            class="float-right px-5 py-2 bg-indigo-600 text-white text-sm font-bold tracking-wide rounded-full"
                            v-show="selectedAnswer != '' && index == count-1" @click="showResults">Finish</button>
                    </div>
                </div>
                <div v-else>
                    <h2 class="font-bold text-3xl">Results</h2>
                    <div class="flex justify-start space-x-4 mt-6">
                        <p>
                            Correct Answers:
                            <span class="text-2xl text-green-700 font-bold">{{ correctAnswer }}</span>
                        </p>
                        <p>
                            Wrong Answers:
                            <span class="text-2xl text-red-700 font-bold">{{ wrongAnswer }}</span>
                        </p>
                    </div>
                    <div class="mt-6 flow-root">
                        <button
                            class="float-right px-5 py-2 bg-indigo-600 text-white text-sm font-bold tracking-wide rounded-full"
                            @click="resetQuiz">
                            Play again
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name: 'Quiz',
    data() {
        return {
            index: 0,
            correctAnswer: 0,
            selectedAnswer: '',
            wrongAnswer: 0,
            count: 3,
            questions: [
                {
                    question: "Rolex is a company that specializes in what type of product?",
                    answers: { a: 'Bags', b: 'Watches', c: 'Shoes', d: 'Laptops' },
                    correctAnswer: 'b'
                },
                {
                    question: "When did Facebook launch?",
                    answers: { a: '2005', b: '2008', c: '2003', d: '2004' },
                    correctAnswer: 'd'
                },
                {
                    question: "Albert Einstein had trouble with mathematics when he was in school",
                    answers: { a: 'True', b: 'False' },
                    correctAnswer: 'b'
                },
            ]
        }
    },
    methods: {
        answered(e) {
            this.selectedAnswer = e.target.value;
            if (this.selectedAnswer == this.questions[this.index]['correctAnswer'])
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