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
        const plugin = document.createElement("script");
        plugin.setAttribute(
            "src",
            "http://cdnjs.cloudflare.com/ajax/libs/gsap/latest/TweenMax.min.js"
        );
        plugin.async = true;
        document.head.appendChild(plugin);

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
            'animation' :                   
                {
                    'type'     : 'spinToStop',  
                    'duration' : 5,             
                    'spins'    : 8,       
                    'callbackAfter': this.drawTriangle,
                    'callbackFinished': this.whenFinished   
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
        },
        whenFinished(){
            var winningSegment = this.winwheel.getIndicatedSegment();
     
            // Basic alert of the segment text which is the prize name.
            console.log("You have won " + winningSegment.text + "!");
        }
    }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>