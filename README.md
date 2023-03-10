---
jupyter:
  colab:
    toc_visible: true
  kernelspec:
    display_name: Python 3
    name: python3
  language_info:
    name: python
  nbformat: 4
  nbformat_minor: 0
---

<div class="cell markdown" id="9xZnRXM7x0Cv">

# CUHK-STAT1013: Practical Assignment Part 1

</div>

<div class="cell markdown" id="9Fy05KAkyJI0">

## Background and basic description of the dataset

**Description**:

Dataset describing the happiness index of different countries around the
world.

**Dataset source**:
<https://github.com/alexarnold630/Happiness_Index_Investigation/blob/main/Happiness/Resources/Horizontal_Merge.csv>

**Sample size**: 173 (Before cleaning); 137 (After cleaning)

**Feature documentation**:

| Feature                             | Dtype before | Dtype after |
|:------------------------------------|:-------------|:------------|
| Country                             | object       | object      |
| Happiness Rank_2015                 | float64      | int64       |
| Happiness Score_2015                |  float64     | float64     |
| Economy (GDP per Capita)\_2015      | float64      | float64     |
| Social Support_2015                 | float64      | float64     |
| Health Life Expectancy_2015         | float64      | float64     |
| Freedom_2015                        | float64      | float64     |
| Generosity_2015                     | float64      | float64     |
| Trust (Government Corruption)\_2015 | float64      | float64     |
| Happiness Rank_2016                 | float64      | int64       |
| Happiness Score_2016                |  float64     | float64     |
| Economy (GDP per Capita)\_2016      | float64      | float64     |
| Social Support_2016                 | float64      | float64     |
| Health Life Expectancy_2016         | float64      | float64     |
| Freedom_2016                        | float64      | float64     |
| Trust (Government Corruption)\_2016 | float64      | float64     |
| Generosity_2016                     | float64      | float64     |
| Happiness Rank_2017                 | float64      | int64       |
| Happiness Score_2017                | float64      | float64     |
| Economy (GDP per Capita)\_2017      |  float64     | float64     |
| Social Support_2017                 | float64      | float64     |
| Health Life Expectancy_2017         | float64      | float64     |
| Freedom_2017                        | float64      | float64     |
| Trust (Government Corruption)\_2017 | float64      | float64     |
| Generosity_2017                     | float64      | float64     |
| Happiness Rank_2018                 | float64      | int64       |
| Happiness Score_2018                | float64      |  float64    |
| Economy (GDP per Capita)\_2018      | float64      | float64     |
| Social Support_2018                 | float64      | float64     |
| Health Life Expectancy_2018         | float64      | float64     |
| Freedom_2018                        | float64      | float64     |
| Generosity_2018                     | float64      | float64     |
| Trust (Government Corruption)\_2018 | float64      | float64     |
| Happiness Rank_2019                 | float64      | int64       |
| Happiness Score_2019                | float64      |  float64    |
| Economy (GDP per Capita)\_2019      | float64      | float64     |
| Social Support_2019                 | float64      | float64     |
| Health Life Expectancy_2019         | float64      | float64     |
| Freedom_2019                        | float64      | float64     |
| Trust (Government Corruption)\_2019 | float64      | float64     |
| Generosity_2019                     | float64      | float64     |
| Happiness Rank_2020                 | float64      | int64       |
| Happiness Score_2020                |  float64     | float64     |
| Economy (GDP per Capita)\_2020      | float64      | float64     |
| Social Support_2020                 | float64      | float64     |
| Health Life Expectancy_2020         | float64      | float64     |
| Freedom_2020                        | float64      | float64     |
| Trust (Government Corruption)\_2020 | float64      | float64     |
| Generosity_2020                     | float64      | float64     |

</div>

<div class="cell markdown" id="k85zO7zxys4H">

## Hypothesis

