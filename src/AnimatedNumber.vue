<template>
    <p :class='mainClass'>
        {{displayNumber}} {{ outOff >= 0 ? ' / ' + outOff : '' }}
    </p>
</template>

<script>
    export default {
        props: {
            number: {
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
                displayNumber: 0,
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
                if(this.multiplier >= Math.E || this.number === this.displayNumber) return;
                this.interval = window.setInterval(
                    function(){
                        this.multiplier += this.delta;
                        if(this.multiplier >= Math.E) {
                            this.displayNumber = this.number;
                            clearInterval( this.interval );
                            this.$emit('on-finish', displayNumber);
                            return;
                        }
                        let newVal = (this.number * Math.log( this.multiplier ));
                        this.displayNumber = Math.round(newVal);
                        this.$emit('on-update', displayNumber);
                    }.bind(this), 20);
            }
        }
    }
</script>
