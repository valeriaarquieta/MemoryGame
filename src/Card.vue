<template>
  <div class="card" :class="{ flipped: flipped, matched: matched }" @click="$emit('flip')">
    <div class="front"> <p>front</p>
    </div>
    <div class="back" :style="{ 'background-image': flipped ? `url(${image})` : '' }">
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      image: {
        type: String,
        required: true,
      },
      flipped: {
        type: Boolean,
        default: false,
      },
      matched: {
        type: Boolean,
        default: false,
      },
    },
  };
</script>
<style>
  .card-container {
    display: flex;
    flex-wrap: wrap;
    max-width: 500px;
    margin: 0 auto;
  }

  .card {
    width: 100px;
    height: 100px;
    perspective: 1000px;
    margin: 5px;
    cursor: pointer;
  }

  .card .back {
    width: 100%;
    height: 100%;
    position: absolute;
    top: 0;
    left: 0;
    transition: transform 0.6s;
    backface-visibility: hidden;
    border-radius: 5px;
    background-size: cover;
    background-position: center;
    
  }

  .card .front {
    background-color: #333;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 24px;
    font-weight: bold;
    color: #eaea;
  }

  .card.flipped {
    transform: rotateY(180deg);
  }

  .card.matched {
    visibility: hidden;
  }
</style>


