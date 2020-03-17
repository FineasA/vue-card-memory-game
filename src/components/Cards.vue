<template>
  <div>
    <b-card-group columns class="card-group">
      <b-card
        :img-src="card.hidden ? cardBackURL : card.imgUrl"
        class="player-card"
        style="min-width: 16rem;"
        v-for="(card, index) in cards"
        :key="index"
        no-body
        @click="flipCard(index)"
      >
      </b-card>
    </b-card-group>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentlySelected: [],
      correctPairs: [],
      phaseOne: true,
      phaseTwo: false,
      isCorrect: false,
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
      ],
      cardBackURL:
        "https://images.unsplash.com/photo-1574110537361-ff1948fc4a57?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1950&q=80"
    };
  },
  methods: {
    createCards() {
      //create two identical card objects that are distinct and point to different references
      for (let i = 0; i < this.imgURLS.length; i++) {
        let cardOne = {
          hidden: true,
          cardId: i,
          imgUrl: this.imgURLS[i].zion
        };
        let cardTwo = {
          hidden: true,
          cardId: i,
          imgUrl: this.imgURLS[i].zion
        };
        this.cards.push(cardOne, cardTwo);
      }
      this.shuffleCards();
      console.log(this.cards);
    },
    shuffleCards() {
      for (let i = this.cards.length - 1; i > 0; i--) {
        let j = Math.floor(Math.random() * (i + 1));
        [this.cards[i], this.cards[j]] = [this.cards[j], this.cards[i]];
      }
    },
    flipCard(index) {
      //store the first click in a variable, then compare to next click
      if (this.phaseOne) {
        this.cards[index].hidden = false;
        this.currentlySelected.push(this.cards[index].cardId);
        this.phaseOne = false;
        this.phaseTwo = true;
        console.log("Currently Selected: ", this.currentlySelected);
        console.log("Phase one complete");
      } else if (this.phaseTwo) {
        this.cards[index].hidden = false;
        this.currentlySelected.push(this.cards[index].cardId);
        if (this.currentlySelected[0] === this.currentlySelected[1]) {
          this.correctPairs.push([
            this.cards[this.currentlySelected[0]],
            this.cards[this.currentlySelected[1]]
          ]);
        }
        if (this.currentlySelected[0] !== this.currentlySelected[1]) {
          //   this.cards[this.currentlySelected[1]].hidden = false;
          setTimeout(() => {
            console.log("hello???");
            console.log("1: ", this.cards[this.currentlySelected[0]]);
            console.log("2: ", this.cards[this.currentlySelected[1]]);
            this.cards[this.currentlySelected[0]].hidden = true;
            this.cards[this.currentlySelected[1]].hidden = true;
            this.currentlySelected.length = 0;
          }, 1500);
        }
        this.phaseOne = true;
        this.phaseTwo = false;
        console.log("Currently Selected: ", this.currentlySelected);
        console.log("Phase two complete");
      }
    }
  },
  created() {
    this.createCards();
  }
};
</script>

<style>
.player-card-hidden {
  visibility: hidden;
  border: 2px solid black;
}
</style>
