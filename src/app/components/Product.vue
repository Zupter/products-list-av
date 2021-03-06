<template>
    <div class="product">
        <div class="product__info">
            <div class="product__info__basic">
                <span class="product__info__basic__name">{{ product.name }}</span>
                <span class="product__info__basic__categories">{{ categories }}</span>
            </div>

            <div class="product__info__price">
                <span class="product__info__price__old">
                    {{ formatCurrency(product.oldPrice || 0) }}
                </span>
                <span class="product__info__price__per">por</span>
                <span class="product__info__price__current">
                    {{ formatCurrency(product.currentPrice || 0) }}
                </span>
            </div>
        </div>

        <div class="product__images">
            <img
                v-for="(image, index) in (product.images || [])"
                :key="index"
                :src="image"
                class="product__images__single">
        </div>
    </div>
</template>

<script>
    export default {
        name: 'Product',

        props: {
            product: {
                type: Object,
                required: true,
            },
        },

        computed: {
            categories() {
                return this.product.categories
                    .map(category => category.name)
                    .join(' · ')
            },
        },

        methods: {
            formatCurrency(value) {
                return `R$ ${value.toFixed(2)}`.replace('.', ',')
            },
        },
    }
</script>

<style lang="scss" scoped>
    @import '~_scss_config/screen';
    @import '~_scss_config/variables';

    $product-image-size : 200px;

    .product {
        height: 145px;

        padding: 5px 10px;

        background-color: $color-white;

        display: flex;
        flex-direction: column;
        align-items: flex-start;
        justify-content: space-between;

        @include media-q($screen-xs) {
            height: 70px;

            flex-direction: row-reverse;
            align-content: center;
        }

        &__info {
            width: 100%;
            height: 60px;

            max-width: 350px;

            display: flex;
            flex-direction: column;
            align-items: flex-start;
            justify-content: space-between;

            @include media-q {
                min-width: calc(100% - #{$product-image-size});
                flex-direction: row;
                align-items: center;
            }

            &__basic {
                display: flex;
                flex-direction: column;

                &__name {
                    margin-bottom: 2px;

                    font-size: 14px;
                }

                &__categories {
                    color: darken($color-grey, 40);
                    font-size: 11px;
                }
            }

            &__price {
                color: darken($color-grey, 30);
                font-size: 14px;

                &__old {
                    text-decoration: line-through;
                }

                &__current {
                    color: black;
                }
            }
        }

        &__images {
            min-width: $product-image-size;

            display: flex;
            justify-content: flex-start;

            &__single {
                width: 60px;
                height: 60px;

                margin-right: 5px;
            }
        }
    }
</style>
