# Proyek Analisis Data: E-Commerce Public Dataset
- **Nama:** Muhammad Zikri Pasa
- **Email:** abangzikri45@gmail.com
- **ID Dicoding:** zikripasa

## Menentukan Pertanyaan Bisnis

- Pertanyaan 1 : Apa metode pembayaran yang paling sering digunakan?
- Pertanyaan 2 : Apakah keterlambatan pengiriman berpengaruh terhadap review pelanggan?

## Import Semua Packages/Library yang Digunakan

import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

## Data Wrangling

### Gathering Data

orders = pd.read_csv('/content/orders_dataset.csv')
payments = pd.read_csv('/content/order_payments_dataset.csv')
reviews = pd.read_csv('/content/order_reviews_dataset.csv')
products = pd.read_csv('/content/products_dataset.csv')
sellers = pd.read_csv('/content/sellers_dataset.csv')
customers = pd.read_csv('/content/customers_dataset.csv')
geolocation = pd.read_csv('/content/geolocation_dataset.csv')
order_items = pd.read_csv('/content/order_items_dataset.csv')
product_category_translation = pd.read_csv('/content/product_category_name_translation.csv')

**Insight:**
- xxx
- xxx

### Assessing Data

def check_data(df, name):
    print(f'\nDataset: {name}')
    print(df.info())
    print(df.head())
    print(f'Jumlah missing values:\n{df.isnull().sum()}')
    print('-'*50)

check_data(orders, 'Orders')
check_data(payments, 'Payments')
check_data(reviews, 'Reviews')


**Insight:**
- xxx
- xxx

### Cleaning Data

orders['order_purchase_timestamp'] = pd.to_datetime(orders['order_purchase_timestamp'])
orders['order_delivered_customer_date'] = pd.to_datetime(orders['order_delivered_customer_date'])
orders.dropna(subset=['order_delivered_customer_date'], inplace=True)

**Insight:**
- xxx
- xxx

## Exploratory Data Analysis (EDA)

### Explore ...



def check_data(df, name):
    print(f'\nDataset: {name}')
    
   
    print("\n--- Deskripsi Kolom Numerik ---")
    print(df.describe()) 
    
    print("\n--- Deskripsi Kolom Kategori ---")
    print(df.describe(include=['object']))  
    
    # Histogram untuk kolom numerik
    numeric_cols = df.select_dtypes(include=['number']).columns
    if len(numeric_cols) > 0:
        df[numeric_cols].hist(figsize=(10, 5), bins=20)
        plt.suptitle(f'Histogram {name}')
        plt.show()
    
    # Korelasi untuk kolom numerik
    if len(numeric_cols) > 1:
        print("\n--- Korelasi Antar Kolom Numerik ---")
        plt.figure(figsize=(8, 5))
        sns.heatmap(df[numeric_cols].corr(), annot=True, cmap="coolwarm", fmt=".2f")
        plt.title(f'Heatmap Korelasi {name}')
        plt.show()


check_data(orders, 'Orders')
check_data(payments, 'Payments')
check_data(reviews, 'Reviews')


**Insight:**
- xxx
- xxx



## Visualization & Explanatory Analysis

### Pertanyaan 1: Apa metode pembayaran yang paling sering digunakan?

payment_counts = payments['payment_type'].value_counts()
sns.barplot(x=payment_counts.index, y=payment_counts.values)
plt.title('Distribusi Metode Pembayaran')
plt.xlabel('Metode Pembayaran')
plt.ylabel('Jumlah Transaksi')
plt.show()

### Pertanyaan 2: Apakah keterlambatan pengiriman berpengaruh terhadap review pelanggan?

# Konversi kolom tanggal ke format datetime
orders['order_delivered_customer_date'] = pd.to_datetime(orders['order_delivered_customer_date'], errors='coerce')
orders['order_estimated_delivery_date'] = pd.to_datetime(orders['order_estimated_delivery_date'], errors='coerce')

# Hitung keterlambatan pengiriman
orders['delivery_delay'] = (orders['order_delivered_customer_date'] - orders['order_estimated_delivery_date']).dt.days

merged_data = orders.merge(reviews, on='order_id')

# Visualisasi keterlambatan pengiriman vs skor review
sns.scatterplot(x=merged_data['delivery_delay'], y=merged_data['review_score'])
plt.title('Pengaruh Keterlambatan Pengiriman terhadap Skor Review')
plt.xlabel('Keterlambatan Pengiriman (Hari)')
plt.ylabel('Skor Review')
plt.show()


**Insight:**
- xxx
- xxx

## Analisis Lanjutan (Opsional)



## Conclusion

- Conclution pertanyaan 1
- Conclution pertanyaan 2

print('Kesimpulan:')
print('1. Metode pembayaran yang paling sering digunakan adalah:', payment_counts.idxmax())
print('2. Terdapat indikasi bahwa keterlambatan pengiriman berpengaruh terhadap skor review pelanggan.')

 pip freeze requirements.txt


