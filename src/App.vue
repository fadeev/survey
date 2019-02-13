<template>
  <div id="app">
    <div v-if="complete">
      <div>{{subcategoryResults}}</div>
      <hr>
      <div>{{categoryResults}}</div>
      <hr>
      <div>{{totalResults}}</div>
    </div>
    <form v-else @submit.prevent="submit">
      <fieldset v-for="(category, ci) in form" :key="ci">
        {{category.category}}
        <fieldset v-for="(subcategory, si) in category.subcategoryList" :key="si">
          {{subcategory.subcategory}}
          <div v-for="(question, qi) in subcategory.questionList" :key="qi">
            {{question.question}} 
            <div v-for="(answer, ai) in question.answerList" :key="ai">
              <label><input v-model.number="question.result" type="radio" :value="answer.value" :name="`${ci}${si}${qi}`">{{answer.answer}}</label>
            </div>
          </div>
        </fieldset>
      </fieldset>
      <button type="submit">Submit</button>
    </form>
  </div>
</template>

<script>
  import axios from 'axios'

  export default {
    methods: {
      submit(e) {
        this.complete = true
        axios.post('https://hooks.zapier.com/hooks/catch/4495909/pb06zn/', { resultString: this.resultString },
         {
           headers : {
           'Content-Type' : 'application/x-www-form-urlencoded; charset=UTF-8'
          }
        })
      },
    },
    computed: {
      resultString() {
        let result = []
        this.form.forEach((category, ci) => {
          category.subcategoryList.forEach((subcategory, si) => {
            subcategory.questionList.forEach((question, qi) => {
              result.push(question.result)
            })
          })
        })
        return result.join(',')
      },
      subcategoryResults() {
        return this.form.map(category => {
          return category.subcategoryList.map(subcategory => {
            return {
              name: subcategory.subcategory,
              result: subcategory.questionList.reduce((acc, cur) => acc + cur.result, 0) / subcategory.questionList.length
            }
          })
        })
      },
      categoryResults() {
        return this.subcategoryResults.map((category, index) => {
          return {
            category: this.form[index].category,
            result: category.reduce((acc, cur) => acc + cur.result, 0) / category.length
          }
        })
      },
      totalResults() {
        return this.categoryResults.reduce((acc, cur) => acc + cur.result, 0) / 3
      },
    },
    data: function() {
      return {
        complete: null,
        form: [
          {
            category: 'Категория 1',
            subcategoryList: [
              {
                subcategory: 'Подкатегория 1',
                questionList: [
                  {
                    question: 'Вопрос 1',
                    result: null,
                    answerList: [
                      {
                        answer: 'Ответ 1',
                        value: '1'
                      },
                      {
                        answer: 'Ответ 2',
                        value: '2'
                      },
                      {
                        answer: 'Ответ 3',
                        value: '3'
                      },
                      {
                        answer: 'Ответ 4',
                        value: '4'
                      },
                      {
                        answer: 'Ответ 5',
                        value: '5'
                      },
                    ],
                  },
                  {
                    question: 'Вопрос 2',
                    result: null,
                    answerList: [
                      {
                        answer: 'Ответ 1',
                        value: '1'
                      },
                      {
                        answer: 'Ответ 2',
                        value: '2'
                      },
                      {
                        answer: 'Ответ 3',
                        value: '3'
                      },
                      {
                        answer: 'Ответ 4',
                        value: '4'
                      },
                      {
                        answer: 'Ответ 5',
                        value: '5'
                      },
                    ],
                  },
                  {
                    question: 'Вопрос 3',
                    result: null,
                    answerList: [
                      {
                        answer: 'Ответ 1',
                        value: '1'
                      },
                      {
                        answer: 'Ответ 2',
                        value: '2'
                      },
                      {
                        answer: 'Ответ 3',
                        value: '3'
                      },
                      {
                        answer: 'Ответ 4',
                        value: '4'
                      },
                      {
                        answer: 'Ответ 5',
                        value: '5'
                      },
                    ],
                  },
                ],
              },
              {
                subcategory: 'Подкатегория 2',
                questionList: [
                  {
                    question: 'Вопрос 1',
                    result: null,
                    answerList: [
                      {
                        answer: 'Ответ 1',
                        value: '1'
                      },
                      {
                        answer: 'Ответ 2',
                        value: '2'
                      },
                      {
                        answer: 'Ответ 3',
                        value: '3'
                      },
                      {
                        answer: 'Ответ 4',
                        value: '4'
                      },
                      {
                        answer: 'Ответ 5',
                        value: '5'
                      },
                    ],
                  },
                  {
                    question: 'Вопрос 2',
                    result: null,
                    answerList: [
                      {
                        answer: 'Ответ 1',
                        value: '1'
                      },
                      {
                        answer: 'Ответ 2',
                        value: '2'
                      },
                      {
                        answer: 'Ответ 3',
                        value: '3'
                      },
                      {
                        answer: 'Ответ 4',
                        value: '4'
                      },
                      {
                        answer: 'Ответ 5',
                        value: '5'
                      },
                    ],
                  },
                  {
                    question: 'Вопрос 3',
                    result: null,
                    answerList: [
                      {
                        answer: 'Ответ 1',
                        value: '1'
                      },
                      {
                        answer: 'Ответ 2',
                        value: '2'
                      },
                      {
                        answer: 'Ответ 3',
                        value: '3'
                      },
                      {
                        answer: 'Ответ 4',
                        value: '4'
                      },
                      {
                        answer: 'Ответ 5',
                        value: '5'
                      },
                    ],
                  },
                ],
              },
              {
                subcategory: 'Подкатегория 3',
                questionList: [
                  {
                    question: 'Вопрос 1',
                    result: null,
                    answerList: [
                      {
                        answer: 'Ответ 1',
                        value: '1'
                      },
                      {
                        answer: 'Ответ 2',
                        value: '2'
                      },
                      {
                        answer: 'Ответ 3',
                        value: '3'
                      },
                      {
                        answer: 'Ответ 4',
                        value: '4'
                      },
                      {
                        answer: 'Ответ 5',
                        value: '5'
                      },
                    ],
                  },
                  {
                    question: 'Вопрос 2',
                    result: null,
                    answerList: [
                      {
                        answer: 'Ответ 1',
                        value: '1'
                      },
                      {
                        answer: 'Ответ 2',
                        value: '2'
                      },
                      {
                        answer: 'Ответ 3',
                        value: '3'
                      },
                      {
                        answer: 'Ответ 4',
                        value: '4'
                      },
                      {
                        answer: 'Ответ 5',
                        value: '5'
                      },
                    ],
                  },
                  {
                    question: 'Вопрос 3',
                    result: null,
                    answerList: [
                      {
                        answer: 'Ответ 1',
                        value: '1'
                      },
                      {
                        answer: 'Ответ 2',
                        value: '2'
                      },
                      {
                        answer: 'Ответ 3',
                        value: '3'
                      },
                      {
                        answer: 'Ответ 4',
                        value: '4'
                      },
                      {
                        answer: 'Ответ 5',
                        value: '5'
                      },
                    ],
                  },
                ],
              },
            ],
          },
          {
            category: 'Категория 2',
            subcategoryList: [
              {
                subcategory: 'Подкатегория 1',
                questionList: [
                  {
                    question: 'Вопрос 1',
                    result: null,
                    answerList: [
                      {
                        answer: 'Ответ 1',
                        value: '1'
                      },
                      {
                        answer: 'Ответ 2',
                        value: '2'
                      },
                      {
                        answer: 'Ответ 3',
                        value: '3'
                      },
                      {
                        answer: 'Ответ 4',
                        value: '4'
                      },
                      {
                        answer: 'Ответ 5',
                        value: '5'
                      },
                    ],
                  },
                  {
                    question: 'Вопрос 2',
                    result: null,
                    answerList: [
                      {
                        answer: 'Ответ 1',
                        value: '1'
                      },
                      {
                        answer: 'Ответ 2',
                        value: '2'
                      },
                      {
                        answer: 'Ответ 3',
                        value: '3'
                      },
                      {
                        answer: 'Ответ 4',
                        value: '4'
                      },
                      {
                        answer: 'Ответ 5',
                        value: '5'
                      },
                    ],
                  },
                  {
                    question: 'Вопрос 3',
                    result: null,
                    answerList: [
                      {
                        answer: 'Ответ 1',
                        value: '1'
                      },
                      {
                        answer: 'Ответ 2',
                        value: '2'
                      },
                      {
                        answer: 'Ответ 3',
                        value: '3'
                      },
                      {
                        answer: 'Ответ 4',
                        value: '4'
                      },
                      {
                        answer: 'Ответ 5',
                        value: '5'
                      },
                    ],
                  },
                ],
              },
              {
                subcategory: 'Подкатегория 2',
                questionList: [
                  {
                    question: 'Вопрос 1',
                    result: null,
                    answerList: [
                      {
                        answer: 'Ответ 1',
                        value: '1'
                      },
                      {
                        answer: 'Ответ 2',
                        value: '2'
                      },
                      {
                        answer: 'Ответ 3',
                        value: '3'
                      },
                      {
                        answer: 'Ответ 4',
                        value: '4'
                      },
                      {
                        answer: 'Ответ 5',
                        value: '5'
                      },
                    ],
                  },
                  {
                    question: 'Вопрос 2',
                    result: null,
                    answerList: [
                      {
                        answer: 'Ответ 1',
                        value: '1'
                      },
                      {
                        answer: 'Ответ 2',
                        value: '2'
                      },
                      {
                        answer: 'Ответ 3',
                        value: '3'
                      },
                      {
                        answer: 'Ответ 4',
                        value: '4'
                      },
                      {
                        answer: 'Ответ 5',
                        value: '5'
                      },
                    ],
                  },
                  {
                    question: 'Вопрос 3',
                    result: null,
                    answerList: [
                      {
                        answer: 'Ответ 1',
                        value: '1'
                      },
                      {
                        answer: 'Ответ 2',
                        value: '2'
                      },
                      {
                        answer: 'Ответ 3',
                        value: '3'
                      },
                      {
                        answer: 'Ответ 4',
                        value: '4'
                      },
                      {
                        answer: 'Ответ 5',
                        value: '5'
                      },
                    ],
                  },
                ],
              },
              {
                subcategory: 'Подкатегория 3',
                questionList: [
                  {
                    question: 'Вопрос 1',
                    result: null,
                    answerList: [
                      {
                        answer: 'Ответ 1',
                        value: '1'
                      },
                      {
                        answer: 'Ответ 2',
                        value: '2'
                      },
                      {
                        answer: 'Ответ 3',
                        value: '3'
                      },
                      {
                        answer: 'Ответ 4',
                        value: '4'
                      },
                      {
                        answer: 'Ответ 5',
                        value: '5'
                      },
                    ],
                  },
                  {
                    question: 'Вопрос 2',
                    result: null,
                    answerList: [
                      {
                        answer: 'Ответ 1',
                        value: '1'
                      },
                      {
                        answer: 'Ответ 2',
                        value: '2'
                      },
                      {
                        answer: 'Ответ 3',
                        value: '3'
                      },
                      {
                        answer: 'Ответ 4',
                        value: '4'
                      },
                      {
                        answer: 'Ответ 5',
                        value: '5'
                      },
                    ],
                  },
                  {
                    question: 'Вопрос 3',
                    result: null,
                    answerList: [
                      {
                        answer: 'Ответ 1',
                        value: '1'
                      },
                      {
                        answer: 'Ответ 2',
                        value: '2'
                      },
                      {
                        answer: 'Ответ 3',
                        value: '3'
                      },
                      {
                        answer: 'Ответ 4',
                        value: '4'
                      },
                      {
                        answer: 'Ответ 5',
                        value: '5'
                      },
                    ],
                  },
                ],
              },
            ],
          },
          {
            category: 'Категория 3',
            subcategoryList: [
              {
                subcategory: 'Подкатегория 1',
                questionList: [
                  {
                    question: 'Вопрос 1',
                    result: null,
                    answerList: [
                      {
                        answer: 'Ответ 1',
                        value: '1'
                      },
                      {
                        answer: 'Ответ 2',
                        value: '2'
                      },
                      {
                        answer: 'Ответ 3',
                        value: '3'
                      },
                      {
                        answer: 'Ответ 4',
                        value: '4'
                      },
                      {
                        answer: 'Ответ 5',
                        value: '5'
                      },
                    ],
                  },
                  {
                    question: 'Вопрос 2',
                    result: null,
                    answerList: [
                      {
                        answer: 'Ответ 1',
                        value: '1'
                      },
                      {
                        answer: 'Ответ 2',
                        value: '2'
                      },
                      {
                        answer: 'Ответ 3',
                        value: '3'
                      },
                      {
                        answer: 'Ответ 4',
                        value: '4'
                      },
                      {
                        answer: 'Ответ 5',
                        value: '5'
                      },
                    ],
                  },
                  {
                    question: 'Вопрос 3',
                    result: null,
                    answerList: [
                      {
                        answer: 'Ответ 1',
                        value: '1'
                      },
                      {
                        answer: 'Ответ 2',
                        value: '2'
                      },
                      {
                        answer: 'Ответ 3',
                        value: '3'
                      },
                      {
                        answer: 'Ответ 4',
                        value: '4'
                      },
                      {
                        answer: 'Ответ 5',
                        value: '5'
                      },
                    ],
                  },
                ],
              },
              {
                subcategory: 'Подкатегория 2',
                questionList: [
                  {
                    question: 'Вопрос 1',
                    result: null,
                    answerList: [
                      {
                        answer: 'Ответ 1',
                        value: '1'
                      },
                      {
                        answer: 'Ответ 2',
                        value: '2'
                      },
                      {
                        answer: 'Ответ 3',
                        value: '3'
                      },
                      {
                        answer: 'Ответ 4',
                        value: '4'
                      },
                      {
                        answer: 'Ответ 5',
                        value: '5'
                      },
                    ],
                  },
                  {
                    question: 'Вопрос 2',
                    result: null,
                    answerList: [
                      {
                        answer: 'Ответ 1',
                        value: '1'
                      },
                      {
                        answer: 'Ответ 2',
                        value: '2'
                      },
                      {
                        answer: 'Ответ 3',
                        value: '3'
                      },
                      {
                        answer: 'Ответ 4',
                        value: '4'
                      },
                      {
                        answer: 'Ответ 5',
                        value: '5'
                      },
                    ],
                  },
                  {
                    question: 'Вопрос 3',
                    result: null,
                    answerList: [
                      {
                        answer: 'Ответ 1',
                        value: '1'
                      },
                      {
                        answer: 'Ответ 2',
                        value: '2'
                      },
                      {
                        answer: 'Ответ 3',
                        value: '3'
                      },
                      {
                        answer: 'Ответ 4',
                        value: '4'
                      },
                      {
                        answer: 'Ответ 5',
                        value: '5'
                      },
                    ],
                  },
                ],
              },
              {
                subcategory: 'Подкатегория 3',
                questionList: [
                  {
                    question: 'Вопрос 1',
                    result: null,
                    answerList: [
                      {
                        answer: 'Ответ 1',
                        value: '1'
                      },
                      {
                        answer: 'Ответ 2',
                        value: '2'
                      },
                      {
                        answer: 'Ответ 3',
                        value: '3'
                      },
                      {
                        answer: 'Ответ 4',
                        value: '4'
                      },
                      {
                        answer: 'Ответ 5',
                        value: '5'
                      },
                    ],
                  },
                  {
                    question: 'Вопрос 2',
                    result: null,
                    answerList: [
                      {
                        answer: 'Ответ 1',
                        value: '1'
                      },
                      {
                        answer: 'Ответ 2',
                        value: '2'
                      },
                      {
                        answer: 'Ответ 3',
                        value: '3'
                      },
                      {
                        answer: 'Ответ 4',
                        value: '4'
                      },
                      {
                        answer: 'Ответ 5',
                        value: '5'
                      },
                    ],
                  },
                  {
                    question: 'Вопрос 3',
                    result: null,
                    answerList: [
                      {
                        answer: 'Ответ 1',
                        value: '1'
                      },
                      {
                        answer: 'Ответ 2',
                        value: '2'
                      },
                      {
                        answer: 'Ответ 3',
                        value: '3'
                      },
                      {
                        answer: 'Ответ 4',
                        value: '4'
                      },
                      {
                        answer: 'Ответ 5',
                        value: '5'
                      },
                    ],
                  },
                ],
              },
            ],
          },
        ],
      }
    }
  }
</script>
