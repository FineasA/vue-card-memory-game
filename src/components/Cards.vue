<template>
  <div>
    <b-card-group columns class="card-group">
      <b-card
        :img-src="card.imgUrl"
        class="player-card"
        style="min-width: 16rem;"
        v-for="(card, index) in cards"
        :key="index"
        no-body
      >
      </b-card>
    </b-card-group>
  </div>
</template>

<script>
export default {
  data() {
    return {
      cards: [],
      imgURLS: [
        {
          zion:
            "https://images.unsplash.com/photo-1473790034954-491b2ee68f30?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1950&q=80"
        },
        {
          zion:
            "https://images.unsplash.com/photo-1473790123798-93586c8a5175?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjF9&auto=format&fit=crop&w=1950&q=80"
        },
        {
          zion:
            "https://images.unsplash.com/photo-1473789810014-375ed569d0ed?ixlib=rb-1.2.1&auto=format&fit=crop&w=800&q=60"
        },
        {
          zion:
            "https://images.unsplash.com/photo-1474401915596-3c5adf84ef01?ixlib=rb-1.2.1&auto=format&fit=crop&w=800&q=60"
        },
        {
          zion:
            "https://images.unsplash.com/photo-1477070730378-b48c1285afea?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=800&q=60"
        },
        {
          zion:
            "https://images.unsplash.com/photo-1475351177616-1e5e440dccef?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=800&q=60"
        }
      ]
    };
  },
  methods: {
    createCards() {
      for (let i = 0; i < this.imgURLS.length; i++) {
        let card = {
          hidden: true,
          cardId: i,
          imgUrl: this.imgURLS[i].zion
        };
        // cardCouplet.push(card, card);
        this.cards.push(card, card);
      }
      this.shuffleCards();
      console.log(this.cards);
    },
    shuffleCards() {
      for (let i = this.cards.length - 1; i > 0; i--) {
        let j = Math.floor(Math.random() * (i + 1));
        [this.cards[i], this.cards[j]] = [this.cards[j], this.cards[i]];
      }
    }
  },
  created() {
    this.createCards();
  }
};
</script>

<style></style>
