<template>
    <div id="app">
        <Header :correctCount="correctCount" :totalCount="totalCount"></Header>

        <b-container class="bv-example-row">
            <b-row>
                <b-col sm="6" offset="3">
                    <Content v-if="questionlist.length" :cQuestion="questionlist[index]" :next="next" :increment="increment"></Content>
                </b-col>
            </b-row>
        </b-container>


    </div>
</template>

<script>
    import Header from './components/Header'
    import Content from './components/Content'

    export default {
        name: 'App',
        components: {Header, Content},
        data() {
            return {
                questionlist : [],
                index: 0,
                correctCount:0,
                totalCount:0
            }
        },methods:{
            next(){
                if (this.index < 9) 
                this.index ++;
            },
            increment(is_correct)
            {
                if(is_correct)
                {
                    this.correctCount++;
                }
                this.totalCount++;

            }

        }, mounted: function () {
            fetch('https://opentdb.com/api.php?amount=10&category=11&type=multiple', {method: 'get'}).then((response) => {
                return response.json();
            }).then((result) => {
                this.questionlist = result.results
            })
        }
    }
</script>

<style>

</style>
