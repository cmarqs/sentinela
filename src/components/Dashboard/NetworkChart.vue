<template>
    <div class="card mb-3 card o-hidden h-200">
        <div class="card-header text-white bg-dark">
            <span class="fload-left">
                <i class="fa fa-sitemap"></i> Uso Médio da Rede 
            </span>
            <span class="float-right">
                <a href="#" @click="fillData()" class="text-white clearfix small z-1">
                    Período de 24h
                </a>
            </span>
        </div>
        <div class="card-body h-100">
            <line-chart ref="lineChart" :height="chartHeight" :chartData="chartData" :options="options">
            </line-chart>
        </div>
    </div>
</template>

<script>
    import LineChart from "./LineChart";
    
    export default {
        name: "network-chart",
        data() {
            return {
                chartData: null,
                options: chartOptions,
                chartHeight: 200
            }
        },
        watch: {
    
        },
        mounted() {
            this.fillData()
        },
        methods: {
            fillData() {
                this.chartData = {
                    labels: [this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt()],
                    datasets: [{
                        label: 'Data One',
                        backgroundColor: '#376273',
                        data: [this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt()]
                    }],
                };
            },
            getRandomInt() {
                return Math.floor(Math.random() * (50 - 5 + 1)) + 5
            },
        },
        components: {
            LineChart,
        }
    };
    
    const chartOptions = {
        responsive: true,
        maintainAspectRatio: false,
        legend: {
            display: false
        },
        scales: {
            xAxes: [{
                gridLines: { display: false },
            }],
            yAxes: [{
                gridLines: { display: false },
                ticks: {display: false }                
            }]
        }
    }
</script>

