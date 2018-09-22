<template>
    <v-container fluid>
        <v-slide-y-transition mode="out-in">
            <v-layout column align-center>
                <blockquote v-if="Object.keys(data).length === 0" style="width: 250px">
                    Здравствуй, мой маленький дружок!<br>Ты отправляешься в увлекательное путешесвие по ебанистической хуйне, которую тебе предстоит выучить и наебать дядей, 
                    что бы они давали тебе денежку. Не отчаивайся если сразу у тебя нихуя не получиться, я в тебя верю!<br>
                    Так что постарайся и наеби 1С!
                    <footer>
                        <small>
                            <em>&mdash;Автор</em>
                        </small>
                    </footer>
                </blockquote>

                <div>{{ data.name }}</div>
                <!-- <div>{{ data.questions }}</div> -->
                <v-stepper v-model="e1">
                    <v-stepper-header>
                        <template v-for="n in data.questions.length">
                        <v-stepper-step
                            :complete="e1 > n"
                            :key="`${n}-step`"
                            :step="n"
                            editable
                        >
                           
                        </v-stepper-step>

                        <v-divider
                            v-if="n !== steps"
                            :key="n"
                        ></v-divider>
                        </template>
                    </v-stepper-header>

                    <v-stepper-items>
                        <v-stepper-content
                        v-for="(question, n) in data.questions"
                        :key="`${n}-content`"
                        :step="n"
                        >
                        <v-card
                            class="mb-5"
                            color="grey lighten-1"
                            height="200px"
                        ></v-card>

                        <v-btn
                            color="primary"
                            @click="nextStep(n)"
                        >
                            Continue
                        </v-btn>

                        <v-btn flat>Cancel</v-btn>
                        </v-stepper-content>
                    </v-stepper-items>
                </v-stepper>

                <v-stepper >
                    <v-stepper-header style="display: block">
                        <template v-for="(question, inx) in data.questions">
                        <v-stepper-step
                            
                            :key="inx"
                            :step="inx"
                            editable
                        >
                            
                        </v-stepper-step>

                        <!-- <v-divider
                            v-if="n !== steps"
                            :key="n"
                        ></v-divider> -->
                        </template>
                    </v-stepper-header>

                    <v-stepper-items>
                        <v-stepper-content
                            v-for="(question, inx) in data.questions"
                            :key="inx"
                            :step="inx"
                        >
                        <v-card
                            class="mb-5"
                            
                        >
                            <!-- <v-responsive v-if="question.image">
                                <v-img 
                                    :src="`./src/assets/data/${data.imagesfolder}/${question.image}`"
                                    aspect-ratio="2.75"
                                />
                            </v-responsive> -->
                            <v-card-title>{{ question.text }}</v-card-title>
                            <!-- <v-card-text>
                                <v-radio-group v-model="radioGroup">
                                    <v-radio
                                        v-for="(variant, inx) in question.variants"
                                        :key="inx"
                                        :label="variant.text"
                                        :value="inx"
                                        mandatory
                                    />
                                </v-radio-group>
                            </v-card-text> -->
                        </v-card>

                        <v-btn
                            color="primary"
                            @click="current++"
                        >
                            Continue
                        </v-btn>

                        <v-btn flat>Cancel</v-btn>
                        </v-stepper-content>
                    </v-stepper-items>
                </v-stepper>
                
                
            </v-layout>
        </v-slide-y-transition>
    </v-container>
</template>

<script>
export default {
    props: {
        data: Object
    },
    data: () => ({
        current: 0,
        e1: 1,
        steps: 5
    }),
    methods: {
        nextStep (n) {
            if (n === this.data.questions.length) {
                this.current = 1
            } else {
                this.current = n + 1
            }
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
