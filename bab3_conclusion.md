## bab 3

#### isi  

- gmn sistem decide how much a person can take a loan based on their collateral asset,example apa suatu kondisi hutang di anggap sakit atau sehat

#### flow :
1. pilih factor terkecil(the smallest risk buat calculate how much a user bs dpet loan)dari 2 token collateral user 

2. calculate max loan buat user

3. cek kondisi loan user

Catatan:
- Max factor 90% (MAX_COLLATERAL_FACTOR_X32) — sistem nggak pernah lebih dari ini
- Ada 2 jenis cap: collateralFactorX32 (per user), collateralValueLimitFactorX32 (system-wide per token)

Contoh: fullValue $1000, factor 70%, debt $650 → max loan $700, sehat.