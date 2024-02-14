# be_tokobangunan
# BE_tokobangunan


# BACA NJING

# END POINT BARANG #

# NGAMBIL SEMUA BARANG
router.get('/barang', verifyUser, index);

#  NGAMBIL BARANG PER ID
router.get('/barang/:id', verifyUser, find);

# NAMBAHIN BARANG
router.post('/barang', verifyUser, create);

const { id_barang, nama_barang, kategori_id, harga, stok } = req.body;
const gambar = req.file ? req.file.filename : null;
 YANG DI BUTUHKAN KALOK NAMBAHIN BARANG, KATEGORI_ID DI AMBIL DARI ID TABEL KATEGORI NYA

# UPDATE BARANG SEKALIAN GANTI GAMBAR
router.patch('/barang/:id', verifyUser, upload.single('gambar'), update);

# DELETE BARANG 
router.delete('/barang/:id', verifyUser, destroy);


# END POINT KATEGORI #

router.get('/kategori', verifyUser,index);
router.get('/kategori/:id', verifyUser,find);
router.post('/kategori', verifyUser,create);
router.patch('/kategori/:id', verifyUser,update);
router.delete('/kategori/:id', verifyUser,destroy);

CRUD BIASA CUMAN UNTUK KETAGORI UNTUK BARANG

# END POINT USER/ADMIN #

router.get("/users", verifyUser, adminRole, index);
router.get("/users/:id", verifyUser, adminRole, find);
router.post("/users", verifyUser, adminRole,create);
router.patch("/users/:id", verifyUser, kasirRole, update);
router.delete("/users/:id", verifyUser, adminRole, destroy);

CRUD BIASA CUMAN NANTI ADMIN YANG BISA AKSES

# END POINT TRANSAKSI ATAU CART #


router.get('/transaksi', verifyUser, index);
UNTUK NGAMBIL SEMUA BARANG YANG ADA DI CART TERUS DI TOTALIN

router.get('/transaksi/:id', verifyUser, find);
UNTUK NGAMBIL PER ID YANG  ADA DI CART

router.post('/transaksi', verifyUser,adminRole, create);
NAMBAHIN BARANG KE CART CUMAN MASUKIN ID_BARANG SAMA QUANTITY NYA,
CUMAN KALOK DI POST SEKALI LAGI DENGAN ID YANG SAMA AUTO NAMBAH 1 QUANTITY NYA
CONTOH JSON NYA :
{
    "barang_id" : 1213115553,
    "quantity" : 1
}

router.put('/transaksi/jumlah/:id_cart_item', updateCartItemQuantity);
NAMBAHIN QUANTITY MANUAL KE CART CUMAN MASUKIN ID_BARANG DI PARM NYA SAMA QUANTITY DI BODY
{
    "quantity" : 1
}

router.put('/transaksi/tambah-quantity/:id_cart_item', addOneQuantity);
NIAT NYA JADI BUTON NAMBAH QUANTITY +1 TINGGAL MASUK KIN ID KE PARAM

router.put('/transaksi/kurang-quantity/:id_cart_item', subtractOneQuantity);
NIAT NYA JADI BUTON NAMBAH QUANTITY -1 TINGGAL MASUK KIN ID KE PARAM


router.delete('/transaksi/:id', verifyUser ,adminRole, destroy);
YA DELETE CART NYA AJA

router.post('/transaction', verifyUser,adminRole,transaction);
UNTUK BAYAR NANTI AUTOMATIS KE TRANSAKASI YANG ADA DICART
CONTOH JSON NYA:
{
  "jumlah_dibayarkan" : 100000
}

# END POINT DETAIL ATAU LAPORAN #

router.get('/detail', verifyUser, index);
router.get('/detail/hari', verifyUser, findhariini);
router.get('/detail/minggu', verifyUser, findmingguini);
router.get('/detail/bulan', verifyUser, findbulanini);
router.get('/detail/:id', verifyUser, find);
router.delete('/detail/:id', verifyUser, destroy);
DAH JELAS LAH YA 


yang baru dan dah bisa
# untuk laporan bulanan #

router.get('/detail/laporan', verifyUser, laporanBulanIni);

# untuk barang dan pendapatan hari ini
router.get('/detail/total', verifyUser, totalHarian);

# untuk refund cuma andmin
router.post('/refund',verifyUser,adminRole, refund);
pakek req body 
{
  "id_transaksi" : "T2024-02-14002"
}