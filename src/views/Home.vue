<template>
    <div class="home">
        <page v-for="product in ProductsList"
              :product="product"
              :key="ProductsList.indexOf(product)"
        ></page>
    </div>
</template>

<script>
    import Page from '@/components/Page.vue';

    export default {
        data() {
            return {
                ProductsList: []
            }
        },
        components: {
            Page,
        },
        created() {
            const xhr = new XMLHttpRequest();
            xhr.open('GET', 'api/products.json', false);
            xhr.send();
            if (xhr.status !== 200) {
                alert(xhr.status + ': ' + xhr.statusText);
            } else {
                this.ProductsList = JSON.parse(xhr.responseText);
            }
        }
    }
</script>

<style lang="scss">
    .home {
        display: flex;
        flex-direction: column;
        align-items: center;
    }
</style>