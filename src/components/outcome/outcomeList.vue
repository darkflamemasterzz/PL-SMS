<template>
    <div>
        <div class="outcomeList" v-for="(outcome,index) in outcomeList" :key="index">
            <div class="listHeader">
                <span class="date">{{outcome.time}}</span>
                <span class="all-count">{{countPerDay[index]}}</span>
            </div>
            <div class="item" v-for="(item, index) in outcome.outcomes" :key="index">
                <span class="dest">{{item.dest}}</span>
                <span class="count">{{item.count}}</span>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'outcomeList',
    data () {
        return {
            outcomeList: [],
            countPerDay: [],
            date: '',
        }
    },
    methods: {
        fetchOutcomeList () {
            axios
                .get('http://localhost:8080/outcome.json')
                .then(response => {this.fetchOutcomeListSuccs(response)})
        },
        fetchOutcomeListSuccs (response) {
            console.log(response)
            this.outcomeList = response.data.outcomeList
            this.outcomeCountPerDay()
        },
        // 计算每份天的支出总额
        outcomeCountPerDay () {
            let outcomes = []
            this.outcomeList.forEach(function(value){
                outcomes.push(value)
            })
            let countPerDay = []
            outcomes.forEach(function(value){
                let countThisDay = 0
                value.outcomes.forEach(function(value){
                    countThisDay += value.count
                })
                countPerDay.push(countThisDay)
            })
            
            this.countPerDay = countPerDay
            console.log(countPerDay)
        }
    },
    mounted () {
        this.fetchOutcomeList()
    }
}
</script>

<style lang="stylus" scoped>

</style>