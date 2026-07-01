<a id="readme-top"></a>

<div align="center">
  <img width="100%" src="https://capsule-render.vercel.app/api?type=waving&height=240&color=0:2F5C3E,100:7EAF8D&text=Nimons360&fontColor=FFFFFF&fontSize=64&desc=Family%20Location%20Tracker&descAlignY=78&descSize=18&descColor=E0F5EC" />
</div>

<br/>

<div align="center">
  <img src="app/src/main/res/drawable/ic_logo.png" alt="Nimons360 Logo" width="100" />
  <h3 align="center">Nimons360</h3>
  <p align="center">
    Aplikasi Android untuk melacak lokasi anggota keluarga secara real-time<br/>
    IF3210 — Pengembangan Aplikasi Piranti Bergerak · K01-TBD<br/>
    Institut Teknologi Bandung · 2026
  </p>
</div>

<div align="center">
<br/>

![Kotlin](https://img.shields.io/badge/Kotlin-7F52FF?style=for-the-badge&logo=kotlin&logoColor=white)
![Android](https://img.shields.io/badge/Android-3DDC84?style=for-the-badge&logo=android&logoColor=white)
![Jetpack Compose](https://img.shields.io/badge/Jetpack%20Compose-4285F4?style=for-the-badge&logo=jetpackcompose&logoColor=white)
![Material3](https://img.shields.io/badge/Material%203-757575?style=for-the-badge&logo=materialdesign&logoColor=white)
![Room](https://img.shields.io/badge/Room%20DB-4A7C59?style=for-the-badge&logo=sqlite&logoColor=white)

</div>

---

<!-- TABLE OF CONTENTS -->
<details>
  <summary>Daftar Isi</summary>
  <ol>
    <li><a href="#about-the-project">Tentang Aplikasi</a></li>
    <li><a href="#tech-stack">Tech Stack & Library</a></li>
    <li><a href="#features">Fitur Aplikasi</a></li>
    <li><a href="#getting-started">Getting Started</a></li>
    <li><a href="#screenshots">Screenshot Aplikasi</a></li>
    <li><a href="#accessibility">Bonus: Accessibility Testing</a></li>
    <li><a href="#project-structure">Project Structure</a></li>
    <li><a href="#pembagian-tugas">Pembagian Tugas</a></li>
  </ol>
</details>

---

## Tentang Aplikasi

<a id="about-the-project"></a>

Nimons360 adalah aplikasi Android yang dirancang untuk komunitas Nimons agar setiap anggota keluarga dapat saling memantau lokasi secara real-time. Terinspirasi dari kebutuhan Gro untuk menjaga keselamatan seluruh anggota keluarga Nimons yang aktif bergerak, aplikasi ini menyediakan fitur pelacakan lokasi berbasis GPS, manajemen grup keluarga, dan komunikasi data real-time via WebSocket.

### Tujuan Utama

- Membangun aplikasi Android native menggunakan Kotlin
- Mengimplementasikan komunikasi real-time dengan WebSocket
- Menerapkan manajemen data lokal menggunakan Room Database
- Mengintegrasikan GPS dan sensor orientasi perangkat
- Menerapkan best practice keamanan penyimpanan token di Android

<div align="right"><a href="#readme-top">↖ Kembali ke atas</a></div>

---

## Tech Stack & Library

<a id="tech-stack"></a>

| Kategori | Library / Teknologi |
|:---|:---|
| **Bahasa** | Kotlin |
| **UI Framework** | Jetpack Compose + Android XML |
| **Navigation** | Jetpack Navigation Compose |
| **HTTP Client** | Retrofit 2 + OkHttp |
| **WebSocket** | Java-WebSocket 1.5.3 |
| **Image Loading** | Glide 4.16.0 |
| **Peta** | osmdroid |
| **Lokasi** | Google Play Services Location |
| **Database Lokal** | Room Database (SQLite) |
| **Keamanan** | AndroidX Security Crypto (EncryptedSharedPreferences) |
| **Desain** | Material Design 3 (Material You) |
| **DI / State** | ViewModel + StateFlow |
| **Push Notification** | Firebase Cloud Messaging (FCM) |
| **Deep Link** | Android Intent Filter + NavDeepLink |
| **QR Code** | ZXing Core (generate QR bitmap) |
| **Chart** | Compose Canvas (bar chart harian analytics) |

<div align="right"><a href="#readme-top">↖ Kembali ke atas</a></div>

---

## Fitur Aplikasi

<a id="features"></a>

<details>
<summary><b>Milestone 1 — Fitur Utama</b></summary>
<br/>

- **Auth** — Login dengan token JWT, penyimpanan aman via EncryptedSharedPreferences, auto-redirect saat token kedaluwarsa (409)
- **Home** — Menampilkan *My Families* dan *Discover Families* dengan avatar stack member
- **Families** — Buat, join, leave, pin family; filter All/My Families; sinkronisasi Room Database untuk pin lokal
- **Family Detail** — Informasi detail family, daftar anggota, salin family code otomatis
- **Map & GPS** — Tampilkan peta dengan pin lokasi real-time via WebSocket; indikator arah perangkat dari sensor kompas
- **Profile** — Avatar inisial, edit nama via bottom sheet, tombol Sign Out, theme toggle (Light/System/Dark)
- **Network Sensing** — Banner otomatis muncul saat offline dan hilang saat kembali online

</details>

<details>
<summary><b>Milestone 1 — Bonus</b></summary>
<br/>

- **Search Family** — Search bar real-time untuk filter daftar family berdasarkan nama
- **Internet Status on Map** — Tampilkan status koneksi (wifi/mobile) member lain di popup peta
- **Accessibility Testing** — Pemindaian UI dengan Accessibility Scanner + perbaikan berdasarkan saran

</details>

<details>
<summary><b>Milestone 2 — Fitur Utama</b></summary>
<br/>

- **Map Extended** — Long press → tandai lokasi (nama, deskripsi, foto); CRUD di SQLite + filesystem; recenter button; background location via ForegroundService; BroadcastReceiver baterai
- **Notifikasi FCM** — Kirim & terima push notification ke/dari anggota family; pesan cepat (Good Morning/Afternoon/Night); preferensi notifikasi via SharedPreferences
- **Upload Foto Profil** — Kamera / galeri → upload via POST /api/me/photo; tampilkan `profileImageUrl` di semua layar user
- **Location Sharing Toggle** — Toggle privasi di halaman Profile; jika mati, WS update_presence tidak dikirim
- **Share Family Link** — Deep link `nimons360://family/<id>?code=<code>` via Android Sharesheet; handler deep link langsung ke FamilyDetailScreen
- **Responsive** — Layout portrait + landscape untuk seluruh layar

</details>

<details>
<summary><b>Milestone 2 — OWASP Security</b></summary>
<br/>

> Analisis berdasarkan [OWASP Mobile Top 10 (2024)](https://owasp.org/www-project-mobile-top-10/). Asumsi: server tidak aman; seluruh validasi dilakukan dari sisi client.

### Praktik Keamanan yang Diimplementasi

| # | Praktik | Detail |
|---|---------|--------|
| 1 | **Secure Token Storage** | JWT disimpan di `EncryptedSharedPreferences` (AES256-GCM + AES256-SIV). Tidak ada plaintext token di disk. |
| 2 | **HTTPS Enforcement** | Seluruh API call menggunakan `https://mad.labpro.hmif.dev`. Tidak ada HTTP fallback. |
| 3 | **Input Validation** | Email divalidasi format `@domain.tld` sebelum login. Family code divalidasi tepat 6 karakter. Foto profil dibatasi 500 KB dengan kompresi adaptif. Semua field required dicek tidak blank sebelum submit. |
| 4 | **Safe Error Handling** | Error server ditampilkan sebagai pesan generik ke user. Stack trace tidak pernah diekspos ke UI. |

---

### M4 — Insufficient Input/Output Validation

**Temuan awal:**
- Form login tidak memvalidasi format email di sisi client; input apapun diterima dan baru ditolak oleh server.
- Form Create Family tidak menampilkan batas panjang nama family kepada user.

**Yang sudah diperbaiki:**
- Validasi format email (`Patterns.EMAIL_ADDRESS`) di `LoginScreen`; request tidak dikirim jika email tidak valid.
- Family code divalidasi tepat 6 karakter sebelum request Join dikirim.
- Semua field required (nama profil, nama family, pesan notifikasi, nama marked location) divalidasi tidak blank sebelum submit.
- Foto profil dikompresi dan dicek ukurannya (max 500 KB) sebelum upload ke server.

**Yang belum diperbaiki:**
- Validasi panjang minimum password belum ada di sisi client; masih bergantung pada penolakan dari server.

---

### M8 — Security Misconfiguration

**Temuan awal:**
- `HttpLoggingInterceptor` dikonfigurasi `Level.BODY` pada semua build termasuk production; Authorization header (JWT) dan response body (data user, family) ter-log ke Logcat dan dapat dibaca pihak ketiga via ADB.
- Tidak ada Network Security Config untuk membatasi domain yang diizinkan.

**Yang sudah diperbaiki:**
- `HttpLoggingInterceptor` kini hanya aktif di debug build (`BuildConfig.DEBUG`). Di release build, level diset ke `NONE`; tidak ada data sensitif yang ter-log.
- Token expired/invalid (HTTP 401/409) otomatis memicu logout dan penghapusan token dari storage.
- Seluruh traffic menggunakan HTTPS tanpa HTTP fallback.

---

### M9 — Insecure Data Storage

**Kondisi yang sudah aman:**
- JWT token disimpan di `EncryptedSharedPreferences` (AES256-GCM + AES256-SIV), aman dari akses langsung ke file sistem.
- Foto profil dan foto marked locations disimpan di `context.filesDir` yang bersifat private (tidak accessible aplikasi lain tanpa root).
- User preferences (notification/location toggle) di SharedPreferences biasa, tidak mengandung data sensitif.

**Temuan:**
- Room database (`nimons360_database`) disimpan tanpa enkripsi (SQLite polos). Data yang tersimpan mencakup marked locations, history lokasi, dan pinned families. Pada device yang di-root, file database dapat dibaca langsung.

**Yang belum diperbaiki:**
- Implementasi SQLCipher untuk mengenkripsi Room database belum dilakukan; data lokasi lokal dapat dibaca pada device rooted.

</details>

<details>
<summary><b>Milestone 2 — Bonus</b></summary>
<br/>

- **Share Family via QR Code** *(Rafizan)* — Generate QR dari deep link, preview di app, share PNG via Sharesheet
- **Analytics** *(Orvin)* — Statistik jarak, active days, grafik harian, recent locations, export CSV
- **Customizable Icon** *(Orvin)* — Download custom pin via ForegroundService + loading bar notifikasi; apply pin ke peta
- **Accessibility Testing** *(Hazim)* — Re-scan seluruh layar ms2, perbaiki semua suggestion
- **Share Story Instagram** *(Hazim)* — Meta SDK untuk share story IG dengan screenshot MapScreen

</details>

<div align="right"><a href="#readme-top">↖ Kembali ke atas</a></div>

---

## Getting Started

<a id="getting-started"></a>

### Prerequisites

- Android Studio Ladybug (2024.2.x) atau lebih baru
- JDK 21
- Android device / emulator (min. API Level 30 / Android 11)

### Instalasi & Menjalankan

1. Clone repository ini
2. Buka project di Android Studio
3. Sync Gradle dependencies
4. Jalankan aplikasi ke device/emulator
5. Login menggunakan akun ITB:
   - **Email:** `{NIM}@std.stei.itb.ac.id`
   - **Password:** `{NIM}`
6. Base URL server: `https://mad.labpro.hmif.dev`

<div align="right"><a href="#readme-top">↖ Kembali ke atas</a></div>

---

## Screenshot Aplikasi

<a id="screenshots"></a>

<div align="center">

### Milestone 2 — Fitur Baru

| Profile (foto + toggle) | Marked Location | Notifikasi |
|:---:|:---:|:---:|
| <img src="screenshots/ms2/ms2_profile.png" height="400"/> | <img src="screenshots/ms2/ms2_marked_location.png" height="400"/> | <img src="screenshots/ms2/ms2_notification.png" height="400"/> |

| Share Family | QR Code | Analytics |
|:---:|:---:|:---:|
| <img src="screenshots/ms2/ms2_share_family.png" height="400"/> | <img src="screenshots/ms2/ms2_qr_code.png" height="400"/> | <img src="screenshots/ms2/ms2_analytics.png" height="400"/> |

| Customize Pin |
|:---:|
| <img src="screenshots/ms2/ms2_customize_pin.png" height="400"/> |

### Milestone 2 — Landscape

| Home (landscape) | Families (landscape) | Map (landscape) |
|:---:|:---:|:---:|
| <img src="screenshots/ms2/ms2_home_landscape.png" height="240"/> | <img src="screenshots/ms2/ms2_families_landscape.png" height="240"/> | <img src="screenshots/ms2/ms2_map_landscape.png" height="240"/> |

| Profile (landscape) | Login (landscape) | Family Detail (landscape) |
|:---:|:---:|:---:|
| <img src="screenshots/ms2/ms2_profile_landscape.png" height="240"/> | <img src="screenshots/ms2/ms2_login_landscape.png" height="240"/> | <img src="screenshots/ms2/ms2_familydetail_landscape.png" height="240"/> |

### Milestone 1 — Auth

| Login |
|:---:|
| <img src="screenshots/login.png" height="400"/> |

### Home & Families

| Home | Families |
|:---:|:---:|
| <img src="screenshots/home.png" height="400"/> | <img src="screenshots/family.png" height="400"/> |

### Family Detail & Dialogs

| My Family Detail | Other Family Detail | Create Family |
|:---:|:---:|:---:|
| <img src="screenshots/myfamilydetail.png" height="400"/> | <img src="screenshots/otherfamilydetail.png" height="400"/> | <img src="screenshots/createfamily.png" height="400"/> |

| Join Family | Leave Family | Pinned Family |
|:---:|:---:|:---:|
| <img src="screenshots/joinfamily.png" height="400"/> | <img src="screenshots/leavefamily.png" height="400"/> | <img src="screenshots/pinnedfamily.png" height="400"/> |

### Map

| Map | User Detail |
|:---:|:---:|
| <img src="screenshots/map.png" height="400"/> | <img src="screenshots/userdetail.png" height="400"/> |

### Profile

| Profile | Logout |
|:---:|:---:|
| <img src="screenshots/profile.png" height="400"/> | <img src="screenshots/logout.png" height="400"/> |

### Network Sensing

| No Internet Banner |
|:---:|
| <img src="screenshots/disconnect.png" height="400"/> |

</div>

<div align="right"><a href="#readme-top">↖ Kembali ke atas</a></div>

---

## Bonus: Accessibility Testing

<a id="accessibility"></a>

Pemindaian aksesibilitas dilakukan menggunakan **Accessibility Scanner** (Google) pada seluruh halaman aplikasi, dilanjutkan dengan audit manual WCAG AA/AAA pada setiap layar.

### Perbaikan yang Dilakukan

#### Milestone 1

| No. | File | Perubahan | Masalah yang Diperbaiki |
|---|---|---|---|
| 1 | `values/colors.xml` | `color_error`: `#FF3B30` → `#C62828` | Kontras tombol Leave (putih di merah) dari 3.55 → 5.62 |
| 2 | `activity_create_family.xml` | `btnCreate` backgroundTint: `color_secondary` → `color_secondary_dark` | Kontras tombol Create dari 4.09 → ≥4.5 |
| 3 | `activity_create_family.xml` | `etFamilyName`: tambah `android:hint` | Field input kini memiliki label untuk screen reader |
| 4 | `FamilyListAdapter.kt` | `btnJoin.contentDescription = "Join ${family.name}"` | Tombol Join memiliki deskripsi unik per family |
| 5 | `MainShell.kt` | `selectedTextColor = colorScheme.primary` | Kontras label nav aktif dari 4.38 → ≥4.5; dark-mode safe |

#### Milestone 2 

| No. | File | Perubahan | Kriteria WCAG |
|---|---|---|---|
| 1 | `HomeScreen.kt` | Avatar palette diganti ke 7 warna accessible; teks gelap untuk bg terang | 1.4.3 AA |
| 2 | `HomeScreen.kt` | "+N more" background `LTGRAY` → `#44403C` (1.79 → 7.5:1) | 1.4.3 AA |
| 3 | `HomeScreen.kt` | `contentDescription` pada clickable card, avatar views, "+N more" | 1.1.1 A, 4.1.2 A |
| 4 | `MainShell.kt` | Profile `IconButton` semantics; `SubcomposeAsyncImageContent` description | 1.1.1 A, 4.1.2 A |
| 5 | `fragment_home.xml` | `accessibilityHeading="true"` pada section headers | 1.3.1 A |
| 6 | `fragment_families.xml` | Chip check icon dikembalikan; floating label diaktifkan; heading roles | 1.4.1 A, 2.4.6 AA, 1.3.1 A |
| 7 | `fragment_family_detail.xml` | `labelFor` pada label MEMBERS dan FAMILY CODE | 1.3.1 A |
| 8 | `FamilyDetailScreen.kt` | Dialog setTitle; avatar palette accessible; btnPin state-aware | 1.3.1 A, 1.4.3 AA, 4.1.2 A |
| 9 | `ProfileScreen.kt` | Avatar semantics; `ToggleRow` `toggleable`+`mergeDescendants`; overlay 28dp dihapus | 1.1.1 A, 4.1.2 A, 2.5.5 AAA |
| 10 | `AnalyticsScreen.kt` | Chart Canvas `contentDescription` dengan data aktual; StatCard merged; heading | 1.1.1 A, 1.3.1 A |
| 11 | `activity_create_family.xml` | `labelFor`+heading pada labels; info icon `color_info` → `color_info_text` | 1.3.1 A, 1.4.11 AA |
| 12 | `CreateFamilyScreen.kt` | Icon contentDescription unik per posisi; `ViewCompat.setStateDescription` | 4.1.2 A |
| 13 | `MapScreen.kt` | Map semantics; clear search description; search label; showArrow konsisten | 1.1.1 A, 4.1.2 A, 1.4.1 A |
| 14 | `NotificationBottomSheet.kt` | `onClickLabel` pada member list items | 4.1.2 A |
| 15 | `NetworkOfflineBanner.kt` | `liveRegion = LiveRegionMode.Assertive` | 4.1.3 A |
| 16 | `MapBottomSheetComponents.kt` | Foto thumbnail `contentDescription = "Foto N dari X"` | 1.1.1 A |
| 17 | `FamilyListAdapter.kt` | `btnPin.contentDescription` unik per family: "Pin/Unpin [nama]" | 4.1.2 A |
| 18 | `HomeScreen.kt` | Hapus kata "tap" dari contentDescription family card | 4.1.2 A |
| 19 | `ProfileScreen.kt` | Hapus "tap to change" dari contentDescription foto profil | 4.1.2 A |
| 20 | `ProfileScreen.kt` | `ToggleRow` tambah `heightIn(min = 48.dp)` untuk touch target | 2.5.5 AA |
| 21 | `AnalyticsScreen.kt` | StatCard value text: `primary` (#4A7C59, 3.74:1) → `onSurface` (#1C1C1E) | 1.4.3 AA |
| 22 | `CustomizePinScreen.kt` | "Use" button semantics unik per pin; "Downloaded" text semantics unik | 4.1.2 A |
| 23 | `CustomizePinScreen.kt` | "Downloaded" text color: `primary` (3.75:1) → `onSurfaceVariant` (#44403C) | 1.4.3 AA |
| 24 | `dialog_join_family.xml` | `textColorHint` pada `etFamilyCode`: outline (#848075, 3.44) → onSurfaceVariant (#44403C) | 1.4.3 AA |
| 25 | `activity_create_family.xml` | `textColorHint` pada `etFamilyName`: default (3.02) → onSurfaceVariant (#44403C) | 1.4.3 AA |
| 26 | `MainShell.kt` | Nav bar `selectedTextColor`/`selectedIconColor`: `primary` (4.38:1) → `ColorPrimaryDark` (#2F5C3E, 7.37:1) | 1.4.3 AA |

### Before & After per Halaman

<details>
  <summary>Families List</summary>
  <br/>
  <div align="center">

  | Before | After |
  |:---:|:---:|
  | <img src="docs/accessibility_results_Nimons360_before/screen1.png" height="400"/> | <img src="docs/accessibility_results_Nimons360_after/screen1.png" height="400"/> |

  </div>

  **Before — Saran dari scanner:**
  - Text contrast: tombol-tombol family terlalu rendah (ratio < 4.50)
  - Item descriptions: beberapa tombol "Join" memiliki deskripsi identik
  - Text scaling: beberapa TextView menggunakan ukuran tetap

  **After — Saran yang tersisa:**
  - Image contrast: ikon family dari server memiliki kontras rendah (foreground/background icon image)
  - Text contrast: tombol dengan background #AF52DE dari Material3 theme default
  - Text scaling: beberapa ViewGroup dengan lebar tetap
  - Item descriptions: duplikat "Home" di nav bar

  ✓ **Diperbaiki:** tombol Join kini memiliki deskripsi unik per nama family
</details>

<details>
  <summary>Family Detail</summary>
  <br/>
  <div align="center">

  | Before | After |
  |:---:|:---:|
  | <img src="docs/accessibility_results_Nimons360_before/screen2.png" height="400"/> | <img src="docs/accessibility_results_Nimons360_after/screen2.png" height="400"/> |

  </div>

  **Before — Saran dari scanner:**
  - Text contrast: `btnLeaveFamily` — teks merah (#FF3B30) pada background putih, ratio 3.39 (butuh 4.50)
  - Text contrast: avatar inisial member (#FFFFFF pada #AF52DE), ratio 4.13
  - Text scaling: avatar container menggunakan ukuran tetap

  **After — Saran yang tersisa:**
  - Text contrast: chip status (#C4622D pada #FAE8DF), ratio 3.44
  - Text contrast: avatar inisial member (#FFFFFF pada #AF52DE), ratio 4.13
  - Text scaling: avatar container dengan ukuran tetap

  ✓ **Diperbaiki:** `btnLeaveFamily` tidak lagi muncul sebagai isu kontras
</details>

<details>
  <summary>Leave Family Dialog</summary>
  <br/>
  <div align="center">

  | Before | After |
  |:---:|:---:|
  | <img src="docs/accessibility_results_Nimons360_before/screen3.png" height="400"/> | <img src="docs/accessibility_results_Nimons360_after/screen3.png" height="400"/> |

  </div>

  **Before — Saran dari scanner:**
  - Text contrast: tombol "Leave" — teks putih (#FFFFFF) pada background merah (#FF3B30), ratio 3.55 (butuh 4.50)

  **After:** Tidak ada saran perbaikan. ✓ Tombol "Leave" berhasil diperbaiki kontrasnya.
</details>

<details>
  <summary>Join Family Dialog</summary>
  <br/>
  <div align="center">

  | Before | After |
  |:---:|:---:|
  | <img src="docs/accessibility_results_Nimons360_before/screen5.png" height="400"/> | <img src="docs/accessibility_results_Nimons360_after/screen5.png" height="400"/> |

  </div>

  **Before & After:** Tidak ada saran perbaikan pada halaman ini. ✓
</details>

<details>
  <summary>Profile</summary>
  <br/>
  <div align="center">

  | Before | After |
  |:---:|:---:|
  | <img src="docs/accessibility_results_Nimons360_before/screen7.png" height="400"/> | <img src="docs/accessibility_results_Nimons360_after/screen6.png" height="400"/> |

  </div>

  **Before — Saran dari scanner:**
  - Text contrast: tombol "Leave" — teks putih pada background #FF3B30, ratio 3.55

  **After:** ✓ `ColorError` di `Color.kt` (Compose) diupdate ke `#C62828` — isu ini berasal dari Compose theme yang terpisah dari `colors.xml`.
</details>

<details>
  <summary>Profile Edit</summary>
  <br/>
  <div align="center">

  | Before | After |
  |:---:|:---:|
  | <img src="docs/accessibility_results_Nimons360_before/screen8.png" height="400"/> | <img src="docs/accessibility_results_Nimons360_after/screen7.png" height="400"/> |

  </div>

  **Before — Saran dari scanner:**
  - Unexposed text: teks "t Profile" mungkin tidak terekspos ke layanan aksesibilitas

  **After — Saran yang tersisa:**
  - Unexposed text: teks "< Profile" mungkin tidak terekspos ke layanan aksesibilitas
</details>

<details>
  <summary>Create Family</summary>
  <br/>
  <div align="center">

  | Before | After |
  |:---:|:---:|
  | <img src="docs/accessibility_results_Nimons360_before/screen12.png" height="400"/> | <img src="docs/accessibility_results_Nimons360_after/screen9.png" height="400"/> |

  </div>

  **Before — Saran dari scanner:**
  - Item label: `etFamilyName` tidak memiliki label yang dapat dibaca screen reader
  - Text contrast: `btnCreate` — teks putih pada background #C4622D, ratio 4.09 (butuh 4.50)
  - Item type label: content description ikon family preview mengandung state "Selected"
  - Image contrast: beberapa ikon family di picker memiliki kontras rendah
  - Item descriptions: beberapa opsi ikon family memiliki deskripsi identik "Family Icon Option"

  **After — Saran yang tersisa:**
  - Image contrast: ikon family di picker (remote image, di luar kendali app)
  - Item descriptions: opsi ikon "Family Icon Option" masih identik (8 opsi)
  - Text contrast: hint text `etFamilyName` (#91918E pada #FAFAF4), ratio 3.02

  ✓ **Diperbaiki:** `etFamilyName` kini memiliki label untuk screen reader; `btnCreate` tidak lagi muncul sebagai isu kontras; content description preview ikon sudah tidak mengandung state "Selected"
</details>

<details>
  <summary>Families Screen (landscape)</summary>
  <br/>
  <div align="center">

  | Before | After |
  |:---:|:---:|
  | <img src="docs/accessibility_results_Nimons360_before/screen13.png" height="300"/> | *(screenshot belum tersedia)* |

  </div>

  **Before — Saran dari scanner:**
  - Text contrast: beberapa item termasuk tombol Join (ratio < 4.50)
  - Text contrast: bottom navigation active text (#4A7C59 pada #F0F4F1), ratio 4.38
  - Item descriptions: tombol "Join" identik pada beberapa family
  - Item descriptions: "Home" muncul duplikat (label teks dan content description ikon sama)
  - Text scaling: beberapa ViewGroup dengan lebar tetap berisi teks yang scalable
</details>

<details>
  <summary>Map Screen</summary>
  <br/>
  <div align="center">

  | Before | After |
  |:---:|:---:|
  | <img src="docs/accessibility_results_Nimons360_before/screen16.png" height="400"/> | <img src="docs/accessibility_results_Nimons360_after/screen11.png" height="400"/> |

  </div>

  **Before — Saran dari scanner:**
  - Item label: satu elemen tidak memiliki label yang dapat dibaca screen reader
  - Text contrast: bottom navigation active text, ratio 4.38
  - Item descriptions: "Map" muncul duplikat (label dan content description ikon identik)

  **After — Saran yang tersisa:**
  - Item descriptions: "Map" masih duplikat antara ikon dan label nav bar
</details>

### Milestone 2 — Hasil Accessibility Scanner

Pemindaian dilakukan pada build MS2 menggunakan **Accessibility Scanner** (Google). Screenshot dan laporan tersimpan di `docs/M2_accessibility_results_Nimons360/`.

<details>
  <summary>Home Screen</summary>
  <br/>
  <div align="center">

  | Before | After |
  |:---:|:---:|
  | <img src="docs/M2_accessibility_results_Nimons360/home_01.png" height="400"/> | <img src="docs/M2_accessibility_results_Nimons360/home_01_after.png" height="400"/> |

  </div>

  **Saran dari scanner:**
  - Image contrast: `ivFamilyIcon` ratio 2.89 (remote image, di luar kendali app)
  - Item type label: contentDescription card mengandung kata "tap" — diperbaiki: dihapus
  - Text scaling: beberapa avatar TextView dengan ukuran tetap (avatar 24dp fixed)
  - Text contrast: nav bar active text ratio 4.38 (#4A7C59 on #F0F4F1) — diperbaiki: `ColorPrimaryDark` (#2F5C3E, 7.37:1)
  - Item descriptions: "Home" duplikat antara label dan icon nav bar
</details>

<details>
  <summary>Families List</summary>
  <br/>
  <div align="center">

  | Before | After |
  |:---:|:---:|
  | <img src="docs/M2_accessibility_results_Nimons360/families_01.png" height="400"/> | <img src="docs/M2_accessibility_results_Nimons360/families_01_after.png" height="400"/> |

  </div>

  **Saran dari scanner:**
  - Clickable items: `fabAddFamily` dua elemen clickable di posisi sama (FAB internal)
  - Image contrast: `ivFamilyIcon` ratio 2.78 (remote image)
  - Item descriptions: `btnPin` teks "Pin" identik untuk semua family — diperbaiki: unik per nama family
  - Item descriptions: `fabAddFamily` "Create Family" duplikat (teks + contentDescription)
  - Text contrast: nav bar active text ratio 4.38 — diperbaiki: `ColorPrimaryDark` (#2F5C3E, 7.37:1)
  - Item descriptions: "Families" duplikat antara label dan icon nav bar
</details>

<details>
  <summary>Family Detail</summary>
  <br/>
  <div align="center">

  | Before | After |
  |:---:|:---:|
  | <img src="docs/M2_accessibility_results_Nimons360/family_detail_01.png" height="400"/> | <img src="docs/M2_accessibility_results_Nimons360/family_detail_01_after.png" height="400"/> |

  </div>

  **Saran dari scanner:**
  - Image contrast: `ivMemberAvatarBg` ratio 2.31 (avatar background image)
  - Text scaling: `flAvatarContainer` ViewGroup ukuran tetap berisi TextView scalable
</details>

<details>
  <summary>Family Detail — Notifikasi</summary>
  <br/>
  <div align="center">

  | Before | After |
  |:---:|:---:|
  | <img src="docs/M2_accessibility_results_Nimons360/family_detail_notif.png" height="400"/> | <img src="docs/M2_accessibility_results_Nimons360/family_detail_notif_after.png" height="400"/> |

  </div>

  **Saran dari scanner:**
  - Text contrast: tombol aksi ratio 4.41 (#4A7C59 on #F7F2FA, tepat di bawah 4.50)
  - Text contrast: hint text ratio 2.22 (#939196 on #DCD8E0)
  - Unexposed Text: nama family dan jumlah member di header tidak terekspos ke accessibility
</details>

<details>
  <summary>Family Detail — QR Code</summary>
  <br/>
  <div align="center">

  | Before | After |
  |:---:|:---:|
  | <img src="docs/M2_accessibility_results_Nimons360/family_detail_qr.png" height="400"/> | <img src="docs/M2_accessibility_results_Nimons360/family_detail_qr_after.png" height="400"/> |

  </div>

  **Saran dari scanner:**
  - Text contrast: tombol aksi ratio 4.41 (#4A7C59 on #F7F2FA)
  - Unexposed Text: label "FAMILY CODE" tidak terekspos ke layanan aksesibilitas
</details>

<details>
  <summary>Create Family</summary>
  <br/>
  <div align="center">

  | Before | After |
  |:---:|:---:|
  | <img src="docs/M2_accessibility_results_Nimons360/create_family_01.png" height="400"/> | <img src="docs/M2_accessibility_results_Nimons360/create_family_01_after.png" height="400"/> |

  </div>

  **Saran dari scanner:**
  - Image contrast: `ivFamilyIcon` di picker (3 ikon, ratio 2.07-2.97, remote image)
  - Text contrast: hint `etFamilyName` ratio 3.02 — diperbaiki: `textColorHint` → #44403C
</details>

<details>
  <summary>Join Family Dialog</summary>
  <br/>
  <div align="center">

  | Before | After |
  |:---:|:---:|
  | <img src="docs/M2_accessibility_results_Nimons360/join_family_01.png" height="400"/> | <img src="docs/M2_accessibility_results_Nimons360/join_family_01_after.png" height="400"/> |

  </div>

  **Saran dari scanner:**
  - Text contrast: hint `etFamilyCode` ratio 3.44 (#848075 on #EBF1ED) — diperbaiki: `textColorHint` → #44403C
</details>

<details>
  <summary>Leave Family Dialog</summary>
  <br/>
  <div align="center">

  | Before | After |
  |:---:|:---:|
  | <img src="docs/M2_accessibility_results_Nimons360/leave_family_dialog_01.png" height="400"/> | <img src="docs/M2_accessibility_results_Nimons360/leave_family_dialog_01_after.png" height="400"/> |

  </div>

  Tidak ada saran perbaikan. Semua elemen memenuhi WCAG AA.
</details>

<details>
  <summary>Profile</summary>
  <br/>
  <div align="center">

  | Before | After |
  |:---:|:---:|
  | <img src="docs/M2_accessibility_results_Nimons360/profile_01.png" height="400"/> | <img src="docs/M2_accessibility_results_Nimons360/profile_01_after.png" height="400"/> |

  </div>

  **Saran dari scanner:**
  - Touch target: `ToggleRow` tinggi 40dp — diperbaiki: `heightIn(min = 48.dp)`
  - Item type label: foto profil contentDescription mengandung "tap" — diperbaiki: dihapus
</details>

<details>
  <summary>Edit Profile</summary>
  <br/>
  <div align="center">

  | Before | After |
  |:---:|:---:|
  | <img src="docs/M2_accessibility_results_Nimons360/edit_profile_01.png" height="400"/> | <img src="docs/M2_accessibility_results_Nimons360/edit_profile_01_after.png" height="400"/> |

  </div>

  **Saran dari scanner:**
  - Text contrast: 3 elemen teks #4A7C59 on #ECE6F0, ratio 3.97 (elemen di balik modal overlay, tidak interaktif saat sheet terbuka)
</details>

<details>
  <summary>Edit Name</summary>
  <br/>
  <div align="center">

  | Before | After |
  |:---:|:---:|
  | <img src="docs/M2_accessibility_results_Nimons360/edit_name_01.png" height="400"/> | <img src="docs/M2_accessibility_results_Nimons360/edit_name_01_after.png" height="400"/> |

  </div>

  **Saran dari scanner:**
  - Unexposed Text: teks "< Profile" pada nav bar mungkin tidak terekspos (system nav element)
</details>

<details>
  <summary>Analytics</summary>
  <br/>
  <div align="center">

  | Before | After |
  |:---:|:---:|
  | <img src="docs/M2_accessibility_results_Nimons360/analytics_01.png" height="400"/> | <img src="docs/M2_accessibility_results_Nimons360/analytics_01_after.png" height="400"/> |

  </div>

  **Saran dari scanner:**
  - Text contrast: 4 StatCard value text ratio 3.74 (#4A7C59 on card bg) — diperbaiki: warna → `onSurface` (#1C1C1E)
  - Item descriptions: "Analytics" duplikat antara heading dan nav bar label
  - Unexposed Text: tanggal di chart bar tidak terekspos (Canvas draw, sudah ada `contentDescription` chart keseluruhan)
</details>

<details>
  <summary>Customize Pin</summary>
  <br/>
  <div align="center">

  | Before | After |
  |:---:|:---:|
  | <img src="docs/M2_accessibility_results_Nimons360/customize_pin_01.png" height="400"/> | <img src="docs/M2_accessibility_results_Nimons360/customize_pin_01_after.png" height="400"/> |

  </div>

  **Saran dari scanner:**
  - Image contrast: 3 ikon pin ratio 1.04-2.32 (SVG custom pin, di luar kendali langsung)
  - Item descriptions: tombol "Use" identik untuk 5 pin — diperbaiki: semantics unik per pin name
  - Item descriptions: teks "Downloaded" identik untuk 5 pin — diperbaiki: semantics unik per pin name
  - Text contrast: teks "Downloaded" ratio 3.75 (#4A7C59) — diperbaiki: warna → `onSurfaceVariant` (#44403C)
</details>

<details>
  <summary>Map</summary>
  <br/>
  <div align="center">

  | Before | After |
  |:---:|:---:|
  | <img src="docs/M2_accessibility_results_Nimons360/map_02.png" height="400"/> | <img src="docs/M2_accessibility_results_Nimons360/map_02_after.png" height="400"/> |

  </div>

  **Saran dari scanner:**
  - Text contrast: nav bar active text ratio 4.38 — diperbaiki: `ColorPrimaryDark` (#2F5C3E, 7.37:1)
  - Item descriptions: "Map" duplikat antara label dan icon nav bar
  - Unexposed Text: nama jalan pada tile peta (konten tile OpenStreetMap, di luar kendali app)
</details>

<details>
  <summary>Map — Profile Bottom Sheet</summary>
  <br/>
  <div align="center">

  | Before | After |
  |:---:|:---:|
  | <img src="docs/M2_accessibility_results_Nimons360/map_profile_01.png" height="400"/> | <img src="docs/M2_accessibility_results_Nimons360/map_profile_01_after.png" height="400"/> |

  </div>

  **Saran dari scanner:**
  - Item descriptions: Battery/Network/Location duplikat (ikon status bar sistem, di luar kendali app)
  - Unexposed Text: konten tile peta (OpenStreetMap tiles, tidak bisa diekspos)
</details>

<details>
  <summary>Map — Tandai Lokasi</summary>
  <br/>
  <div align="center">

  | Before | After |
  |:---:|:---:|
  | <img src="docs/M2_accessibility_results_Nimons360/map_mark_location_01.png" height="400"/> | <img src="docs/M2_accessibility_results_Nimons360/map_mark_location_01_after.png" height="400"/> |

  </div>

  **Saran dari scanner:**
  - Text contrast: tombol aksi ratio 4.41 (#4A7C59 on #F7F2FA)
  - Unexposed Text: konten tile peta
</details>

<details>
  <summary>Map — Detail Lokasi</summary>
  <br/>
  <div align="center">

  | Before | After |
  |:---:|:---:|
  | <img src="docs/M2_accessibility_results_Nimons360/map_location_detail_01.png" height="400"/> | <img src="docs/M2_accessibility_results_Nimons360/map_location_detail_01_after.png" height="400"/> |

  </div>

  **Saran dari scanner:**
  - Text contrast: tombol aksi ratio 4.41 (#4A7C59 on #F7F2FA)
  - Unexposed Text: konten tile peta dan label "Map"
</details>

<div align="right"><a href="#readme-top">↖ Kembali ke atas</a></div>

---

## Project Structure

<a id="project-structure"></a>

```
app/src/main/
├── java/com/nimons360/app/
│   ├── data/
│   │   ├── api/            (RetrofitClient, ApiService)
│   │   ├── local/          (Room DB, EncryptedSharedPrefs, TokenManager)
│   │   ├── model/          (data classes)
│   │   ├── repository/     (Auth, User, Family, MarkedLocation, ...)
│   │   └── websocket/      (WebSocketManager)
│   ├── services/           (LocationService, NimonsFCMService)
│   ├── ui/
│   │   ├── adapter/        (FamilyListAdapter, ...)
│   │   ├── components/     (QRCodeSheet, NotificationBottomSheet, ...)
│   │   ├── navigation/     (AppNavHost, AppRoute)
│   │   ├── screen/         (HomeScreen, MapScreen, ProfileScreen, ...)
│   │   ├── shell/          (MainShell)
│   │   ├── theme/          (Color, Typography, Theme)
│   │   └── viewmodel/      (MapViewModel, ProfileViewModel, ...)
│   └── MainActivity.kt
├── res/
│   ├── drawable/
│   ├── layout/             (XML layouts)
│   ├── layout-land/        (landscape overrides)
│   ├── values/
│   └── values-night/
openapi.yml
```

<div align="right"><a href="#readme-top">↖ Kembali ke atas</a></div>

---

## Pembagian Tugas

<a id="pembagian-tugas"></a>

**Kelompok K01-TBD**

### Milestone 1

| NIM | Nama | Fitur |
|---|---|---|
| 13523009 | Hazim | Auth (Login & Logout), Profile, Header & Navbar, Network Sensing, OpenAPI, Accessibility Testing (bonus) |
| 13523017 | Orvin | Map & GPS Tracking, WebSocket Engine, Phone Orientation, User Info Map, Internet Status on Map (bonus) |
| 13523034 | Rafizan | Home & List Families, Create & Detail Family, Join & Leave Family, Pinned & Filter (SQLite), Search Family (bonus) |

### Milestone 2

| NIM | Nama | Fitur |
|---|---|---|
| 13523009 | Hazim | Upload Profile Photo, Location Sharing Toggle, OWASP Security, OpenAPI Update, Responsive (Auth & Profile), Accessibility Testing (bonus), Share Story Instagram (bonus) |
| 13523017 | Orvin | Map Extended (long press, CRUD marked location, background location, BroadcastReceiver baterai, recenter), Responsive (Map & Home), Customizable Icon (bonus), Analytics + Export CSV (bonus) |
| 13523034 | Rafizan | Share Family Link, Deep Link Handler, Notifikasi FCM (kirim & terima), Preferensi Notifikasi, Responsive (Families & CreateFamily), Share Family via QR Code (bonus) |

### Jam Persiapan dan Pengerjaan

| Nama | Persiapan (jam) | Pengerjaan (jam) | Total |
|---|:---:|:---:|:---:|
| Hazim | 12 | 75 | 87 |
| Rafizan | 8 | 52 | 60 |
| Orvin | 7 | 55 | 62 |

<div align="right"><a href="#readme-top">↖ Kembali ke atas</a></div>

---

<div align="center">
  <p>
    <strong>IF3210 — Pengembangan Aplikasi Piranti Bergerak</strong><br/>
    Sekolah Teknik Elektro dan Informatika<br/>
    Institut Teknologi Bandung · 2026
  </p>
</div>

<div align="center">
  <img width="100%" src="https://capsule-render.vercel.app/api?type=waving&height=120&color=0:7EAF8D,100:2F5C3E&section=footer" />
</div>
