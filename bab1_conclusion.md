## Bab 1 — Nilai tiket (getValue)

Konteksnya: ada kolam/market (Uniswap v4 pool), gw shareholder di situ karena tanam modal. Jatah gw berbentuk sepasang token — token0 & token1. Modal ini juga dapet pajak dari tiap orang yang transaksi lewat market. Pajaknya numpuk di tiket gw, bebas gw mau klaim jadi token0 atau token1.

`getValue(tokenId, token)` tugasnya: jawab "tiket gw worth berapa, dalam satuan token patokan yang gw pilih (misal USDC atau WETH)." Lending protocol butuh angka ini buat tau gw boleh minjem berapa.

Alurnya 6 langkah urut:

1. **`_loadPositionState`** — kumpulin semua data mentah tiket: pool-nya apa, liquidity, range tick, harga live pool, harga oracle.
2. **`_getAmounts`** — itung modal gw berapa: pecah liquidity jadi jumlah token0 & token1.
3. **`_getFees`** — itung pajak klaim gw: berapa pajak numpuk, belum diklaim.
4. **`_feeObligation`** — itung utang ongkos plugin: hook pool (RevertHook) ngambil jatah berapa dari pajak gw.
5. **`_quoteTokenPrice`** — ambil harga token patokan (satuan akhir, misal USDC).
6. **`_netValues`** — ratain semua jadi satu angka akhir:
   - Pake `_netCurrency` buat tiap token: ongkos plugin dibayar pakai pajak dulu, baru modal kalo pajak kurang. 3 kasus:
     - pajak nutup ongkos → modal utuh, pajak sisa
     - pajak kurang → modal nalangin, pajak jadi 0
     - dua-duanya kurang → dua-duanya amblas
   - Sisa modal & pajak dikaliin harga token patokan → jadi satu angka akhir dalam satuan patokan.

Output `getValue`: `value` (nilai total tiket, bersih dari ongkos plugin, dalam token patokan), `feeValue` (bagian pajak doang, dalam token patokan), `price0X96` & `price1X96` (harga token0/1 dalam token patokan).