
<template>
<div>
  <button v-on:click="createWorld" v-if="!gameStarted">
    Start game
  </button>
    <div id="canvas"></div>
 </div>
</template>
<script>
import matter from 'matter-js'
export default {
  name: 'GameWorld',
  data: function() {
        return {
            gameStarted: false
        }
    },
  methods:{
    createWorld(){
        this.gameStarted = true;
    // module aliases
    var Engine = matter.Engine,
        Render = matter.Render,
        World = matter.World,
        Bodies =matter.Bodies;
        
    // create an engine
    var engine = Engine.create();
    // create a renderer
    var render = Render.create({
        element: document.getElementById("canvas"),
        engine: engine
    });

    // create two boxes and a ground
    var boxA = Bodies.rectangle(300, 200, 80, 160);
    var boxB = Bodies.rectangle(450, 50, 80, 80);
    var ground = Bodies.rectangle(400, 610, 810, 60, { isStatic: true });

    // add all of the bodies to the world
    World.add(engine.world, [boxA, boxB, ground]);

    // run the engine
    Engine.run(engine);

    // run the renderer
    Render.run(render);
    }
  }
}
</script>
