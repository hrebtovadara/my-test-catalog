<template>
    <div class="product-page">
        <description :product="product"></description>
        <price-list :product="product"></price-list>
    </div>
</template>

<script>
    import Description from "@/components/Description.vue"
    import PriceList from "@/components/PriceList.vue"

    export default {
        data() {
            return {}
        },
        components: {
            Description,
            PriceList
        },
        props: {
            product: {type: Object}
        },


    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">

    .product-page {
        width: 990px;
        min-height: 305px;
        border: 1px solid #e0e0e0;
        padding: 10px 10px 18px;
        margin: 10px 5px 0;
        display: flex;
        align-items: flex-start;
        justify-content: space-between;
    }

    @media screen and (max-width: 1249px) {
        .product-page {
            width: 742px;
            min-height: 260px;
        }
    }

    @media screen and (max-width: 999px) {
        .product-page {
            width: 240px;
            height: 545px;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            position: relative;
        }
    }
</style>
