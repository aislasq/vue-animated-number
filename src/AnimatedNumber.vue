<template>
    <p :class='mainClass'>
        {{display}} {{ outOff >= 0 ? ' / ' + outOff : '' }}
    </p>
</template>

<script>
    export default {
        props: {
            goal: {
                default: 0,
                required: true
            },
            mainClass: {
                default: '',
                required: false
            },
            seconds: {
                default: 1,
                required: false
            },
            outOff: {
                default: -1,
                required: false
            }
        },
        data: function(){
            return {
                display: 0,
                interval: -1,
                multiplier: 1
            }
        },
        mounted: function(){
            this.animate();
        },
        computed: {
            delta: function(){
                return (Math.E - 1) / ( this.seconds * 50 );
            }
        },
        methods:{
            animate: function(){
                if(this.multiplier >= Math.E || this.goal === this.display) return;
                this.interval = window.setInterval(
                    function(){
                        this.multiplier += this.delta;
                        if(this.multiplier >= Math.E) {
                            this.display = this.goal;
                            clearInterval( this.interval );
                            this.$emit('on-finish', this.display);
                            return;
                        }
                        let newVal = (this.goal * Math.log( this.multiplier ));
                        this.display = Math.round(newVal);
                        this.$emit('on-update', this.display);
                    }.bind(this), 20);
            }
        }
    }
</script>
