<template>
  <div id="card-actions">
	<button v-if="currentPos>0" id="prevBttn" v-on:click="shiftLeft"> Previous </button>
	<button v-if="currentPos<52" id="nextBttn" v-on:click="shiftRight">Next</button>		
	<div v-if="currentCard" id="card-display">		
		<h4>Remaining : {{cards.length - currentPos}} </h4>
		<h2>Don't forget to rest between sets!</h2>
		<div v-if="currentCard.Set === 'Pushups'" id="center-display">
			<div>
				<h1 id="number-display">{{currentCard.Number}}</h1>
				<img id="suit-display" :alt="currentCard.Suit" src="../assets/spade.png" />
				<h1 id="set-display">{{currentCard.Set}}</h1>
			</div>
			<img id="set-display" :alt="currentCard.Set" src="../assets/pushups.gif" />						
		</div>
		<div v-else-if="currentCard.Set === 'Pullups'">
			<div>
				<h1 id="number-display">{{currentCard.Number}}</h1>
				<img id="suit-display" :alt="currentCard.Suit" src="../assets/diamond.png" />		
				<h1 id="set-display">{{currentCard.Set}}</h1>
			</div>
			<img id="set-display" :alt="currentCard.Set" src="../assets/pullups.gif" />			
		</div>		
		<div v-else-if="currentCard.Set === 'Squats'">		
			<div>
				<h1 id="number-display">{{currentCard.Number}}</h1>
				<img id="suit-display" :alt="currentCard.Suit" src="../assets/club.png" />	
				<h1 id="set-display">{{currentCard.Set}}</h1>
			</div>
			<img id="set-display" :alt="currentCard.Set" src="../assets/squats.gif" />					
		</div>		
		<div v-else-if="currentCard.Set === 'Abs'">
			<div>
				<h1 id="number-display">{{currentCard.Number}}</h1>
				<img id="suit-display" :alt="currentCard.Suit" src="../assets/heart.png" />
				<h1 id="set-display">{{currentCard.Set}}</h1>
			</div>
			<img id="set-display" :alt="currentCard.Set" src="../assets/abs.gif" />			
		</div>			
	</div>
	<div v-else>
		<button id="shuffle-cards" v-on:click="shuffle">
			<img alt="Vue logo" src="../assets/logo.png">		
		</button>
		<h1> Click on Deck to Shuffle </h1>
		<h3>Instructions</h3>
		<p> - Shuffle the deck -</p>
		<p> - Do each exercise for the number of times shown. - </p>
		<p> - Go the the next exercise - </p>
		<p> - See if you can do them all! - </p>
	</div>
  </div>
</template>

<script>
  export default {
    name:"cardactions",
	props: {
		cards: Array,
		currentCard:Object,
		currentPos:Number
	},
	methods: {
		shiftLeft: function()
		{
			let index = this.currentPos;
			if(index >0)
			{
				index--;
				this.currentPos = index;
				this.currentCard = this.cards[index];
			}
				
		},
		shiftRight: function()
		{
			let index = this.currentPos;
			if(index <52)
			{
				index++;
				this.currentPos = index;
				this.currentCard = this.cards[index];
			}
		},
		assignCard: function()
		{
			
			
			
		},
		shuffle: function ()
		{
			let suits = ["spades","diamonds","clubs","hearts"];
			let values = ["11","2","3","4","5","6","7","8","9","10","10","10","10"];
			let set =["Pushups", "Pullups", "Squats", "Abs"];
			var deck = new Array();
			
			for(let i=0;i<suits.length;i++)
			{
				for(let j=0;j<values.length;j++)
				{					
					let card =
						{
							Set: set[i], 
							Number: values[j], 
							Suit: suits[i], 
							id:i+j
						};
					deck.push(card);
				}
			}
			
			for(let i=0;i<1000;i++)
			{
				let first = Math.floor((Math.random()*deck.length));
				let secnd = Math.floor((Math.random()*deck.length));
				let tmp = deck[first];
				
				deck[first]=deck[secnd];
				deck[secnd]=tmp;		
			}
			
			this.cards = deck;			
			this.currentPos = 0;
			this.currentCard = deck[0];
		}
	}
  }
</script>

<style scoped>	
	#shuffle-cards
	{
		background:none;
		border:none;
	}
	#set-display
	{
		margin:0;
	}
	#card-display
	{
		overflow:hidden;
		width:100%;
	}
	#prevBttn
	{
		width: 100px;
	}
	#nextBttn
	{
		width:100px;
	}
	#center-display
	{
		
	}
	#suit-display 
	{
		position:relative;	
		margin-bottom: 0;				
	}
	#number-display
	{
		position:relative;		
		top:90px;
		z-index:1;
		-webkit-text-stroke-width: 1px;
		-webkit-text-stroke-color: white;
	}
	#set-display
	{
		position:relative;		
	}
</style>