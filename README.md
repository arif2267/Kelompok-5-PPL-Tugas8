# 🛍️ Sistem Manajemen Produk Django

Sistem manajemen produk sederhana yang dibangun dengan Django, dilengkapi dengan fitur CRUD (Create, Read, Update, Delete) dan interface yang modern.

## ✨ Fitur

- ✅ Tambah produk baru
- ✅ Lihat daftar produk (Table & Grid view)
- ✅ Edit produk
- ✅ Hapus produk
- ✅ Pencarian produk
- ✅ Pesan notifikasi sukses
- ✅ Interface responsif dan modern
- ✅ Validasi form
- ✅ Admin panel terintegrasi

## 📋 Prerequisites

Pastikan Anda telah menginstall:

- Python 3.8+ ([Download Python](https://python.org/downloads/))
- pip (Python package manager)
- Git (opsional, untuk clone repository)

### Cek instalasi Python:
```bash
python --version
# atau
python3 --version
```

### Cek instalasi pip:
```bash
pip --version
# atau
pip3 --version
```

## 🚀 Instalasi

### 1. Clone atau Download Project

**Opsi A: Clone dengan Git**
```bash
git clone https://github.com/username/product-management-django.git
cd product-management-django
```

**Opsi B: Download ZIP**
1. Download file ZIP project
2. Extract ke folder yang diinginkan
3. Buka terminal/command prompt di folder tersebut

### 2. Buat Virtual Environment (Disarankan)

**Windows:**
```bash
python -m venv venv
venv\Scripts\activate
```

**macOS/Linux:**
```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install django
```

**Atau jika ada file requirements.txt:**
```bash
pip install -r requirements.txt
```

### 4. Buat Project Django

```bash
# Buat project baru
django-admin startproject product_management .

# Buat aplikasi products
python manage.py startapp products
```

### 5. Konfigurasi Settings

Edit file `product_management/settings.py` dan tambahkan `'products'` ke `INSTALLED_APPS`:

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'products',  # Tambahkan ini
]
```

### 6. Setup Database

```bash
# Buat migrasi untuk model bawaan Django
python manage.py makemigrations

# Jalankan migrasi
python manage.py migrate
```

### 7. Buat Superuser (Opsional)

```bash
python manage.py createsuperuser
```

Ikuti instruksi untuk membuat username, email, dan password admin.

### 8. Jalankan Development Server

```bash
python manage.py runserver
```

Server akan berjalan di: `http://127.0.0.1:8000/`

## 📁 Struktur Project

```
product_management/
├── product_management/
│   ├── __init__.py
│   ├── asgi.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── products/
│   ├── migrations/
│   ├── static/
│   │   └── products/
│   │       ├── css/
│   │       │   └── style.css
│   │       └── js/
│   │           └── main.js
│   ├── templates/
│   │   └── products/
│   │       ├── base.html
│   │       ├── product_list.html
│   │       ├── add_product.html
│   │       ├── update_product.html
│   │       └── delete_product.html
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── forms.py
│   ├── models.py
│   ├── tests.py
│   ├── urls.py
│   └── views.py
├── db.sqlite3
├── manage.py
└── README.md
```

## 🔧 Konfigurasi File

### 1. Models (`products/models.py`)

```python
from django.db import models

class Product(models.Model):
    name = models.CharField(max_length=200)
    description = models.TextField()
    price = models.DecimalField(max_digits=10, decimal_places=2)
    stock = models.IntegerField()
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    def __str__(self):
        return self.name

    class Meta:
        ordering = ['-created_at']
```

### 2. Forms (`products/forms.py`)

```python
from django import forms
from .models import Product

class ProductForm(forms.ModelForm):
    class Meta:
        model = Product
        fields = ['name', 'description', 'price', 'stock']
        widgets = {
            'name': forms.TextInput(attrs={
                'class': 'form-control',
                'placeholder': 'Masukkan nama produk'
            }),
            'description': forms.Textarea(attrs={
                'class': 'form-control',
                'rows': 3,
                'placeholder': 'Deskripsi produk'
            }),
            'price': forms.NumberInput(attrs={
                'class': 'form-control',
                'placeholder': '0'
            }),
            'stock': forms.NumberInput(attrs={
                'class': 'form-control',
                'placeholder': '0'
            }),
        }
```

### 3. URLs (`products/urls.py`)

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.product_list, name='product_list'),
    path('add/', views.add_product, name='add_product'),
    path('update/<int:pk>/', views.update_product, name='update_product'),
    path('delete/<int:pk>/', views.delete_product, name='delete_product'),
]
```

### 4. Main URLs (`product_management/urls.py`)

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('products.urls')),
]
```

## 🏃‍♂️ Cara Menjalankan

### 1. Aktivasi Virtual Environment

**Windows:**
```bash
venv\Scripts\activate
```

**macOS/Linux:**
```bash
source venv/bin/activate
```

### 2. Jalankan Server

```bash
python manage.py runserver
```

### 3. Akses Aplikasi

- **Frontend:** `http://127.0.0.1:8000/`
- **Admin Panel:** `http://127.0.0.1:8000/admin/`

## 🛠️ Development

### Menambah Migrasi Setelah Perubahan Model

```bash
python manage.py makemigrations products
python manage.py migrate
```

### Mengumpulkan Static Files (untuk Production)

```bash
python manage.py collectstatic
```

### Menjalankan Tests

```bash
python manage.py test
```

## 📱 Fitur Interface

### Halaman Utama
- Daftar semua produk dalam format tabel
- Tombol tambah produk baru
- Pencarian produk
- Toggle antara Table dan Grid view

### Form Tambah/Edit
- Form yang user-friendly dengan validasi
- Field: Nama, Deskripsi, Harga, Stok
- Pesan error jika ada kesalahan input

### Konfirmasi Hapus
- Modal konfirmasi sebelum menghapus
- Peringatan bahwa aksi tidak dapat dibatalkan

## 🎨 Kustomisasi

### Mengubah Tema Warna

Edit file `products/static/products/css/style.css`:

```css
:root {
    --primary-color: #your-color;
    --secondary-color: #your-color;
    /* Ubah variabel CSS sesuai keinginan */
}
```

### Menambah Field Baru

1. Tambah field di `models.py`
2. Tambah field di `forms.py`
3. Update template
4. Buat dan jalankan migrasi

## 🚨 Troubleshooting

### Error: ModuleNotFoundError

```bash
# Pastikan virtual environment aktif
pip install django
```

### Error: No module named 'products'

```bash
# Pastikan 'products' sudah ditambahkan di INSTALLED_APPS
# di file settings.py
```

### Error: Table doesn't exist

```bash
python manage.py makemigrations
python manage.py migrate
```

### Port sudah digunakan

```bash
# Gunakan port lain
python manage.py runserver 8001
```

## 📞 Support

Jika mengalami masalah:

1. Pastikan semua dependencies terinstall
2. Check log error di terminal
3. Pastikan virtual environment aktif
4. Restart development server

## 📝 TODO / Enhancement

- [ ] Upload gambar produk
- [ ] Kategori produk
- [ ] Export data ke Excel/PDF
- [ ] API REST untuk mobile app
- [ ] Sistem user management
- [ ] Dashboard analytics
- [ ] Notifikasi stok habis

## 🤝 Contributing

1. Fork project
2. Buat branch fitur (`git checkout -b feature/AmazingFeature`)
3. Commit perubahan (`git commit -m 'Add some AmazingFeature'`)
4. Push ke branch (`git push origin feature/AmazingFeature`)
5. Buat Pull Request