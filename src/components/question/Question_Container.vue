<template>
    <div class = "question-box-div">
        <b-jumbotron header-level="4" v-bind:header="$t('questions.title')">


            <template slot="lead" class="mx-1">
                <div style="text-align: center; display:flex; justify-content: center; align-items: center">

                </div>


                <!--                <b-container fluid class="vertical-center">-->
                <b-container fluid>
                    <p >
                        {{questions[index].question}}
                    </p>

                    <div class="accordion" role="tablist" v-if="questions[index].hint!==undefined">
                        <b-card no-body class="mb-1" >
                            <b-card-header header-tag="header" class="p-1" role="tab">
                                <b-button block v-b-toggle.accordion-1 variant="warning">{{$t('questions.hint')}}</b-button>
                            </b-card-header>
                            <b-collapse id="accordion-1" accordion="my-accordion" role="tabpanel">
                                <b-card-body>
                                    <b-card-text>{{questions[index].hint}}</b-card-text>
                                </b-card-body>
                            </b-collapse>
                        </b-card>
                    </div>


                </b-container>

                <Question_Progress_Bar
                        :user_results="user_results"
                />
            </template>

            <b-list-group>
                <b-list-group-item
                        v-for="answer in answers"
                        :key="answer"
                        @click="update_results(index, answer)"
                        :class="[user_results[index]===answer?'active':'']"
                >

                    {{num2level(answer)}}
                </b-list-group-item>
            </b-list-group>

            <b-button-group style="display: flex">
                <b-button style="flex-grow: initial; width: 50px" @click="set_scene('welcome')">&laquo;</b-button>
                <b-button style="flex-grow: initial; width: 50px" v-bind:disabled="index===0" @click="back()">&lsaquo;</b-button>
                <b-button class="notabutton" style="width: unset" disabled>{{index+1}}/{{questions.length}}</b-button>
                <b-button style="flex-grow: initial; width: 50px" v-bind:disabled="index===questions.length-1" @click="next()">&rsaquo;</b-button>
                <b-button style="flex-grow: initial; width: 50px" @click="set_scene('star')">&raquo;</b-button>
            </b-button-group>

        </b-jumbotron>

    </div>
</template>

<script>
    import Question_Progress_Bar from "@/components/question/Question_Progress_Bar";
    export default {

        name: "Question_Container",
        components: {Question_Progress_Bar},
        props:{
            questions: Array,
            answers: Array,
            update_results: Function,
            user_results: Array,
            set_scene: Function,
            set_results_length: Function,
        },

        data(){
            return {
                index: 0
            }
        },

        methods:{
            num2level(i){
                switch (i) {
                    case -1: return this.$t('badge.disagree')
                    case 0: return this.$t('badge.neutral')
                    case 1: return this.$t('badge.agree')
                    default: return "Error"
                }
            },
            next: function(){
                this.index++
            },
            back: function(){
                this.index--
            }
        },
        created(){
            // console.log(this.user_results.length)
            if(this.user_results.length===0)this.set_results_length(this.questions.length)
        }
    }
</script>

<style scoped>
    .list-group {
        margin: 20px 0px;
    }
    .list-group-item:hover:not(.active) {
        background: lightgrey;
        cursor: pointer;
    }
    .vertical-center {
        min-height: 8rem;

        display: flex;
        align-items: center;
    }
    .btn.notabutton{
        cursor: default;
    }
</style>
