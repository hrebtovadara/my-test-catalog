<template>
    <div class="price-list">
        <span class="price-list__availability">{{product.isActive? "Наличие" : "Нет в наличии"}}</span>
        <div class="price-list__price price">
            <span class="price__card">По карте клуба</span>
            <div class="price__container">
                <p class="price__container--discount">
                    <span class="price__item price__item--discount">{{priceDiscont}}</span>
                    <svg class="price__svg--discount" width="19" height="19">
                        <use xlink:href="../assets/sprite.svg#rouble"></use>
                    </svg>
                </p>
                <p class="price__container--standard">
                    <span class="price__item price__item--standard">{{priceStandard}}</span>
                    <svg class="price__svg--standard" width="19" height="19">
                        <use xlink:href="../assets/sprite.svg#rouble"></use>
                    </svg>
                </p>
            </div>
        </div>
        <span class="price-list__points">Можно купить за {{product.bonusAmount}} баллов</span>
        <div class="price-list__button-container">
            <button class="price-list__button" :class="[condition === 'square'? 'price-list__button--active' : '']"
                    @click="condition = 'square'"><span>За м. кв.</span></button>
            <button class="price-list__button" :class="[condition === 'piece'? 'price-list__button--active' : '']"
                    @click="condition = 'piece'"><span>За упаковку</span></button>
        </div>
        <div class="price-list__proviso proviso">
            <div class="proviso__container">
                <img class="proviso__image" src="../assets/unit--i.png" width="15px" height="15px">
                <span class="proviso__text">Продается упаковками:<br>1 упак. = 2.47 м.кв</span>
            </div>
        </div>
        <functional
                :product="product"
                @change-price="changePrice"
        ></functional>
    </div>
</template>

<script>
    import Functional from "@/components/Functional.vue"

    export default {
        data() {
            return {
                condition: 'square',
                counter: 1
            }
        },
        components: {
            Functional
        },
        computed: {
            priceDiscont: function () {
                return ((this.condition === 'square' ? this.product.priceGoldAlt : this.product.priceRetailAlt) * this.counter).toFixed(2)
            },
            priceStandard: function () {
                return ((this.condition === 'square' ? this.product.priceGold : this.product.priceRetail) * this.counter).toFixed(2)
            },
        },
        props: {
            product: {
                type: Object
            }
            ,
        }
        ,
        methods: {
            changePrice(counter) {
                this.counter = counter;
            }
        }
    }

</script>

<style scoped lang="scss">
    .price-list {
        text-align: right;
        min-width: 222px;

        &__availability {
            cursor: pointer;
            color: #093;
            border-bottom: 1px dotted #093;
            font-size: 14px;
            line-height: 1.4;

            &:hover {
                border-bottom: none;
            }
        }

        &__points {
            font-size: 12px;
            line-height: 17px;
            color: #999;
        }

        &__button {
            border: none;
            background-color: transparent;
            font-size: 13px;
            line-height: 13px;
            cursor: default;
            padding: 2px 5px;
            margin-left: 5px;
            border-radius: 0;

            &-container {
                margin: 4px 0;
            }

            & span {
                border-bottom: 1px dotted #707070;
            }

            &--active {
                background-color: #000;
                outline: none;
                border: none;

                & span {
                    border: none;
                    color: #ffffff;
                }
            }
        }
    }

    .price {
        height: 80px;
        display: flex;
        justify-content: space-between;
        padding: 12px 0 6px 32px;

        &__card {
            width: 58px;
            font-weight: 400;
            font-size: 14px;
            display: inline-block;
            text-align: right;
            line-height: 17px;
        }

        &__container {
            &--discount {
                padding-top: 10px;
            }

            &--standard {
                padding-top: 6px;
            }
        }

        &__item {
            font-size: 25px;
            line-height: 16px;

            &--discount {
                color: #000;
                font-weight: 700;
            }

            &--standard {
                color: #a7a7a7;
            }
        }

        &__svg {

            &--discount {
                fill: #010101;
            }

            &--standard {
                fill: #a7a7a7;
            }
        }
    }

    .proviso {
        position: relative;

        &::before {
            content: '';
            position: absolute;
            left: 15px;
            bottom: -8px;
            width: 0;
            height: 0;
            border-left: 8px solid transparent;
            border-right: 8px solid transparent;
            border-top: 8px solid #ccc;
        }

        &::after {
            content: '';
            position: absolute;
            left: 16px;
            bottom: -6px;
            width: 0;
            height: 0;
            border-left: 7px solid transparent;
            border-right: 7px solid transparent;
            border-top: 7px solid #fff;
        }

        &__container {
            min-height: 44px;
            width: 222px;
            margin: 10px 0 10px;
            padding: 3px 10px 3px 40px;
            background: #fff;
            border: 1px solid #ccc;
            background-color: transparent;
            text-align: left;
        }

        &__text {
            font-size: 13px;
            line-height: 15px;
            color: #000;
        }

        &__image {
            position: absolute;
            left: 11px;
            top: 12px;
        }
    }

    @media screen and (max-width: 999px) {
        .price-list {
            max-width: 220px;

            &__availability {
                position: absolute;
                top: 6px;
                right: 10px;
            }

            &__points {
                display: none;
            }

            &__button-container {
                margin: 6px 0;
            }
        }

        .price {
            padding: 0 0 0 45px;
            height: 70px;

            &__item {
                &--discount {
                    font-size: 28px;
                    font-weight: 700;
                }

                &--standard {
                    font-size: 26px;
                }
            }
        }

        .proviso {
            display: none;
        }
    }

</style>