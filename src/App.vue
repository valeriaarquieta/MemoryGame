<template>
  <div>
    <div class="card-container">
      <Card v-for="card in cards" :key="card.id" :image="card.image"   :flipped="card.flipped" :matched="card.matched" @flip="flipCard(card.id)"/>
    </div>
    <button @click="resetGame">Reset</button>
  </div>
</template>

<script>
  import Card from './Card.vue';

  export default {
    components: {
      Card,
    },
    data() {
      return {
        images: [
        'https://picsum.photos/id/1/200/300', 
        'https://picsum.photos/id/2/200/300', 
        'https://picsum.photos/id/3/200/300', 
        'https://picsum.photos/id/4/200/300', 
        'https://picsum.photos/id/5/200/300', 
        'https://picsum.photos/id/6/200/300',
        ],
        cards: [],
        flippedCards: [], 
        tries: 0,
      };
    },
    created() {
      this.generateCards();
    },
    methods: {
      generateCards() {
        this.images.forEach((image, index) => {
          this.cards.push({ id: index, image, flipped: false, matched: false });
          this.cards.push({ id: index + this.images.length, image, flipped: false, matched: false });
        });
        this.cards.sort(() => Math.random() - 0.5);
      },
      resetGame() {
        this.cards = [];
        this.generateCards();
        this.flippedCards = [];
        this.tries = 0;
      },
      flipCard(cardId) {
        const card = this.cards.find((c) => c.id === cardId);
        if (!card.flipped && !card.matched) {
          card.flipped = true;
          this.flippedCards.push(card);
          if (this.flippedCards.length === 2) {
            this.checkMatch();
          }
        }
      },
      checkMatch() {
        const [card1, card2] = this.flippedCards;
        this.tries++;
        if (card1.image === card2.image) {
          card1.matched = true;
          card2.matched = true;
        } else {
          setTimeout(() => {
            card1.flipped = false;
            card2.flipped = false;
          }, 1000);
        }
        this.flippedCards = [];
      },
    },
  };
</script>