<template>
    <div class="description">
        <a class="description__link" href="#"><img class="description__link--image" :src="imageUrl" alt=""></a>
        <div class="description__container">
            <span class="description__code">Код: {{product.code}}</span>
            <a href="#"><h2 class="description__name">{{product.title}}</h2></a>
            <div class="description__additionally additionally">
                <ul class="additionally__list">
                    <span class="additionally__title-list">Могут понадобиться: </span>
                    <li v-for="elem in additionallyList"
                        :key="additionallyList.indexOf(elem)"
                        class="additionally__item"
                    ><a href="#">{{elem === additionallyList[additionallyList.length - 1]? elem + '.' :elem + ','}}</a>
                    </li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {}
        },
        props: {
            product: {type: Object}
        },
        computed: {
            additionallyList() {
                const arr = this.product.assocProducts.split(';');
                const result = [];
                for (const str of arr) {
                    if (!result.includes(str)) {
                        result.push(str);
                    }
                }
                return result.filter((elem) => elem !== "");
            },
            imageUrl() {
                const imageUrl = this.product.primaryImageUrl.split('.');
                imageUrl[imageUrl.length - 2] = imageUrl[imageUrl.length - 2] + '_220x220_1';
                return imageUrl.join('.')
            }
        }
    }


</script>

<style scoped lang="scss">

    .description {
        width: 900px;
        display: flex;

        &__link {
            display: block;
            min-width: 220px;
            height: 160px;

            &--image {
                width: 160px;
                height: 160px;
            }
        }

        &__container {
            min-height: 209px;
            width: 505px;
            padding: 1px 0px 65px 18px;
            text-align: left;
        }

        &__code {
            font-size: 12px;
        }

        &__name {
            font-size: 16px;
            line-height: 24px;
            padding: 12px 0;
            color: #000;
            max-width: 416px;
        }
    }

    .additionally {
        padding: 3px 1px;

        &__title-list {
            color: #545454;
            font-weight: 700;

        }

        &__list {
            list-style: none;
            padding: 0;
        }

        &__item {
            display: inline;
        }
    }


    @media screen and (max-width: 1249px) {
        .description {
            width: 490px;

            &__link {
                min-width: 160px;
            }

            &__container {
                min-height: 200px;
                width: 330px;
            }
        }
    }

    @media screen and (max-width: 999px) {
        .description {
            width: 220px;
            flex-direction: column;
            justify-content: flex-start;
            height: 310px;

            &__code {
                position: absolute;
                top: 10px;
                left: 10px;
            }

            &__link {
                margin: 0;
                min-width: 220px;
                min-height: 220px;
            }

            &__container {
                max-height: 80px;
                min-height: 0;
                width: 220px;
                padding: 0;
            }

            &__name {
                font-size: 14px;
                line-height: 20px;
                max-width: 220px;
                padding: 5px 0;
            }
        }

        .additionally {
            display: none;
        }
    }
</style>