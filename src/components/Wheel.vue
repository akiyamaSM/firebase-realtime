<template>
  <div>
      <canvas id='myCanvas' width='880' height='300'>
          Canvas not supported, use another browser.
      </canvas>
      <button @click="bingo">Spin the Wheel</button>
  </div>
</template>

<script>

import Winwheel from 'winwheel'

export default {
    name: 'wheel',
    data(){
        return{
            winwheel: {}
        }
    },
    mounted(){
        this.winwheel = new Winwheel({
            'canvasId'    : 'myCanvas',
            'numSegments' : 6,
            'fillStyle'   : '#e7706f',
            'lineWidth'   : 3,
            'segments'       :
                [
                    {'text' : 'Segment 1'},
                    {'text' : 'Segment 2'},
                    {'text' : 'Segment 3'},
                    {'text' : 'Segment 4'},
                    {'text' : 'Segment 5'},
                    {'text' : 'Segment 6'}
                ],
            'animation' :                   // Note animation properties passed in constructor parameters.
                {
                    'type'     : 'spinToStop',  // Type of animation.
                    'duration' : 5,             // How long the animation is to take in seconds.
                    'spins'    : 8,              // The number of complete 360 degree rotations the wheel is to do.
                    'callbackAfter' : 'drawTriangle'
                }
        });
    },
    methods:{
        bingo(){
            this.winwheel.startAnimation()
        },
        drawTriangle(){
            var ctx = this.winwheel.ctx;

            ctx.strokeStyle = 'navy';     // Set line colour.
            ctx.fillStyle   = 'aqua';     // Set fill colour.
            ctx.lineWidth   = 2;
            ctx.beginPath();              // Begin path.
            ctx.moveTo(170, 5);           // Move to initial position.
            ctx.lineTo(230, 5);           // Draw lines to make the shape.
            ctx.lineTo(200, 40);
            ctx.lineTo(171, 5);
            ctx.stroke();                 // Complete the path by stroking (draw lines).
            ctx.fill();                   // Then fill.
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>