-   Tell us what your idea is and why you have chosen to pursue this
    idea.
    -   I am interested in the issue of the happiness of people and I
        feel like people in Hong Kong are becoming less happy.
    -   Therefore, I chose to pursue the idea of "whether the happiness
        index in 2015 is higher than that in 2020".
-   What two groups you are comparing:
    -   **G1**: 2015; **G2**: 2020
-   What you will be measuring (i.e., what your response variable will
    be)
    -   `Happiness index`
-   Is your response variable quantitative rather than categorical?
    -   `Happiness index` is a quantitative continuous variable. Its
        data type is float64 and its data can take any values between a
        certain interval.
-   Make a prediction about what kind of difference you expect to see
    between your samples and WHY.
    -   It is expected that **G1** \> **G2** because 2020 is the year
        when COVID-19 pandemic broke out. The happiness index is
        expected to fall when people had to go through sudden changes in
        lives and deal with different difficulties.
-   Talk about how you will gather your data
    -   From GitHub link:
        <https://github.com/alexarnold630/Happiness_Index_Investigation/blob/main/Happiness/Resources/Horizontal_Merge.csv>
-   If you had unlimited resources (time, money, staff, etc.) how would
    you collect your data?
    -   Collect more data by increasing the sample size and collecting
        data from more countries
    -   Investigate if the provided dataset is a good random sampling
        subset of the whole population, e.g. if the data are collected
        randomly over the country or collected in those areas with
        better economic performance only

</div>

<div class="cell markdown" id="3GOdPWT03PQB">

## Prepare your dataset

</div>

<div class="cell code" execution_count="36"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:334}"
id="mUxJb4hxvpHQ" outputId="c092719e-f042-4224-807d-54ea56821f50">

``` python
## load dataset from github

import pandas as pd

df = pd.read_csv("https://raw.githubusercontent.com/alexarnold630/Happiness_Index_Investigation/main/Happiness/Resources/Horizontal_Merge.csv")
df.head(5)
```

<div class="output execute_result" execution_count="36">

           Country  Happiness Rank_2015  Happiness Score_2015  \
    0  Switzerland                  1.0                 7.587   
    1      Iceland                  2.0                 7.561   
    2      Denmark                  3.0                 7.527   
    3       Norway                  4.0                 7.522   
    4       Canada                  5.0                 7.427   

       Economy (GDP per Capita)_2015  Social Support_2015  \
    0                        1.39651              1.34951   
    1                        1.30232              1.40223   
    2                        1.32548              1.36058   
    3                        1.45900              1.33095   
    4                        1.32629              1.32261   

       Health Life Expectancy_2015  Freedom_2015  Generosity_2015  \
    0                      0.94143       0.66557          0.29678   
    1                      0.94784       0.62877          0.43630   
    2                      0.87464       0.64938          0.34139   
    3                      0.88521       0.66973          0.34699   
    4                      0.90563       0.63297          0.45811   

       Trust (Government Corruption)_2015  Happiness Rank_2016  ...  \
    0                             0.41978                  2.0  ...   
    1                             0.14145                  3.0  ...   
    2                             0.48357                  1.0  ...   
    3                             0.36503                  4.0  ...   
    4                             0.32957                  6.0  ...   

       Trust (Government Corruption)_2019  Generosity_2019  Happiness Rank_2020  \
    0                               0.343            0.263                  3.0   
    1                               0.118            0.354                  4.0   
    2                               0.410            0.252                  2.0   
    3                               0.341            0.271                  5.0   
    4                               0.308            0.285                 11.0   

       Happiness Score_2020  Economy (GDP per Capita)_2020  Social Support_2020  \
    0                7.5599                       1.097993             0.942847   
    1                7.5045                       1.077256             0.974670   
    2                7.6456                       1.077400             0.955991   
    3                7.4880                       1.108780             0.952487   
    4                7.2321                       1.069237             0.927177   

       Health Life Expectancy_2020  Freedom_2020  \
    0                     0.741024      0.921337   
    1                     0.730000      0.948892   
    2                     0.724025      0.951444   
    3                     0.732008      0.955750   
    4                     0.736016      0.933913   

       Trust (Government Corruption)_2020  Generosity_2020  
    0                            0.303728         0.105911  
    1                            0.711710         0.246944  
    2                            0.168489         0.066202  
    3                            0.263218         0.134533  
    4                            0.390843         0.124771  

    [5 rows x 49 columns]

