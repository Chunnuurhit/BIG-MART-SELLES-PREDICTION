{
 "cells": [
  {
   "cell_type": "code",
   "execution_count": 1,
   "metadata": {},
   "outputs": [],
   "source": [
    "import pandas as pd\n",
    "import numpy as np\n",
    "import seaborn as sns\n",
    "import matplotlib.pyplot as plt\n",
    "import warnings"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "metadata": {},
   "outputs": [],
   "source": [
    "warnings.filterwarnings('ignore')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "metadata": {},
   "outputs": [],
   "source": [
    "data = pd.read_csv('big_mart_Train.csv')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Item_Identifier</th>\n",
       "      <th>Item_Weight</th>\n",
       "      <th>Item_Fat_Content</th>\n",
       "      <th>Item_Visibility</th>\n",
       "      <th>Item_Type</th>\n",
       "      <th>Item_MRP</th>\n",
       "      <th>Outlet_Identifier</th>\n",
       "      <th>Outlet_Establishment_Year</th>\n",
       "      <th>Outlet_Size</th>\n",
       "      <th>Outlet_Location_Type</th>\n",
       "      <th>Outlet_Type</th>\n",
       "      <th>Item_Outlet_Sales</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2070</th>\n",
       "      <td>FDH02</td>\n",
       "      <td>7.270</td>\n",
       "      <td>Regular</td>\n",
       "      <td>0.020764</td>\n",
       "      <td>Canned</td>\n",
       "      <td>89.0488</td>\n",
       "      <td>OUT013</td>\n",
       "      <td>1987</td>\n",
       "      <td>High</td>\n",
       "      <td>Tier 3</td>\n",
       "      <td>Supermarket Type1</td>\n",
       "      <td>181.0976</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>6886</th>\n",
       "      <td>FDX13</td>\n",
       "      <td>NaN</td>\n",
       "      <td>Low Fat</td>\n",
       "      <td>0.047552</td>\n",
       "      <td>Canned</td>\n",
       "      <td>249.1092</td>\n",
       "      <td>OUT027</td>\n",
       "      <td>1985</td>\n",
       "      <td>Medium</td>\n",
       "      <td>Tier 3</td>\n",
       "      <td>Supermarket Type3</td>\n",
       "      <td>8217.3036</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>6188</th>\n",
       "      <td>FDE26</td>\n",
       "      <td>9.300</td>\n",
       "      <td>Low Fat</td>\n",
       "      <td>0.089144</td>\n",
       "      <td>Canned</td>\n",
       "      <td>144.9786</td>\n",
       "      <td>OUT049</td>\n",
       "      <td>1999</td>\n",
       "      <td>Medium</td>\n",
       "      <td>Tier 1</td>\n",
       "      <td>Supermarket Type1</td>\n",
       "      <td>1011.3502</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2351</th>\n",
       "      <td>FDA28</td>\n",
       "      <td>16.100</td>\n",
       "      <td>Regular</td>\n",
       "      <td>0.048072</td>\n",
       "      <td>Frozen Foods</td>\n",
       "      <td>126.5362</td>\n",
       "      <td>OUT017</td>\n",
       "      <td>2007</td>\n",
       "      <td>NaN</td>\n",
       "      <td>Tier 2</td>\n",
       "      <td>Supermarket Type1</td>\n",
       "      <td>1761.7068</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5381</th>\n",
       "      <td>NCS30</td>\n",
       "      <td>5.945</td>\n",
       "      <td>Low Fat</td>\n",
       "      <td>0.093215</td>\n",
       "      <td>Household</td>\n",
       "      <td>129.1652</td>\n",
       "      <td>OUT045</td>\n",
       "      <td>2002</td>\n",
       "      <td>NaN</td>\n",
       "      <td>Tier 2</td>\n",
       "      <td>Supermarket Type1</td>\n",
       "      <td>2841.6344</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "     Item_Identifier  Item_Weight Item_Fat_Content  Item_Visibility  \\\n",
       "2070           FDH02        7.270          Regular         0.020764   \n",
       "6886           FDX13          NaN          Low Fat         0.047552   \n",
       "6188           FDE26        9.300          Low Fat         0.089144   \n",
       "2351           FDA28       16.100          Regular         0.048072   \n",
       "5381           NCS30        5.945          Low Fat         0.093215   \n",
       "\n",
       "         Item_Type  Item_MRP Outlet_Identifier  Outlet_Establishment_Year  \\\n",
       "2070        Canned   89.0488            OUT013                       1987   \n",
       "6886        Canned  249.1092            OUT027                       1985   \n",
       "6188        Canned  144.9786            OUT049                       1999   \n",
       "2351  Frozen Foods  126.5362            OUT017                       2007   \n",
       "5381     Household  129.1652            OUT045                       2002   \n",
       "\n",
       "     Outlet_Size Outlet_Location_Type        Outlet_Type  Item_Outlet_Sales  \n",
       "2070        High               Tier 3  Supermarket Type1           181.0976  \n",
       "6886      Medium               Tier 3  Supermarket Type3          8217.3036  \n",
       "6188      Medium               Tier 1  Supermarket Type1          1011.3502  \n",
       "2351         NaN               Tier 2  Supermarket Type1          1761.7068  \n",
       "5381         NaN               Tier 2  Supermarket Type1          2841.6344  "
      ]
     },
     "execution_count": 4,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "data.sample(5)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Find Shape of Our Dataset (Number of Rows And Number of Columns)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(8523, 12)"
      ]
     },
     "execution_count": 5,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "data.shape"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Get Information About Our Dataset Like Total Number Rows, Total Number of Columns, Datatypes of Each Column And Memory Requirement"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Item_Weight</th>\n",
       "      <th>Item_Visibility</th>\n",
       "      <th>Item_MRP</th>\n",
       "      <th>Outlet_Establishment_Year</th>\n",
       "      <th>Item_Outlet_Sales</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>count</th>\n",
       "      <td>7060.000000</td>\n",
       "      <td>8523.000000</td>\n",
       "      <td>8523.000000</td>\n",
       "      <td>8523.000000</td>\n",
       "      <td>8523.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>mean</th>\n",
       "      <td>12.857645</td>\n",
       "      <td>0.066132</td>\n",
       "      <td>140.992782</td>\n",
       "      <td>1997.831867</td>\n",
       "      <td>2181.288914</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>std</th>\n",
       "      <td>4.643456</td>\n",
       "      <td>0.051598</td>\n",
       "      <td>62.275067</td>\n",
       "      <td>8.371760</td>\n",
       "      <td>1706.499616</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>min</th>\n",
       "      <td>4.555000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>31.290000</td>\n",
       "      <td>1985.000000</td>\n",
       "      <td>33.290000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>25%</th>\n",
       "      <td>8.773750</td>\n",
       "      <td>0.026989</td>\n",
       "      <td>93.826500</td>\n",
       "      <td>1987.000000</td>\n",
       "      <td>834.247400</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>50%</th>\n",
       "      <td>12.600000</td>\n",
       "      <td>0.053931</td>\n",
       "      <td>143.012800</td>\n",
       "      <td>1999.000000</td>\n",
       "      <td>1794.331000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>75%</th>\n",
       "      <td>16.850000</td>\n",
       "      <td>0.094585</td>\n",
       "      <td>185.643700</td>\n",
       "      <td>2004.000000</td>\n",
       "      <td>3101.296400</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>max</th>\n",
       "      <td>21.350000</td>\n",
       "      <td>0.328391</td>\n",
       "      <td>266.888400</td>\n",
       "      <td>2009.000000</td>\n",
       "      <td>13086.964800</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "       Item_Weight  Item_Visibility     Item_MRP  Outlet_Establishment_Year  \\\n",
       "count  7060.000000      8523.000000  8523.000000                8523.000000   \n",
       "mean     12.857645         0.066132   140.992782                1997.831867   \n",
       "std       4.643456         0.051598    62.275067                   8.371760   \n",
       "min       4.555000         0.000000    31.290000                1985.000000   \n",
       "25%       8.773750         0.026989    93.826500                1987.000000   \n",
       "50%      12.600000         0.053931   143.012800                1999.000000   \n",
       "75%      16.850000         0.094585   185.643700                2004.000000   \n",
       "max      21.350000         0.328391   266.888400                2009.000000   \n",
       "\n",
       "       Item_Outlet_Sales  \n",
       "count        8523.000000  \n",
       "mean         2181.288914  \n",
       "std          1706.499616  \n",
       "min            33.290000  \n",
       "25%           834.247400  \n",
       "50%          1794.331000  \n",
       "75%          3101.296400  \n",
       "max         13086.964800  "
      ]
     },
     "execution_count": 6,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "data.describe()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Check Null Values In The Dataset"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Item_Identifier                 0\n",
       "Item_Weight                  1463\n",
       "Item_Fat_Content                0\n",
       "Item_Visibility                 0\n",
       "Item_Type                       0\n",
       "Item_MRP                        0\n",
       "Outlet_Identifier               0\n",
       "Outlet_Establishment_Year       0\n",
       "Outlet_Size                  2410\n",
       "Outlet_Location_Type            0\n",
       "Outlet_Type                     0\n",
       "Item_Outlet_Sales               0\n",
       "dtype: int64"
      ]
     },
     "execution_count": 7,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "data.isnull().sum()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 8,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Item_Identifier               0.000000\n",
      "Item_Weight                  17.165317\n",
      "Item_Fat_Content              0.000000\n",
      "Item_Visibility               0.000000\n",
      "Item_Type                     0.000000\n",
      "Item_MRP                      0.000000\n",
      "Outlet_Identifier             0.000000\n",
      "Outlet_Establishment_Year     0.000000\n",
      "Outlet_Size                  28.276428\n",
      "Outlet_Location_Type          0.000000\n",
      "Outlet_Type                   0.000000\n",
      "Item_Outlet_Sales             0.000000\n",
      "dtype: float64\n"
     ]
    }
   ],
   "source": [
    "per = data.isnull().sum() * 100 / len(data)\n",
    "print(per)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Taking Care of Duplicate Values"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 9,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "False"
      ]
     },
     "execution_count": 9,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "data.duplicated().any()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Handling The missing Values"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 10,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0        9.300\n",
       "1        5.920\n",
       "2       17.500\n",
       "3       19.200\n",
       "4        8.930\n",
       "         ...  \n",
       "8518     6.865\n",
       "8519     8.380\n",
       "8520    10.600\n",
       "8521     7.210\n",
       "8522    14.800\n",
       "Name: Item_Weight, Length: 8523, dtype: float64"
      ]
     },
     "execution_count": 10,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "data['Item_Weight']"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 11,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0       Medium\n",
       "1       Medium\n",
       "2       Medium\n",
       "3          NaN\n",
       "4         High\n",
       "         ...  \n",
       "8518      High\n",
       "8519       NaN\n",
       "8520     Small\n",
       "8521    Medium\n",
       "8522     Small\n",
       "Name: Outlet_Size, Length: 8523, dtype: object"
      ]
     },
     "execution_count": 11,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "data['Outlet_Size']"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Univariate Imputation"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 12,
   "metadata": {},
   "outputs": [],
   "source": [
    "mean_weight = data['Item_Weight'].mean()\n",
    "median_weight = data['Item_Weight'].median()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 13,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "12.857645184136183 12.6\n"
     ]
    }
   ],
   "source": [
    "print(mean_weight,median_weight)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 14,
   "metadata": {},
   "outputs": [],
   "source": [
    "data['Item_Weight_mean']=data['Item_Weight'].fillna(mean_weight)\n",
    "data['Item_Weight_median']=data['Item_Weight'].fillna(median_weight)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 15,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Item_Identifier</th>\n",
       "      <th>Item_Weight</th>\n",
       "      <th>Item_Fat_Content</th>\n",
       "      <th>Item_Visibility</th>\n",
       "      <th>Item_Type</th>\n",
       "      <th>Item_MRP</th>\n",
       "      <th>Outlet_Identifier</th>\n",
       "      <th>Outlet_Establishment_Year</th>\n",
       "      <th>Outlet_Size</th>\n",
       "      <th>Outlet_Location_Type</th>\n",
       "      <th>Outlet_Type</th>\n",
       "      <th>Item_Outlet_Sales</th>\n",
       "      <th>Item_Weight_mean</th>\n",
       "      <th>Item_Weight_median</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>FDA15</td>\n",
       "      <td>9.3</td>\n",
       "      <td>Low Fat</td>\n",
       "      <td>0.016047</td>\n",
       "      <td>Dairy</td>\n",
       "      <td>249.8092</td>\n",
       "      <td>OUT049</td>\n",
       "      <td>1999</td>\n",
       "      <td>Medium</td>\n",
       "      <td>Tier 1</td>\n",
       "      <td>Supermarket Type1</td>\n",
       "      <td>3735.138</td>\n",
       "      <td>9.3</td>\n",
       "      <td>9.3</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "  Item_Identifier  Item_Weight Item_Fat_Content  Item_Visibility Item_Type  \\\n",
       "0           FDA15          9.3          Low Fat         0.016047     Dairy   \n",
       "\n",
       "   Item_MRP Outlet_Identifier  Outlet_Establishment_Year Outlet_Size  \\\n",
       "0  249.8092            OUT049                       1999      Medium   \n",
       "\n",
       "  Outlet_Location_Type        Outlet_Type  Item_Outlet_Sales  \\\n",
       "0               Tier 1  Supermarket Type1           3735.138   \n",
       "\n",
       "   Item_Weight_mean  Item_Weight_median  \n",
       "0               9.3                 9.3  "
      ]
     },
     "execution_count": 15,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "data.head(1)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 16,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Original Weight variable variance 21.56168825983637\n",
      "Item Weight variance after mean imputation 17.86012173506042\n",
      "Item Weight variance after median imputation 17.869561454073366\n"
     ]
    }
   ],
   "source": [
    "print(\"Original Weight variable variance\",data['Item_Weight'].var())\n",
    "print(\"Item Weight variance after mean imputation\",data['Item_Weight_mean'].var())\n",
    "print(\"Item Weight variance after median imputation\",data['Item_Weight_median'].var())"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 17,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "data['Item_Weight'].plot(kind = \"kde\",label=\"Original\")\n",
    "\n",
    "data['Item_Weight_mean'].plot(kind = \"kde\",label = \"Mean\")\n",
    "\n",
    "data['Item_Weight_median'].plot(kind = \"kde\",label = \"Median\")\n",
    "\n",
    "plt.legend()\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 18,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<AxesSubplot:>"
      ]
     },
     "execution_count": 18,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "data[['Item_Weight','Item_Weight_mean','Item_Weight_median']].boxplot()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 19,
   "metadata": {},
   "outputs": [],
   "source": [
    "data['Item_Weight_interploate']=data['Item_Weight'].interpolate(method=\"linear\")"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 20,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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
