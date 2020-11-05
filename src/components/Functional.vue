<template>
    <div class="functional">
        <div class="functional__container">
            <input class="functional__counter" placeholder="1" v-model="counter">
            <div class="functional__button-container">
                <button class="functional__button functional__button--add" @click="addCounter"></button>
                <button class="functional__button functional__button--remove" @click="removeCounter"></button>
            </div>
        </div>
        <button class="functional__buy">В корзину</button>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                counter: 1
            }
        },
        props: {
            product: {type: Object}
        },
        methods: {
            removeCounter() {
                this.counter--
                this.$emit('change-price', this.counter)
                return this.counter
            },
            addCounter() {
                this.counter++
                this.$emit('change-price', this.counter)
                return this.counter
            }
        }

    }
</script>

<style scoped lang="scss">
    .functional {

        display: flex;
        justify-content: space-between;

        &__counter {
            width: 41px;
            height: 40px;
            border-radius: 0;
            border: 1px solid #ccc;
            margin-right: -1px;
            text-align: center;

            &::-webkit-input-placeholder,
            &::-moz-placeholder,
            &::-ms-input-placeholder {
                color: #000;
            }

            &:active, &:focus {
                outline: none;
            }
        }

        &__container {
            display: flex;
        }

        &__button {
            width: 27px;
            border-radius: 0;
            border: 1px solid #ccc;
            background-color: white;
            background-image: url("../assets/count--i.png");
            background-repeat: no-repeat;

            &--add {
                background-position: -28px -2px;
                margin-bottom: -1px;
                height: 21px;

                &:hover {
                    background-position: -1px -2px;
                }
            }

            &--remove {
                background-position: -28px -21px;
                height: 20px;

                &:hover {
                    background-position: -1px -21px;
                }
            }

            &:hover {
                background-color: #666;
                border: 1px solid #ccc;
            }

            &:active, &:focus {
                outline: none;
            }

            &-container {
                display: flex;
                flex-direction: column;
            }
        }

        &__buy {
            width: 148px;
            height: 40px;
            padding: 0 0 0 20px;
            cursor: pointer;
            background-color: #f90;
            border: none;
            color: #fff;
            font-size: 14px;
            text-transform: uppercase;
            position: relative;

            &:hover {
                background-color: #333;
            }

            &::before {
                content: '';
                position: absolute;
                left: 10px;
                bottom: 10px;
                width: 20px;
                height: 20px;
                background-image: url("../assets/shopping-cart.svg");
            }
        }
    }
</style>