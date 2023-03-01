<script lang="ts">
    const cardSuit: string[] = ['♠', '♣', '♥', '♦'];
    const cardNumber: string[] = ['A', '2', '3', '4', '5', '6', '7', '8', '9', '10', 'J', 'Q', 'K'];
    
    let isCardGenerated: boolean = false;
    let suit: string = '';
    let number: string = '';

    const generateCard = () => {
        suit = cardSuit[Math.floor(Math.random() * cardSuit.length)];
        number = cardNumber[Math.floor(Math.random() * cardNumber.length)];
        isCardGenerated = true;
    }

    $: cardColor = suit === '♠' || suit === '♣' ? 'black' : 'red';
    
</script>

<div class="wrapper flex flex-col h-screen">
    <div class="card mx-auto my-40 w-80 flex flex-row 
    { isCardGenerated === true ? 'rounded-lg border-gray-800 border-solid border-2' : ''}" 
    style="color: {cardColor}">
        <div class="left-side flex flex-col">            
            <div class="top-number absolute ml-3">{number}</div>
            <div class="top-suit absolute ml-3 pt-10">{suit}</div>
        </div>
        <div class="middle flex flex-grow"></div>
        <div class="right-side flex flex-col">
            <div class="bottom-suit absolute mr-4">{suit}</div>
            <div class="bottom-number mr-3 pb-10 bottom-0">{number}</div>
        </div>
    </div>
    <div class="button-area mx-auto mt-52">
        <button class="" on:click={generateCard}>Click to draw a card</button>
    </div>
</div>

<style>
    .wrapper {

        background-color: darkgreen;
    }
    .card {
        font-size: 50px;
        height: 450px;
    }
    .bottom-suit {
        margin-top: 325px;
        transform: rotate(180deg);
    }
    .bottom-number {
        margin-top: 325px;
        transform: rotate(180deg);
    }

</style>