</div>

</div>

<div class="cell code" execution_count="37"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:522}"
id="3tNcDDRuNWbI" outputId="b0d0f858-7568-4e34-a9c4-bb7a02b30075">

``` python
## data pre-processing

# dropping the rows with missing values
df.dropna(inplace=True)

# changing the data type of happiness rank to int64
df["Happiness Rank_2015"] = df["Happiness Rank_2015"].astype("int64")
df["Happiness Rank_2016"] = df["Happiness Rank_2016"].astype("int64")
df["Happiness Rank_2017"] = df["Happiness Rank_2017"].astype("int64")
df["Happiness Rank_2018"] = df["Happiness Rank_2018"].astype("int64")
df["Happiness Rank_2019"] = df["Happiness Rank_2019"].astype("int64")
df["Happiness Rank_2020"] = df["Happiness Rank_2020"].astype("int64")
df
```

<div class="output execute_result" execution_count="37">

             Country  Happiness Rank_2015  Happiness Score_2015  \
    0    Switzerland                    1                 7.587   
    1        Iceland                    2                 7.561   
    2        Denmark                    3                 7.527   
    3         Norway                    4                 7.522   
    4         Canada                    5                 7.427   
    ..           ...                  ...                   ...   
    152  Afghanistan                  153                 3.575   
    153       Rwanda                  154                 3.465   
    154        Benin                  155                 3.340   
    156      Burundi                  157                 2.905   
    157         Togo                  158                 2.839   

         Economy (GDP per Capita)_2015  Social Support_2015  \
    0                          1.39651              1.34951   
    1                          1.30232              1.40223   
    2                          1.32548              1.36058   
    3                          1.45900              1.33095   
    4                          1.32629              1.32261   
    ..                             ...                  ...   
    152                        0.31982              0.30285   
    153                        0.22208              0.77370   
    154                        0.28665              0.35386   
    156                        0.01530              0.41587   
    157                        0.20868              0.13995   

         Health Life Expectancy_2015  Freedom_2015  Generosity_2015  \
    0                        0.94143       0.66557          0.29678   
    1                        0.94784       0.62877          0.43630   
    2                        0.87464       0.64938          0.34139   
    3                        0.88521       0.66973          0.34699   
    4                        0.90563       0.63297          0.45811   
    ..                           ...           ...              ...   
    152                      0.30335       0.23414          0.36510   
    153                      0.42864       0.59201          0.22628   
    154                      0.31910       0.48450          0.18260   
    156                      0.22396       0.11850          0.19727   
    157                      0.28443       0.36453          0.16681   

         Trust (Government Corruption)_2015  Happiness Rank_2016  ...  \
    0                               0.41978                    2  ...   
    1                               0.14145                    3  ...   
    2                               0.48357                    1  ...   
    3                               0.36503                    4  ...   
    4                               0.32957                    6  ...   
    ..                                  ...                  ...  ...   
    152                             0.09719                  154  ...   
    153                             0.55191                  152  ...   
    154                             0.08010                  153  ...   
    156                             0.10062                  157  ...   
    157                             0.10731                  155  ...   

         Trust (Government Corruption)_2019  Generosity_2019  Happiness Rank_2020  \
    0                                 0.343            0.263                    3   
    1                                 0.118            0.354                    4   
    2                                 0.410            0.252                    2   
    3                                 0.341            0.271                    5   
    4                                 0.308            0.285                   11   
    ..                                  ...              ...                  ...   
    152                               0.025            0.158                  153   
    153                               0.411            0.217                  150   
    154                               0.082            0.175                   86   
    156                               0.180            0.176                  140   
    157                               0.085            0.177                  135   

         Happiness Score_2020  Economy (GDP per Capita)_2020  Social Support_2020  \
    0                  7.5599                       1.097993             0.942847   
    1                  7.5045                       1.077256             0.974670   
    2                  7.6456                       1.077400             0.955991   
    3                  7.4880                       1.108780             0.952487   
    4                  7.2321                       1.069237             0.927177   
    ..                    ...                            ...                  ...   
    152                2.5669                       0.746286             0.470367   
    153                3.3123                       0.760010             0.540835   
    154                5.2160                       0.767432             0.468671   
    156                3.7753                       0.649264             0.490326   
    157                4.1872                       0.735771             0.551313   

         Health Life Expectancy_2020  Freedom_2020  \
    0                       0.741024      0.921337   
    1                       0.730000      0.948892   
    2                       0.724025      0.951444   
    3                       0.732008      0.955750   
    4                       0.736016      0.933913   
    ..                           ...           ...   
    152                     0.525900      0.396573   
    153                     0.610988      0.900589   
    154                     0.543125      0.735183   
    156                     0.534000      0.626350   
    157                     0.547199      0.649829   

         Trust (Government Corruption)_2020  Generosity_2020  
    0                              0.303728         0.105911  
    1                              0.711710         0.246944  
    2                              0.168489         0.066202  
    3                              0.263218         0.134533  
    4                              0.390843         0.124771  
    ..                                  ...              ...  
    152                            0.933687        -0.096429  
    153                            0.183541         0.055484  
    154                            0.740533        -0.003537  
    156                            0.606935        -0.017552  
    157                            0.757733         0.002668  

    [137 rows x 49 columns]

