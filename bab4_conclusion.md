## bab 4

### isi
- gmn sistem eksekusi likuidasi — nentuin bonus penyita, siapa nombok kalo dana kurang, dan nasib tiket setelah kena sikat.

### flow
1. tentuin bonus buat penyita between 2%(min) - 10% (max) ``` _calculateLiquidation```

2. see if liquidator kuat buat handle hutng,if not continue flow no3

3. reserveCost handle - if liquidator+ reserveCost gk kuat nombok hutang
``` reserveCost```
4. marking token in process of liquidating
```  liquidatingTokenId```

5. setttlement buat liquidator & sistem between liquidator bonus and rest of the collateralValue of the loaner (biasnaya udh gk ada wkwkw klo smpe kena liquid artiya dhy pailit)
