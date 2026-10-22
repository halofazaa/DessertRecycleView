Berikut adalah draf **README.md** GitHub teknis yang disesuaikan untuk **Modul 2: Modifikasi Tampilan Halaman Dessert menjadi RecyclerView** berdasarkan gambar UI terbaru:

---

# Modul 2: Modifikasi Tampilan Halaman Dessert (RecyclerView)

Proyek ini merupakan bagian dari **Modul 2** yang berfokus pada modifikasi antarmuka halaman *Dessert* ("Droid Desserts") menggunakan komponen **`RecyclerView`** di Android (Kotlin). Tampilan diperbarui dari list standar menjadi daftar kustom dinamis yang menampilkan gambar item berlatar belakang lingkaran warna (*tint background*), teks deskripsi, dan tata letak modern.

---

## 🚀 Fitur Utama

* **Custom Dynamic List**: Menampilkan daftar makanan penutup (*donuts, ice cream sandwich, froyo*) menggunakan `RecyclerView`.


* **Dynamic Background Tint**: Warna lingkaran latar belakang gambar menyesuaikan kode HEX secara dinamis menggunakan `GradientDrawable`.


* **Custom Layout Integration**: Menggabungkan `ImageView`, `FrameLayout`, dan `TextView` di dalam item layout kustom (`itemdesert.xml`).
* **Data Class Model**: Penggunaan `data class Dessert` sebagai struktur data yang menampung deskripsi, ID gambar drawable, dan kode warna HEX.

---

## 🛠️ Detail Arsitektur & Komponen Teknis

### 1. Data Model (`Dessert.kt`)

Model data untuk menyimpan informasi setiap item dessert:

```kotlin
data class Dessert(
    val description: String,
    val imageRes: Int,
    val colorHex: String
)

```

### 2. Custom Adapter & ViewHolder (`DessertAdapter.kt`)

Mengatur pembuatan tampilan item (`itemdesert.xml`) dan mengikat data (*binding*), termasuk mewarnai background lingkaran secara dinamis:

```kotlin
class DessertAdapter(private val dessertList: List<Dessert>) :
    RecyclerView.Adapter<DessertAdapter.DessertViewHolder>() {

    class DessertViewHolder(itemView: View) : RecyclerView.ViewHolder(itemView) {
        val imgContainer: FrameLayout = itemView.findViewById(R.id.imgContainer)
        val imgDessert: ImageView = itemView.findViewById(R.id.imgDessert)
        val tvDescription: TextView = itemView.findViewById(R.id.tvDescription)
    }

    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): DessertViewHolder {
        val view = LayoutInflater.from(parent.context)
            .inflate(R.layout.itemdesert, parent, false)
        return DessertViewHolder(view)
    }

    override fun onBindViewHolder(holder: DessertViewHolder, position: Int) {
        val dessert = dessertList[position]

        holder.tvDescription.text = dessert.description
        holder.imgDessert.setImageResource(dessert.imageRes)

        // Mengubah warna background lingkaran secara dinamis
        val circleBg = GradientDrawable().apply {
            shape = GradientDrawable.OVAL
            setColor(Color.parseColor(dessert.colorHex))
        }
        holder.imgContainer.background = circleBg
    }

    override fun getItemCount(): Int = dessertList.size
}

```

### 3. Controller Utama (`MainActivity.kt`)

Menyiapkan *dataset* item dessert dan menghubungkannya ke `RecyclerView`:

```kotlin
val desserts = listOf(
    Dessert(
        description = "Donuts are glazed and sprinkled with candy.",
        imageRes = R.drawable.donut_circle,
        colorHex = "#C1E8C5"
    ),
    Dessert(
        description = "Ice cream sandwiches have chocolate wafers and vanilla filling.",
        imageRes = R.drawable.icecream_circle,
        colorHex = "#BBE0F8"
    ),
    Dessert(
        description = "Froyo is premium self-serve frozen yogurt.",
        imageRes = R.drawable.froyo_circle,
        colorHex = "#E4BCDF"
    )
)

val recyclerView: RecyclerView = findViewById(R.id.recyclerView)
recyclerView.layoutManager = LinearLayoutManager(this)
recyclerView.adapter = DessertAdapter(desserts)

```

---

## 📱 Tampilan Antarmuka (UI Preview)

| Header | Item Dessert | Lingkaran Warna |
| --- | --- | --- |
| Droid Desserts

 | Donuts, Ice Cream Sandwiches, Froyo

 | Hijau (`#C1E8C5`), Biru (`#BBE0F8`), Ungu (`#E4BCDF`) |

---

## ⚙️ Cara Menjalankan Project

1. Clone repositori ini:
```bash
git clone https://github.com/username/repository-name.git

```


2. Buka project menggunakan **Android Studio**.
3. Lakukan **Gradle Sync**.
4. Jalankan aplikasi pada emulator Android atau perangkat fisik.