</div>

</div>

<div class="cell code" execution_count="38"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="eYUhQkW5O_gE" outputId="76af5e43-e17b-40fd-90b8-9082802966ab">

``` python
df.info()
```

<div class="output stream stdout">

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 137 entries, 0 to 157
    Data columns (total 49 columns):
     #   Column                              Non-Null Count  Dtype  
    ---  ------                              --------------  -----  
     0   Country                             137 non-null    object 
     1   Happiness Rank_2015                 137 non-null    int64  
     2   Happiness Score_2015                137 non-null    float64
     3   Economy (GDP per Capita)_2015       137 non-null    float64
     4   Social Support_2015                 137 non-null    float64
     5   Health Life Expectancy_2015         137 non-null    float64
     6   Freedom_2015                        137 non-null    float64
     7   Generosity_2015                     137 non-null    float64
     8   Trust (Government Corruption)_2015  137 non-null    float64
     9   Happiness Rank_2016                 137 non-null    int64  
     10  Happiness Score_2016                137 non-null    float64
     11  Economy (GDP per Capita)_2016       137 non-null    float64
     12  Social Support_2016                 137 non-null    float64
     13  Health Life Expectancy_2016         137 non-null    float64
     14  Freedom_2016                        137 non-null    float64
     15  Trust (Government Corruption)_2016  137 non-null    float64
     16  Generosity_2016                     137 non-null    float64
     17  Happiness Rank_2017                 137 non-null    int64  
     18  Happiness Score_2017                137 non-null    float64
     19  Economy (GDP per Capita)_2017       137 non-null    float64
     20  Social Support_2017                 137 non-null    float64
     21  Health Life Expectancy_2017         137 non-null    float64
     22  Freedom_2017                        137 non-null    float64
     23  Trust (Government Corruption)_2017  137 non-null    float64
     24  Generosity_2017                     137 non-null    float64
     25  Happiness Rank_2018                 137 non-null    int64  
     26  Happiness Score_2018                137 non-null    float64
     27  Economy (GDP per Capita)_2018       137 non-null    float64
     28  Social Support_2018                 137 non-null    float64
     29  Health Life Expectancy_2018         137 non-null    float64
     30  Freedom_2018                        137 non-null    float64
     31  Generosity_2018                     137 non-null    float64
     32  Trust (Government Corruption)_2018  137 non-null    float64
     33  Happiness Rank_2019                 137 non-null    int64  
     34  Happiness Score_2019                137 non-null    float64
     35  Economy (GDP per Capita)_2019       137 non-null    float64
     36  Social Support_2019                 137 non-null    float64
     37  Health Life Expectancy_2019         137 non-null    float64
     38  Freedom_2019                        137 non-null    float64
     39  Trust (Government Corruption)_2019  137 non-null    float64
     40  Generosity_2019                     137 non-null    float64
     41  Happiness Rank_2020                 137 non-null    int64  
     42  Happiness Score_2020                137 non-null    float64
     43  Economy (GDP per Capita)_2020       137 non-null    float64
     44  Social Support_2020                 137 non-null    float64
     45  Health Life Expectancy_2020         137 non-null    float64
     46  Freedom_2020                        137 non-null    float64
     47  Trust (Government Corruption)_2020  137 non-null    float64
     48  Generosity_2020                     137 non-null    float64
    dtypes: float64(42), int64(6), object(1)
    memory usage: 53.5+ KB

