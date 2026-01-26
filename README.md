# Portfolio

This repository contains various past projects, including Data Analyst (SQL, Python), Data Visualization, and IoT SMART Manufacturing

# [Project 1: E-Commerce Sales Analysis using MySQL]

## Table of Contents

- [Project Overview](#project-overview)
- [Recommendations](#recommendations)
- [Data Sources](#data-sources)

### Project Overview

![Dashboard Data Analyst Page 1](https://github.com/user-attachments/assets/3aa8b2c1-2a65-42ea-babb-08772cf1821c)

This data analysis project utilized MySQL to evaluate data on e-commerce transactions from 2021 to 2022. The goal is to provide recommendations on marketing budget and business insights.

### Data Sources

- Order data: The primary dataset used for this analysis is the "order_detail.csv" file, containing detailed sales information.
- Payment data: The sub-dataset used for this analysis is the "payment_detail.csv" file, containing information about payment methods used in transactions.
- Customer data: The sub-dataset used for this analysis is the "customer_detail.csv" file, containing customer IDs and customer registration dates.
- SKU (Stock-Keeping Unit): The sub-dataset used for this analysis is the "sku_detail.csv" file, containing detailed product prices and cost details.

### Tools

- Excel - Data Cleaning
  [Order_detail](https://github.com/user-attachments/files/24330793/Order_detail.csv)
  [Payment_detail](https://github.com/user-attachments/files/24345167/Payment_detail.csv)
  [Customer_detail](https://github.com/user-attachments/files/24335458/Customer_detail.csv)
  [Sku_detail](https://github.com/user-attachments/files/24345175/Sku_detail.csv)
- MySQL - Data Analysis
- Looker - Creating reports

### Data Cleaning/Preparation

In the initial data preparation phase, we performed the following tasks:
1. Data loading and inspection.
2. Handling missing values.
3. Data cleaning and formatting.
4. Making CTE for combining 4 datasets.

### Exploratory Data Analysis

EDA involved exploring the sales data to answer key questions, such as:

- Which month had the highest transaction volume in 2021?
- Which category had the highest transaction volume in 2022?
- How do transaction volumes by category compare between 2021 and 2022?
- What are the five most widely used payment methods?
- What is the ranking of categories based on transaction value?

### Data Analysis

Include some interesting code/features worked with

```sql
--table name with case_1, case_2, case_3, etc

SELECT * FROM case_1;
```

### Results/Findings


![Quantity and Customer by Category](https://github.com/user-attachments/assets/2dfe357a-7917-4dba-ba7c-93d151065dfe)
![Total Transactions by Payment Method](https://github.com/user-attachments/assets/2a73c511-5ccf-4aae-ae0c-b3196c151b7d)


The analysis results are summarized as follows:
1. Overall, transaction trends have steadily increased from mid-year to the end of the year, with a noticeable surge starting in July 2021.
2. In August 2021, total transactions reached Rp 227,862,744.00, marking the peak of sales for that year.
3. The Mobiles & Tablets category ranked first as the category with the highest total transaction value in 2022, amounting to Rp 918,451,576.00.
4. The Others category declined by 46.27%, while the Books category decreased by 32.91%.
5. Cash on Delivery ranked as the most popular payment method.

### Recommendations

Based on the analysis, we recommend the following actions:
1. Optimize targeted marketing (ads) toward young professionals and students who require devices.
2. Plan inventory and SKUs based on sales trends by model and capacity to ensure product availability during peak demand.
3. Evaluate the performance and market trends of physical books.
4. Improve the user experience (UX) of e-wallet applications.

### Limitations

In the SKU_detail table, several iPhone, MacBook, and Mac Mini products in the sku_name column do not include the brand name “Apple,” which should be considered during data processing.
   


# [Project 2: E-Commerce data insights analysis using Python] (in Bahasa Indonesia)

### Project Overview

Project ini merupakan project data analyst dengan bahasa python menggunakan aplikasi Google Colab untuk mengevaluasi data dari bisnis e-commerce.

### Data Sources

#Dataset

Data yang digunakan adalah data yang berasal dari Tokopedia (***bukan data sesungguhnya***). Mengenai penjelasan dataset adalah sebagai berikut:

|variable                       |class     |description |
|:------------------------------|:---------|:-----------|
**order_detail:**
id 			|object| angka unik dari order / id_order
customer_id 		|object|angka unik dari pelanggan
order_date 		|object| tanggal saat dilakukan transaksi
sku_id 			|object| angka unik dari produk (sku adalah stock keeping unit)
price			|int64| harga yang tertera pada tagging harga
qty_ordered 		|int64| jumlah barang yang dibeli oleh pelanggan
before_discount	|float64| nilai harga total dari produk (price * qty_ordered)
discount_amount	|float64| nilai diskon product total
after_discount		|float64| nilai harga total produk ketika sudah dikurangi dengan diskon
is_gross 		|int64| menunjukkan pelanggan belum membayar pesanan
is_valid		|int64| menunjukkan pelanggan sudah melakukan pembayaran
is_net			|int64| menunjukkan transaksi sudah selesai
payment_id 		|int64| angka unik dari metode pembayaran
||
**sku_detail:**
id |object| angka unik dari produk (dapat digunakan untuk key saat join)
sku_name 		|object| nama dari produk
base_price		|float64| harga barang yang tertera pada tagging harga / price
cogs 			|int64| cost of goods sold / total biaya untuk menjual 1 produk
category		|object| kategori produk
||
**customer_detail:**
id 			|object| angka unik dari pelanggan
registered_date	|object| tanggal pelanggan mulai mendaftarkan diri sebagai anggota
||
**payment_detail:**
id			|int64| angka unik dari metode pembayaran
payment_method	|object| metode pembayaran yang digunakan

### Data Cleaning/Preparation

Berikut langkah-langkah yang dilakukan untuk Data Cleaning/Data Preparation pada data tersebut:
1. Memanggil fungsi library
```sql

import pandas as pd -- untuk Memanipulasi Data
import numpy as np -- untuk Operasi Numerik
import matplotlib.pyplot as plt -- untuk membuat visualisasi dasar
import seaborn as sns -- untuk membuat visualisasi statistik, memudahkan data analysis
from pandas.tseries.offsets import BDay -- untuk operasi tanggal berbasis hari kerja, mengabaikan weekend

```

2. Menjalankan fungsi sql di colab
```sql

from sqlite3 import connect
conn = connect(':memory:')
df_od.to_sql('order_detail',conn, index=False, if_exists='replace')
df_pd.to_sql('payment_detail', conn, index=False, if_exists='replace')
df_sd.to_sql('sku_detail', conn, index=False, if_exists='replace')
df_cd.to_sql('customer_detail', conn, index=False, if_exists='replace')

```

3. Menggabungkan data menjadi satu tabel
```sql

df = pd.read_sql("""
SELECT
    order_detail.*,
    payment_detail.payment_method,
    sku_detail.sku_name,
    sku_detail.base_price,
    sku_detail.cogs,
    sku_detail.category,
    customer_detail.registered_date
FROM order_detail
LEFT JOIN payment_detail
    on payment_detail.id = order_detail.payment_id
LEFT JOIN sku_detail
    on sku_detail.id = order_detail.sku_id
LEFT JOIN customer_detail
    on customer_detail.id = order_detail.customer_id
""", conn)

```

4. Mengubah tipe data agar mudah dilakukan pengolahan data
```sql

df = df.astype({"before_discount":'int', "discount_amount":'int', "after_discount":'int',"base_price":'int'})
df.dtypes

```

5. Mengubah tipe kolom Date menjadi datetime
```sql

df['order_date']= pd.to_datetime(df['order_date'])
df['registered_date']= pd.to_datetime(df['registered_date'])
df.dtypes

```

### Exploratory Data Analysis

1. Menentukan pemenang kompetisi Festival Akhir Tahun yang akan diambil dari TOP 5 produk kategori mobile & tablets selama tahun 2022 dengan jumlah kuantitas penjualan paling tinggi (Tim Marketing)
2. Menyediakan data TOP 20 nama produk yang mengalami penuruna paling tinggi pada 2022 jika dibandingkan dengan 2021 (Tim Warehouse)
3. Menyediakan data ID customer dan Registered date pelanggan yang sudah check out namun belum melakukan pembayaran untuk diberikan informasi promo (Tim Digital Marketing) 
4. Menampilkan data rata-rata harian penjualan weekends(sabtu-minggu) vs rata-rata harian penjualan weekdays(senin-jum'at) pada bulan Oktober-Desember 2022. Apakah ada peningkatan penjualan pada masing-masing bulan tersebut (Tim Campaign)

### Results/Findings

1. Berikut hasil penjuala tertinggi TOP 5 pada kategori mobile & tablets

``` sql
 
  
    

    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }


  
    
      
      sku_name
      qty_ordered
    
  
  
    
      1
      IDROID_BALRX7-Gold
      1000
    
    
      2
      IDROID_BALRX7-Jet black
      31
    
    
      3
      Infinix Hot 4-Gold
      15
    
    
      4
      samsung_Grand Prime Plus-Black
      11
    
    
      5
      infinix_Zero 4-Grey
      10
    
  


    

  
    

  
    
  
    

  
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  

    
      const buttonEl =
        document.querySelector('#df-fc604df1-62b8-4bb5-afd7-c526d72c4a26 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-fc604df1-62b8-4bb5-afd7-c526d72c4a26');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    
  


    
      


    
        
    

      


  .colab-df-quickchart {
      --bg-color: #E8F0FE;
      --fill-color: #1967D2;
      --hover-bg-color: #E2EBFA;
      --hover-fill-color: #174EA6;
      --disabled-fill-color: #AAA;
      --disabled-bg-color: #DDD;
  }

  [theme=dark] .colab-df-quickchart {
      --bg-color: #3B4455;
      --fill-color: #D2E3FC;
      --hover-bg-color: #434B5C;
      --hover-fill-color: #FFFFFF;
      --disabled-bg-color: #3B4455;
      --disabled-fill-color: #666;
  }

  .colab-df-quickchart {
    background-color: var(--bg-color);
    border: none;
    border-radius: 50%;
    cursor: pointer;
    display: none;
    fill: var(--fill-color);
    height: 32px;
    padding: 0;
    width: 32px;
  }

  .colab-df-quickchart:hover {
    background-color: var(--hover-bg-color);
    box-shadow: 0 1px 2px rgba(60, 64, 67, 0.3), 0 1px 3px 1px rgba(60, 64, 67, 0.15);
    fill: var(--button-hover-fill-color);
  }

  .colab-df-quickchart-complete:disabled,
  .colab-df-quickchart-complete:disabled:hover {
    background-color: var(--disabled-bg-color);
    fill: var(--disabled-fill-color);
    box-shadow: none;
  }

  .colab-df-spinner {
    border: 2px solid var(--fill-color);
    border-color: transparent;
    border-bottom-color: var(--fill-color);
    animation:
      spin 1s steps(1) infinite;
  }

  @keyframes spin {
    0% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
      border-left-color: var(--fill-color);
    }
    20% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    30% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
      border-right-color: var(--fill-color);
    }
    40% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    60% {
      border-color: transparent;
      border-right-color: var(--fill-color);
    }
    80% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-bottom-color: var(--fill-color);
    }
    90% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
    }
  }


      
        async function quickchart(key) {
          const quickchartButtonEl =
            document.querySelector('#' + key + ' button');
          quickchartButtonEl.disabled = true;  // To prevent multiple clicks.
          quickchartButtonEl.classList.add('colab-df-spinner');
          try {
            const charts = await google.colab.kernel.invokeFunction(
                'suggestCharts', [key], {});
          } catch (error) {
            console.error('Error during call to suggestCharts:', error);
          }
          quickchartButtonEl.classList.remove('colab-df-spinner');
          quickchartButtonEl.classList.add('colab-df-quickchart-complete');
        }
        (() => {
          let quickchartButtonEl =
            document.querySelector('#df-831c569e-41ac-4391-9938-f4c5edb0983b button');
          quickchartButtonEl.style.display =
            google.colab.kernel.accessAllowed ? 'block' : 'none';
        })();
      
    

  
    
      .colab-df-generate {
        background-color: #E8F0FE;
        border: none;
        border-radius: 50%;
        cursor: pointer;
        display: none;
        fill: #1967D2;
        height: 32px;
        padding: 0 0 0 0;
        width: 32px;
      }

      .colab-df-generate:hover {
        background-color: #E2EBFA;
        box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
        fill: #174EA6;
      }

      [theme=dark] .colab-df-generate {
        background-color: #3B4455;
        fill: #D2E3FC;
      }

      [theme=dark] .colab-df-generate:hover {
        background-color: #434B5C;
        box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
        filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
        fill: #FFFFFF;
      }
    
    

  
    
  
    
    
      (() => {
      const buttonEl =
        document.querySelector('#id_8629a2b7-668c-49a8-bc20-44803222ff52 button.colab-df-generate');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      buttonEl.onclick = () => {
        google.colab.notebook.generateWithVariable('top_5');
      }
      })();
    
  ```

    
  

