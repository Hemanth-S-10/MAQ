<template>
    <div>
        <div v-for="(quiz, index) in quizez" v-show="index === questionindex" :key="index">
        <el-card>
        <h1>{{ quiz.category }}</h1>
        <h2>{{ quiz.question }}</h2>
        <ol style="list-style-type:none;">
            <el-checkbox-group v-model="answers[index]">
                <li v-for="answer in quiz.incorrect_answers" :key="answer">
                    <el-checkbox :label="answer"><b>{{answer}}</b></el-checkbox>
                </li>
            </el-checkbox-group>  
        </ol>
        </el-card>
        </div><br><br>
        <div v-if="questionindex < quizez.length">
        <center>
        <el-button type="danger" v-if="questionindex > 0" v-on:click="prev">
        prev
        </el-button>&emsp;
        <el-button type="success" v-on:click="next">
        next
        </el-button>
        </center>
        </div>
            <h1 v-if="questionindex == quizez.length">Your Total score is {{score}} / {{quizez.length}}</h1>
        </div>
</template>
<script>
import isEqual from "lodash/isEqual"

export default {

  name: 'app',
  
  data : function (){
  return{
    questionindex:0,
    quizez:[],
    answers:[],
  }
  },
  methods: {
        next: function() {
        this.questionindex++;
        },
        prev: function() {
        this.questionindex--;
        }
    },
computed:{
        score: function() {
        var total = 0;
        for (var i =0; i <this.answers.length; i++) {
        if(isEqual(this.answers[i],this.quizez[i].correct_answer)){total +=1;}
        }
        return total;
        }
    },
    mounted(){
        const z=JSON.parse(window.localStorage.getItem('arr'))
        this.quizez=z
        console.log(this.quizez)
        console.log(z)
        this.answers=Array(z.length).fill([])
        console.log(this.answers)
    }
}
</script>