</div>

</div>

<div class="cell markdown" id="55xAIxVa3hpQ">

-   Tell us what groups you want to compare in the dataset
    -   **G1** (Happiness Score_2015) vs. **G2** (Happiness Score_2020)

</div>

<div class="cell markdown" id="13PdL3ht3902">

-   Print first 5 records of each group, respectively.

</div>

<div class="cell code" execution_count="39"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="UNL0WXav3hLj" outputId="66cc8a14-9ead-411c-88e0-890217f6e24a">

``` python
## first 5 records of G1 (Happiness Score_2015)
(df["Happiness Score_2015"]).head(5)
```

<div class="output execute_result" execution_count="39">

    0    7.587
    1    7.561
    2    7.527
    3    7.522
    4    7.427
    Name: Happiness Score_2015, dtype: float64

</div>

</div>

<div class="cell code" execution_count="40"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="dhe52HVB4T1O" outputId="4c6cbe45-159d-4046-cb16-ce1ed208f327">

``` python
## first 5 records of G2 (Happiness Score_2020)
(df["Happiness Score_2020"]).head(5)
```

<div class="output execute_result" execution_count="40">

    0    7.5599
    1    7.5045
    2    7.6456
    3    7.4880
    4    7.2321
    Name: Happiness Score_2020, dtype: float64

</div>

</div>

<div class="cell code" execution_count="41" id="zEgfWXaKGvNC">

``` python
## Any other data description and visualization you want to add.

import seaborn as sns
import matplotlib.pyplot as plt
```

</div>

<div class="cell code" execution_count="42"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:544}"
id="0zSXHtTfnfxU" outputId="746a5394-8500-4d5a-d67a-8fc44367c8c5">

``` python
# histogram
sns.histplot(data=df, x="Happiness Score_2015", bins='auto')
plt.show()
sns.histplot(data=df, x="Happiness Score_2020", bins='auto')
plt.show()
```

<div class="output display_data">

![](71f79fdf8805113fd7f46ce14836fe521ba186f4.png)

</div>

<div class="output display_data">

![](5b863cb4b528f4380219e1b0fcba5b1d9d953ddc.png)

</div>

</div>

<div class="cell code" execution_count="43"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:543}"
id="hTiXKFbLnpEn" outputId="03777b9d-514d-4026-81a5-ec6abc3f0072">

``` python
# violinplot
sns.violinplot(data=df, x="Happiness Score_2015")
plt.show()
sns.violinplot(data=df, x="Happiness Score_2020")
plt.show()
```

<div class="output display_data">

![](a70ca1f42dcc1a8ea44c02d8e0bc9d8b1a468011.png)

</div>

<div class="output display_data">

![](b0392062e0741b97f4dd35bdc18fd9fbabb62f6d.png)

</div>

</div>
