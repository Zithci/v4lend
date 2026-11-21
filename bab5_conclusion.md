## bab 5

### isi
gmn sistem set hard limit @uniswapV4(settlement bound 2^127) biar posisi gde gk stuck pas di liquidasi

### flow
1. uniV4 bakal reject stiap angka yg over 2^127(int128 limit)
```
79:    uint256 private constant V4_SETTLEMENT_BOUND = 1 << 127;
````
2. first solution : chunked liquidation - cut liquidation into small chunk (narik 200 jt ,50 juta x 4 withdraw)

3. second solution : tolak token dari constructor +  ``` setTokenConfig  ``` if totalSupply > V4_SETTLEMENT_BOUND = reject.

4.  prevent bayar gas yang berlebihan,price drifting

5. biar fee ke settle dluan sblm principal =  
``` FeeFirstRemovalLib ``` — INCREASE(0) sebelum DECREASE

6. calculate how much necessry token to calculate ```oracle.getLiquidityForValue() ```


