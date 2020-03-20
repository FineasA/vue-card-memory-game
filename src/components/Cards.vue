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
      previous: null,
      mostRecent: null,
      correctPairs: [],
      phaseOne: true,
      phaseTwo: false,
      isCorrect: false,
      cards: [],
      hidden: true,
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
          hidden: this.hidden,
          cardId: i,
          imgUrl: this.imgURLS[i].zion
        };
        let cardTwo = {
          hidden: this.hidden,
          cardId: i,
          imgUrl: this.imgURLS[i].zion
        };
        this.cards.push(cardOne, cardTwo);
      }
      // this.shuffleCards();
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
        this.previous = this.cards[index].cardId;
        console.log(this.previous);
        this.phaseOne = false;
        this.phaseTwo = true;
      } else if (this.phaseTwo) {
        this.cards[index].hidden = false;
        this.mostRecent = this.cards[index].cardId;
        console.log(
          "Previous: ",
          this.previous,
          "Most Recent: ",
          this.mostRecent
        );
        //begin testing to see if matched
        if (this.previous !== this.mostRecent) {
          console.log("incorrect");
          setTimeout(() => {
            console.log("cards should flip");
            this.cards[this.previous].hidden = true;
            //i have no idea why mostRecent is not changing to hidden
            this.cards[this.mostRecent].hidden = true;
          }, 1500);
        }
      }
    }
  },
  created() {
    console.log("created");
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
