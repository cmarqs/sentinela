<script>
    import {
        Line,
        mixins
    } from 'vue-chartjs'
    
    export default {
        extends: Line,
        mixins: [mixins.reactiveProp],
        props: ['dataData', 'options'],
        mounted() {
            this.renderChart(this.chartData, this.options)
        },
        watch: {
            'options': {
                handler(newOption, oldOption) {
                    this.renderChart(this.chartData, this.options)
                },
                deep: true
            }
        }
    
    }
</script>
