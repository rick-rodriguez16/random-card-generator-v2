<script lang="ts">
    const cardSuit: string[] = ['♠', '♣', '♥', '♦'];
    const cardNumber: string[] = ['A', '2']//, '3', '4', '5', '6', '7', '8', '9', '10', 'J', 'Q', 'K'];
    
    let isCardGenerated: boolean = false;
    let suit: string = '';
    let number: string = '';

    const generateCard = () => {
        suit = cardSuit[Math.floor(Math.random() * cardSuit.length)];
        number = cardNumber[Math.floor(Math.random() * cardNumber.length)];
        isCardGenerated = true;
    }

    $: cardColor = suit === '♠' || suit === '♣' ? 'black' : 'red';
    $: centerDesign = () => {
        if (number === 'A') {
            return `<div class="middle flex-grow text-center mt-32 text-8xl">${suit}</div>`
        }
        if (number === '2') {
            return `<div class="relative middle flex-grow text-8xl">
                        <div class="">${suit}</div>
                        <div class="bottom-suit">${suit}</div>
                    </div>`
        }
    }
    // create a reactive statement for J, Q, K, and Ace since they are not centered
    
    generateCard();
</script>

<div class="wrapper flex flex-col h-screen">
    <div class="card mx-auto my-40 w-64 flex flex-row 
    { isCardGenerated === true ? 'rounded-lg border-gray-800 border-solid border-2 bg-white' : ''}" 
    style="color: {cardColor}">
        <div class="left-side w-10">            
            <div class="top-number text-center ml-2">{number}</div>
            <div class="top-suit text-center {number !== '10' ? 'ml-2' : 'ml-3'} -mt-6">{suit}</div>
        </div>
        {@html centerDesign()}
        <div class="right-side relative w-10">
            <div class="bottom-suit text-center {number !== '10' ? 'ml-2' : 'ml-1'} absolute bottom-9">{suit}</div>
            <div class="bottom-number text-center {number !== '10' ? 'ml-2' : '-ml-2'} -mt-8 absolute bottom-0">{number}</div>
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
        transform: rotate(180deg);
    }
    .bottom-number {
        transform: rotate(180deg);
    }
</style>