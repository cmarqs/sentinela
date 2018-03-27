<template>
    <!-- Icon Cards-->
    <div class="row">
        <div class="col-xl-4 col-sm-6 mb-4" v-for="item in data" :key="item.index">
            <div class="card text-white o-hidden h-100" v-bind:class="[ item.color ]">
                <div class="card-body">
                    <div class="card-body-icon">
                        <i class="fa fa-fw" v-bind:class="[ item.icon ]"></i>
                    </div>
                    <div class="mr-5">{{ item.total }} {{ item.text }}</div>
                </div>
                <span class="card-footer clearfix small">
                    <a class="text-white" href="#" v-for="status in item.status" :key="status.index">
                        <i class="fa fa-fw" v-bind:class="[ status.i ]"></i> {{ status.q }} {{ status.t }}  
                    </a>
                </span>
            </div>
        </div>
    </div>
</template>

<script>
    import axios from "axios";
    
    export default {
        name:"icon-cards",
        data() {
            return {
                data: null,
                timer: timer
            };
        },
        mounted() {
            this.getData();
            setInterval(function() {
                this.getData();
                console.log('getData: ' + this.timer.time)
            }.bind(this), 30000);
        },
        methods: {
            getData() {
                axios.get('http://localhost:3000/resumo')
                    .then(response => {
                        try {
                            this.handleData(response.data)
                            //console.log(response.data)
                        } catch (err) {
                            console.log(err)
                        }
                    })
                    .catch(error => {
                        console.log(error.data)
                    })
            },
            handleData(dataPar) {
                let monitor = []
                if (dataPar) {
                    // soma total monitorado e define a cor com base no status
                    dataPar.forEach(m => {
                        //console.log(m)
    
                        let icon = ""
                        let text = ""
                        let color = "bg-primary"
                        let total = 0
    
                        let status = []
                        m.statusMonitor.forEach(s => {
                            let i = "" //icone do status
                            let q = 0 //qtd do status
                            let t = "" // texto do status
                            total += s.quantidade; // acumula a qtd por status
    
                            //define o icone e a cor de acordo com o status
                            if (s.quantidade > 0) {
                                if (s.status === "warning") {
                                    color = "bg-warning"
                                    t = "Atenção"
                                    i = "fa-exclamation-triangle"
                                    q = s.quantidade
                                } else if (s.status === "danger") {
                                    color = "bg-danger"
                                    t = "Perigo!"
                                    i = "fa-exclamation-circle"
                                    q = s.quantidade
                                } else {
                                    color = "bg-success"
                                    t = "Normal"
                                    i = "fa-check-circle"
                                    q = s.quantidade
                                }
    
                                status.push({
                                    i,
                                    t,
                                    q
                                });
                            }
                        });
    
                        // define o icone de acordo com o tipo do monitor
                        switch (m.tipoMonitor) {
                            case "server":
                                icon = "fa-server"
                                text = "Servidores monitorados"
                                break;
                            case "http":
                                icon = "fa-cloud"
                                text = "HTTP Sites e API`s"
                                break;
                            case "service":
                                icon = "fa-cogs"
                                text = "Serviços automáticos"
                                break;
                            default:
                                icon = "fa-desktop"
                                text = "Dispositivos monitorados"
                                break;
                        }
    
                        monitor.push({
                            type: m.tipoMonitor,
                            total: total,
                            color: color,
                            icon: icon,
                            text: text,
                            status: status
                        });
                    });
                }
                this.data = monitor;
                // console.log('this.data')
                // console.log(this.data)
            }
        },
    };

    Date.prototype.timeNow = function() {
        return ((this.getHours() < 10) ? "0" : "") + this.getHours() + ":" + ((this.getMinutes() < 10) ? "0" : "") + this.getMinutes() + ":" + ((this.getSeconds() < 10) ? "0" : "") + this.getSeconds();
    }
    Date.prototype.today = function() {
        return ((this.getDate() < 10) ? "0" : "") + this.getDate() + "/" + (((this.getMonth() + 1) < 10) ? "0" : "") + (this.getMonth() + 1) + "/" + this.getFullYear();
    }
    let timer = {
        datetime: new Date().today(),
        time: new Date().timeNow()
    }
</script>

<style scoped>
    .card-body-icon {
        position: absolute;
        z-index: 0;
        top: -5px;
        right: -0.1px;
        font-size: 3rem;
        /*
        -webkit-transform: rotate(15deg);
        -ms-transform: rotate(15deg);
        transform: rotate(15deg); 
        */
    }
    
    @media (min-width: 576px) {
        .card-columns {
            column-count: 1;
        }
    }
    
    @media (min-width: 768px) {
        .card-columns {
            column-count: 2;
        }
    }
    
    @media (min-width: 1200px) {
        .card-columns {
            column-count: 2;
        }
    }
</style>
