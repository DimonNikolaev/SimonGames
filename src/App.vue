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
            <button data-action="start" v-on:click="startGame">Start</button>
            <p data-action="lose">Sorry, you lost after <span data-round="0"></span> rounds!</p>
        </div>
        <div class="game-options">
            <h2>Game Options:</h2>
            <label>
                <input type="radio" name="mode" value="normal" checked="">
            </label>Normal<br>
            <label>
                <input type="radio" name="mode" value="sound-only">
            </label>Sound Only<br>
            <label>
                <input type="radio" name="mode" value="light-only">
            </label>Light Only<br>
            <label>
                <input type="radio" name="mode" value="free-board">
            </label>Free board
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
    export default {
        name: 'App',
        mounted() {
            document.querySelectorAll('.simon__item').forEach(item => item.addEventListener('mousedown', () => {
                item.classList.add('active')
            }))
            document.querySelectorAll('.simon__item').forEach(item => item.addEventListener('mouseup', () => {
                item.classList.remove('active')
            }))

        },
        data: function () {
            return {
                isError: true
            }
        },
        methods: {
            startGame: function (level) {
                this.getRandomActiveElemOrder = 0

                function returnRandomElemForGame(level) {

                    level === 'low' ? level = 1500 : ''
                    level === 'medium' ? level = 1000 : ''
                    level === 'high' ? level = 400 : ''

                    let allSimonItemsElem = document.querySelectorAll('.simon__item')
                    let getLengthSimonItems = allSimonItemsElem.length
                    let getRandomActiveElem = (max) => Math.floor(Math.random() * Math.floor(max));
                    this.getRandomActiveElemOrder = getRandomActiveElem(getLengthSimonItems)

                    setTimeout(() => {
                        allSimonItemsElem[this.getRandomActiveElemOrder].classList.add('active')
                    }, 1000)
                    setTimeout(() => {
                        allSimonItemsElem[this.getRandomActiveElemOrder].classList.remove('active')
                    }, 1400)
                }

                function successLevel() {
                    document.querySelectorAll('.simon__item')[this.getRandomActiveElemOrder].addEventListener('click', () => console.log('ты кликнул правильно'))
                }

                returnRandomElemForGame.call(this, level)

                successLevel.call(this)
            }
        }
    }
</script>

