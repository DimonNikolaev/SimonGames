<template>
    <div class="container">
        <h1>Simon Says</h1>
        <div class="simon">
            <ul>
                <li class="red simon__item" data-tile="1"></li>
                <li class="blue simon__item" data-tile="2"></li>
                <li class="yellow simon__item" data-tile="3"></li>
                <li class="green simon__item" data-tile="4"></li>
            </ul>
        </div>
        <div class="game-info">
            <h2>Round: <span data-round="0">0</span></h2>
            <button data-action="start" v-on:click="startGame('high')">Start</button>
            <p data-action="lose">Sorry, you lost after <span data-round="0"></span> rounds!</p>
        </div>
        <div class="game-options">
            <h2>Game Options:</h2>
            <input type="radio" name="mode" value="normal" checked="">Normal<br>
            <input type="radio" name="mode" value="sound-only">Sound Only<br>
            <input type="radio" name="mode" value="light-only">Light Only<br>
            <input type="radio" name="mode" value="free-board">Free board
        </div>
    </div>

<!--    <div data-action="sound">-->
<!--        <audio autoplay>-->
<!--            <source src="./assets/sounds/1.ogg" type="audio/ogg">-->
<!--            <source src="./assets/sounds/1.mp3" type="audio/mp3">-->
<!--        </audio>-->
<!--    </div>-->
</template>


<script>
    let simonGames = new Vue({
        name: 'App',
        // mounted() {
        //     // function activeSimonItem(){
        //     //     let allSimonItemsElem = document.querySelectorAll('.simon__item')
        //     //
        //     //     allSimonItemsElem.forEach(element=>{
        //     //         element.addEventListener('mouseup', ()=> element.classList.toggle('active'))
        //     //     })
        //     //     allSimonItemsElem.forEach(element=>{
        //     //         element.addEventListener('mousedown', ()=> element.classList.toggle('active'))
        //     //     })
        //     // }
        //     // activeSimonItem()
        //
        // },
        methods:{
            startGame: function startGame(level){
                function getRandomInt(max){
                    return Math.floor(Math.random() * Math.floor(max));
                }

                function returnRandomElemForGame(level){
                    level == 'low' ? level = 1500: ''
                    level == 'medium' ? level = 1000: ''
                    level == 'high' ? level = 400: ''


                    let allSimonItemsElem = document.querySelectorAll('.simon__item')
                    let allSimonItemsElemLength = allSimonItemsElem.length
                    let getRandomActiveElem = getRandomInt(allSimonItemsElemLength)

                    setTimeout(()=>{
                        document.querySelectorAll('.simon__item')[getRandomActiveElem].classList.add('active')
                    }, 1000)
                    setTimeout(()=>{
                        document.querySelectorAll('.simon__item')[getRandomActiveElem].classList.remove('active')
                    }, 1400)
                }
                returnRandomElemForGame(level)
            }
        }
    })
</script>

