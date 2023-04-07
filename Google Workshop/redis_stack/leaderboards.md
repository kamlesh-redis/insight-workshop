## Sorted sets

```redis Add all bought product ids in the Bloom filter
BF.MADD user:778:bought_products  4545667 9026875 3178945 4848754 1242449
```

```redis Has a user bought this product?
BF.EXISTS  user:778:bought_products 1234567  // No, the user has not bought this product
BF.EXISTS  user:778:bought_products 3178945  // The user might have bought this product
```
