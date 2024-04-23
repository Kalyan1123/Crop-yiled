{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# Predicting Crops Yield  : A Machine Learning  Approach \n",
    " \n",
    "The science of training machines to learn and produce models for future predictions is widely used, and not for nothing.\n",
    "Agriculture plays a critical role in the global economy. With the continuing expansion of the human population understanding worldwide crop yield is central to addressing food security challenges and reducing the impacts of climate change. \n",
    "\n",
    "Crop yield prediction is an important agricultural problem. The Agricultural yield primarily depends on weather conditions (rain, temperature, etc), pesticides and accurate information about history of crop yield is an important thing for making decisions related to agricultural risk management and future predictions.  The basic ingredients that sustain humans are similar. We eat a lot of corn, wheat, rice and other simple crops. In this project the prediction of top 10 most consumed yields all over the world is established by applying machine learning techniques. In this project I will predict crops yield worldwide for 10 most consumed crops. It is a regression problem\n",
    "\n",
    "Cuisine varies greatly around the world, the basic ingredients that sustain humans are pretty similar. We eat a lot of corn, wheat, rice and other simple crops. In this project the prediction of top 10 most consumed yields all over the world is established by applying machine learning techniqus. \n",
    " \n",
    " These corps include :\n",
    "\n",
    "- Cassava                \n",
    "- Maize                  \n",
    "- Plantains and others   \n",
    "- Potatoes                \n",
    "- Rice, paddy             \n",
    "- Sorghum                \n",
    "- Soybeans               \n",
    "- Sweet potatoes       \n",
    "- Wheat                  \n",
    "- Yams             \n",
    "\n",
    "\n",
    "In the project, machine learning methods are applied to predict crop yield using publicly available data from FAO and World Data Bank. \n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# Part One: Gathering & Cleaning Data\n",
    "\n",
    "### Crops Yield Data:\n",
    "\n",
    "\n",
    " \n",
    "After importing required libraries, crops yield of ten most consumed crops around the world was downloaded from FAO webiste.The collected data include country, item, year starting from 1961 to 2016 and yield value. "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 1,
   "metadata": {},
   "outputs": [],
   "source": [
    "import numpy as np \n",
    "import pandas as pd "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(56717, 12)"
      ]
     },
     "execution_count": 2,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df_yield = pd.read_csv('yield.csv')\n",
    "df_yield.shape"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "metadata": {
    "scrolled": true
   },
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
       "      <th>Domain Code</th>\n",
       "      <th>Domain</th>\n",
       "      <th>Area Code</th>\n",
       "      <th>Area</th>\n",
       "      <th>Element Code</th>\n",
       "      <th>Element</th>\n",
       "      <th>Item Code</th>\n",
       "      <th>Item</th>\n",
       "      <th>Year Code</th>\n",
       "      <th>Year</th>\n",
       "      <th>Unit</th>\n",
       "      <th>Value</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>QC</td>\n",
       "      <td>Crops</td>\n",
       "      <td>2</td>\n",
       "      <td>Afghanistan</td>\n",
       "      <td>5419</td>\n",
       "      <td>Yield</td>\n",
       "      <td>56</td>\n",
       "      <td>Maize</td>\n",
       "      <td>1961</td>\n",
       "      <td>1961</td>\n",
       "      <td>hg/ha</td>\n",
       "      <td>14000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>QC</td>\n",
       "      <td>Crops</td>\n",
       "      <td>2</td>\n",
       "      <td>Afghanistan</td>\n",
       "      <td>5419</td>\n",
       "      <td>Yield</td>\n",
       "      <td>56</td>\n",
       "      <td>Maize</td>\n",
       "      <td>1962</td>\n",
       "      <td>1962</td>\n",
       "      <td>hg/ha</td>\n",
       "      <td>14000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>QC</td>\n",
       "      <td>Crops</td>\n",
       "      <td>2</td>\n",
       "      <td>Afghanistan</td>\n",
       "      <td>5419</td>\n",
       "      <td>Yield</td>\n",
       "      <td>56</td>\n",
       "      <td>Maize</td>\n",
       "      <td>1963</td>\n",
       "      <td>1963</td>\n",
       "      <td>hg/ha</td>\n",
       "      <td>14260</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>QC</td>\n",
       "      <td>Crops</td>\n",
       "      <td>2</td>\n",
       "      <td>Afghanistan</td>\n",
       "      <td>5419</td>\n",
       "      <td>Yield</td>\n",
       "      <td>56</td>\n",
       "      <td>Maize</td>\n",
       "      <td>1964</td>\n",
       "      <td>1964</td>\n",
       "      <td>hg/ha</td>\n",
       "      <td>14257</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>QC</td>\n",
       "      <td>Crops</td>\n",
       "      <td>2</td>\n",
       "      <td>Afghanistan</td>\n",
       "      <td>5419</td>\n",
       "      <td>Yield</td>\n",
       "      <td>56</td>\n",
       "      <td>Maize</td>\n",
       "      <td>1965</td>\n",
       "      <td>1965</td>\n",
       "      <td>hg/ha</td>\n",
       "      <td>14400</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "  Domain Code Domain  Area Code         Area  Element Code Element  Item Code  \\\n",
       "0          QC  Crops          2  Afghanistan          5419   Yield         56   \n",
       "1          QC  Crops          2  Afghanistan          5419   Yield         56   \n",
       "2          QC  Crops          2  Afghanistan          5419   Yield         56   \n",
       "3          QC  Crops          2  Afghanistan          5419   Yield         56   \n",
       "4          QC  Crops          2  Afghanistan          5419   Yield         56   \n",
       "\n",
       "    Item  Year Code  Year   Unit  Value  \n",
       "0  Maize       1961  1961  hg/ha  14000  \n",
       "1  Maize       1962  1962  hg/ha  14000  \n",
       "2  Maize       1963  1963  hg/ha  14260  \n",
       "3  Maize       1964  1964  hg/ha  14257  \n",
       "4  Maize       1965  1965  hg/ha  14400  "
      ]
     },
     "execution_count": 3,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df_yield.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "metadata": {
    "scrolled": true
   },
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
       "      <th>Domain Code</th>\n",
       "      <th>Domain</th>\n",
       "      <th>Area Code</th>\n",
       "      <th>Area</th>\n",
       "      <th>Element Code</th>\n",
       "      <th>Element</th>\n",
       "      <th>Item Code</th>\n",
       "      <th>Item</th>\n",
       "      <th>Year Code</th>\n",
       "      <th>Year</th>\n",
       "      <th>Unit</th>\n",
       "      <th>Value</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>56712</th>\n",
       "      <td>QC</td>\n",
       "      <td>Crops</td>\n",
       "      <td>181</td>\n",
       "      <td>Zimbabwe</td>\n",
       "      <td>5419</td>\n",
       "      <td>Yield</td>\n",
       "      <td>15</td>\n",
       "      <td>Wheat</td>\n",
       "      <td>2012</td>\n",
       "      <td>2012</td>\n",
       "      <td>hg/ha</td>\n",
       "      <td>24420</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>56713</th>\n",
       "      <td>QC</td>\n",
       "      <td>Crops</td>\n",
       "      <td>181</td>\n",
       "      <td>Zimbabwe</td>\n",
       "      <td>5419</td>\n",
       "      <td>Yield</td>\n",
       "      <td>15</td>\n",
       "      <td>Wheat</td>\n",
       "      <td>2013</td>\n",
       "      <td>2013</td>\n",
       "      <td>hg/ha</td>\n",
       "      <td>22888</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>56714</th>\n",
       "      <td>QC</td>\n",
       "      <td>Crops</td>\n",
       "      <td>181</td>\n",
       "      <td>Zimbabwe</td>\n",
       "      <td>5419</td>\n",
       "      <td>Yield</td>\n",
       "      <td>15</td>\n",
       "      <td>Wheat</td>\n",
       "      <td>2014</td>\n",
       "      <td>2014</td>\n",
       "      <td>hg/ha</td>\n",
       "      <td>21357</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>56715</th>\n",
       "      <td>QC</td>\n",
       "      <td>Crops</td>\n",
       "      <td>181</td>\n",
       "      <td>Zimbabwe</td>\n",
       "      <td>5419</td>\n",
       "      <td>Yield</td>\n",
       "      <td>15</td>\n",
       "      <td>Wheat</td>\n",
       "      <td>2015</td>\n",
       "      <td>2015</td>\n",
       "      <td>hg/ha</td>\n",
       "      <td>19826</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>56716</th>\n",
       "      <td>QC</td>\n",
       "      <td>Crops</td>\n",
       "      <td>181</td>\n",
       "      <td>Zimbabwe</td>\n",
       "      <td>5419</td>\n",
       "      <td>Yield</td>\n",
       "      <td>15</td>\n",
       "      <td>Wheat</td>\n",
       "      <td>2016</td>\n",
       "      <td>2016</td>\n",
       "      <td>hg/ha</td>\n",
       "      <td>18294</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "      Domain Code Domain  Area Code      Area  Element Code Element  \\\n",
       "56712          QC  Crops        181  Zimbabwe          5419   Yield   \n",
       "56713          QC  Crops        181  Zimbabwe          5419   Yield   \n",
       "56714          QC  Crops        181  Zimbabwe          5419   Yield   \n",
       "56715          QC  Crops        181  Zimbabwe          5419   Yield   \n",
       "56716          QC  Crops        181  Zimbabwe          5419   Yield   \n",
       "\n",
       "       Item Code   Item  Year Code  Year   Unit  Value  \n",
       "56712         15  Wheat       2012  2012  hg/ha  24420  \n",
       "56713         15  Wheat       2013  2013  hg/ha  22888  \n",
       "56714         15  Wheat       2014  2014  hg/ha  21357  \n",
       "56715         15  Wheat       2015  2015  hg/ha  19826  \n",
       "56716         15  Wheat       2016  2016  hg/ha  18294  "
      ]
     },
     "execution_count": 4,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df_yield.tail()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Looking at the columns in the csv, we can rename **Value** to **hg/ha_yield** to make it easier to recognise that this is our crops yields production value. In addition to removal of unnecessary coloumns like Area Code, Domain, Item Code, etc."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "metadata": {
    "scrolled": true
   },
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
       "      <th>Domain Code</th>\n",
       "      <th>Domain</th>\n",
       "      <th>Area Code</th>\n",
       "      <th>Area</th>\n",
       "      <th>Element Code</th>\n",
       "      <th>Element</th>\n",
       "      <th>Item Code</th>\n",
       "      <th>Item</th>\n",
       "      <th>Year Code</th>\n",
       "      <th>Year</th>\n",
       "      <th>Unit</th>\n",
       "      <th>hg/ha_yield</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>QC</td>\n",
       "      <td>Crops</td>\n",
       "      <td>2</td>\n",
       "      <td>Afghanistan</td>\n",
       "      <td>5419</td>\n",
       "      <td>Yield</td>\n",
       "      <td>56</td>\n",
       "      <td>Maize</td>\n",
       "      <td>1961</td>\n",
       "      <td>1961</td>\n",
       "      <td>hg/ha</td>\n",
       "      <td>14000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>QC</td>\n",
       "      <td>Crops</td>\n",
       "      <td>2</td>\n",
       "      <td>Afghanistan</td>\n",
       "      <td>5419</td>\n",
       "      <td>Yield</td>\n",
       "      <td>56</td>\n",
       "      <td>Maize</td>\n",
       "      <td>1962</td>\n",
       "      <td>1962</td>\n",
       "      <td>hg/ha</td>\n",
       "      <td>14000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>QC</td>\n",
       "      <td>Crops</td>\n",
       "      <td>2</td>\n",
       "      <td>Afghanistan</td>\n",
       "      <td>5419</td>\n",
       "      <td>Yield</td>\n",
       "      <td>56</td>\n",
       "      <td>Maize</td>\n",
       "      <td>1963</td>\n",
       "      <td>1963</td>\n",
       "      <td>hg/ha</td>\n",
       "      <td>14260</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>QC</td>\n",
       "      <td>Crops</td>\n",
       "      <td>2</td>\n",
       "      <td>Afghanistan</td>\n",
       "      <td>5419</td>\n",
       "      <td>Yield</td>\n",
       "      <td>56</td>\n",
       "      <td>Maize</td>\n",
       "      <td>1964</td>\n",
       "      <td>1964</td>\n",
       "      <td>hg/ha</td>\n",
       "      <td>14257</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>QC</td>\n",
       "      <td>Crops</td>\n",
       "      <td>2</td>\n",
       "      <td>Afghanistan</td>\n",
       "      <td>5419</td>\n",
       "      <td>Yield</td>\n",
       "      <td>56</td>\n",
       "      <td>Maize</td>\n",
       "      <td>1965</td>\n",
       "      <td>1965</td>\n",
       "      <td>hg/ha</td>\n",
       "      <td>14400</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "  Domain Code Domain  Area Code         Area  Element Code Element  Item Code  \\\n",
       "0          QC  Crops          2  Afghanistan          5419   Yield         56   \n",
       "1          QC  Crops          2  Afghanistan          5419   Yield         56   \n",
       "2          QC  Crops          2  Afghanistan          5419   Yield         56   \n",
       "3          QC  Crops          2  Afghanistan          5419   Yield         56   \n",
       "4          QC  Crops          2  Afghanistan          5419   Yield         56   \n",
       "\n",
       "    Item  Year Code  Year   Unit  hg/ha_yield  \n",
       "0  Maize       1961  1961  hg/ha        14000  \n",
       "1  Maize       1962  1962  hg/ha        14000  \n",
       "2  Maize       1963  1963  hg/ha        14260  \n",
       "3  Maize       1964  1964  hg/ha        14257  \n",
       "4  Maize       1965  1965  hg/ha        14400  "
      ]
     },
     "execution_count": 5,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# rename columns.\n",
    "df_yield = df_yield.rename(index=str, columns={\"Value\": \"hg/ha_yield\"})\n",
    "df_yield.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "metadata": {
    "scrolled": false
   },
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
       "      <th>Area</th>\n",
       "      <th>Item</th>\n",
       "      <th>Year</th>\n",
       "      <th>hg/ha_yield</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>Afghanistan</td>\n",
       "      <td>Maize</td>\n",
       "      <td>1961</td>\n",
       "      <td>14000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>Afghanistan</td>\n",
       "      <td>Maize</td>\n",
       "      <td>1962</td>\n",
       "      <td>14000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>Afghanistan</td>\n",
       "      <td>Maize</td>\n",
       "      <td>1963</td>\n",
       "      <td>14260</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>Afghanistan</td>\n",
       "      <td>Maize</td>\n",
       "      <td>1964</td>\n",
       "      <td>14257</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Afghanistan</td>\n",
       "      <td>Maize</td>\n",
       "      <td>1965</td>\n",
       "      <td>14400</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "          Area   Item  Year  hg/ha_yield\n",
       "0  Afghanistan  Maize  1961        14000\n",
       "1  Afghanistan  Maize  1962        14000\n",
       "2  Afghanistan  Maize  1963        14260\n",
       "3  Afghanistan  Maize  1964        14257\n",
       "4  Afghanistan  Maize  1965        14400"
      ]
     },
     "execution_count": 6,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# drop unwanted columns.\n",
    "df_yield = df_yield.drop(['Year Code','Element Code','Element','Year Code','Area Code','Domain Code','Domain','Unit','Item Code'], axis=1)\n",
    "df_yield.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "metadata": {
    "scrolled": true
   },
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
       "      <th>Year</th>\n",
       "      <th>hg/ha_yield</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>count</th>\n",
       "      <td>56717.000000</td>\n",
       "      <td>56717.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>mean</th>\n",
       "      <td>1989.669570</td>\n",
       "      <td>62094.660084</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>std</th>\n",
       "      <td>16.133198</td>\n",
       "      <td>67835.932856</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>min</th>\n",
       "      <td>1961.000000</td>\n",
       "      <td>0.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>25%</th>\n",
       "      <td>1976.000000</td>\n",
       "      <td>15680.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>50%</th>\n",
       "      <td>1991.000000</td>\n",
       "      <td>36744.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>75%</th>\n",
       "      <td>2004.000000</td>\n",
       "      <td>86213.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>max</th>\n",
       "      <td>2016.000000</td>\n",
       "      <td>1000000.000000</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "               Year     hg/ha_yield\n",
       "count  56717.000000    56717.000000\n",
       "mean    1989.669570    62094.660084\n",
       "std       16.133198    67835.932856\n",
       "min     1961.000000        0.000000\n",
       "25%     1976.000000    15680.000000\n",
       "50%     1991.000000    36744.000000\n",
       "75%     2004.000000    86213.000000\n",
       "max     2016.000000  1000000.000000"
      ]
     },
     "execution_count": 7,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df_yield.describe()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "From cell above, we know the dataframe starts at 1961 and ends at 2016, this is all the avialable data up to date from FAO. "
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
      "<class 'pandas.core.frame.DataFrame'>\n",
      "Index: 56717 entries, 0 to 56716\n",
      "Data columns (total 4 columns):\n",
      "Area           56717 non-null object\n",
      "Item           56717 non-null object\n",
      "Year           56717 non-null int64\n",
      "hg/ha_yield    56717 non-null int64\n",
      "dtypes: int64(2), object(2)\n",
      "memory usage: 2.2+ MB\n"
     ]
    }
   ],
   "source": [
    "df_yield.info()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "All of the columns type are in right type. "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Climate Data : Rainfall \n",
    "The climatic factors include rainfall and temperature. They are abiotic components, including pesticides and soil, of the environmental factors that influence plant growth and development.\n",
    "\n",
    "\n",
    "Rainfall has a dramatic effect on agriculture. For this project rain fall per year information was gathered from World Data Bank. "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 9,
   "metadata": {
    "scrolled": true
   },
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
       "      <th>Area</th>\n",
       "      <th>Year</th>\n",
       "      <th>average_rain_fall_mm_per_year</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>Afghanistan</td>\n",
       "      <td>1985</td>\n",
       "      <td>327</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>Afghanistan</td>\n",
       "      <td>1986</td>\n",
       "      <td>327</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>Afghanistan</td>\n",
       "      <td>1987</td>\n",
       "      <td>327</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>Afghanistan</td>\n",
       "      <td>1989</td>\n",
       "      <td>327</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Afghanistan</td>\n",
       "      <td>1990</td>\n",
       "      <td>327</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "          Area  Year average_rain_fall_mm_per_year\n",
       "0  Afghanistan  1985                           327\n",
       "1  Afghanistan  1986                           327\n",
       "2  Afghanistan  1987                           327\n",
       "3  Afghanistan  1989                           327\n",
       "4  Afghanistan  1990                           327"
      ]
     },
     "execution_count": 9,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df_rain = pd.read_csv('rainfall.csv')\n",
    "df_rain.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 10,
   "metadata": {},
   "outputs": [],
   "source": [
    "df_rain = df_rain.rename(index=str, columns={\" Area\": 'Area'})"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Making sure that names of columns are unified across all dataframes is important for merging after cleaning afterwards. "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 11,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "<class 'pandas.core.frame.DataFrame'>\n",
      "Index: 6727 entries, 0 to 6726\n",
      "Data columns (total 3 columns):\n",
      "Area                             6727 non-null object\n",
      "Year                             6727 non-null int64\n",
      "average_rain_fall_mm_per_year    5953 non-null object\n",
      "dtypes: int64(1), object(2)\n",
      "memory usage: 210.2+ KB\n"
     ]
    }
   ],
   "source": [
    "# check data types \n",
    "df_rain.info()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "We can see from cell above that average_rain_fall_mm_per_year type is an object, we need to turn it to a float value. "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 12,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "<class 'pandas.core.frame.DataFrame'>\n",
      "Index: 6727 entries, 0 to 6726\n",
      "Data columns (total 3 columns):\n",
      "Area                             6727 non-null object\n",
      "Year                             6727 non-null int64\n",
      "average_rain_fall_mm_per_year    5947 non-null float64\n",
      "dtypes: float64(1), int64(1), object(1)\n",
      "memory usage: 210.2+ KB\n"
     ]
    },
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "C:\\Users\\hajiralmahdi\\AppData\\Local\\Continuum\\anaconda3\\lib\\site-packages\\ipykernel_launcher.py:2: FutureWarning: convert_objects is deprecated.  To re-infer data dtypes for object columns, use DataFrame.infer_objects()\n",
      "For all other conversions use the data-type specific converters pd.to_datetime, pd.to_timedelta and pd.to_numeric.\n",
      "  \n"
     ]
    }
   ],
   "source": [
    "# convert average_rain_fall_mm_per_year from object to float\n",
    "df_rain = df_rain.convert_objects(convert_numeric=True)\n",
    "df_rain.info()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Next, droping any empty rows from dataset and merge yield dataframe with rain dataframe by year and area columns"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 13,
   "metadata": {},
   "outputs": [],
   "source": [
    "df_rain = df_rain.dropna()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 14,
   "metadata": {
    "scrolled": true
   },
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
       "      <th>Year</th>\n",
       "      <th>average_rain_fall_mm_per_year</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>count</th>\n",
       "      <td>5947.000000</td>\n",
       "      <td>5947.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>mean</th>\n",
       "      <td>2001.365899</td>\n",
       "      <td>1124.743232</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>std</th>\n",
       "      <td>9.526335</td>\n",
       "      <td>786.257365</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>min</th>\n",
       "      <td>1985.000000</td>\n",
       "      <td>51.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>25%</th>\n",
       "      <td>1993.000000</td>\n",
       "      <td>534.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>50%</th>\n",
       "      <td>2001.000000</td>\n",
       "      <td>1010.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>75%</th>\n",
       "      <td>2010.000000</td>\n",
       "      <td>1651.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>max</th>\n",
       "      <td>2017.000000</td>\n",
       "      <td>3240.000000</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "              Year  average_rain_fall_mm_per_year\n",
       "count  5947.000000                    5947.000000\n",
       "mean   2001.365899                    1124.743232\n",
       "std       9.526335                     786.257365\n",
       "min    1985.000000                      51.000000\n",
       "25%    1993.000000                     534.000000\n",
       "50%    2001.000000                    1010.000000\n",
       "75%    2010.000000                    1651.000000\n",
       "max    2017.000000                    3240.000000"
      ]
     },
     "execution_count": 14,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df_rain.describe()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "The rainfall dataframe begins at 1985 and ends at 2016. "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 15,
   "metadata": {},
   "outputs": [],
   "source": [
    "# merge yield dataframe with rain dataframe by year and area columns \n",
    "yield_df = pd.merge(df_yield, df_rain, on=['Year','Area'])"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Now, we view the final shape of the dataframe and info of values:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 16,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(25385, 5)"
      ]
     },
     "execution_count": 16,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "yield_df.shape"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 17,
   "metadata": {
    "scrolled": true
   },
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
       "      <th>Area</th>\n",
       "      <th>Item</th>\n",
       "      <th>Year</th>\n",
       "      <th>hg/ha_yield</th>\n",
       "      <th>average_rain_fall_mm_per_year</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>Afghanistan</td>\n",
       "      <td>Maize</td>\n",
       "      <td>1985</td>\n",
       "      <td>16652</td>\n",
       "      <td>327.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>Afghanistan</td>\n",
       "      <td>Potatoes</td>\n",
       "      <td>1985</td>\n",
       "      <td>140909</td>\n",
       "      <td>327.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>Afghanistan</td>\n",
       "      <td>Rice, paddy</td>\n",
       "      <td>1985</td>\n",
       "      <td>22482</td>\n",
       "      <td>327.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>Afghanistan</td>\n",
       "      <td>Wheat</td>\n",
       "      <td>1985</td>\n",
       "      <td>12277</td>\n",
       "      <td>327.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Afghanistan</td>\n",
       "      <td>Maize</td>\n",
       "      <td>1986</td>\n",
       "      <td>16875</td>\n",
       "      <td>327.0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "          Area         Item  Year  hg/ha_yield  average_rain_fall_mm_per_year\n",
       "0  Afghanistan        Maize  1985        16652                          327.0\n",
       "1  Afghanistan     Potatoes  1985       140909                          327.0\n",
       "2  Afghanistan  Rice, paddy  1985        22482                          327.0\n",
       "3  Afghanistan        Wheat  1985        12277                          327.0\n",
       "4  Afghanistan        Maize  1986        16875                          327.0"
      ]
     },
     "execution_count": 17,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "yield_df.head()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "We can see that now the years start from the first yield dataframe the starting year was 1961, now it's 1985 because that's when the rainfall data begins. "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 18,
   "metadata": {
    "scrolled": true
   },
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
       "      <th>Year</th>\n",
       "      <th>hg/ha_yield</th>\n",
       "      <th>average_rain_fall_mm_per_year</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>count</th>\n",
       "      <td>25385.000000</td>\n",
       "      <td>25385.000000</td>\n",
       "      <td>25385.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>mean</th>\n",
       "      <td>2001.278787</td>\n",
       "      <td>68312.278353</td>\n",
       "      <td>1254.849754</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>std</th>\n",
       "      <td>9.143915</td>\n",
       "      <td>75213.292733</td>\n",
       "      <td>804.449430</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>min</th>\n",
       "      <td>1985.000000</td>\n",
       "      <td>50.000000</td>\n",
       "      <td>51.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>25%</th>\n",
       "      <td>1994.000000</td>\n",
       "      <td>17432.000000</td>\n",
       "      <td>630.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>50%</th>\n",
       "      <td>2001.000000</td>\n",
       "      <td>38750.000000</td>\n",
       "      <td>1150.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>75%</th>\n",
       "      <td>2009.000000</td>\n",
       "      <td>94286.000000</td>\n",
       "      <td>1761.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>max</th>\n",
       "      <td>2016.000000</td>\n",
       "      <td>554855.000000</td>\n",
       "      <td>3240.000000</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "               Year    hg/ha_yield  average_rain_fall_mm_per_year\n",
       "count  25385.000000   25385.000000                   25385.000000\n",
       "mean    2001.278787   68312.278353                    1254.849754\n",
       "std        9.143915   75213.292733                     804.449430\n",
       "min     1985.000000      50.000000                      51.000000\n",
       "25%     1994.000000   17432.000000                     630.000000\n",
       "50%     2001.000000   38750.000000                    1150.000000\n",
       "75%     2009.000000   94286.000000                    1761.000000\n",
       "max     2016.000000  554855.000000                    3240.000000"
      ]
     },
     "execution_count": 18,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "yield_df.describe()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Pesticides Data:\n",
    "Pesticides used for each item and country was also collected from FAO database.  "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 19,
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
       "      <th>Domain</th>\n",
       "      <th>Area</th>\n",
       "      <th>Element</th>\n",
       "      <th>Item</th>\n",
       "      <th>Year</th>\n",
       "      <th>Unit</th>\n",
       "      <th>Value</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>Pesticides Use</td>\n",
       "      <td>Albania</td>\n",
       "      <td>Use</td>\n",
       "      <td>Pesticides (total)</td>\n",
       "      <td>1990</td>\n",
       "      <td>tonnes of active ingredients</td>\n",
       "      <td>121.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>Pesticides Use</td>\n",
       "      <td>Albania</td>\n",
       "      <td>Use</td>\n",
       "      <td>Pesticides (total)</td>\n",
       "      <td>1991</td>\n",
       "      <td>tonnes of active ingredients</td>\n",
       "      <td>121.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>Pesticides Use</td>\n",
       "      <td>Albania</td>\n",
       "      <td>Use</td>\n",
       "      <td>Pesticides (total)</td>\n",
       "      <td>1992</td>\n",
       "      <td>tonnes of active ingredients</td>\n",
       "      <td>121.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>Pesticides Use</td>\n",
       "      <td>Albania</td>\n",
       "      <td>Use</td>\n",
       "      <td>Pesticides (total)</td>\n",
       "      <td>1993</td>\n",
       "      <td>tonnes of active ingredients</td>\n",
       "      <td>121.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Pesticides Use</td>\n",
       "      <td>Albania</td>\n",
       "      <td>Use</td>\n",
       "      <td>Pesticides (total)</td>\n",
       "      <td>1994</td>\n",
       "      <td>tonnes of active ingredients</td>\n",
       "      <td>201.0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "           Domain     Area Element                Item  Year  \\\n",
       "0  Pesticides Use  Albania     Use  Pesticides (total)  1990   \n",
       "1  Pesticides Use  Albania     Use  Pesticides (total)  1991   \n",
       "2  Pesticides Use  Albania     Use  Pesticides (total)  1992   \n",
       "3  Pesticides Use  Albania     Use  Pesticides (total)  1993   \n",
       "4  Pesticides Use  Albania     Use  Pesticides (total)  1994   \n",
       "\n",
       "                           Unit  Value  \n",
       "0  tonnes of active ingredients  121.0  \n",
       "1  tonnes of active ingredients  121.0  \n",
       "2  tonnes of active ingredients  121.0  \n",
       "3  tonnes of active ingredients  121.0  \n",
       "4  tonnes of active ingredients  201.0  "
      ]
     },
     "execution_count": 19,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df_pes = pd.read_csv('pesticides.csv')\n",
    "df_pes.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 20,
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
       "      <th>Area</th>\n",
       "      <th>Year</th>\n",
       "      <th>pesticides_tonnes</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>Albania</td>\n",
       "      <td>1990</td>\n",
       "      <td>121.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>Albania</td>\n",
       "      <td>1991</td>\n",
       "      <td>121.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>Albania</td>\n",
       "      <td>1992</td>\n",
       "      <td>121.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>Albania</td>\n",
       "      <td>1993</td>\n",
       "      <td>121.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Albania</td>\n",
       "      <td>1994</td>\n",
       "      <td>201.0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "      Area  Year  pesticides_tonnes\n",
       "0  Albania  1990              121.0\n",
       "1  Albania  1991              121.0\n",
       "2  Albania  1992              121.0\n",
       "3  Albania  1993              121.0\n",
       "4  Albania  1994              201.0"
      ]
     },
     "execution_count": 20,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df_pes = df_pes.rename(index=str, columns={\"Value\": \"pesticides_tonnes\"})\n",
    "df_pes = df_pes.drop(['Element','Domain','Unit','Item'], axis=1)\n",
    "df_pes.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 21,
   "metadata": {
    "scrolled": true
   },
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
       "      <th>Year</th>\n",
       "      <th>pesticides_tonnes</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>count</th>\n",
       "      <td>4349.000000</td>\n",
       "      <td>4.349000e+03</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>mean</th>\n",
       "      <td>2003.138883</td>\n",
       "      <td>2.030334e+04</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>std</th>\n",
       "      <td>7.728044</td>\n",
       "      <td>1.177362e+05</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>min</th>\n",
       "      <td>1990.000000</td>\n",
       "      <td>0.000000e+00</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>25%</th>\n",
       "      <td>1996.000000</td>\n",
       "      <td>9.300000e+01</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>50%</th>\n",
       "      <td>2003.000000</td>\n",
       "      <td>1.137560e+03</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>75%</th>\n",
       "      <td>2010.000000</td>\n",
       "      <td>7.869000e+03</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>max</th>\n",
       "      <td>2016.000000</td>\n",
       "      <td>1.807000e+06</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "              Year  pesticides_tonnes\n",
       "count  4349.000000       4.349000e+03\n",
       "mean   2003.138883       2.030334e+04\n",
       "std       7.728044       1.177362e+05\n",
       "min    1990.000000       0.000000e+00\n",
       "25%    1996.000000       9.300000e+01\n",
       "50%    2003.000000       1.137560e+03\n",
       "75%    2010.000000       7.869000e+03\n",
       "max    2016.000000       1.807000e+06"
      ]
     },
     "execution_count": 21,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df_pes.describe()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 22,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "<class 'pandas.core.frame.DataFrame'>\n",
      "Index: 4349 entries, 0 to 4348\n",
      "Data columns (total 3 columns):\n",
      "Area                 4349 non-null object\n",
      "Year                 4349 non-null int64\n",
      "pesticides_tonnes    4349 non-null float64\n",
      "dtypes: float64(1), int64(1), object(1)\n",
      "memory usage: 135.9+ KB\n"
     ]
    }
   ],
   "source": [
    "df_pes.info()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 23,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(18949, 6)"
      ]
     },
     "execution_count": 23,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# merge Pesticides dataframe with yield dataframe \n",
    "yield_df = pd.merge(yield_df, df_pes, on=['Year','Area'])\n",
    "yield_df.shape"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 24,
   "metadata": {
    "scrolled": true
   },
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
       "      <th>Area</th>\n",
       "      <th>Item</th>\n",
       "      <th>Year</th>\n",
       "      <th>hg/ha_yield</th>\n",
       "      <th>average_rain_fall_mm_per_year</th>\n",
       "      <th>pesticides_tonnes</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>Albania</td>\n",
       "      <td>Maize</td>\n",
       "      <td>1990</td>\n",
       "      <td>36613</td>\n",
       "      <td>1485.0</td>\n",
       "      <td>121.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>Albania</td>\n",
       "      <td>Potatoes</td>\n",
       "      <td>1990</td>\n",
       "      <td>66667</td>\n",
       "      <td>1485.0</td>\n",
       "      <td>121.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>Albania</td>\n",
       "      <td>Rice, paddy</td>\n",
       "      <td>1990</td>\n",
       "      <td>23333</td>\n",
       "      <td>1485.0</td>\n",
       "      <td>121.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>Albania</td>\n",
       "      <td>Sorghum</td>\n",
       "      <td>1990</td>\n",
       "      <td>12500</td>\n",
       "      <td>1485.0</td>\n",
       "      <td>121.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Albania</td>\n",
       "      <td>Soybeans</td>\n",
       "      <td>1990</td>\n",
       "      <td>7000</td>\n",
       "      <td>1485.0</td>\n",
       "      <td>121.0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "      Area         Item  Year  hg/ha_yield  average_rain_fall_mm_per_year  \\\n",
       "0  Albania        Maize  1990        36613                         1485.0   \n",
       "1  Albania     Potatoes  1990        66667                         1485.0   \n",
       "2  Albania  Rice, paddy  1990        23333                         1485.0   \n",
       "3  Albania      Sorghum  1990        12500                         1485.0   \n",
       "4  Albania     Soybeans  1990         7000                         1485.0   \n",
       "\n",
       "   pesticides_tonnes  \n",
       "0              121.0  \n",
       "1              121.0  \n",
       "2              121.0  \n",
       "3              121.0  \n",
       "4              121.0  "
      ]
     },
     "execution_count": 24,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "yield_df.head()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Average Temprature: \n",
    "\n",
    "Average Temprature for each country was colleced from World Bank Data. "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 33,
   "metadata": {},
   "outputs": [],
   "source": [
    "avg_temp=  pd.read_csv('temp.csv')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 34,
   "metadata": {
    "scrolled": true
   },
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
       "      <th>year</th>\n",
       "      <th>country</th>\n",
       "      <th>avg_temp</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>1849</td>\n",
       "      <td>C么te D'Ivoire</td>\n",
       "      <td>25.58</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>1850</td>\n",
       "      <td>C么te D'Ivoire</td>\n",
       "      <td>25.52</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>1851</td>\n",
       "      <td>C么te D'Ivoire</td>\n",
       "      <td>25.67</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>1852</td>\n",
       "      <td>C么te D'Ivoire</td>\n",
       "      <td>NaN</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>1853</td>\n",
       "      <td>C么te D'Ivoire</td>\n",
       "      <td>NaN</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   year        country  avg_temp\n",
       "0  1849  C么te D'Ivoire     25.58\n",
       "1  1850  C么te D'Ivoire     25.52\n",
       "2  1851  C么te D'Ivoire     25.67\n",
       "3  1852  C么te D'Ivoire       NaN\n",
       "4  1853  C么te D'Ivoire       NaN"
      ]
     },
     "execution_count": 34,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "avg_temp.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 35,
   "metadata": {
    "scrolled": true
   },
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
       "      <th>year</th>\n",
       "      <th>avg_temp</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>count</th>\n",
       "      <td>71311.000000</td>\n",
       "      <td>68764.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>mean</th>\n",
       "      <td>1905.799007</td>\n",
       "      <td>16.183876</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>std</th>\n",
       "      <td>67.102099</td>\n",
       "      <td>7.592960</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>min</th>\n",
       "      <td>1743.000000</td>\n",
       "      <td>-14.350000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>25%</th>\n",
       "      <td>1858.000000</td>\n",
       "      <td>9.750000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>50%</th>\n",
       "      <td>1910.000000</td>\n",
       "      <td>16.140000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>75%</th>\n",
       "      <td>1962.000000</td>\n",
       "      <td>23.762500</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>max</th>\n",
       "      <td>2013.000000</td>\n",
       "      <td>30.730000</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "               year      avg_temp\n",
       "count  71311.000000  68764.000000\n",
       "mean    1905.799007     16.183876\n",
       "std       67.102099      7.592960\n",
       "min     1743.000000    -14.350000\n",
       "25%     1858.000000      9.750000\n",
       "50%     1910.000000     16.140000\n",
       "75%     1962.000000     23.762500\n",
       "max     2013.000000     30.730000"
      ]
     },
     "execution_count": 35,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "avg_temp.describe()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "So average temprature starts from 1743 and ends at 2013, with some empty rows that we have to drop."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 36,
   "metadata": {
    "scrolled": true
   },
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
       "      <th>Year</th>\n",
       "      <th>Area</th>\n",
       "      <th>avg_temp</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>1849</td>\n",
       "      <td>C么te D'Ivoire</td>\n",
       "      <td>25.58</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>1850</td>\n",
       "      <td>C么te D'Ivoire</td>\n",
       "      <td>25.52</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>1851</td>\n",
       "      <td>C么te D'Ivoire</td>\n",
       "      <td>25.67</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>1852</td>\n",
       "      <td>C么te D'Ivoire</td>\n",
       "      <td>NaN</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>1853</td>\n",
       "      <td>C么te D'Ivoire</td>\n",
       "      <td>NaN</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   Year           Area  avg_temp\n",
       "0  1849  C么te D'Ivoire     25.58\n",
       "1  1850  C么te D'Ivoire     25.52\n",
       "2  1851  C么te D'Ivoire     25.67\n",
       "3  1852  C么te D'Ivoire       NaN\n",
       "4  1853  C么te D'Ivoire       NaN"
      ]
     },
     "execution_count": 36,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "avg_temp = avg_temp.rename(index=str, columns={\"year\": \"Year\", \"country\":'Area'})\n",
    "avg_temp.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 37,
   "metadata": {
    "scrolled": true
   },
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
       "      <th>Area</th>\n",
       "      <th>Item</th>\n",
       "      <th>Year</th>\n",
       "      <th>hg/ha_yield</th>\n",
       "      <th>average_rain_fall_mm_per_year</th>\n",
       "      <th>pesticides_tonnes</th>\n",
       "      <th>avg_temp</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>Albania</td>\n",
       "      <td>Maize</td>\n",
       "      <td>1990</td>\n",
       "      <td>36613</td>\n",
       "      <td>1485.0</td>\n",
       "      <td>121.0</td>\n",
       "      <td>16.37</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>Albania</td>\n",
       "      <td>Potatoes</td>\n",
       "      <td>1990</td>\n",
       "      <td>66667</td>\n",
       "      <td>1485.0</td>\n",
       "      <td>121.0</td>\n",
       "      <td>16.37</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>Albania</td>\n",
       "      <td>Rice, paddy</td>\n",
       "      <td>1990</td>\n",
       "      <td>23333</td>\n",
       "      <td>1485.0</td>\n",
       "      <td>121.0</td>\n",
       "      <td>16.37</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>Albania</td>\n",
       "      <td>Sorghum</td>\n",
       "      <td>1990</td>\n",
       "      <td>12500</td>\n",
       "      <td>1485.0</td>\n",
       "      <td>121.0</td>\n",
       "      <td>16.37</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Albania</td>\n",
       "      <td>Soybeans</td>\n",
       "      <td>1990</td>\n",
       "      <td>7000</td>\n",
       "      <td>1485.0</td>\n",
       "      <td>121.0</td>\n",
       "      <td>16.37</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "      Area         Item  Year  hg/ha_yield  average_rain_fall_mm_per_year  \\\n",
       "0  Albania        Maize  1990        36613                         1485.0   \n",
       "1  Albania     Potatoes  1990        66667                         1485.0   \n",
       "2  Albania  Rice, paddy  1990        23333                         1485.0   \n",
       "3  Albania      Sorghum  1990        12500                         1485.0   \n",
       "4  Albania     Soybeans  1990         7000                         1485.0   \n",
       "\n",
       "   pesticides_tonnes  avg_temp  \n",
       "0              121.0     16.37  \n",
       "1              121.0     16.37  \n",
       "2              121.0     16.37  \n",
       "3              121.0     16.37  \n",
       "4              121.0     16.37  "
      ]
     },
     "execution_count": 37,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "yield_df = pd.merge(yield_df,avg_temp, on=['Area','Year'])\n",
    "yield_df.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 38,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(28242, 7)"
      ]
     },
     "execution_count": 38,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "yield_df.shape"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 39,
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
       "      <th>Year</th>\n",
       "      <th>hg/ha_yield</th>\n",
       "      <th>average_rain_fall_mm_per_year</th>\n",
       "      <th>pesticides_tonnes</th>\n",
       "      <th>avg_temp</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>count</th>\n",
       "      <td>28242.000000</td>\n",
       "      <td>28242.000000</td>\n",
       "      <td>28242.00000</td>\n",
       "      <td>28242.000000</td>\n",
       "      <td>28242.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>mean</th>\n",
       "      <td>2001.544296</td>\n",
       "      <td>77053.332094</td>\n",
       "      <td>1149.05598</td>\n",
       "      <td>37076.909344</td>\n",
       "      <td>20.542627</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>std</th>\n",
       "      <td>7.051905</td>\n",
       "      <td>84956.612897</td>\n",
       "      <td>709.81215</td>\n",
       "      <td>59958.784665</td>\n",
       "      <td>6.312051</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>min</th>\n",
       "      <td>1990.000000</td>\n",
       "      <td>50.000000</td>\n",
       "      <td>51.00000</td>\n",
       "      <td>0.040000</td>\n",
       "      <td>1.300000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>25%</th>\n",
       "      <td>1995.000000</td>\n",
       "      <td>19919.250000</td>\n",
       "      <td>593.00000</td>\n",
       "      <td>1702.000000</td>\n",
       "      <td>16.702500</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>50%</th>\n",
       "      <td>2001.000000</td>\n",
       "      <td>38295.000000</td>\n",
       "      <td>1083.00000</td>\n",
       "      <td>17529.440000</td>\n",
       "      <td>21.510000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>75%</th>\n",
       "      <td>2008.000000</td>\n",
       "      <td>104676.750000</td>\n",
       "      <td>1668.00000</td>\n",
       "      <td>48687.880000</td>\n",
       "      <td>26.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>max</th>\n",
       "      <td>2013.000000</td>\n",
       "      <td>501412.000000</td>\n",
       "      <td>3240.00000</td>\n",
       "      <td>367778.000000</td>\n",
       "      <td>30.650000</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "               Year    hg/ha_yield  average_rain_fall_mm_per_year  \\\n",
       "count  28242.000000   28242.000000                    28242.00000   \n",
       "mean    2001.544296   77053.332094                     1149.05598   \n",
       "std        7.051905   84956.612897                      709.81215   \n",
       "min     1990.000000      50.000000                       51.00000   \n",
       "25%     1995.000000   19919.250000                      593.00000   \n",
       "50%     2001.000000   38295.000000                     1083.00000   \n",
       "75%     2008.000000  104676.750000                     1668.00000   \n",
       "max     2013.000000  501412.000000                     3240.00000   \n",
       "\n",
       "       pesticides_tonnes      avg_temp  \n",
       "count       28242.000000  28242.000000  \n",
       "mean        37076.909344     20.542627  \n",
       "std         59958.784665      6.312051  \n",
       "min             0.040000      1.300000  \n",
       "25%          1702.000000     16.702500  \n",
       "50%         17529.440000     21.510000  \n",
       "75%         48687.880000     26.000000  \n",
       "max        367778.000000     30.650000  "
      ]
     },
     "execution_count": 39,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "yield_df.describe()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 40,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Area                             0\n",
       "Item                             0\n",
       "Year                             0\n",
       "hg/ha_yield                      0\n",
       "average_rain_fall_mm_per_year    0\n",
       "pesticides_tonnes                0\n",
       "avg_temp                         0\n",
       "dtype: int64"
      ]
     },
     "execution_count": 40,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "yield_df.isnull().sum()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Great, no empty values!"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# Part Two: Data Exploration\n",
    "\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "**yield_df** is the final obtained dataframe; "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 41,
   "metadata": {
    "scrolled": true
   },
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
       "      <th>Area</th>\n",
       "      <th>Year</th>\n",
       "      <th>hg/ha_yield</th>\n",
       "      <th>average_rain_fall_mm_per_year</th>\n",
       "      <th>pesticides_tonnes</th>\n",
       "      <th>avg_temp</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Item</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>Cassava</th>\n",
       "      <td>2045</td>\n",
       "      <td>2045</td>\n",
       "      <td>2045</td>\n",
       "      <td>2045</td>\n",
       "      <td>2045</td>\n",
       "      <td>2045</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Maize</th>\n",
       "      <td>4121</td>\n",
       "      <td>4121</td>\n",
       "      <td>4121</td>\n",
       "      <td>4121</td>\n",
       "      <td>4121</td>\n",
       "      <td>4121</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Plantains and others</th>\n",
       "      <td>556</td>\n",
       "      <td>556</td>\n",
       "      <td>556</td>\n",
       "      <td>556</td>\n",
       "      <td>556</td>\n",
       "      <td>556</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Potatoes</th>\n",
       "      <td>4276</td>\n",
       "      <td>4276</td>\n",
       "      <td>4276</td>\n",
       "      <td>4276</td>\n",
       "      <td>4276</td>\n",
       "      <td>4276</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Rice, paddy</th>\n",
       "      <td>3388</td>\n",
       "      <td>3388</td>\n",
       "      <td>3388</td>\n",
       "      <td>3388</td>\n",
       "      <td>3388</td>\n",
       "      <td>3388</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Sorghum</th>\n",
       "      <td>3039</td>\n",
       "      <td>3039</td>\n",
       "      <td>3039</td>\n",
       "      <td>3039</td>\n",
       "      <td>3039</td>\n",
       "      <td>3039</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Soybeans</th>\n",
       "      <td>3223</td>\n",
       "      <td>3223</td>\n",
       "      <td>3223</td>\n",
       "      <td>3223</td>\n",
       "      <td>3223</td>\n",
       "      <td>3223</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Sweet potatoes</th>\n",
       "      <td>2890</td>\n",
       "      <td>2890</td>\n",
       "      <td>2890</td>\n",
       "      <td>2890</td>\n",
       "      <td>2890</td>\n",
       "      <td>2890</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Wheat</th>\n",
       "      <td>3857</td>\n",
       "      <td>3857</td>\n",
       "      <td>3857</td>\n",
       "      <td>3857</td>\n",
       "      <td>3857</td>\n",
       "      <td>3857</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Yams</th>\n",
       "      <td>847</td>\n",
       "      <td>847</td>\n",
       "      <td>847</td>\n",
       "      <td>847</td>\n",
       "      <td>847</td>\n",
       "      <td>847</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                      Area  Year  hg/ha_yield  average_rain_fall_mm_per_year  \\\n",
       "Item                                                                           \n",
       "Cassava               2045  2045         2045                           2045   \n",
       "Maize                 4121  4121         4121                           4121   \n",
       "Plantains and others   556   556          556                            556   \n",
       "Potatoes              4276  4276         4276                           4276   \n",
       "Rice, paddy           3388  3388         3388                           3388   \n",
       "Sorghum               3039  3039         3039                           3039   \n",
       "Soybeans              3223  3223         3223                           3223   \n",
       "Sweet potatoes        2890  2890         2890                           2890   \n",
       "Wheat                 3857  3857         3857                           3857   \n",
       "Yams                   847   847          847                            847   \n",
       "\n",
       "                      pesticides_tonnes  avg_temp  \n",
       "Item                                               \n",
       "Cassava                            2045      2045  \n",
       "Maize                              4121      4121  \n",
       "Plantains and others                556       556  \n",
       "Potatoes                           4276      4276  \n",
       "Rice, paddy                        3388      3388  \n",
       "Sorghum                            3039      3039  \n",
       "Soybeans                           3223      3223  \n",
       "Sweet potatoes                     2890      2890  \n",
       "Wheat                              3857      3857  \n",
       "Yams                                847       847  "
      ]
     },
     "execution_count": 41,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "yield_df.groupby('Item').count()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 42,
   "metadata": {
    "scrolled": false
   },
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
       "      <th>Year</th>\n",
       "      <th>hg/ha_yield</th>\n",
       "      <th>average_rain_fall_mm_per_year</th>\n",
       "      <th>pesticides_tonnes</th>\n",
       "      <th>avg_temp</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>count</th>\n",
       "      <td>28242.000000</td>\n",
       "      <td>28242.000000</td>\n",
       "      <td>28242.00000</td>\n",
       "      <td>28242.000000</td>\n",
       "      <td>28242.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>mean</th>\n",
       "      <td>2001.544296</td>\n",
       "      <td>77053.332094</td>\n",
       "      <td>1149.05598</td>\n",
       "      <td>37076.909344</td>\n",
       "      <td>20.542627</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>std</th>\n",
       "      <td>7.051905</td>\n",
       "      <td>84956.612897</td>\n",
       "      <td>709.81215</td>\n",
       "      <td>59958.784665</td>\n",
       "      <td>6.312051</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>min</th>\n",
       "      <td>1990.000000</td>\n",
       "      <td>50.000000</td>\n",
       "      <td>51.00000</td>\n",
       "      <td>0.040000</td>\n",
       "      <td>1.300000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>25%</th>\n",
       "      <td>1995.000000</td>\n",
       "      <td>19919.250000</td>\n",
       "      <td>593.00000</td>\n",
       "      <td>1702.000000</td>\n",
       "      <td>16.702500</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>50%</th>\n",
       "      <td>2001.000000</td>\n",
       "      <td>38295.000000</td>\n",
       "      <td>1083.00000</td>\n",
       "      <td>17529.440000</td>\n",
       "      <td>21.510000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>75%</th>\n",
       "      <td>2008.000000</td>\n",
       "      <td>104676.750000</td>\n",
       "      <td>1668.00000</td>\n",
       "      <td>48687.880000</td>\n",
       "      <td>26.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>max</th>\n",
       "      <td>2013.000000</td>\n",
       "      <td>501412.000000</td>\n",
       "      <td>3240.00000</td>\n",
       "      <td>367778.000000</td>\n",
       "      <td>30.650000</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "               Year    hg/ha_yield  average_rain_fall_mm_per_year  \\\n",
       "count  28242.000000   28242.000000                    28242.00000   \n",
       "mean    2001.544296   77053.332094                     1149.05598   \n",
       "std        7.051905   84956.612897                      709.81215   \n",
       "min     1990.000000      50.000000                       51.00000   \n",
       "25%     1995.000000   19919.250000                      593.00000   \n",
       "50%     2001.000000   38295.000000                     1083.00000   \n",
       "75%     2008.000000  104676.750000                     1668.00000   \n",
       "max     2013.000000  501412.000000                     3240.00000   \n",
       "\n",
       "       pesticides_tonnes      avg_temp  \n",
       "count       28242.000000  28242.000000  \n",
       "mean        37076.909344     20.542627  \n",
       "std         59958.784665      6.312051  \n",
       "min             0.040000      1.300000  \n",
       "25%          1702.000000     16.702500  \n",
       "50%         17529.440000     21.510000  \n",
       "75%         48687.880000     26.000000  \n",
       "max        367778.000000     30.650000  "
      ]
     },
     "execution_count": 42,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "yield_df.describe()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "It can be noticed the high variance in the values for each columns, later on I'll account for that will scaling. "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 43,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "101"
      ]
     },
     "execution_count": 43,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "yield_df['Area'].nunique()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "The dataframe has 101 Countries, ordering these by 10 the highest yield production: "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 44,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Area\n",
       "India             327420324\n",
       "Brazil            167550306\n",
       "Mexico            130788528\n",
       "Japan             124470912\n",
       "Australia         109111062\n",
       "Pakistan           73897434\n",
       "Indonesia          69193506\n",
       "United Kingdom     55419990\n",
       "Turkey             52263950\n",
       "Spain              46773540\n",
       "Name: hg/ha_yield, dtype: int64"
      ]
     },
     "execution_count": 44,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "yield_df.groupby(['Area'],sort=True)['hg/ha_yield'].sum().nlargest(10)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "India has the highest yield production in the dataset. Inclusing items in the groupby:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 45,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Item            Area          \n",
       "Cassava         India             142810624\n",
       "Potatoes        India              92122514\n",
       "                Brazil             49602168\n",
       "                United Kingdom     46705145\n",
       "                Australia          45670386\n",
       "Sweet potatoes  India              44439538\n",
       "Potatoes        Japan              42918726\n",
       "                Mexico             42053880\n",
       "Sweet potatoes  Mexico             35808592\n",
       "                Australia          35550294\n",
       "Name: hg/ha_yield, dtype: int64"
      ]
     },
     "execution_count": 45,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "yield_df.groupby(['Item','Area'],sort=True)['hg/ha_yield'].sum().nlargest(10)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "India is the highest for production of cassava and potatoes. Potatoes seems to be the dominated crop in the dataset, being the highest in 4 countries. "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "The final dataframe starts from 1990 and ends in 2013, that's 23 years worth of data for 101 countries. "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Now, exploring the relationships between the colunms of the dataframe, a good way to quickly check correlations among columns is by visualizing the correlation matrix as a heatmap."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 46,
   "metadata": {},
   "outputs": [],
   "source": [
    "import sklearn\n",
    "import seaborn as sns\n",
    "import matplotlib.pyplot as plt"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 47,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 792x648 with 2 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "correlation_data=yield_df.select_dtypes(include=[np.number]).corr()\n",
    "\n",
    "mask = np.zeros_like(correlation_data, dtype=np.bool)\n",
    "mask[np.triu_indices_from(mask)] = True\n",
    "\n",
    "f, ax = plt.subplots(figsize=(11, 9))\n",
    "\n",
    "# Generate a custom diverging colormap\n",
    "cmap = sns.palette=\"vlag\"\n",
    "\n",
    "# Draw the heatmap with the mask and correct aspect ratio\n",
    "sns.heatmap(correlation_data, mask=mask, cmap=cmap, vmax=.3, center=0,\n",
    "            square=True, linewidths=.5, cbar_kws={\"shrink\": .5});"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "It can be seen from the above correlation map that there is no correlation between any of the colmuns in the dataframe. "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# Part Three: Data Preprocessing"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Data Preprocessing is a technique that is used to convert the raw data into a clean data set. In other words, whenever the data is gathered from different sources it is collected in raw format which is not feasible for the analysis.  \n",
    "\n",
    "\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 48,
   "metadata": {
    "scrolled": true
   },
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
       "      <th>Area</th>\n",
       "      <th>Item</th>\n",
       "      <th>Year</th>\n",
       "      <th>hg/ha_yield</th>\n",
       "      <th>average_rain_fall_mm_per_year</th>\n",
       "      <th>pesticides_tonnes</th>\n",
       "      <th>avg_temp</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>Albania</td>\n",
       "      <td>Maize</td>\n",
       "      <td>1990</td>\n",
       "      <td>36613</td>\n",
       "      <td>1485.0</td>\n",
       "      <td>121.0</td>\n",
       "      <td>16.37</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>Albania</td>\n",
       "      <td>Potatoes</td>\n",
       "      <td>1990</td>\n",
       "      <td>66667</td>\n",
       "      <td>1485.0</td>\n",
       "      <td>121.0</td>\n",
       "      <td>16.37</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>Albania</td>\n",
       "      <td>Rice, paddy</td>\n",
       "      <td>1990</td>\n",
       "      <td>23333</td>\n",
       "      <td>1485.0</td>\n",
       "      <td>121.0</td>\n",
       "      <td>16.37</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>Albania</td>\n",
       "      <td>Sorghum</td>\n",
       "      <td>1990</td>\n",
       "      <td>12500</td>\n",
       "      <td>1485.0</td>\n",
       "      <td>121.0</td>\n",
       "      <td>16.37</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Albania</td>\n",
       "      <td>Soybeans</td>\n",
       "      <td>1990</td>\n",
       "      <td>7000</td>\n",
       "      <td>1485.0</td>\n",
       "      <td>121.0</td>\n",
       "      <td>16.37</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "      Area         Item  Year  hg/ha_yield  average_rain_fall_mm_per_year  \\\n",
       "0  Albania        Maize  1990        36613                         1485.0   \n",
       "1  Albania     Potatoes  1990        66667                         1485.0   \n",
       "2  Albania  Rice, paddy  1990        23333                         1485.0   \n",
       "3  Albania      Sorghum  1990        12500                         1485.0   \n",
       "4  Albania     Soybeans  1990         7000                         1485.0   \n",
       "\n",
       "   pesticides_tonnes  avg_temp  \n",
       "0              121.0     16.37  \n",
       "1              121.0     16.37  \n",
       "2              121.0     16.37  \n",
       "3              121.0     16.37  \n",
       "4              121.0     16.37  "
      ]
     },
     "execution_count": 48,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "yield_df.head()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Encoding Categorical Variables:\n",
    "There are two categorical columns in the dataframe, categorical data are variables that contain label values rather than numeric values. The number of possible values is often limited to a fixed set, like in this case, items and countries values.\n",
    "Many machine learning algorithms cannot operate on label data directly. They require all input variables and output variables to be numeric.\n",
    "\n",
    "This means that categorical data must be converted to a numerical form. One hot encoding is a process by which categorical variables are converted into a form that could be provided to ML algorithms to do a better job in prediction. For that purpose, One-Hot Encoding will be used to convert these two columns to one-hot numeric array.\n",
    "\n",
    "The categorical value represents the numerical value of the entry in the dataset. This encoding will create a binary column for each category and returns a matrix with the results. \n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 49,
   "metadata": {},
   "outputs": [],
   "source": [
    "from sklearn.preprocessing import OneHotEncoder"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 50,
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
       "      <th>Year</th>\n",
       "      <th>average_rain_fall_mm_per_year</th>\n",
       "      <th>pesticides_tonnes</th>\n",
       "      <th>avg_temp</th>\n",
       "      <th>Country_Albania</th>\n",
       "      <th>Country_Algeria</th>\n",
       "      <th>Country_Angola</th>\n",
       "      <th>Country_Argentina</th>\n",
       "      <th>Country_Armenia</th>\n",
       "      <th>Country_Australia</th>\n",
       "      <th>...</th>\n",
       "      <th>Item_Cassava</th>\n",
       "      <th>Item_Maize</th>\n",
       "      <th>Item_Plantains and others</th>\n",
       "      <th>Item_Potatoes</th>\n",
       "      <th>Item_Rice, paddy</th>\n",
       "      <th>Item_Sorghum</th>\n",
       "      <th>Item_Soybeans</th>\n",
       "      <th>Item_Sweet potatoes</th>\n",
       "      <th>Item_Wheat</th>\n",
       "      <th>Item_Yams</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>1990</td>\n",
       "      <td>1485.0</td>\n",
       "      <td>121.0</td>\n",
       "      <td>16.37</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>...</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>1990</td>\n",
       "      <td>1485.0</td>\n",
       "      <td>121.0</td>\n",
       "      <td>16.37</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>...</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>1990</td>\n",
       "      <td>1485.0</td>\n",
       "      <td>121.0</td>\n",
       "      <td>16.37</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>...</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>1990</td>\n",
       "      <td>1485.0</td>\n",
       "      <td>121.0</td>\n",
       "      <td>16.37</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>...</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>1990</td>\n",
       "      <td>1485.0</td>\n",
       "      <td>121.0</td>\n",
       "      <td>16.37</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>...</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>5 rows 脳 115 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "   Year  average_rain_fall_mm_per_year  pesticides_tonnes  avg_temp  \\\n",
       "0  1990                         1485.0              121.0     16.37   \n",
       "1  1990                         1485.0              121.0     16.37   \n",
       "2  1990                         1485.0              121.0     16.37   \n",
       "3  1990                         1485.0              121.0     16.37   \n",
       "4  1990                         1485.0              121.0     16.37   \n",
       "\n",
       "   Country_Albania  Country_Algeria  Country_Angola  Country_Argentina  \\\n",
       "0                1                0               0                  0   \n",
       "1                1                0               0                  0   \n",
       "2                1                0               0                  0   \n",
       "3                1                0               0                  0   \n",
       "4                1                0               0                  0   \n",
       "\n",
       "   Country_Armenia  Country_Australia  ...  Item_Cassava  Item_Maize  \\\n",
       "0                0                  0  ...             0           1   \n",
       "1                0                  0  ...             0           0   \n",
       "2                0                  0  ...             0           0   \n",
       "3                0                  0  ...             0           0   \n",
       "4                0                  0  ...             0           0   \n",
       "\n",
       "   Item_Plantains and others  Item_Potatoes  Item_Rice, paddy  Item_Sorghum  \\\n",
       "0                          0              0                 0             0   \n",
       "1                          0              1                 0             0   \n",
       "2                          0              0                 1             0   \n",
       "3                          0              0                 0             1   \n",
       "4                          0              0                 0             0   \n",
       "\n",
       "   Item_Soybeans  Item_Sweet potatoes  Item_Wheat  Item_Yams  \n",
       "0              0                    0           0          0  \n",
       "1              0                    0           0          0  \n",
       "2              0                    0           0          0  \n",
       "3              0                    0           0          0  \n",
       "4              1                    0           0          0  \n",
       "\n",
       "[5 rows x 115 columns]"
      ]
     },
     "execution_count": 50,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "yield_df_onehot = pd.get_dummies(yield_df, columns=['Area',\"Item\"], prefix = ['Country',\"Item\"])\n",
    "features=yield_df_onehot.loc[:, yield_df_onehot.columns != 'hg/ha_yield']\n",
    "label=yield_df['hg/ha_yield']\n",
    "features.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 51,
   "metadata": {},
   "outputs": [],
   "source": [
    "features = features.drop(['Year'], axis=1)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 52,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "<class 'pandas.core.frame.DataFrame'>\n",
      "Int64Index: 28242 entries, 0 to 28241\n",
      "Columns: 114 entries, average_rain_fall_mm_per_year to Item_Yams\n",
      "dtypes: float64(3), uint8(111)\n",
      "memory usage: 3.9 MB\n"
     ]
    }
   ],
   "source": [
    "features.info()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 53,
   "metadata": {
    "scrolled": true
   },
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
       "      <th>average_rain_fall_mm_per_year</th>\n",
       "      <th>pesticides_tonnes</th>\n",
       "      <th>avg_temp</th>\n",
       "      <th>Country_Albania</th>\n",
       "      <th>Country_Algeria</th>\n",
       "      <th>Country_Angola</th>\n",
       "      <th>Country_Argentina</th>\n",
       "      <th>Country_Armenia</th>\n",
       "      <th>Country_Australia</th>\n",
       "      <th>Country_Austria</th>\n",
       "      <th>...</th>\n",
       "      <th>Item_Cassava</th>\n",
       "      <th>Item_Maize</th>\n",
       "      <th>Item_Plantains and others</th>\n",
       "      <th>Item_Potatoes</th>\n",
       "      <th>Item_Rice, paddy</th>\n",
       "      <th>Item_Sorghum</th>\n",
       "      <th>Item_Soybeans</th>\n",
       "      <th>Item_Sweet potatoes</th>\n",
       "      <th>Item_Wheat</th>\n",
       "      <th>Item_Yams</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>1485.0</td>\n",
       "      <td>121.0</td>\n",
       "      <td>16.37</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>...</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>1485.0</td>\n",
       "      <td>121.0</td>\n",
       "      <td>16.37</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>...</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>1485.0</td>\n",
       "      <td>121.0</td>\n",
       "      <td>16.37</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>...</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>1485.0</td>\n",
       "      <td>121.0</td>\n",
       "      <td>16.37</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>...</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>1485.0</td>\n",
       "      <td>121.0</td>\n",
       "      <td>16.37</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>...</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>5 rows 脳 114 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "   average_rain_fall_mm_per_year  pesticides_tonnes  avg_temp  \\\n",
       "0                         1485.0              121.0     16.37   \n",
       "1                         1485.0              121.0     16.37   \n",
       "2                         1485.0              121.0     16.37   \n",
       "3                         1485.0              121.0     16.37   \n",
       "4                         1485.0              121.0     16.37   \n",
       "\n",
       "   Country_Albania  Country_Algeria  Country_Angola  Country_Argentina  \\\n",
       "0                1                0               0                  0   \n",
       "1                1                0               0                  0   \n",
       "2                1                0               0                  0   \n",
       "3                1                0               0                  0   \n",
       "4                1                0               0                  0   \n",
       "\n",
       "   Country_Armenia  Country_Australia  Country_Austria  ...  Item_Cassava  \\\n",
       "0                0                  0                0  ...             0   \n",
       "1                0                  0                0  ...             0   \n",
       "2                0                  0                0  ...             0   \n",
       "3                0                  0                0  ...             0   \n",
       "4                0                  0                0  ...             0   \n",
       "\n",
       "   Item_Maize  Item_Plantains and others  Item_Potatoes  Item_Rice, paddy  \\\n",
       "0           1                          0              0                 0   \n",
       "1           0                          0              1                 0   \n",
       "2           0                          0              0                 1   \n",
       "3           0                          0              0                 0   \n",
       "4           0                          0              0                 0   \n",
       "\n",
       "   Item_Sorghum  Item_Soybeans  Item_Sweet potatoes  Item_Wheat  Item_Yams  \n",
       "0             0              0                    0           0          0  \n",
       "1             0              0                    0           0          0  \n",
       "2             0              0                    0           0          0  \n",
       "3             1              0                    0           0          0  \n",
       "4             0              1                    0           0          0  \n",
       "\n",
       "[5 rows x 114 columns]"
      ]
     },
     "execution_count": 53,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "features.head()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "\n",
    "### Scaling Features: \n",
    "\n",
    "Taking a look at the dataset above, it contains features highly varying in magnitudes, units and range. The features with high magnitudes will weigh in a lot more in the distance calculations than features with low magnitudes.\n",
    "\n",
    "To supress this effect, we need to bring all features to the same level of magnitudes. This can be acheived by scaling."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 54,
   "metadata": {},
   "outputs": [],
   "source": [
    "from sklearn.preprocessing import MinMaxScaler\n",
    "scaler=MinMaxScaler()\n",
    "features=scaler.fit_transform(features) "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "After dropping year column in addition to scaling all values in features, the resulting array will look something like this : "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 55,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "array([[4.49670743e-01, 3.28894097e-04, 5.13458262e-01, ...,\n",
       "        0.00000000e+00, 0.00000000e+00, 0.00000000e+00],\n",
       "       [4.49670743e-01, 3.28894097e-04, 5.13458262e-01, ...,\n",
       "        0.00000000e+00, 0.00000000e+00, 0.00000000e+00],\n",
       "       [4.49670743e-01, 3.28894097e-04, 5.13458262e-01, ...,\n",
       "        0.00000000e+00, 0.00000000e+00, 0.00000000e+00],\n",
       "       ...,\n",
       "       [1.90028222e-01, 6.93361288e-03, 6.28960818e-01, ...,\n",
       "        0.00000000e+00, 0.00000000e+00, 0.00000000e+00],\n",
       "       [1.90028222e-01, 6.93361288e-03, 6.28960818e-01, ...,\n",
       "        1.00000000e+00, 0.00000000e+00, 0.00000000e+00],\n",
       "       [1.90028222e-01, 6.93361288e-03, 6.28960818e-01, ...,\n",
       "        0.00000000e+00, 1.00000000e+00, 0.00000000e+00]])"
      ]
     },
     "execution_count": 55,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "features"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Training Data: \n",
    "\n",
    "The dataset will be split to two datasets, the training dataset and test dataset. The data is usually tend to be split inequality because training the model usually requires as much data-points as possible.The common splits are 70/30 or 80/20 for train/test.\n",
    "\n",
    "The training dataset is the intial dataset used to train ML algorithm to learn and produce right predictions. (70% of dataset is training dataset)\n",
    "\n",
    "The test dataset, however, is used to assess how well ML algorithm is trained with the training dataset. You can鈥檛 simply reuse the training dataset in the testing stage because ML algorithm will already 鈥渒now鈥� the expected output, which defeats the purpose of testing the algorithm. (30% of dataset is testing dataset) \n",
    "\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 56,
   "metadata": {},
   "outputs": [],
   "source": [
    "from sklearn.model_selection import train_test_split\n",
    "train_data, test_data, train_labels, test_labels = train_test_split(features, label, test_size=0.3, random_state=42)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 57,
   "metadata": {},
   "outputs": [],
   "source": [
    "#write final df to csv file \n",
    "yield_df.to_csv('yield_df.csv')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 58,
   "metadata": {},
   "outputs": [],
   "source": [
    "from sklearn.model_selection import train_test_split\n",
    "train_data, test_data, train_labels, test_labels = train_test_split(features, label, test_size=0.3, random_state=42)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# Part Four: Model Comparison & Selection \n",
    "\n",
    "Before deciding on an algorithem to use, first we need to evaluate, compare and choose the best one that fits this specific dataset.\n",
    "\n",
    "Usually, when working on a machine learning problem with a given dataset, we try different models and techniques to solve an optimization problem and fit the most accurate model, that will neither overfit nor underfit the model. \n",
    " \n",
    "For this project, we'll compare between the following models : \n",
    "\n",
    "- Gradient Boosting Regressor\n",
    "- Random Forest Regressor\n",
    "- SVM \n",
    "- Decision Tree Regressor\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 59,
   "metadata": {},
   "outputs": [],
   "source": [
    "from sklearn.metrics import r2_score\n",
    "def compare_models(model):\n",
    "    model_name = model.__class__.__name__\n",
    "    fit=model.fit(train_data,train_labels)\n",
    "    y_pred=fit.predict(test_data)\n",
    "    r2=r2_score(test_labels,y_pred)\n",
    "    return([model_name,r2])"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 60,
   "metadata": {},
   "outputs": [],
   "source": [
    "from sklearn.ensemble import RandomForestRegressor\n",
    "from sklearn.ensemble import GradientBoostingRegressor\n",
    "from sklearn import svm\n",
    "from sklearn.tree import DecisionTreeRegressor\n",
    "\n",
    "models = [\n",
    "    GradientBoostingRegressor(n_estimators=200, max_depth=3, random_state=0),\n",
    "     RandomForestRegressor(n_estimators=200, max_depth=3, random_state=0),\n",
    "    svm.SVR(),\n",
    "   DecisionTreeRegressor()\n",
    "]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 61,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "C:\\Users\\hajiralmahdi\\AppData\\Local\\Continuum\\anaconda3\\lib\\site-packages\\sklearn\\svm\\base.py:193: FutureWarning: The default value of gamma will change from 'auto' to 'scale' in version 0.22 to account better for unscaled features. Set gamma explicitly to 'auto' or 'scale' to avoid this warning.\n",
      "  \"avoid this warning.\", FutureWarning)\n"
     ]
    }
   ],
   "source": [
    "model_train=list(map(compare_models,models)) "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 62,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "['GradientBoostingRegressor', 0.8965731164462923]\n",
      "['RandomForestRegressor', 0.6842532317855172]\n",
      "['SVR', -0.20353376480360752]\n",
      "['DecisionTreeRegressor', 0.9590644980817136]\n"
     ]
    }
   ],
   "source": [
    "print(*model_train, sep = \"\\n\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "The evaluation metric is set based on **R^2 (coefficient of determination)** regression score function, that will represents the proportion of the variance for items (crops) in the regression model. **R^2** score shows how well terms (data points) fit a curve or line.\n",
    "\n",
    "**R^2** is a statistical measure between 0 and 1 which calculates how similar a regression line is to the data it鈥檚 fitted to. If it鈥檚 a 1, the model 100% predicts the data variance; if it鈥檚 a 0, the model predicts none of the variance. \n",
    "\n",
    "From results viewd above, **Decision Tree Regressor** has the highest R^2 score 0f **96%**, **GradientBoostingRegressor** comes second. \n",
    "\n",
    "\n",
    " I'll also calculate **Adjusted R^2** also indicates how well terms fit a curve or line, but adjusts for the number of terms in a model. If you add more and more useless variables to a model, adjusted r-squared will decrease. If you add more useful variables, adjusted r-squared will increase.\n",
    "Adjusted R2 will always be less than or equal to R2. "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 63,
   "metadata": {},
   "outputs": [],
   "source": [
    "yield_df_onehot = yield_df_onehot.drop(['Year'], axis=1)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 64,
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
       "      <th>hg/ha_yield</th>\n",
       "      <th>average_rain_fall_mm_per_year</th>\n",
       "      <th>pesticides_tonnes</th>\n",
       "      <th>avg_temp</th>\n",
       "      <th>Country_Albania</th>\n",
       "      <th>Country_Algeria</th>\n",
       "      <th>Country_Angola</th>\n",
       "      <th>Country_Argentina</th>\n",
       "      <th>Country_Armenia</th>\n",
       "      <th>Country_Australia</th>\n",
       "      <th>...</th>\n",
       "      <th>Item_Cassava</th>\n",
       "      <th>Item_Maize</th>\n",
       "      <th>Item_Plantains and others</th>\n",
       "      <th>Item_Potatoes</th>\n",
       "      <th>Item_Rice, paddy</th>\n",
       "      <th>Item_Sorghum</th>\n",
       "      <th>Item_Soybeans</th>\n",
       "      <th>Item_Sweet potatoes</th>\n",
       "      <th>Item_Wheat</th>\n",
       "      <th>Item_Yams</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>36613</td>\n",
       "      <td>1485.0</td>\n",
       "      <td>121.0</td>\n",
       "      <td>16.37</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>...</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>66667</td>\n",
       "      <td>1485.0</td>\n",
       "      <td>121.0</td>\n",
       "      <td>16.37</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>...</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>23333</td>\n",
       "      <td>1485.0</td>\n",
       "      <td>121.0</td>\n",
       "      <td>16.37</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>...</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>12500</td>\n",
       "      <td>1485.0</td>\n",
       "      <td>121.0</td>\n",
       "      <td>16.37</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>...</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>7000</td>\n",
       "      <td>1485.0</td>\n",
       "      <td>121.0</td>\n",
       "      <td>16.37</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>...</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>5 rows 脳 115 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "   hg/ha_yield  average_rain_fall_mm_per_year  pesticides_tonnes  avg_temp  \\\n",
       "0        36613                         1485.0              121.0     16.37   \n",
       "1        66667                         1485.0              121.0     16.37   \n",
       "2        23333                         1485.0              121.0     16.37   \n",
       "3        12500                         1485.0              121.0     16.37   \n",
       "4         7000                         1485.0              121.0     16.37   \n",
       "\n",
       "   Country_Albania  Country_Algeria  Country_Angola  Country_Argentina  \\\n",
       "0                1                0               0                  0   \n",
       "1                1                0               0                  0   \n",
       "2                1                0               0                  0   \n",
       "3                1                0               0                  0   \n",
       "4                1                0               0                  0   \n",
       "\n",
       "   Country_Armenia  Country_Australia  ...  Item_Cassava  Item_Maize  \\\n",
       "0                0                  0  ...             0           1   \n",
       "1                0                  0  ...             0           0   \n",
       "2                0                  0  ...             0           0   \n",
       "3                0                  0  ...             0           0   \n",
       "4                0                  0  ...             0           0   \n",
       "\n",
       "   Item_Plantains and others  Item_Potatoes  Item_Rice, paddy  Item_Sorghum  \\\n",
       "0                          0              0                 0             0   \n",
       "1                          0              1                 0             0   \n",
       "2                          0              0                 1             0   \n",
       "3                          0              0                 0             1   \n",
       "4                          0              0                 0             0   \n",
       "\n",
       "   Item_Soybeans  Item_Sweet potatoes  Item_Wheat  Item_Yams  \n",
       "0              0                    0           0          0  \n",
       "1              0                    0           0          0  \n",
       "2              0                    0           0          0  \n",
       "3              0                    0           0          0  \n",
       "4              1                    0           0          0  \n",
       "\n",
       "[5 rows x 115 columns]"
      ]
     },
     "execution_count": 64,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "yield_df_onehot.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 65,
   "metadata": {},
   "outputs": [],
   "source": [
    "#setting test data to columns from dataframe and excluding 'hg/ha_yield' values where ML model should be predicting \n",
    "\n",
    "test_df=pd.DataFrame(test_data,columns=yield_df_onehot.loc[:, yield_df_onehot.columns != 'hg/ha_yield'].columns) \n",
    "\n",
    "# using stack function to return a reshaped DataFrame by pivoting the columns of the current dataframe\n",
    "\n",
    "cntry=test_df[[col for col in test_df.columns if 'Country' in col]].stack()[test_df[[col for col in test_df.columns if 'Country' in col]].stack()>0]\n",
    "cntrylist=list(pd.DataFrame(cntry).index.get_level_values(1))\n",
    "countries=[i.split(\"_\")[1] for i in cntrylist]\n",
    "itm=test_df[[col for col in test_df.columns if 'Item' in col]].stack()[test_df[[col for col in test_df.columns if 'Item' in col]].stack()>0]\n",
    "itmlist=list(pd.DataFrame(itm).index.get_level_values(1))\n",
    "items=[i.split(\"_\")[1] for i in itmlist]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 66,
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
       "      <th>average_rain_fall_mm_per_year</th>\n",
       "      <th>pesticides_tonnes</th>\n",
       "      <th>avg_temp</th>\n",
       "      <th>Country_Albania</th>\n",
       "      <th>Country_Algeria</th>\n",
       "      <th>Country_Angola</th>\n",
       "      <th>Country_Argentina</th>\n",
       "      <th>Country_Armenia</th>\n",
       "      <th>Country_Australia</th>\n",
       "      <th>Country_Austria</th>\n",
       "      <th>...</th>\n",
       "      <th>Item_Cassava</th>\n",
       "      <th>Item_Maize</th>\n",
       "      <th>Item_Plantains and others</th>\n",
       "      <th>Item_Potatoes</th>\n",
       "      <th>Item_Rice, paddy</th>\n",
       "      <th>Item_Sorghum</th>\n",
       "      <th>Item_Soybeans</th>\n",
       "      <th>Item_Sweet potatoes</th>\n",
       "      <th>Item_Wheat</th>\n",
       "      <th>Item_Yams</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>0.183443</td>\n",
       "      <td>0.110716</td>\n",
       "      <td>0.542078</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>...</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>0.458451</td>\n",
       "      <td>0.000413</td>\n",
       "      <td>0.627257</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>...</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>0.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>0.183443</td>\n",
       "      <td>0.106159</td>\n",
       "      <td>0.518228</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>...</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.224154</td>\n",
       "      <td>0.890971</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>...</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>0.458451</td>\n",
       "      <td>0.000355</td>\n",
       "      <td>0.625213</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>...</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>5 rows 脳 114 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "   average_rain_fall_mm_per_year  pesticides_tonnes  avg_temp  \\\n",
       "0                       0.183443           0.110716  0.542078   \n",
       "1                       0.458451           0.000413  0.627257   \n",
       "2                       0.183443           0.106159  0.518228   \n",
       "3                       1.000000           0.224154  0.890971   \n",
       "4                       0.458451           0.000355  0.625213   \n",
       "\n",
       "   Country_Albania  Country_Algeria  Country_Angola  Country_Argentina  \\\n",
       "0              0.0              0.0             0.0                0.0   \n",
       "1              0.0              0.0             0.0                0.0   \n",
       "2              0.0              0.0             0.0                0.0   \n",
       "3              0.0              0.0             0.0                0.0   \n",
       "4              0.0              0.0             0.0                0.0   \n",
       "\n",
       "   Country_Armenia  Country_Australia  Country_Austria  ...  Item_Cassava  \\\n",
       "0              0.0                0.0              0.0  ...           0.0   \n",
       "1              0.0                0.0              0.0  ...           0.0   \n",
       "2              0.0                0.0              0.0  ...           0.0   \n",
       "3              0.0                0.0              0.0  ...           0.0   \n",
       "4              0.0                0.0              0.0  ...           0.0   \n",
       "\n",
       "   Item_Maize  Item_Plantains and others  Item_Potatoes  Item_Rice, paddy  \\\n",
       "0         0.0                        0.0            0.0               1.0   \n",
       "1         0.0                        0.0            0.0               0.0   \n",
       "2         0.0                        0.0            0.0               0.0   \n",
       "3         0.0                        0.0            1.0               0.0   \n",
       "4         0.0                        0.0            0.0               0.0   \n",
       "\n",
       "   Item_Sorghum  Item_Soybeans  Item_Sweet potatoes  Item_Wheat  Item_Yams  \n",
       "0           0.0            0.0                  0.0         0.0        0.0  \n",
       "1           0.0            0.0                  0.0         1.0        0.0  \n",
       "2           1.0            0.0                  0.0         0.0        0.0  \n",
       "3           0.0            0.0                  0.0         0.0        0.0  \n",
       "4           0.0            0.0                  1.0         0.0        0.0  \n",
       "\n",
       "[5 rows x 114 columns]"
      ]
     },
     "execution_count": 66,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "test_df.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 67,
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
       "      <th>average_rain_fall_mm_per_year</th>\n",
       "      <th>pesticides_tonnes</th>\n",
       "      <th>avg_temp</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>0.183443</td>\n",
       "      <td>0.110716</td>\n",
       "      <td>0.542078</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>0.458451</td>\n",
       "      <td>0.000413</td>\n",
       "      <td>0.627257</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>0.183443</td>\n",
       "      <td>0.106159</td>\n",
       "      <td>0.518228</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.224154</td>\n",
       "      <td>0.890971</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>0.458451</td>\n",
       "      <td>0.000355</td>\n",
       "      <td>0.625213</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   average_rain_fall_mm_per_year  pesticides_tonnes  avg_temp\n",
       "0                       0.183443           0.110716  0.542078\n",
       "1                       0.458451           0.000413  0.627257\n",
       "2                       0.183443           0.106159  0.518228\n",
       "3                       1.000000           0.224154  0.890971\n",
       "4                       0.458451           0.000355  0.625213"
      ]
     },
     "execution_count": 67,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "test_df.drop([col for col in test_df.columns if 'Item' in col],axis=1,inplace=True)\n",
    "test_df.drop([col for col in test_df.columns if 'Country' in col],axis=1,inplace=True)\n",
    "test_df.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 68,
   "metadata": {
    "scrolled": true
   },
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
       "      <th>average_rain_fall_mm_per_year</th>\n",
       "      <th>pesticides_tonnes</th>\n",
       "      <th>avg_temp</th>\n",
       "      <th>Country</th>\n",
       "      <th>Item</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>0.183443</td>\n",
       "      <td>0.110716</td>\n",
       "      <td>0.542078</td>\n",
       "      <td>Spain</td>\n",
       "      <td>Rice, paddy</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>0.458451</td>\n",
       "      <td>0.000413</td>\n",
       "      <td>0.627257</td>\n",
       "      <td>Madagascar</td>\n",
       "      <td>Wheat</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>0.183443</td>\n",
       "      <td>0.106159</td>\n",
       "      <td>0.518228</td>\n",
       "      <td>Spain</td>\n",
       "      <td>Sorghum</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.224154</td>\n",
       "      <td>0.890971</td>\n",
       "      <td>Colombia</td>\n",
       "      <td>Potatoes</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>0.458451</td>\n",
       "      <td>0.000355</td>\n",
       "      <td>0.625213</td>\n",
       "      <td>Madagascar</td>\n",
       "      <td>Sweet potatoes</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   average_rain_fall_mm_per_year  pesticides_tonnes  avg_temp     Country  \\\n",
       "0                       0.183443           0.110716  0.542078       Spain   \n",
       "1                       0.458451           0.000413  0.627257  Madagascar   \n",
       "2                       0.183443           0.106159  0.518228       Spain   \n",
       "3                       1.000000           0.224154  0.890971    Colombia   \n",
       "4                       0.458451           0.000355  0.625213  Madagascar   \n",
       "\n",
       "             Item  \n",
       "0     Rice, paddy  \n",
       "1           Wheat  \n",
       "2         Sorghum  \n",
       "3        Potatoes  \n",
       "4  Sweet potatoes  "
      ]
     },
     "execution_count": 68,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "test_df['Country']=countries\n",
    "test_df['Item']=items\n",
    "test_df.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 71,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Item\n",
       "Cassava                 0.926622\n",
       "Maize                   0.894963\n",
       "Plantains and others    0.817372\n",
       "Potatoes                0.910895\n",
       "Rice, paddy             0.896925\n",
       "Sorghum                 0.802025\n",
       "Soybeans                0.847838\n",
       "Sweet potatoes          0.840751\n",
       "Wheat                   0.922150\n",
       "Yams                    0.928241\n",
       "dtype: float64"
      ]
     },
     "execution_count": 71,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "clf=DecisionTreeRegressor()\n",
    "model=clf.fit(train_data,train_labels)\n",
    "\n",
    "test_df[\"yield_predicted\"]= model.predict(test_data)\n",
    "test_df[\"yield_actual\"]=pd.DataFrame(test_labels)[\"hg/ha_yield\"].tolist()\n",
    "test_group=test_df.groupby(\"Item\")\n",
    "test_group.apply(lambda x: r2_score(x.yield_actual,x.yield_predicted))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 77,
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
    "# So let's run the model actual values against the predicted ones \n",
    "\n",
    "fig, ax = plt.subplots() \n",
    "\n",
    "ax.scatter(test_df[\"yield_actual\"], test_df[\"yield_predicted\"],edgecolors=(0, 0, 0))\n",
    "\n",
    "ax.set_xlabel('Actual')\n",
    "ax.set_ylabel('Predicted')\n",
    "ax.set_title(\"Actual vs Predicted\")\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "The figure above shows the goodness of the fit with the predictions visualized as a line. It can be seen that R Square score is excellent. This means that we have found a good fitting model to predict the crops yield value for a certain country. Adding more features, like climate data; wind and pollution, the economical situation of a given country and so on will probably enhance the model鈥檚 predictions. \n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 86,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Item\n",
       "Cassava                 0.925669\n",
       "Maize                   0.894284\n",
       "Plantains and others    0.807946\n",
       "Potatoes                0.910346\n",
       "Rice, paddy             0.896068\n",
       "Sorghum                 0.800251\n",
       "Soybeans                0.846604\n",
       "Sweet potatoes          0.839268\n",
       "Wheat                   0.921607\n",
       "Yams                    0.925723\n",
       "dtype: float64"
      ]
     },
     "execution_count": 86,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "def adjusted_r_squared(y,yhat,x):\n",
    "    score=1- (((1-(r2_score(y,yhat)))*(len(y)-1))/(len(y)-x.shape[1]-2))\n",
    "    return score\n",
    "\n",
    "test_group.apply(lambda x: adjusted_r_squared(x.yield_actual,x.yield_predicted,x))"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# Part Five: Model Results & Conclusions\n",
    "\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 87,
   "metadata": {},
   "outputs": [],
   "source": [
    "varimp= {'imp':model.feature_importances_,'names':yield_df_onehot.columns[yield_df_onehot.columns!=\"hg/ha_yield\"]}"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 88,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "image/png": "iVBORw0KGgoAAAANSUhEUgAAApYAAAO5CAYAAACjf2VdAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAALEgAACxIB0t1+/AAAADh0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uMy4xLjAsIGh0dHA6Ly9tYXRwbG90bGliLm9yZy+17YcXAAAgAElEQVR4nOzdebiVVf3+8fctWqIoaJriiJFoiogKphZ+Mc36WjmUhoopaTjlEKVm2oClZmnilAP5U6w053nCEcEZJAbB1Jy+5mwKigMi3L8/1trwsNnTmeAAn9d1cbnPs9eznrX3OdfVag33km1CCCGEEEJoqWUWdQNCCCGEEMKSITqWIYQQQgihVUTHMoQQQgghtIroWIYQQgghhFYRHcsQQgghhNAqomMZQgghhBBaxbKLugEhtAerrbaau3XrtqibEUIIIbR7TzzxxNu2V6/0XnQsl0CSZtjuJKkbsJ3tK9rwWUOBwcBbpL+nE2zfXKP87sAztqfWqbehcq1lZofOdNzu5wvjUSGEEMJCMeacvdqkXkkvVXsvpsKXbN2AfRfCc4bZ7g3sBVwiqdbf1e7AJg3U2Wi5EEIIIbQT0bFcsp0G9JM0QdIQSR0knS5prKRJkg4BkNRf0gOSrpb0jKTTJA2U9LikyZK6N/Iw208BnwKrSVpf0r35OfdKWk/SdsCuwOm5Td0lDc7tmSjpOkkrVCnXW9Kjub4bJK2S295d0p2SnpA0RtLG+fpekp7M9Y5ug+82hBBCCGWiY7lkOx4YY7u37WHAQcB0232BvsBgSRvkspsDRwObAT8AetjeGrgYOLKRh0n6MjCHNC1+HvBX272Ay4FzbD8M3Awcm9v0HHC97b62NweeAg6qUu6vwM9zfZOB3+THDgeOtL0VcAxwfr7+a+Abud5dq7T3YEnjJI2b9dF7jXzEEEIIIdQQayyXLjsDvSTtmX/uDGwIfAKMtf0agKTngLtymcnADnXqHSJpP+B9YIBtS9oW+G5+/2/AH6vc21PSyUAXoBMwsryApM5AF9sP5EuXAddI6gRsl1+Xin82//chYISkq4HrKz3Y9nBSx5SV1ujuOp8xhBBCCHVEx3LpItLo3nydN0n9gZmFS3MKP8+h/t/JMNtn1ClTreM2Atjd9kRJg4D+deopWgaYltd3zv8w+9A8gvotYIKk3rb/24S6QwghhNBE0bFcsr0PrFT4eSRwmKT7bM+S1AN4pY2e/TCwN2m0ciDwYJU2rQS8Jmm5XO6V8nK2p0t6V1I/22NIU/UP2H5P0guS9rJ9jdKwZa/cSe1u+zHgMUnfAdYFqnYsN1p3lTbbPRdCCCEsLWKN5ZJtEvBp3sAyhLReciowXtKTwEW03f+5OAr4oaRJpI7g0fn6lcCxkv6ZNwX9CngMuBv4V+H+8nIHkDbzTAJ6A7/N5QYCB0maCEwBdsvXT88bj54ERgMT2+hzhhBCCCGTHUvLllQLM88yP29/4DjSlLuASxqYIm8XVl6ju/vse9qibkZYiO4bFiPUIYTQHJKesN2n0nsxYrl06EYb51lK+l/gJ8DOtjcFtgSmt+UzQwghhNC+RMdy6dAaeZavS5qa6yj9O7HwjF8Ax9h+FcD2x7b/kutdIKsyX18ga1LSpvl5E3LbNszXb8xZlVMkHZyvHSZp7m5zSYMknVutfAghhBDaVmzeWTocT+r0fRtSfiM5z1LSZ4GHJJXihTYHvgS8AzwPXGx7a0lHAxvY/kmVZ/QEnqjy3vWFTubJpDzNc5mXNfmKpC657KHA2bYvl/QZoEO+fqDtdyR1BMZKug64FniENP0OMAA4pVr58l3h+Xs4GOCzK61W9csLIYQQQmNixHLptDOwv6QJpI0znyPlWULOs7Q9EyjPs+zWzOf1zKfiTCZtttk0Xy9lTQ5mXgfyEeAEST8H1rf9Ub5+VN6g8yhph/eGtt8Cnpe0jaTPARvlOiuWL2+U7eG2+9ju85mOKzfzo4UQQgihJEYsl05tkWc5BdgKuK/CeyOokFVZJWvyCkmP5WsjJf0oP3snYFvbH0oaBSyf674K+D5pR/kNOZy9f43yIYQQQmgj0bFcOiyMPMvfA3+U9G3br+cp9kNsn0OVrMpKWZP5lJ3nbZ8j6QtAL+AF4N3cSdwY2Kbw3OuBE4GXgJ/na51rlK+ox7qrxC7hEEIIoYWiY7l0mJtnSRo9PJs0rT0+h4q/BezekgfYvl3SGsA9uU4Dl+S3S1mVL5Gm1Eud3NPz5hwB95KyJo8H9pM0C3idlFf5AXBozrB8mjS9XXruu5KmApvYfjxfvrNa+RBCCCG0ncixXILkKeBPbD+cfz4U+ND2X6uUXws4x/aeFd4bRdrwM64V2rU78IztqS2tq62svGZ3bzPwD4u6GaEV3PWnBf6cQwghtKJaOZYxYrlk6Q/MIB2niO0LaxXO0UAL43+FdwduJZ36E0IIIYQlVOwKbyckdZP0L0mX5fzGayWtIGmrnC35hKSRkrrm8kflXMlJkq7Mp+scCgzJGZD9JA2VdEwu/0VJ9+TMyPGSuudnPpnf75jrmSTpKqBjoW07S3ok3zc5l5kg6Q1JHytlXFY8YUfSdsCupGnvCfm5vSU9muu5QdIquewoSX/IOZbPSOqXrw+SdL2kOyU9W5ZdWWzbNZI65eunFb6fxeL0nxBCCGFxFyOW7ctGwEG2H5J0CfBjYA9gN9tvSSrlNB5IWou4ge2ZkrrYnibpQmBG6RhFSTsW6r4cOM32DZKWJ/2fis8X3j+MNG3eS1IvYHyuYzXgl8BOtj/IMUCfBc4jRQOtmXdid6EC2w9Luhm41fa1uc5JpF3pD0j6LfAb0qk9AMvm3Mxd8vWd8vXewBakXepPKwWhf1ShbT+VdF7+3jau1TYVciyXjxzLEEIIocWiY9m+vGy7lMP4d+AEUvD43Wk/DB2A1/L7k4DLJd0I3FirUkkrAWvbvgHSqTj5erHY9sA5+f1JufMHaUf1JqQQdYDPkDqU7wEfAxdLuo001V1X3vXdxfYD+dJlwDWFItfn/z7B/LmZ99qenuuYCqwPdGlJ22wPB4ZDWmPZSPtDCCGEUF10LNuX8s7N+8AU29tWKPstUmdwV+BXkjatUKZENd6r9fzSvXfb3meBN6StgR2BvYEjgK81+JxaSrmZs5n/77OYr1l6b2G3LYQQQgg1RMeyfVlP0ra2HwH2IcXkDC5dU8qB7AE8Baxr+35JDwL7Ap1IHdEFjpCx/Z6k/0ja3faNShmTHcqKjSZlTN4vqScpP5Lchj9L+qLtfyud870O8CqwQo4ZehT4d43PNTdH0/Z0Se9K6md7DPAD4IEa99bSGm0DoMc6q8Ru4hBCCKGFomPZvjwFHCDpIuBZ0nnaI4Fz8hTyssBZwDPA3/M1AcPyGstbgGsl7QYcWVb3D4CL8prGWcBepBNtSi4ALs1T4BOAxwHy2s5BwD9yhxTSusb3gZvyek0BQ2p8riuBv0g6irQL/QDgwtwRfB74YVO+pJJWalsIIYQQWknkWLYiSTNsd8o7tLezfUUT7u1G2uDSs8HyGwEXkdYZfhYYY/vgpra5wWedYPvUVqprEHBXjjpqcbnW0nnN7v7KDyLHsr27/fQYVQ4hhEVNNXIsI26obXQjTU+3pXNII5W9bX+JNLrZVk5oxboGAWu1YrkQQgghtBPRsWwbpwH9cm7jEEkdJJ0uaWzOVTwE0kk5ShmVVwN3AbdKGphzHCdL6l7jGV2B/5R+sD0513l7jgtC0j8l/Tq//p2kH+XXxxbaclKpDkn75WdPkHRRbvdpQMd87fLyRkiaIelPOUfyudzuCZKelvSBUsblDZJWkbQn0Ie0m32CUnbmr3NbnpQ0XEmlcjvmzzNZ0iWlqW81mPPZ3F9kCCGEEBoXHcu2cTxparq37WHAQcB0232BvqQNORvkspsDRwObkdZB9rC9NXAxC66TLBoG3Cfpjtx5LWU1jiZ1alcGPgW+kq9/FRgjaWdgQ2BrUjbkVpK2l/QlYADwFdu9STuvB9o+Hvgof5aBFdqxIjDe9pak6KAH8v0zgV1sr0k6H/w3OcdyXK63t+2PgPNs981LADoC3y4vR9qtPgIYYHsz0lrTw/JmpnOBPW1vRTqb/JTC72AL271IwfELkHSwpHGSxn3y4Xs1vuoQQgghNCI6lgvHzsD+kiYAjwGfI3XuAMbafs32TOA50sglpM5Yt2oV2r4U+BIpA7I/8GgexRtDiiH6KnAb0Clvkulm++nclp2Bf5JC0DfObdkR2AoYm9u5I/CFBj7bHOCq/PrvwFdVOaty+yr37yDpMUmTSZFAlWKTNgJesP1MWX0bMS/ncwJp4846uUwp53M/Ugd7AbaH2+5ju89nVlhgM30IIYQQmih2hS8cIp00M3K+i1J/5s9nnFP4eQ51fj95Y8slwCVKRzP2BMaSppGfB+4GVgMGkwLHS235ve2LytpyJHCZ7V809cOVN6vRgnnX9vlAH9svSxoKLF+paLUqaELOp+2KHcwQQgghtI7oWLaNubmN2UjS1O19tmdJ6gG80pIHSPom6TSaWZLWJI2CvmL7E0kvA98HfgesDpyR/5Xa8jtJl9ueIWltUvzQvaSInmG235S0KrCS7ZeAWZKWsz2rQlOWIUUIXUnasPRgnazK4ndT6kS+rXTG957AtRXK/QvoppxXWajvaWB1NZ7zOa3a97nhOqvEjuMQQgihhaJj2TYmAZ9KmkhaG3g2aVp7vCQBbwG7t/AZOwNnS/o4/3ys7dfz6zHAjrY/lDSGND08BsD2XXk95SOpKcwA9rM9VdIvgbskLUPqbP4YeIl07OEkSeMrrLP8ANhU0hPAdNI6TaieVTkiX/8I2Bb4C2na/0XSaCtVyv0QuEbSsrnchbkTvScN5nw25csNIYQQQtNFjuUSLI9knkXaMDST1Hn7SWGtYkvr7w/cbnuFVqhrKDDD9hn1yhbuGQUcY3ucpNuBfZvbgezStbv7H/DH5ty6VLjxtO8t6iaEEEJoJ1QjxzJGLJdQeWT0BtK6yb3ztd7AGqQRvdbQnwWPhiw9f9mFuabR9i4L61khhBBCqCx2hbdzkk7MWY7Ffyc2cOsOwCzbF5Yu2J4APKiUqflkzoQckJ/TX9Ktheeep3T6DZJelHRSzqqcLGljpZOCDiWtj5wgqZ+kEZLOlHQ/cLqkZyWtnutYRtK/Ja3WwGceJekPSpmaz0jql693lHRlzqa8ihRPVLrnxVLdkm7MuZZTJLXJaUQhhBBCWFCMWLZztk9hXjZjU/Rk3k7wou+S8is3J+0YHytpdAP1vW17S0mHk6affyTpQgrT15IOIm2e2cn2bEnTgIGk6fidgIm2326w/cva3lrSLsBv8v2HAR/a7qUUAj++yr0H2n5HUsf8+a6z/d/yQrnTeTBAx5Xr9ndDCCGEUEeMWC59vgr8w/Zs22+Qdlf3beC+6/N/n6BGviZwje3Z+fUlwP759YHApU1oZ6XnbU/KysT2JNImqUqOyhunHgXWZV5m6HwixzKEEEJoXdGxXHJNIQWel6uWCfkp8/89lOdJlvI1Z1N7pPuD0gvbLwNvSPoa8GXgjloNbvB5NXeb5Q1FOwHb2t6cFARfKRszhBBCCK0spsKXXPcBp0oabPsvAJL6Au8CAyRdBqxKGgU8FlgO2CSf3rM86eSdB+s8432g3lDfxaRRxr8VRjKbazRpav1+ST2BXhXKdAbezVFLGwPbNFLxF9deJXY+hxBCCC0UI5ZLKKccqT2Ar0t6TtIUYChwBWkKeSKp83mc7dfz6OLV+b3LSSN99dwC7FHavFOlzM2kcPKmTINXcwHpiMpJwHHA4xXK3Aksm8v8jjQdHkIIIYSFIHIs20BzMxXzCNuVpOnePW0/V6Xci6RjEN+WNMN2p5a2ua1I6kMKKK/W8WwXVun6Re/4wyUrx/LaU7+7qJsQQghhCVQrx3KJGbGUVDFPcVE8y/YuzQzq3h24yfYW1TqVixNJxwPXARXPH8+n6CystsSyjxBCCKGNLbKOZXnWoKTDJP2x8P4gSefm1/vlTMMJki4qdewkzZD0W0mPAdtK+rWksTmjcXgOCUdS35x9+EgpwzFf75B/HpvfP6RGe/tLul/SFaQjCKvmJZYyFSV1k/SUpL/kMnflCJxK9e8C/AT4Uc6BbHEeY27zA5KuznmQp0kamL/LyZK653IjJF2QP9/zkv5H0iW57SPqPGOGpD8pZVzeq3m5ld1JAepvA7/Po7Hkcm9Keh94VWW5nEp5lxXzLyWtLum6/PsaK+kruczWkh6W9M/8343y9UGSrpF0C3BXU7+/EEIIITTNohyxPND2VkAf4ChSvExx7m4AcJXSudYDgK/Y7k3aJVw6r3pF4EnbX7b9IHCe7b62e5LCs7+dy10KHGp723x/yUHAdNt9SZE7gyVtUKPNWwMn2t6k0meQ9LkK92wI/Nn2psA0oOIOEdu3AxeSpo13aEL99WwOHA1sBvwA6GF7a9KmmiML5VYBvgYMIa2dHAZsCmymdGJPNSsC421vSYou+k2+Phw4Mrf/GOD8fH0SaW1kF9uft907Z3WWvoc5pM0+pd9xMf/ybNL305f0PV6cy/wL2N72FsCvgVML7dsWOMD218obnv8PzThJ42Z+OL3GRwwhhBBCIxbl9OBRkvbIr9cFNgCel7QN8CywEfAQ8GNSbM7YPADZEXgz3zebNNVasoOk44AVSDuep0gaA6xk++Fc5grmdTh3BnpJ2jP/3JnUEXyhSpsft118r/wzbAiUB3G/kE+8gfoZkOUaqb+esbZfA5D0HPNG7iaTTucpucW2JU0G3rBdGpWdkts8gcrmAFfl138HrpfUCdgOuCb/zgA+W7inmHVZySXATaRg9WL+5U6kneulcitLWon0e7tM0oak9anLFeq62/Y7lR5iezipA8wqXb8Yi41DCCGEFlokHUvNnzX4oaRRpIibq4Dvk0agbsgdHZHOu660Tu/jUgdF0vKkUbE+tl+WNDTXWS23kfzekbZHNtj0uRmNNT5DuZmF17MpHENYSxPqr6f4/DmFn+cw/+9/ZoUylcrVY9JI+LQ8wlzJB1WupwrS76+Yf1kavVyG9H18VCyvtGTiftt7KB01OarRZ4UQQgih9SyqEctqWYPXAycCLwE/z9fuBW6SNMz2m5JWJY1AvlRWZ6nT9XYeMdsTuNb2u5Lel7SN7UeBvQv3jAQOk3Sf7VmSegCv2G6kM9KsvMQmaOv6W8sypO/6SmBf4EHb70l6QdJetq/J/+egl+2JTai3Uv7lXcARwOkAknrn0eDOwCu5zKDmfIjua3eJXdQhhBBCCy2qNZYVswZtvwtMBda3/Xi+NhX4JXBXLn830LW8wrwL+y+kKd4bgbGFtw8Chkt6hDRKWVpQd3F+3nilDT0X0Xhnu63zEheXPMYPgE0lPUFao/nbfH0gcJDS0YpTgN2qVZA32axVdrlS/uVRQB+ljVZTgUPz9T+SNgg9BCy0dIAQQgghzG+pyLGU1Mn2jPz6eKCr7aMXcbOWCGqFHM08zX+M7XGFaws1/3LVtb7orx+0+ORYXvW7GF0NIYSwaGhpyLGs41s51uZJoB9w8qJu0OJIFSKigM8U3i9GRP1K0r8k3S3pH5KOqVLnnqRd75fn31HHXMeDwOqSRkrqmsuOkjRM0milKKS+kq7P8UQn5zLd8nMvyyOb10paoY2/mhBCCCGwlJwVbvsq5u1crknSZsDfyi7PtP3l1mqPpD8DXym7fLbtZh17uJDa/Bhpt/1s4FNS9M83gf8rFBsAnJJHG78HbEH6GxtP2hFfXucPSVFIRWeSIpLWtf2WpAHAKaTd4QCf2N5e0tGkneNbAe8Az0kalstsBBxk+yFJlwCHA2e05POHEEIIob6lomPZFDlmp1ZuY2s848etXN/CaPOX8077UvzRJ6Td45Uioo4mnSD0EUAOKK9U56XApcWpcEk9gYeBu3OsUAfgtcJtN+f/TgamFKKUnidFMk0DXrb9UC73d9LazAU6lkqh8wcDrLDyak35OkIIIYRQQXQsQ0OaERHV7EeROozbVnm/kVik8oXDFRcSF3MsV10rcixDCCGEllpa1liGlqsVEbU7sA/zlhs8CHxH0vI5+ulbdep+H1gpv36atLZyWwBJy0natIltXa90f27Xg028P4QQQgjNECOWoVF3Aofm+KOnKURE5eifTQoRUWMl3QxMJGWSjmNexFMlI4ALJX1EOoJxT+AcSZ1Jf6NnkSKLGvUUcICki0hT9BfUu+ELa3WJndYhhBBCCy0VcUNh4StFPOUd2aOBg22PXwjP7Qbcms+Lb1ifPn08bty4+gVDCCGEpVytuKEYsQwLKGVT5k7adravaEY1wyVtQlqHeVmlTqWknYGT8jMsqQNp9/jhhbPdF4oXXp3GwN/csDAfWdHlJ+1Rv1AIIYTQTkXHMtTSjXRMY5M7lrb3Lb9WJWZpJulkpIuBI4GxLelU2n4RaNJoZQghhBBaR3QsQy2nAV+SNAG4DDgnX+sPfBb4s+2L8o7xk4A3SLFH15PigI4GOgK7236uUsxSDj9/MB+3eQSwdb6+G3ACKYD9LWC/fFb8ycA6wFpAD+AnpND7b5DWc+5m+1NJp5M2DX0K3GH754QQQgihTcWu8FDL8cAY271tDyONLE633RfoCwyWtEEuuzmpI7kZ8AOgh+2tmTcSWVHOoTwLeAQ42fY7+a3RwDa2tyB1VH9WuG0DYBdSCPsVwJ15TeUc4JuS1sjvb2q7F/D7Ss/OpweNkzTu4w/fa9IXE0IIIYQFRccyNMXOwP55BPMx4HPAhvm9sbZfsz0TeA64K1+fTJpSr+XPQAfbIwrX1gPukjQZ+ClQjBy63fanuW5s3132rHdIncy/SNoD+KDSQ20Pt93Hdp/lV1i5ThNDCCGEUE90LENTCDgyj2D2tr2B7VIHsjysvBhkXnPJhe05LBhi/mdgmO3NSEcyLl94r1j3J2XPXdb2LNL54zeSRjVva+TDhRBCCKFlYo1lqKUYXA4wEjhM0n22Z0nqAbzSRs/uDLyST/E5oCk3SloJWN72rfmM86n17tlgrS6xIzuEEEJooehYhlomAZ9KmkgKMT+bNNU8Pnf43iKdutMWhgI3AP8BHge6NuHezsD1kj5LGpX/ab0bXnxtGoN+e2Mzmtk0I37dVl9XCCGEsOhFQPoSRtKapM0wfUlTxi8CP7H9TCvV3x/4pDVyJiUNBWbYPqOldbXUamt/0d8+pO2bER3LEEIIi7taAemxxnIJkkcRbwBG2e5uexNSZM8arfiY/sB2VZ4fI+AhhBDCUiw6lkuWHYBZti8sXbA9gZQTebqkJyVNljQA0uijpFtLZSWdJ2lQfv2ipJMkjc/3bJxP4jkUGCJpgqR+kkZIOlPS/cDpkp6VtHquYxlJ/5a0mqQT8z1z/5HyJ0vPHixprKSJkq7LR0GS679Q0hhJz0j6dr7eLV8bn/9tV/hMoyRdK+lfki7PHe4QQgghtLHoWC5ZepKORCz3XVJw+ebATqQOYCNrFt+2vSVwAXBMPtXmQtJu7d62x+RyPYCdbA8B/g4MzNd3Aibaftv2KYXd5L1t9wbGFJ51ve2+tjcHniJlZpZ0A/6HFHh+oaTlgTeBr+f2DSCFt5dsQQpO3wT4Ague9gOU5Vh+EDmWIYQQQktFx3Lp8FXgH7Zn234DeIC0BrOe6/N/n6B2FuU1tmfn15cA++fXBwKXNtjGnnkEcjKpY1rMrbza9hzbzwLPAxsDy5FyKicD15A6kSWP2/5PjjGaUK3t8+VYrhg5liGEEEJLRcdyyTIF2KrC9WpTwZ8y/9/A8mXvl/IiZ1M7QWBuALntl4E3JH0N+DJwR60GF4wAjsi5lSeVtaV8h5mBIaQjJDcnZVZ+pkK7G2l7CCGEEFpJ/A/ukuU+4FRJg23/BUBSX+BdYICky4BVge2BY0mjfpvkWJ7lgR2BB+s8432g3vDexaQp8b8VRjLrWQl4TdJypBHLYj7mXrntG5Cmtp8mRQr9x/YcSQcAHRp8TkXdunaJHdshhBBCC0XHcgli2/kIw7MkHQ98TI4bAjoBE0mjfcfZfh1A0tWkvMpngX828JhbgGsl7Ub1M8BvJk2B15sGX5Z5o4u/Ih0T+RLpaMZiMPvTpOn7NYBDbX8s6XzgOkl7AfdT5djGRr342jQOOrntciz/3y+j0xpCCGHJt1R3LNs68zE/oz+tl/s4ArjV9rWFazNsdyr9bPtV4Ptl910MnGn7WEkn2L6qUP444LjyZ9nuVvixJ/Bkvv4M0CvXO4iUQ3mtpGVIHcnZwPmkafbX63ykTYGHc70XkDYJVbIzcIDtcYX2PVtqR/aLfH0UMKpQ7og6bQghhBBCK1lq11gupMxHaAe5j7Z/ZLt0rOEJrV1//i4vJE2tPwtcB+xqe1qNeyaTzva+q1qZEEIIISxeltqOJVUyH22PUbJIcx+b+mFq5Tfm630knQZ0zG25PL+3n6TH87WLJHXI13+YcyMfoEpcT8HZwOeA/W3/3vb6wN9zfmU3SW9K+q+kjyS9p3RE5JXAaaTjIR8pfd/52R0lXSlpEtARmFH4nPvk7/dJSX8oXJ8h6Q+SnpB0j6St8+d+XtKuTf0+QwghhNB0S3PHslrmI7SD3MfmfCDq5DfaPh74KLdloKQvkTIgv5JzJWcDA/NnPSnf/3Xmj/Ipty9pJ/retj+tUmZVYEfbHYE7gdNtn0KaOj/U9rb52SWHAR/a7gWckutH0lrAH4CvkX4/fSWVFi+uSBp93oq0wejk3PY9gN9WalTkWIYQQgita2nuWNbSXnMfKx3sXrzWUH5jwY6kTttYpZNwdiR1SL9M6qS9ZfsT4KoadYwH1ge2rlHmhXwCEOTvRlIXYKXC2tMrCuW3J3W4sT2JtLkI0u+g1K5PgctzWYBPSJ1WSJt/HrA9K7/uVqlRkWMZQgghtK6luWNZLfMR2m/u43+BVeY2UloVKI5uNjW/UcBlhdNwNrI9tNS0OveW/Iu0WegqSZtWKVOpXfWOWaz0/Fr3zLJdumdO6Zm5k71Ub1ILIYQQFpal+X9wq2U+rgCMBg5ph7mPo4CfSLosjyQOIkXtNMUsScvl0bx7gSxl1QsAACAASURBVJskDbP9Zu6orkSK/Tlb0ueA94C9SFFFFdl+WNKhwG2Strf9f/UaYftdSe9L2sb2o8DehbdHk5YH3C+pJ/N2f5fatRopm3Mf4Nwmfv6KunXtEpFAIYQQQgsttR3LOpmPo4FtaWe5j7ZvlbQV8ISk2cBzpM1BTTEcmCRpfF5n+UvgrhwXNAv4se1HJQ0FHgFeI0131wwgz21bHbhTUr8G23IQ6VjGD0id5un5+gXApXnzzgTg8fyM1yT9gtSZFnC77Zsa/eC1vPTaNA4+tVWqYvgJu7VKPSGEEMLiRvNmD5dsynmPeaf2dravqHNLS541FBgMvEXqvJ9g++Z8fYbtM8rK9yFt8KnaIWu03XmDyzm292zJZ2ipap+1rEwn2zPy67+S/h5/kH8eRdoANa7a/a1p9bW/6D1+/KdWqSs6liGEEJZkkp6w3afSe0vjGstupJ3MbW1Y3mm9F3BJHhFcQB4tvY4c8F1DNxpot+1XF3Wnsgm+lWOOniTFPzV1Wr+iUmRSCCGEEBaupbFjeRrQL3dohkjqkDMUx0qaJOkQmJsL+YCkq3Oe42mSBubMx8mSujfyMNtPkTb9zJdNKWmwpLGkdYLjSNPNKOVcPizpA0kzJb2Qd2z/tazd3SSNUcrNHC9pu3x/t0Ie5CBJ10u6Uykv84/5eof8nFJO55Dydkv6jqTHJP0z50Kuka8PlXRJISPyqMI9J0p6WtI9wEaVvg9J60u6N09zHwzsmv+7IvCr/PlK3+1e+ft+pjS9Xuf3db+kK4DJklaUdJukiflzDmjk9xVCCCGE5lsa11geT5pi/TakLENguu2+eVPOQ5JKp8FsDnwJeAd4HrjY9taSjiatl/xJvYdJ+jJpl/JbZW9dX9g0dDJpvWFpI8orpMijjYGbbfdWOhqy2O4VgK/nc7M3BP4BVBqW7k3Kt5wJPC3pXODzwNq2e+a6ulS470Fgm7wW9UekYx9/lt/bmDTCuFKu8wLSBpu987OWJXWUK+WEngf81fZlkg4kTdvvLulmCsdVKmW7L5u/712A35ByPg+i+u9ra6Cn7RckfQ941fa3cn2dyxuSf/cHA3TqvHqFpoYQQgihKZbGjmW5nYFekkrTx52BDUm5iGNtvwYg6TnmHT84mdSxqmWIpP1Iu8IH5A5a8f2euUPZBegEjCy8d2OOyZlaGimsYDngPEmlYPMeVcrda3t6/gxTSZmTU4Av5E7mbVQ+VnEdUoRQV+AzwAuF926zPROYKelN0jGY/YAbbH+Yn3VzlfZsSwqgB/gb8Mcq5aByLmit39fjtkvtnAycoXQ6z62FcPq5bA8nbWZi9bW/uHQsNg4hhBDa0NI4FV5OwJGFLMcNbJc6WsX8xTmFnxvJRiydttOvUqcGGAEcYXsz0ik3xUzM4nOrZTcOAd4gjar2IXX+KlkgQ9L2u/m+UcCPSXFH5c4FzsvtO6RG+4p5mc3pnNW6p1IuaK3fVzEf9BlSTulk4PeSft2MtoUQQgihCZbGEcv3SVO4JSOBwyTdZ3uWpB6kqei2thLwmqTlSJmN9Z5Z3u7OwH9sz5F0AHXigIqUciA/sX1dHokdUaFY50KbDmig2tHACKXzyJcFvgNcVKHcw6Qp87+RPncpB7T881XT0O9LaXf8O7b/LmkGKfOzqvW7dond3CGEEEILLY0dy0nAp5ImkjpUZ5OmWccrzVW/BSyMpOxfkQK/XyKNqtXrVJW3+3zgOkl7kXZTf1Dj3nJrk3IiSyPWlXakDwWukfQK8CiwQa0KbY+XdBUpd/IloNIoLcBRpF3yx5K+6x/m61eSMi2PAmrtar+Yxn5fm5HOeJ9Dyuc8rFb7/+/1aRx+WrXZ+8adf/yuLa4jhBBCWFwtNTmWiwNJawJnkc7EnkkObM/Tuq1Rf3/SSOXD9co2oc6JwFTb+zTz/i7AvrbPb8a9LwJ9bL8t6WHb2zWnDQCfX+eL3vOIM5t7+1zRsQwhhLCkU+RYtn959O0GYJTt7rY3AU4gbYxpLf2Bip0vSU0evZb0JdLf0PaSVmxmm7oAh1epv+Hp/ZZ0KkMIIYTQOqJj2QI5t3FC2b8Tm1ndDsAs2xeWLtieADyYcxtLmZMD8rP7S7q10JbzJA3Kr1+UdJJSvuVkSRsrndxzKGm3+gRJ/ZSyLM+UdD9p2vhZpWMZkbSMpH/n9ZjV7EtaK3kXKY+y1JZRSqcJIWm1PLKIpE1zLuWEnEG5ISlXtHu+dnp5HmW+70ZJT0iakiOCFpDXUSKpk1JOZumzx8LJEEIIYSFZGtdYthrbpwCntFJ1Pamc+/hdUhbl5qSQ9bGSRjdQ39u2t5R0OCn/8keSLqRwzKKkg0gxRTvZni1pGmlDzVmkzMiJtt+u8YwBwNdJYehHkLI0azkUONv25ZI+Q9pwdDwpe7J3blN/CnmU+b4Dbb8jqWP+/NfZ/m+VZ3wM7GH7vdwpflTSza6w5mO+HMsukWMZQgghtFSMWLZ/XwX+YXu27TeAB0hrMOuplAFZyTW2Z+fXlwD759cHApdWu0lSX+At2y8B9wJbSlqlTpseAU6Q9HNgfdsfVSlXzKMEOCqv5XwUWJeUW1m1acCpSif73EPaqFRxOYHt4bb72O7TccWV6zQ9hBBCCPVEx7L9mELKXSxXLcfyU+b//S1f9n6lDMhKitmPLwNvSPoa8GXgjhr37QNsnKe5nwNWBr5XoW1z22X7CtKU+UfAyPycmm3KI5g7Adva3hz4Jwt+1qKBwOrAVnkU9I065UMIIYTQSmIqvP24jzTSNrhw1GNf4F1ggKTLgFWB7YFjSSfvbKJ0rOHywI7My4Ss5n1SB7CWi4G/A38rjGTOJ8cU7QX0sv1KvrYD8Mt8/4ukTvLjFKKDJH0BeN72Ofl1L2AitaOWOgPv2v5Q0sbANnXa3xl4M2dc7kA6aaiu9dbsEju6QwghhBaKjmU7kY983AM4S9LxpLWCL5LOI+9E6oAZOM726wCSriblWz5LGsmr5xbg2ryh5cgqZW4mTYFXnQYndW5fKXUqs9Gkjm5X4Azgakk/IHWYSwYA+0maBbwO/DavnXxI0pOkEdLbyp51J3Bontp+mjQdXsvlwC2SxpEyNf9VpzwA//f6dI784y2NFJ3r3OO+06TyIYQQwpIuciwXEwsr4zL/G2a7Xwvr2x84jjSVL+CS0qahtiBpKIWNSU31+XU29ICjmpZjGR3LEEIIS6NaOZYxYrkYKGRcXmZ773ytN2lTSqt0LEkZl31Ju9MHlj1/WdufNqG9/0saad3Z9quSlgd+0ErtDCGEEEI7FZt3Fg8LK+OyN2lNpwoZl88Dr0qamctPkPTLOhmXvyBFHL2a2/pxYd3oYEljJU2UdJ2kFfL1EZLOkfSwpOcl7ZmvV82lVMoRfVrSPaTII2o9I4QQQghtKzqWi4dGMi53IoWcd22gvrdtbwlcQOoAvghcSJoC7227dM53D2BD258HTgX+X95p/Ti1My6rtRfgett98w7vp4CDCu91JcUrfZsUnA7zcim3JHWw/6RkK2BvYIv8PRQjmGo9Yy5JB0saJ2ncRx9Mr9LcEEIIITQqOpaLt3aZcVlHT0ljJE0mTblvWnjvRttzbE9lXvZktVzKfsANtj+0/R5p01Ejz5hr/hzLzs38OCGEEEIoiY7l4mFxy7is1l6AEcARtjcDTipr28zC69Jnq5VLWW3nWa1nhBBCCKGNxOadxcNik3GZ/R74o6Rv2349t+MQ2+eQMitfk7QcqdP4So16oHou5WhghKTTSH/H3wEuyu819Rmst2bn2OUdQgghtFB0LBcDi1nGJbZvl7QGcE/e0W7SVDrAr4DHgJeAydQOR4cquZS2x0u6Kl97CRhTuKepz+DlN6Yz5E+3Vn1/2M++Xa+KEEIIYakXOZbN1Na5kvkZ/YFPbD/cCnUNJeVKdrP9Zr42w3anJtTRhyoZl5I6sOCGnXWAe20PaGZ7m51LWVbXCOBW29dWK7PGuht6358Mq1pHdCxDCCGEpFaOZayxbIZCruQo291tbwKcwLwNJ62lP7BdlTY0Z7T5beBnzWlIHim9jhQltIC8gah36R/wv6QzwX/XnOeFEEIIYfETHcvmqZgraXtMjsJpzWzJITk7sl8hW/J+UrTQs5JWz3UsUydbEtJ09ABJq5a/IWk/SY/nZ10kqYOk70sqHUfzETDb9oOSukt6MOdITij7d2LueF8GnG77yVz/VpIekPSEpJGlWKRGMiebkX2p/P1OlXQb8PlKX0bEDYUQQgitKzqWzVMrp3FhZEvuZHsIaSNN6ZScnaidLQkwg9S5PLp4UdKXSOd4fyWPNs7O9Y4mxfqQ//tfSWuTYo7G2D6lOEqZ/50CDCHtTD83179cfr2n7a1yG07J9TaSOdnU7Ms9SIHpmwGDqTLqG3FDIYQQQuuKzTutb262JCmep5Qt+V6d+4rZkt+tUa48W/Im0lrPRrMlzwEmSPpT4dqOpHigsWmwkY6kndivK518sxKwLnAFaed5v0J75yNpc9Kmor6et4B3I1Jn/O5cfwfgtfxeT0knA11IG5FGVqi2Vpkbbc8BpuYNQ+Q2ln4Hr0q6r4HvJYQQQggtFB3L5pkC7FnlvYWaLSmpmC05sPptc++ZJukK4PCyNl9mu9L6yUeAHwJPk3ZeHwhsS4W1mpI6knZxH54D24v1T7G9bYX6RwC7256Ylwb0b2KZStmXUD3jMoQQQghtJDqWzVMtV3IF0vTxIWp/2ZJFZwJjmff7vxe4SdIw22/mNZgr2X4pf57f5n//JK0v/ch2pUWJZwAP2C7P7XkaWF3StrYfyVPjPWxPobHMyabmUpZ+B38lra/cgTTaWtW6a3SOnd8hhBBCC0XHshnq5EqOJo3otatsybL2vy3pBtJaSGxPlfRL4C5JywCzgB8zLx9yXWC07dmSXiZnSRZJWos0CvovSRMKb02xPTBvrDlHUmfS391ZpJHfRjInm5pLeQPwtVz2GdJRlzX9543pHDPstorvnTHkW/VuDyGEEAKRY9lqtIhyLVUjW7JOXRuRTqrpAnyWtBnn4Ga26wTbp+bX3UiZkT0bvHciMNX2PoVrGwNXkjrme9p+ruye24F9bU9rTnsrWXPdDb3fT8+q+F50LEMIIYR5FDmWbSvH6yz0XEsVsiXV9FzLc5i34/xL5B3czXRCc27Ku9GXAbaXtGLhrd2Bm2xvUexU5hihZWzv0pqdyhBCCCG0juhYto5FkmsJbEzqWP6OebmWpxQyJWfm+0+s0OauwH8K7Z2cn728pEvzff9UOp8bSYMknVdo7635M5wGdMzPuzy/3UHSXyRNkXRX3tRTyb7A34C7gF1zvbuQlhT8SNL9krpJekrS+cB4YN38/ayWy+8vaZJSxuXf8rXvSHost/+ewm7x+RRzLD+MHMsQQgihxaJj2TraU67lWzmL8jjSlPRmOVuy3DDgPkl3SBoiqUu+/mMA25sB+wCXSSrfwT6X7eNJm3l62y7tSt8Q+LPtTYFpwPeq3D4AuAr4R34Wtm8vfM4dcrmNgL/mEcyXSjdL2hQ4Efhazrgs5XM+CGxjewvSlPpxVdo+N8dyhcixDCGEEFosOpZtb26uZY7gKeVa1lPMtexWo1x5ruX++XXNXEvblwJfAq4hTbE/mnesf5U0iojtf5E2zPRooL1FL9gubeCp2P68i/6t3FG8F9hS0ipV6nvJ9qMVrn8NuLYUCm/7nXx9HWCkpMmkHfmbNrH9IYQQQmiG6Fi2jimkgPFKFmquJSmUvZRreUeN+7D9qu1LbO+W29OzBe2t1Hao3v59gI0lvQg8R4pVqjay+UGV66JyXuW5wHl51PWQOm0NIYQQQiuJuKHWsdjlWkr6JnCv7Vl5R/vnSPmQo0lZkfdJ6gGsR8qhXBk4PMcRrQ1sXahulqTlbM+q07bSs5cB9gJ62X4lX9sB+GVuf6PuBW7I+Zv/lbRqHrXszLysywMaqWidNTrH7u8QQgihhaJj2QoW01zLnYGzJX2cfz42H+F4PnBhnkb+FBhke6akh4AXSNmQT5I20pQMByZJGk9a81jP9sArpU5lNprU0W5k/SkAtqdIOgV4QNJs0nc4CBgKXCPpFeBRYIN6df3nzen8/OzbF7j+h6N3abQ5IYQQwlIvcixbUVtnWVbKsaxQpqFcS0lDSZtautl+M1+bYbtTnfuanVlZpb5BQB/bRzS3jkJdQ4EZts9o6r1rrrehD/jZ2Qtcj45lCCGEML/IsVwIFlKWZX8KOZZlz1+2mGvZYH1vU+HM7zqalVlZSTOyN0MIIYTQjkXHsvVUzLIEHmyrHEtJIySdKel+4HTgINLo34OSlpH077Jcy9K/0nT1JcAApbPB5yNpP0mP5/IXSerQlMxKSd0l3SnpCUljlE7ToazNfyh7ZsX8SUlDJV0iaZSk5yUdVbjnRElPS7qHFEtUun6UpKlKGZdXVvqFFXMsP5oROZYhhBBCS0XHsvVUy7Jc2DmWpSzJnYCJtk/M5Yv/SrmWM0idy1L+IzD3RJwBwFdyJuZsYGATMyuHA0fa3go4Bji/8IhSm8tHS2vlT24MfIO0aeg3kpaTtBWwN7AF6XsuxjgdD2xhuxepQ76AYo5lx06RYxlCCCG0VExFtr25OZakKKBSjuV7de4r5lh+t0a58hzLm0jrPGvmWBacA0yQ9KfCtR1J8Ulj0ww/HYE3q9y/QGalpE6kKftr8v2QziOv1OaidYCrcsf7M6TNQiW32Z4JzJT0JmmJQT/gBtsfAki6uVB+EnC5pBuBG6t++hBCCCG0muhYtp4pwJ4Vri/UHEtJxRzLgdVvm3vPNElXAIeXtfky242s1SzPrOxI+lzT8mhnzTaXORc40/bNeaPS0BrPKX0n1XaffYu0+3xX4FeSNrX9abUPEUIIIYSWi45l66mWZfkuaR1ju8qxLHMmMJZ5fw/3AjflfMg38xrMlfIpOXUzK22/J+kFSXvZviZvbOple2KddjQ1f3I0MCKv/VwW+A5wkVJO5rq275f0IOlM8k6kqfqK1vl859gBHkIIIbRQdCxbSZ0sy060vxzLYtvflnQDMCT/PFXSL4G7cidtFukM8ZdoPLNyIHBBrmc50prJeh3LoTQhf9L2eElXARNy20rrTjsAf5fUmTT6Osx21U4lwCtvTueEcxfMsTz1yOhshhBCCI2KHMt2rDm5mI3mWOay/amTi9mEtg4FBgNvFS73r9eha8HzRpE2NY1rjfq6rrehf3jsgjmW0bEMIYQQ5lcrxzJGLNupQi7mZbb3ztd6kzatVOxY5pHSw2hgbWXWn7QzfIGOpaRlm7EmcVhzwskXBkkdmrA0IIQQQgjNEHFD7VeTczGBr9peP+dYnidpUM55/ETS65I+lPSRpGGN5GJKelbS6rn+Ui7mak35EDn/8ozc1kmSjszXXyzVJalPHoFE0taSHs5Zlg9L2ihf7yjpylzHVaRNQqVn7JPrf1LSHwrXZ0j6raTHSMdqlrdtbo7lh5FjGUIIIbRYjFi2X43kYq5GigQaXa0S26dIGgz8yfa5kg4HtrT9oqQLKRyBKOkg5mVMzpY0jTT6eRbzcjHfrtHmIZL2y6/ftb0DcDBpreQWtj9VhTD2Mv8Cts9ldwJOJWVjHgZ8aLuXpF7ks8olrUUKWt+KtFHqLkm7274RWBF40vavq3w3w0lrRum63oaxJiSEEEJooRixXPzMzcW0/QZQysWsp5iL2a1GufJczP3z60ZyMUvh7b1zpxJSh/TC0rS67Xfq1NGZtIHnSWAYsGm+vj1ptzu2J5E2PUH67KNsv5WfcXkuCymW6Lo6zwshhBBCK4mOZfs1hTQKV26h5mKSQt1LuZh31GpwFaJy1mSxvcW2/g6433ZPUnxQ8b1K9VT7PgA+jnWVIYQQwsITU+Ht1+Kci1l0F3CopFGlqfA8avkiqeN8B/OOgYT5sywHFa6PJk3L3y+pJ9ArX38MODuv13wX2IcUtN4ka3++c+wADyGEEFooOpYLQXNig5qSi0k6R/sToFVyMfM6yeNIeZCfktZyXttAfcU1lgC7k4LXdyZlX84C/gKcB5wE/D9JJ5A6hyV/BC6T9FNS57rkAuBSSZNIuZWPA9h+TdIvSCO8c0gd4JsaaOt8Xn3rPX5z/p0LXD/p8G82taoQQghhqRU5lm0sxwY9TIoNujBf6006yWZMzZsbf8ZQCptwyt5rUmyQpG8CpwC72n5F0takEcvv2H66GW0bBPSxfURT723ic4ZS5TtoxFrr9/Dgn5+zwPXoWIYQQgjzq5VjGWss216TY4Mk3VoqW4oNyq9flHSSpPH5no3bIDboRFLw+Ct5pPQa4MBSp7IpMUGSPgP8ljR1P0HSAEkrSrpE0thcdrd8/yBJN0q6Rek4yCMk/TSXebS0m1zS4HzvREnXSVqh/AM0UiaEEEIIrS86lm2vkdignUgdwK4N1Pe27S1JU8PH2H4RuJB5O7JLo6Cl2KAhpBHHUmh6vdigTclRPrZPK+ViFt7vTFrnOIG0A7uPpBOZFxO0BfBr4FTbn+TXV+W2XUXquN5nuy+p0326pBUL39W+wNakUdMPc32PMG93+vW2+9reHHgKOKjCZ2ikTORYhhBCCK0sOpaLTnuODQJA0mZ5pPG50ogqMB3YwXZvUmd1nO1TqB4TVG5n4PjcMR1F2mi0Xn7vftvv234rP+eWfH1y4bP2lDRG0uT8/ErPaaQMtofb7mO7zwqdOtf/QkIIIYRQU3Qs297iFhs0Bdgy3zc5dyDvYN5JN82JCSoS8L1C3uV6tp8q+2yQNuLMLLwufdYRwBG2NyNtAKr0nEbKhBBCCKGVRcey7d0HfDaffgMsEBvUIa9/3J600/klcmyQpM6k2KB63gdWqlOmFBt0dZ3YoN8DZ0hap3CtY+H1i8zrKDcSE1TetpHAkXlTE5K2qNPucisBr0lajupnojdSJoQQQgitLOKG2lhTYoNsvw4gqVVig8rcTJoCrzkNbvv23NG9Q1IHYBrwJKlDCE2PCbqfeVPfvyeNbJ5Fih8S6bv4dgOfseRX+bkvkabIK3WoGykzn7VWXzl2gIcQQggtFHFD7VRzsi/r1NeHtMGnX/65P/CJ7Ydboa1DgcHAW6T/s3KC7ZvrlF8gGkjSb4HRtu+pct/uwDO2p7a0zeXWXr+HDzlhwVz1Xx/yjdZ+VAghhLBYi7ihxUweybuBdAZ2d9ubACcAazSzvuNJZ2b/onC5P7BdlfLNGckeltdj7gVcIqnJf1u2f12tU5ntDmzSjLaFEEIIYSGIjmX71KrZl6Q1kv8FLihkX/6MdGTkRznn8h1JDzYz+3KuvBHnU2A1Sd+R9FjOorxH0gId45w5eYekjkr5m3vm66dJmippkqQzJG0H7JrbNkFS92p5lbmec5TyNJ8v1RlCCCGEthVrLNunRrIvVwPGShrdQH1v295S0uGk7MsfSfoTheloSSNynbvZni1pGmnjy1nUz76cS9KXSbu43yKdVb5NXmf6I9IxkT8rlD2CFD+0u+2ZeT8POQx9D2DjfG8X29Mk3QzcavvaXG5a4Rz1k0l5laX57K6kSKeNSetLFziSUtLBwMEAnVf9fANfYwghhBBqiRHLxUt7zr4ckjfonAEMcFq8uw4wMudJHsv8eZI/AP6XFD00s6yu90ibnC6W9F3gwyrPrJVXeaPtOXk9ZsUlBMUcyxUjxzKEEEJosehYtk+LW/YlzDv5p1/h9J9zgfNynuQhZe16ktTJXYcy+WzzrUnrQncH7qzyzBFUz6ssdlarfW8hhBBCaEUxFd4+3Uda/zi4MNVbzL68DFiVlH15LLAcOfuS1LnakTQNXcv7wMp1ypSyL/9WJ/uymmK25QFl7/2TdCzlzZK+YfvV0huSOgEr5OijR4F/F9pcjA4qz6t8hWbquvrKsQM8hBBCaKEYsWyH8jTyHsDX83GKU4ChwBWkfMuJpM7ncbZfz6OLpezLy2k8+3KPvBGmX5UyN5OyNhs6ArKCoaRjHscAC6zPzGeQHwPcVrYxaCXgVkmTSNP9Q/L1K4Fj82ag7szLq7ybdFZ5CCGEEBahyLEM85E0w3anvHN8IPDNUvZlGzxrKPAbYEPb/87XhgBnAn1tj6tx78XAma2Vabl2tx4+/MTzFrh+4uCdW6P6EEIIYYlRK8cypsJDNScA+5F2bbelycDewMn55z2Bup1F2z9qy0aFEEIIoeliKjxU0wuYBZwnaUg+03yMpA9z9uXLeRr9YkkPSLpa0jM5f3KgpMdz1mb3Os+5EdgNQNIXgOmkqCLytQskjZM0RdJJheujJPWRtGtuxwRJT0t6Ib+/VW7XE5JGSura2l9QCCGEEOYXHctQzfHAmLzTexgpI3Kk7RWALsAbpHWgfyflah4NbEaKEephe2vS5p9qZ5eXvAe8LKknsA9wVdn7J+bh9l7A/0jqVXzT9s25jb1Ja0/PyJt5zgX2tL0VKTrplPIHSzo4d1rHffD+9Aa/lhBCCCFUE1PhoVE7A70Kp9h0BjYEPgHG2n4NQNJzwF25zGTSKUL1XEmaDv8GaUf7DwvvfT8HmS9LCj3fhLRJaT6SjgM+sv3n3EntCdydQ9c7AK+V32N7ODAc0hrLBtoZQgghhBqiYxkaJeBI2yPnuyj1Z/7MyDmFn+fQ2N/YLcDpwDjb7xVO4NmAtGu8r+138+lA5RmdSNqRdEb59oW2TrG9bUOfLIQQQgitIjqWoZryzMiRwGGS7rM9S1IPWpAbWWT7I0k/B54pe2tlUmj79HzO+P8Co4oFJK0PnE/avf5Rvvw0sLqkbW0/kqfGe9ieUq0NXVdbOXaAhxBCCC0UHctQzSTgU0kTSSfcnE06KWe80pDiW6RTcVqF7SsrXJso6Z+kk4ieBx6qcOsg4HPADXmk81Xbu+Qp+3MkdSb9nZ+V6wkhhBBCG4kcy3ZC0pqkzk9f0lTyi/+fvTuPAy3L2gAAIABJREFUu6qq2z/+uRwyFQQcsyxJHJBBSdHUHFDR6mkwytK0THPIBi161CysMIcszSmfNPWnmDmlZmFqjqjgbMjomEpZzgkqDjjw/f2x1oHN4Uz3fc59c2663q8XLw777L322if/+Lb2WtcCvhcR5aN4nW1/BPBWRNzZgrbGAgeSisuVSXMpj2pVpmSzcv/mRsRJjV6zTv8N4zs//r9Fjh25/y4t7pmZmVnPVyvH0qvC20AeAbwKuDUiBkTEIFKO5FotvM0IYJsq9+/MyHVpb/ANSCu5b5G0RhP9a4lOPouZmZm1gAvL9rAj8HZEnFU6EBFTgEmSTpQ0I2dC7gFp9FHSX0rnSjpD0r758yxJR0uanK8ZmHfRORgYXdrCUdI4SSdLmgCcKOmxUmEoaRlJfy/bZrGqiLiMtBJ8r3x9eYbkz/N950p6TtJrkl4sbSUpaV9Jf5J0taQnJX1H0vfz1o13S1o1n3egpPskTZV0paSV8vHis/yi2Ld8zXWSVuzw/ypmZmbWIS4s28MQ4G8Vjn8eGEbKiRxJKgAbCfp+MSI2A84EDouIWcBZLBxlnJjP2xAYGRGjSXmUe+fjI4GpEbHY/t41TAYGVsmQXCvnTN4P/D4iVgb2IW3nWDKEVJhuScqcfD0iPgLclc8F+GNEbBERmwIPkbI1S0rP8r+lA5K+A3wG+FxhYQ+F751jaWZm1kJ+bdjetgUuiYh3geck3Uaag/lKnev+mP/+G6k4reby3DakAvDPpHmeXwfO72Bflf/eiNoZksW+9S8cnxARrwKvSnqZFEEEaf5mKRR9iKRjSQHtvUgr1Ss9C6Sg9n+Risq3K3W4mGO5jnMszczMmubCsj3MJO2RXU4VjgG8w6KjzeXZjqUcyXep/b/xa6UPEfFUfk29E/BRFo5eNuojpBHJehmS1frWSBbmOFKhODW/+h9R6VmyGaTR3nWAJxt9CDMzM+s8F5bt4RbgeEkHRsQ5AJK2AGYDe0i6AFiVFAB+OLA8MEjSCqSicmdgUp17vErKhazlXNIr8QvLRv9qkvQF0s48/0va67tDGZId0Bt4Jre5N7VzNB8gTQUYL+njEfF0rYbft/oqXgVuZmbWJM+xbAORMp9GAbtIelzSTGAscDEpT3Iqqfg8IiKejYingD/k7y4iFVH1XA2MKi3eqXLOeNIr5kZeg5cWAj0GfAXYKSJeiIi3SKOvv8gZmFOoshq9E34M3APcCDxc7+SImETaueeaRhcimZmZWec5x7JNSZobEb3yiu5tIuLiLrzXWFIu5VzSq+MDIuKS/N3PgNsj4qauun9HlX6bCsfHAX+JiCs62uY6/TeM7/70N4scO3y/kZ3uo5mZ2dLKOZY9W39yjE8Xm0J6rb4/8Nv8upmI+Ek7FZVmZmbWvlxYtr8TgO3ya+fRkpbN2Zb3SZom6RuwINvyNkl/kPSopBMk7S3p3pxnOaDOfSZExLp5a8XXgX6Sxkh6KWdLTpH0iKR/5BzJeyX1rtafWnKe5a9y1ubNhfzMajmVH5Z0V/7umEI7UsrwfFDSNcCa+fjOkq4qnLeLpD9iZmZmXcqFZfs7EpiY8ydPIY0ovhwRW5Cihw6U9OF87qbAd4GhpLidDSNiS9KinEMauZmkzYDHIuL5iDiONO/ycFK+5PKkfMpSruYbdfpTzcrA5Jy1eRsL8yyr5VSeBpyZ7/FsoZ1RpHijoaRX+aW5nLcAG2vhTkD7UWHe6CI5lnOdY2lmZtYsF5Y9z67APpKmkBayrAZskL+7LyKeiYh5wOOk3XAgZUH2r9PuaEmP5DbHVvh+I+CZiLgPICJeiYh36vSnmvmkbSAhrULfNn8eImmipOmkVd+D8/GPAZfkzxcW2tmenPOZV33fkvsW+byvSOoLbA1cV96JiDg7IoZHxPCVe/Wp02UzMzOrx3FDPY+AQyLi+kUOSiNoLAuymlMi4iRJnwd+J2lARLxZdt9KK70q9qeDSu2Oo3pOZbVVZtWOn09aCf8mKTz9nSb6Z2ZmZg1wYdn+XiXlN5ZcD3xT0i0R8bakDamd59ghEfFHSV8Dvgb8tvDVw8D7JW0REfdJ6k16FV6xPxHxmqSHI2JghdssQ4okupS0MKmUwVktp/IOYE8W3XYS4HbgG5J+R5pfuSMpoomIeFrS08BRQN2AyvetvopXgZuZmTXJhWX7mwa8kzMhx5HmG/YHJivtmfgC8LkW3/NnwMWSzikdiIi3JO0B/FrSiqSiciRp/uZi/cm5kdV2DnoNGCzpb6RA9T3y8VJO5T9Ir+9LBfV3c3++C1xZaOcqYKd87qOk+ZpFFwFrRMSDHXt8MzMz6wznWHYRSe8j7bu9BemV9CzgexHxaIvaHwG8FRF3tqCtjUijk32BFUiLhQ5q4Lr3A6dHxO6ShgHvj4hr83efBtaLiNMrXFcxh7Kj5zTQvzOAfwL7RMSQWud+8MMbxfePPnORY6P32amZ25uZmS2VauVYesSyC+SRu6uACyJiz3xsGLAWaWStFUaQAs0XKywlLdfBOYWnk+ZY/jlfP7SRi/KCmdIe58OA4cC1+bu/dOD+C0hatiPbSdZo52+kkdHTgX2abc/MzMzq86rwrrEj8HZEnFU6EBFTgEk583FGzpbcAxZkUC4oxHI247758yxJR+fMx+mSBirtxnMwC7dV3E7SOEknS5oAnCjpsUI+5DKS/i7puHx+8c8YYG3gX4W+Ts/XXStpk/z5AUk/yZ+PkXSApP75Wd5Den2+R25zj3xt6R4vS/qacuYl8JAWz+CcIOli0mvtBST1Usq6LD3/bvl4f0kPSTpH0kxJN+RX9EjanPR/mpYnxRCZmZlZN/CIZdcYAvytwvHPk0b2NgVWB+6TdHsD7b0YEZtJ+hZwWEQcIOksYG5EnAQgaX9gQ2BkRLwraQ5pocuppLmQUyNiDDCmvPG8yOUWSXeSIorOj4g5pMUx20maBbxDiv2BFA/0+9L1ef7lT4DhEfGdfPiy3PbmpBXaf6KQeSlpBeAOSaVIpC2BIRHxZFn33gRGRcQred7m3ZLG5+82AL4cEQdK+gPwhdyv80kr1W/LhWxFkg4CDgLot9qa1U4zMzOzBnnEsntty8LcxedIi022aOC60q4xf6N2HuXlhdfI57HwFfDXqRAQXhIR5wMbA5eTXrHfnQu/iaSsyG2Ba4BeSrvh9I+IR+p1OheCFwJ7RcTL1M68vLdCUQlpAdDxkqYBNwEfIE0pAHgyjwRD/m0k9QH6RkRpIc+FVLFIjmXvvvUex8zMzOrwiGXXmMnCuYdF1VZJv8OiRf57y74v5VG+S+3/zV4rfYiIpyQ9J2kn4KMsGtOzmDxf8jzgPEkzSKOu95HmTT4B3EgaZT2QyqOxi5C0LClO6GcRMaN0mOoZnK9R2d7AGsDmOc5oFgt/n2Ju57vAilTP2zQzM7Mu5sKya9xCGmU7MCLOAZC0BTCbNA/xAmBV0mjg4aS5gIPyKOF7gZ1ZmO1YzavAKnXOOZf0avjCWgtiJH0CuDkXbu8jjST+O7/ifgr4EnAMqcA7Kf+p1J9i3uYJwLS893hJZzI4+wDP5/N3BNatdXJEzMlzOreNiEnUKahL1lqtt1eBm5mZNcmvwrtA3lJwFLCLpMclzSRtk3gxKZdyKqn4PCIino2Ip4A/5O8uAh5o4DZXA6NKi3eqnDMe6EWN1+DZrsAMpazM64HDI6K0J/dE4LmIeD1/Xif/XW4CqTiekhclHQbsWljA81lSofsgKfNyBiniqN7/ubkIGC7pflKR+HCd8yHtDf5/ku4i5W2amZlZN3COZZtQF+ReShpOihHaTi3MvcxtfwU4AliW9Cr/PtLCojmtaL+7fWi9jeKwn521yLFDv7LjEuqNmZlZ+1KNHEuPWLYBaUHu5a0RMSAiBgE/YuEilc60eSRpl5of5kMjgG2qnNuhKRH51flo4JMRMRjYjJSn2XB/O3pPMzMza38uLNtDy3MvSfMiXwFeLORe/ljSGznj8iVJz0t6guq5l6tX6e8Y0ujkv3Nf342I80orxSVtLuk2SX+TdL2ktfPxWyUdL+k24LtK2Ztn5gzLJyTtIOm8nE85rvB8Z0q6P+dVHl04Xinjc5kOPouZmZm1iAvL9tBI7uVIUgG4dgPtvRgRmwFnkgrAWcBZwDERsWJEbECaf3kvsEFEjCYt8iktdCnlXr5Ypf3BwORKX0haHvg1sHtEbE5aaX5c4ZS+EbFDRPwq/7sfab/v0aR5o6fk9ocq7VYEMCYPuW8C7KAc2l7lWec3+iySDsoF6/1zX3m5yqOamZlZo1xYtre2zL0skjQ0L855PI+obkQqlG/MeZVHkRb8lFxW1sTVebHTdNIioem5OJxZ6PuXJE0mLWoaDAyq86wNPUsxx7LXKn0aeVwzMzOrwfPc2kNPy72cSZpXOSFv/zhM0hkszJGcGRFb17tnWV/ns2gu5XxgOUkfJq0w3yIiZudX5O+tcP2CZ+1ohqeZmZm1hgvL9tCjci+BnwMnSdotIkp7jK+Y/34EWEPS1hFxV341vmFEzKxz72pWIRWjL0taC/gkcGsD1zX6LACsuWpvrwI3MzNrkgvLNhARIWkUcGpezf0mOW6IlEM5lbSbzBGlfEmlvbGnAY/ReO7lFZJ2Aw6pcs540mvjmq/BI+LavDjmurzDzhxgBnB9DlXfHThdaXvF5UgxSp0qLCNiqqQH8vVPAHc0eGlDz2JmZmat4xzLNtYV2ZZl7Y+gkG1ZzL3sRFtjSds9vkAaRZ0AfDvPl6x1zdyIqLSTT+mc4cA+EXFoB/vToWf50HobxQ+O/e2Cf397rxEduZ2Zmdl/DedY9kBdkW1ZwQhytmV57mUncyZPiYhhpMU1Q4Edmu1gRNzfiaKyPMPTzMzMuoELy/bV8mzLsrzH/qRsy9F59fYdpFHGz0uaQIo2ejGfX9qWcZ6kYnRQNe8hjVrOzvcfIOmvOddyoqSB5RdI2kLSNEl3lZ6v/LkkjZV0WOGaGZL65z8PSzo3XzcU2B/4Rc603LLB39zMzMya4MKyfXVXtuUpETEsIkr7f28IjMzZlr8G/l8ehTwC+EtEjKlxj1KR+gzwaC6EAc4GDsm5locBv6lw7fnAwXk1ed3FNhWsD5xGyrocCOxFims6jDTSu5hFcixfdY6lmZlZs1xY9jztnG1ZehW+JrCypD0l9SK9br88F52/BRYphCX1BXoX9jG/uIHnKfdkWQbmzYV8zP6VLlgkx7K3cyzNzMya5VXh7aunZVsuEBFvS/orKR7pWmBOLjirqfZM5Wo9Y3kGZjEf0/+dm5mZdQOPWLavW4AVJB1YOlCWbblsjvzZnrQ14z/I2ZY55mfnBu7xKtC7zjmlPMg/NJIHmfsp0ijl4xHxCvCkpC+WvpO0afH8iJgNvCppq3xozypNzyIFsyNpM+DDjfSnEWuu2ptv7zViwR8zMzPrOBeWbSq/xh0F7JK3S5wJjCW9Jp5Gyra8hZxtGRFPAaVsy4toPNtyVF6YUy2WZzwpS7ORPMjSHMsZpFHC0lzKvYH9JU0ljcTuVuHa/YGzJd1FGsGsNOnxSmDVfI9vAi2JXTIzM7PWcI5lF+rqHMp8jxEUsiibbGssC7MoS74HnA78MyI+XXb+SsA5pAUzIgWlfyIi5ta4xyxgeES8WHa8V+m6HBe0dkR8t05fa2ZgdsS6AzaKHx5/NgAH79F0SpKZmdlSyzmWS0A35VBCIYuyQh86nUWZ50ReClxAKh4r+S7wXEQMjYghpFHHtztxT4BP5ZHTGcB2wLGdbKeiTv4WZmZm1gEuLLtOxRzKiJiY5xm2PItS0naSxkk6uZBF+Viei4mkZST9XdLqjTxARJwQEeuSVlaX+jSmlGsJfJ8033NMPv+RiJiXz/tTzq2cKemg8rYl/ULStwqHNgYuBLYiLcq5Pj/nboVrxkh6RNJNwEaF48Mk3Z1zMK+S1C8fv1XS8ZJuIxXBZmZm1oVcWHadajmU0L1ZlL9n4WrukcDU8tfQZUpF6pRcnC4iIo4rjGjuAiwPfFrSsZI2KJz69ZxbORw4VNJqZU1dCuxR+PeXgMtJ+6SPys+5I/CrXIhvTlrU8xHS71eMWPod8IOI2IRUBP+08F3fiNghIn5V/iyL5Fi+4hxLMzOzZrmwXDLaPosy/9mx1ok5AH094ERgVeA+SRvnrw/Ni3XuBj4IbFB27QPAmpLen1eJz46If5Lmah4vaRpwE/AB0vSB7YCrIuL1vNJ8PEBeAd83Im7LTV9AWilfclmN/i/MsVzFOZZmZmbN8ryzrlMthxJ6QBZlo/KCmz8Cf5Q0H/gfSWuRRke3jojXJd3K4s8CcAXpN3ofaQST3L81gM1zHuaswrWdWWn2Wv1TzMzMrBU8Ytl1KuZQStoBuJ02z6JshKSPFeYzvgcYRHqGPqQRyNeV9gXfqkoTl5Jeb+9OKjLJ1z6fi8odgXXz8dtJ0UgrSuoNfAYgIl4GZhfikr5KGgHukDX69ebgPXbwinAzM7MmeMSyi0RESBoFnJrjc94kxw2RiqStSVmUQc6iBJBUyqJ8jMazKK/Ii1wOqXLOeNIr8EazKL9S+Pfnapw7ADgzr4BfBriGlDX5HuDg/Dr7EdLr8MVExMxcJP47Ip7Jhy8CrpZ0PzAFeDifO1nSZfnYP4CJhaa+BpyV44+eAPZr4DnNzMysxZxjuYR1ddZlzrlcD9gvIqqFoDfa1kakvb77AisAEyNisRXfddo4Fzg5Ih5spi+t1n/AwDjqFylV6YDdm/qZzMzMlmq1ciw9YrkEFbIuL4iIPfOxYaTFKq0KUT8K2Jz86rjs/stFxDsdaOt00uKeP+frh3akI5KWjYgDOnKNmZmZ9RyeY7lkVcy6BCa1MOdyCPA6cEYh53KSpFeBpyXNy+ePaSDncm3gX4W+Ts/33lfSGYV+/SWPlCJprqSfSboH2DpnSw4vfHecpKk5h3KtfPwzku6R9ICkmwrHx0q6QNIN+Xk/L+mXuf9/lbR8Pm9zSbcp5Whe32CUk5mZmTXJheWSVS3rsqtzLueQInrWBI4H/l9EHEf9nMtTgFskXSdptKS+DfRpZWBGRHw0IiZV+O7uiNiUNO+0tNBpErBVRHyEtMDniMI1A4BPkfYb/z0wISKGAm+Qdu9ZHvg1sHvO0TwPOK5Sx4o5lq++MqeBRzEzM7NaXFi2p7bMuYyI80k75FxO2krybkkr1OnTu6QFPZW8BZRGYIt9Xoe88w5wODC4cM11EfE2KQh9WeCv+fj0fP1GpIL9RqXdgY7K7VV6ngU5lr1XaaRGNjMzs1pcWC5ZM0nzH8t1a84lUMy5vK5WhyPi6Yg4LyJ2y/0ZUqdfb9aIOHo7Fq4eK/b518AZeSTyG2Xtzcv9mF92/fx8vYCZhZD3oRGxa61nMjMzs9ZwYblkVcy6BGbThjmXkj5RmMf4PmA14N+klezD8hzNDwJbNtCvWvrkdiFFCXXEI8AakrbO/Vxe0uA617B6v14csPt2XhFuZmbWBK8KX4LqZF32ov1yLncFTpP0Zv734RHxrKTngCdJr6NnAJMb6FctY4HLJf2blIH54UYvjIi3JO0OnJ6L7+VIcU4zm+yTmZmZ1eEcyx5O0tyI6JVXgG8TERd3oo3hpAU+NYfrWpFjmdsZC8yNiJM6em1X6b/+wPjpL88FYL/Pb7uEe2NmZta+auVY+lX40qM/sFdHL8ojpVcCP2zg9FKO5bCI2Jg0F9LMzMwMcGG5NDkB2E7SlBwFtGzOwrxP0jRJ34AFWZi3SfqDpEdJo48/Ak7OeZADcqbllLI/Y6ieY/leSefn6x9Q2uMbSROVAt/J/75D0ib5n5tKukXSY2VzTA8v9PnowvE/5VzKmZIOKhyvloX5RaUc0KmSbm/5r21mZmaL8RzLpceRpOzKT0PKaARejogtciTQHZJuyOduSooNeom0t/a5EbGlpO8Ch0TE96iQ/SjpaVKO5Z3ADcD5ETEH+DZARAyVNBC4QdKGpEVB+wLfy/9eISKmSfo8sAmwFSnL8gFJ15BWmG9AWvwjYLyk7SPiduDrEfGSpBWB+yRdGRH/YWEW5hhJvyRlYR4L/AT4eET8u1reZv6NDgJYbfW1Ov6Lm5mZ2SI8Yrn02hXYJ2c53kNawb1B/u6+iHgmIuYBj5OKRFiYBVlRjRzLbYEL8zkPk1avb5jP+3ReSf51YFyhuT9HxBs5jH0CqZjcNf95gLQAaGChz4dKmkpazPPBwvFqWZh3AOPyaOiyVZ5nQY5lrz7OsTQzM2uWRyyXXiKNPl6/yMG01eK8wqH5hX+XsiCrioinSaHq50maQRplrJi7GRGvS7qRtEvOl4DiRN/yVWOR2/l5RPy2Qp9HAlvnNm9lYbZlxSzMiDhY0kdJu/RMkTQsj3CamZlZF/GI5dKjPK/yeuCbhdzJDSWt3MwNauRY3g7sXboP8CFSniSk1+Gnk0ZJXyo0t1uem7kaafTzvtznr0vqldv6gKQ1SbmWs3NROZD0Cr1eXwdExD0R8RPgRdIoZ1Wr9+3Ffp/f1ivCzczMmuARy6XHNOCd/Lp4HHAa6bXwZEkCXgA+1+Q9quVY/gY4S2kLxneAffNrdiLib5JeYfGMzHuBa0hF6DF5JPRpSRsDd6UuMxf4CmnbxoMlTSMVrHc30NcTJW1AGgW9mZQJamZmZl3IOZY9QB4dPJW0X/g8coh6RDzaovZHAG9FxJ0taKs86/JvpPmTA/M2jM22P5YuyMD88PoD4+iTzmOfz23TymbNzMyWOs6x7MHyaONVwK0RMSAiBpHigVq5jHkEULGiktTRUe0FWZfAz0lzI8e0oqg0MzOz9ubCsv3tSFqgclbpQERMASblnMoZOT9yD1iQU1laJY2kMyTtmz/PknS0pMn5moFKO/YcDIzOeZXb5e+fl/Qq6fX0PEnH5TaWkfR3SatX6e+CrMuI+F1EvC8iLpd0bSnDMmdd/iR/PkbSAflztQzLMZIekXQTsFHh+ABJf835lhPz/EskjZN0uqQ7JT2htMWjmZmZdTHPsWx/Q0ivk8t9HhhGyqRcnZTt2EgQ+IsRsZmkb5FyLw+QdBaF18t5LuPTwG4R8a6knwIv5+tHAlNzTFAlp1A56/J2UoD7LNI8zI/l87cFfi9pVypkWAKvAXsCHyH99zq58HucDRwcEY/lFeC/AXbK362d2x5I2gv9ivKOLpJjuYZzLM3MzJrlEcuea1vgkoh4NyKeA24jzcGs54/572LmYyWXR8S7+fN5wD7589dZfCHOAjWyLicC2+d+XwP0krQS0D8iHqF6huV2wFUR8XpEvEIqEskrx7cBLs9Znb8lFZMlf4qI+RHxIFWmDRRzLHuv4hxLMzOzZnnEsv3NBCq9yq2YHUkaDSz+H4b3ln1fyqxckPlYxWulDxHxlKTnJO0EfJQcLVRNlazL+0g5lk8AN5JGWQ9k4ehjtQzL77F45iWkZ5yT53JWUszqrPZbmZmZWQt5xLL93QKsoEX3094CmA3sobQn+Bqk0cB7SbveDJK0gqQ+wM4N3KM8A7OSc4HfA38ojGQuplrWZUS8BTxFCkq/mzSCeVj+G6pnWN4OjJK0oqTewGcA8ujlk5K+mM+XpE0beNaKVuvbyyvCzczMmuQRyzYXESFpFHCqpCOBN8lxQ0AvUj5jAEdExLMAkv5AyrV8jPRquZ6rgSsk7QYcUuWc8aRX4FVfg2cVsy7z54nAzjnofCKwTj5GRNxQKcMyIiZLugyYQiqaJxbutTdwpqSjgOWBS3FepZmZ2RLjHMseaEnkWkoaTooR2q6DbY0FfgpsEBF/z8dGAycDW0TE/Z3o37XAXnlRUEust/7GcczJ57H3Z7duVZNmZmZLJedYLkWWRK5lHim9EvhhJ3ItAaaTVnaX7A482NnORcT/tLKoNDMzs9ZwYdnzdHuuJWmF9pXAMaStEh+TdFz+fkrOuZwuaUyVPv8J2C3fcz1SdNELhT7tKumu3I/LJfWS1CdnV26Uz7mkNM8093v1/HmfnHs5VdKF+di6km7Ox2+W9KEmf3MzMzNrgOdY9jxLItdyf2BDYGTOtZwDvBwRw3L+5Dci4gs17vEK8JSkIaQC8zJgv9z26sBRue3XJP0A+H5E/EzSd4Bxkk4D+kXEOcVGJQ0GxgAfi4gXJa2avzoD+F1EXCDp66TdgBbbJ905lmZmZq3lEculR1vmWhZcSnod/jnSq/ySrYBBwB05j/JrwLoAEXEj6TX6/wEHVGhzJ+CKUlh7RLyUj28NXJw/X0j6bRZTzLFcZZV+DTyCmZmZ1eIRy56nx+VaZlcDJwL3R8QreeV3qd83RsSXyy+QtAwpbP0NYFXyVpHFU6iccVnOK9TMzMy6gUcse54elWtZEhFvAD8Ajiv76m7gY5LWz8+ykqQN83ejgYeAL5PC1pcvu/Zm4EuSVsvXll6F38nCxUJ7A5Pq9W/Vvit7RbiZmVmTPGLZw/TAXMti3y+tcOyFvJjoEqWtHwGOyiOaBwBbRsSreb7oUaTootK1MyUdB9wm6V3Ss+0LHEoqRA8nLRLar9E+mpmZWec5x7KbLInsySbaGkud7MnO5loW7jEc2CciDm1F3yXdGRGd3jpnwAYbx89PG8eX/uejnW3CzMzsv4JzLJewJZE9WXb/lmZPFnMtO9EukpaLiPsj4tB8aARV+t6oZopKMzMzaw2/Cu8eFbMnlZwIfJL0+vrYiLgsj+AdFhGfhpQ9SVr0Mk7SLOAC0p7ZywNfJL0OPxh4V9JXSK+v9wdeAj4CTJH0aWCb/Op5GeBRYKvSiuoKStmTxxayJ9/OfT9B0rqk1/ErAlcAb+W+DAIeIS0GuhMYFBEj8ijo+0krz1+UdDZpr/DvVOh7X9Jr7/cA/wH2jojnchsfAtbLf58aEafn32huRPRS2mv8z0C//PscFRF/buh/JTMzM2uKC8vu0S7Zk3uTXsePBKbWKCqTCrYPAAAgAElEQVShRvZkNiYiXpK0LGkRzaERcVwufHfMuZLDgZMK12wObBsRb+TimYiYVaHv/UhFb0g6ADgC+N/cxkBSod4beETSmRHxduEebwKj8srz1YG7JY2PCnM+ijmWq6/xvho/hZmZmTXCr8KXrJ6aPQlpNfZk0oKZwaSRynrG59Xh9awDXC9pOnB4br/kmoiYl4vi51l8OoGA4yVNA24CPlDhHKAsx7JP3wa6ZWZmZrW4sOweM0mjdeW6NXsSKGZPXlerw9nVwFeBf0bEKws6LX2Y9Bp754jYBLim0Mdi38v7/RqN+TVwRkQMBb5R1s68wudKz783sAaweUQMA56r0A8zMzPrAi4su8fSlj25CqlIfFnSWqQ5oiWzWFhE19rmsai8732Af+fPX2uwjeK1z0fE25J2JO/iU0+/Pit7RbiZmVmTXFh2gzy/bxSwi6THJc0ExpK2HZxGyp68hZw9mUcXS9mTF9F49uQoSVMkVYsAGk/KuuxQ9mRETC47NjX3aSbpFfsdha+PBk6TNJE0otiI8r6PBS7PbdSaB1rJRcBwSfeTRi8f7uD1ZmZm1knOseyBOpuJ2Wj2ZBdkYi5YmNPgNfsCwyPiO911/wEbbhy/PP0CvvCJLZu9pZmZ2VLNOZZLkc5mYnYwe3IErc3E7LJ2zMzMrH24sOx5KmZiApMknShphqTpkvaANPoo6S8RcUJErAvsmUcEkTRb0rOSXpf0hqSHcq7mwcDo0qtpSeMknSxpAnCipMfynFAkLSPp7znapyZJt0o6XtJtwHclrSHpSkn35T8fq3DNZyTdI+kBSTflOZ1IGivpvNzmE5IOLVwzRtIjkm4CNur0L21mZmYd4lGjnqeVmZgvA7+KiF/nTMzNIuJwSa/R2kzMor4RsUNu92LSq/lJkj4EXA9sXHb+JDqQaQlsQopI+gjpv+/JVP69Fs2xXNM5lmZmZs1yYbn0WJCJSYoVKmVivlL7skUyMT9f47zyTMw/kwrLRjMxSy4rfB5JWv1e+vcqkspXtq8DXCZpbdJOPE8WvrsmIuYB8ySVMi23A66KiNcBJI2v1pGIOBs4G9Icyw48g5mZmVXgV+E9T0/NxFysndyvrSNiWP7zgYh4tez8zmRaukg0MzNbAlxY9jw9MhOzihtIe4UDIGlYhXM6mml5Oym6aMU8+vmZRjrSb5WVvSLczMysSS4se5ienIlZwaGkzMlpkh4kLRoqN5YOZFrmzM3LgCmkVfATm+ifmZmZdYBzLHuAzuZWdqD9EXQwt7JaJmZncis7StK5wMkR8WCr2lx/w0Fx4hm/Y9SuFWO5zMzMLKuVY+nFO22ukFt5QUTsmY8NIy1UaUlhScqtnAssVlhKWi4i3ik7diTwTdLK8G4XEQcsifuamZlZbX4V3v46lVtZOlfSGYXcylmSjpY0OV8zUFJ/OphbCRwAbB4Rkwr3GSNpSllbV+V8yqk5r3KlfO44SWdKmpAzKHfImZQPSRpXaPNMSfdLminp6MLxW/OIKZI+kZ9nqqSb87EtJd2Zsy/vlOQsSzMzs27gEcv218rcSoAXI2KznFt5WEQcIOksmsytjIjjgOOKr8IlrRYR/8ltHgvsT1rlDdAP2An4LGlO58dIBet9kobl4nlMRLwkaVngZkmbRMS00j1zsXsOsH1EPClp1fzVw/nYO5JGAscDXyj/IYo5lms4x9LMzKxpHrHsuRbkVkbEc0Apt7KeYm5l/xrnledW7pM/dyS3coikiZKmkwrTwYXvrs4LkaYDz0XE9IiYT4pTKvXrS5ImkxYcDQYGlbW/FXB7RDwJEBEv5eN9SAt+ZgCnlN13gYg4OyKGR8TwVfr0a/CRzMzMrBoXlu2vJ+dWjgO+kzMoj6ZyBuV8Fs2jnA8sJ+nDwGHAzhGxCXBNhWcRlTMrjwEmRMQQUtxQ+XVmZmbWBVxYtr+enFvZG3hG0vJ0fKHPKqTi9mWl/cE/WeGcu4AdchFK4VV4Mfty30Zu1neVlbwi3MzMrEmeY9nm8h7Zo4BT82rsN8lxQ6QcyamkUbsjIuJZAEml3MrHaDy38gpJuwGHVDlnPOkVeL3X4MuxcATyx8A9pGJ3OvWL1wUiYqqkB0gjtk8Ad1Q454U8T/KPeVHR88AuwC+BCyR9n1SYm5mZWTdwjmUPs6QyLavlVla4/irgnIi4tnBsKvBgRHy5k33qC+wVEb+pcc6dEbFNZ9oHWH+jQXHyby7ksztXmnVgZmZmJbVyLP0qvAcpZFreGhEDImIQ8CNSpmWrjAAWKdDySOmVwFF1+jedNEfyhsKxjUn/nW0vaeVO9qkv8K0q91wWoJmi0szMzFrDhWXPskQyLYE1Sa+jP1fKtCzlVkqal6+fAlwaEV8oC1TfC7iQVGx+ttCXYhbl6pJm5c+DJd2b254maQPgBGBAPnZifq4Jki4mvWJH0tz8dy9JNxeea7dW/fhmZmZWm+dY9ixtk2kZEcdJug/4RkQslhFZsAdp3uNGwHeAS+r06WDgtIi4SNJ7gGWBI4EhETEs92kEsGU+9mTZ9W8CoyLiFUmrA3dLGh8V5nw4x9LMzKy1PGK5dGjLTMu8ev2FiPgHcDOwmaR6gZF3AT+S9ANg3Yh4o8p591YoKiFFEB0vaRpwE/ABqkwVWCTHsq9zLM3MzJrlwrJn6WmZll8GBubX3I+TIoRKo5vFvi3oV0RcTHpl/gZwfb5PzT6V2RtYg7Tl5DDgOZxjaWZm1i1cWPYsPSbTMsf/fBHYJCL6R0R/YDdSsQlpNXupSN69cN16wBMRcTop4miTBvtU0gd4PiLelrQjsG4jF/XtvZJXhJuZmTXJhWUPkucJjgJ2kfS4pJnAWOBiUm7lVFLxeUREPJtHF0uZlhfReKblqNLinSrnjCdlaNbKtNwe+HdE/Ltw7HZSobs2cBLwTUl3kuaFluwBzMiLgQYCv8v7jd+RFyedWKf/FwHDJd1PGr18uM75ZmZm1iLOsWxCV2dK5nuMoEKuZCfbGgscCLxAej08Afh23qO7I/05BqCYaSnps8CgiDihBf2cRRqlLI2GfqsVz1/LBhsNisceebArb2FmZrZUqJVj6VXhnVTIlLwgIvbMx4aRFoq0rLAk5UrOBRYrrCQtVxbt04hTIuKk/Kr6dmAHUoFZl6TlSPFBmwO7Fr+LiPGkkcxW2TEiXmxhe2ZmZtbF/Cq88ypmSkbERCVdlisp6WRJE4ATS7mSuY1lJP09x+zU8x7SqOXsfG21XMl9JV0u6WpSFuXFwC0RMUnSFpIekHSSpH9KeiH38yVJd+Y/T0jaPbfV6YzJatdKWlnSNZKm5t+79FvvnPs2XdJ5klZo9F5mZmbWOR6x7LxqmZKwBHIlSa/kRwJT64z0jZb0FdKilutywHo9W5MW4byUX4UjaRvg18BuEfFPSTOA4RHxHaVQ9ZVJ8yUHkkYyr6ADGZPABEnvAvMi4qPVrgU+ATwdEZ/K/eoj6b3AOGDniHhU0u+Ab+bfaIFFcizXco6lmZlZszxi2TXaMlcyOyXH8KwJrCxpzwb6dWNEvFT498bA2cBnIuKfVa75U0TMj4gHWZgj2XDGJOlV+LBcVNa6djowUtIvJG0XES+TwtifLMx1vYC0mGgRxRzLPn2cY2lmZtYsF5adVy1TEto3V3KBiHgb+CsLC66KuZLl98ueIY0gfqTGLeYVPpd+j2YyJitem4vHzUkF5s8l/YTqv7+ZmZl1IReWnVcxU1LSDqRFMW2VK1kuLz7ahhRcDlVyJauYA3yKNII4opH7ZZ3KmKx1raT3A69HxO9JEUabkSKG+ktaP1/7VdKocfXGe6/Uga6YmZlZJS4sO6lGpuTTpNXi7ZYrWTI6Z0TOII2K/iYfr5YrWVF+xf8Z4P8kfbTe+VkzGZPVrh0K3JufaQxwbES8CewHXC5pOjAfOKtCmwu8MrfazpFmZmbWKOdYLgFqcf5lXs19SilXUi3Mvszt7QMcQXrFLOC80mKipcWGAwfHow/PXNLdMDMza3uqkWPpEctull9BXwXcGhEDImIQ8COqL2Kp196RwJXADwuHR5Bec1c6v0NJAJI+CXwP2DUiBpNeNb/cmb52hqRlu+teZmZm1hwXlt2vYv4lMKkz2ZfAisB/gDML2Zf/S5r/+EbOuXxJ0qROZl/+kBR99HTu65sRcU6+9kBJ9+UMySslrZSPj5N0pqQJOcdyh5wl+VCOIio9y66S7srZlJdL6lV6Lkk/kTQJ+KKkYZLuljRN0lWS+uXzqh2/Na8Sv1fSozWmEJiZmVkLubDsftXyL4vZlyNJBeDaDbT3YkRsBpxJKgBnAb8CfhQRK0bEBqQ5mHNI2ZejSQt99s7X18u+rJXX+ceI2CIiNgUeAvYvfNcP2AkYTZonegowGBiaC8LVgaNynzYD7ge+X7j+zYjYNiIuBX4H/CAiNiGt/v5pPqfacYDlImJL0mhr8fgCkg6SdL+k+1+eM7vKI5qZmVmjXFi2j3bOvqxmiKSJeYHM3qTCseTqvMBpOvBcREzPe5LPzP3cChgE3JEX3nyNRVeJXwYp8BzoGxGlVd0XANtXO164vu7vskiOZV/nWJqZmTXLO+90v5lUjvPp1uxLScXsy72rX7Ygr/OWCt+NAz4XEVPz6/kRFfo1n0UzLefnfr5LCl7/cr3+dlKjv4uZmZm1iEcsu1/F/EvSnt3tmH35c+CXeSU7uR+H5u96A89IWp7axWkldwMfK2VNSlpJ0oblJ+WddGYX5kl+Fbit2vEO9mGBVXqt2NlLzczMLPNITjeLiJA0Cjg1r+h+kxw3RMqinAoEOfsSQFIp+/IxGs++vELSbsAhVc4ZT3oFXvM1eERcK2kt4Ka8oj1Ir9IBfgzcQyp+p1O/mC22+0Ie5bxE0gr58FFApcilrwFn5cVBT5AyKmsd77BXnWNpZmbWNOdY9gCtzr3MbS7Ivmxl7qWkscDcrsi5zIXoDaUV6nlV/PAaC48attHAwfGIcyzNzMzqco5lD9bq3MvcZnn25QhalHvZxfYF3r+kO2FmZmaVubBsfy3NvZR0NPAl4BXgxZx7eTDw47Lcy+clPUHHcy8rkvSVnCs5RdJv81zSZXPmZekZRudzF8unlLQ7MBy4KLdRmhR5SM7BnC5pYL5+VUl/ytffLWmTjv7oZmZm1nEuLNtfd+RengUcU5Z7eS+wQSdyLxcjaWNgD+BjETGMtFJ779z/D0TEkIgYysL5novlU0bEFaSsy70jYlhElCZFLvI8+djRwAP5+h/l9ir1a0GO5RznWJqZmTXNhWXP1ZNyL3cmRRbdlzMrdwbWIy24WU/SryV9AnilgXzKRp5nW+BCgIi4BVgtt7uIYo5lX+dYmpmZNa2d5s9ZZT0t97ISARdExA8X+0LaFPg48G3SK/rRHWy70vNU+m28Ss3MzKyLecSy/fW03MtKbgZ2l7Rm7v+qktbN8zSXiYgrSdFFm9XJp2yknwC3k4vfvOL9xYh4pdYFvZ1jaWZm1jSPWLa5npZ7mR0l6XuFZ1hH0lHADZKWAd4mjVC+AZyfj8HCVerV8inH5eNvAFvXuP/Y3O404PXcXk2vvuYcSzMzs2Y5x7INdEVOZVn7I2gyp7KUe0kaffwpaWHP3/N3o4GTgS0i4v4W9Hc4sE9EHFred0kHA69HRMUFOZ210caD45GHnGNpZmZWj3Ms21hX5FRWMIImcior5F5OB/YsnLI78GBzXVzYn4i4PyJK20aOoND3iDir1UWlmZmZtYYLyyWv5TmVxVzHQk7l6Jz/uF3OjjxZ0gQayKmMiBMiYt2ImJQP/Qk4OLf3IDAUWJe0YhxJZ+YYn5k5N5NC/1bPn4dLujV/HivpbEk3AL8rPWOVvo+VdFi+7tY8uomk1ZV24kHS4EJm5jRJGzT7P5KZmZnV5zmWS14jOZWrk6J6bm+gvRcjYjNJ3yLlVB4g6SwK2yxK2h/YEBgZEe9KmkNa7HIqjeVUvkJaKPQTYDfgX6R5kKU9xMdExEuSlgVulrRJREyr0+/NgW0j4o38+puImFWh740sRjoYOC0iLpL0HmDZSidJOgg4CGCttRqJADUzM7NaPGLZvto9p/JS0uvwz5Fe5Rd9SdJk0sKhwcCgBtobXwg9b9ZdwI8k/QBYt1q7xRzLPv2cY2lmZtYsF5ZL3kzSaF25bs2pBIo5ldfV6nB2NSkK6J/FKB9JHybtgLNz3vnmmkIfi30v7/drdFzF9iLiYuCzpFXn1+fnMjMzsy7mwnLJ65E5lXkU8AfAcWVfrUIqEl+WtBbwycJ3s1hYRH+hfreB2n0vtrcgRF7SesATEXE6KSap7l7hvVd2jqWZmVmzXFguYZHynkYBu0h6XNJMUg7jxaQsyqmk4vOIiHg2jy6WciovovGcylGlBTBVzhlPysVseLvGiLg0IiaXHZua+zST9Ir9jsLXRwOnSZpIGlFtRK2+nwR8U9KdpHmoJXsAM5S2jxxIlb3Ci+a+9maD3TEzM7NqnGP5X07S3IjoJekzwIkRMbCL7tMXeBxYPYe+bw3cCXwwIv6VR1+fJBWIt5AWHjWViZnvuVdE/KbeuQM3HhIPPzSjmduZmZn9V3COpdWUcyrPAf7TVfeIiDnAs8DG+dA2pJHNUkblVsA9ETG/hbftC3yrhe2ZmZlZDS4sjYg4gTRfcUh+5Txa0lGSnpf0uqQ3JD0laUzOmLxN0h8kPSrpBEl759zI6ZIG1LjVHSwsJLch7eRT/HdxZ6Av5jYfLb0Cz/NNT5R0X86n/EY+3kvSzYX8zt1yGycAA/IzndiSH8vMzMyqcmFpJUcCEyNiWEScAjwPnB4RK5FG/p4jzfuElK35XVIw+leBDSNiS9ICoGp7jUMqHEuF5HrA5UBpKH0bFp2PuVxu83ukLSQB9gdejogtSNFLB+ZV6G8CoyJiM1Lg/K8kKT/T4/mZDi/vjKSDcpD7/XPmvNTAT2RmZma1uLC0anYF9skLYO4BVgNKO9jcFxHPRMQ80rzJG/Lx6dTOzrwD2CYXg7Mi4k3Srpa9SKu77y2cWymPs1qfBBwvaRpwE/ABGtgSs5hj2bfvqvVONzMzszq8845VI+CQiLh+kYNpV5x5hUPzC/+eT43/piLiMUn9gM+QQswhFY77AU9GxNzC6ZXyOKv1aV9gDWDziHg7b+1YnpNpZmZmXcwjllZSnhd5PSnKZ3kASRtKWrkF97mL9Br9rsK/v8ei8yurqdanPsDzuajckbRvOTSW3wlAr5Vdh5qZmTXLI5ZWMg14R9JUYBxwGukV9OQ8X/EF0vaNzboD+B+gFCV0F2m+ZSOF5blV+nQRcLWk+4EpwMMAEfEfSXdImgFcV2meZclrrzvH0szMrFnOsWxzkt4HnEparDKPtHr7exHxaIvaHwG8FRGNFHb12toI+C1psc8KpMVABzXbbpN96g/8JSKG1Dpv40FD4qEHnWNpZmZWT60cS49YtrE8KncVcEFE7JmPDSMtTGlJYQmMAOZSYcRQ0nIR8U4H2jodOCUi/pyvH9qSHpqZmVmP4DmW7W1H4O2IOKt0ICKmAJNynuOMnNu4B6TRR0l/KZ0r6Yy8sAVJsyQdXch6HJhH8w4GRpe2TJQ0TtLJkiYAJ0p6LO9VjqRlJP1dUnH7xKK1gX/lvMspwIW53SmSJlbInxwh6VZJV0h6WNJFuZhG0uY5L/Nvkq6XtHY+vkVu467Sb5CP98/3mJz/bFOlj2ZmZtZFXFi2tyGkVdPlPg8MI+VJjiQVgGs30N6LOevxTNKWibOAs0ijjMMiYmI+b0NgZESMBn4P7J2PjwSmRsSLVdo/hbQd47bABcCIiBgG/Aa4vkL+JMBHSIt3BpHmWn4sL875NbB7RGxO2nP8uHz++cDBEbE1i+43/jywS36+PUijpzUVcyxnz55d73QzMzOrw4Vlz7QtcElEvBsRzwG3kQq2eiplQ1ZyeUSUirbzgH3y56+TCruKIuJ80paNl5Nesd8taQVqZ2LeGxH/yls5Tsn92ohUVN+YrzkKWEdp7+/ehfmgpcB2gOWBcyRNz/cfVOP5Sv1dkGPZr1+/eqebmZlZHZ5j2d5mArtXOK4q57/Dov9noTxDp1I2ZCWvlT5ExFOSnpO0E/BRFo5eVhQRT5OK0fPya+ohNJ6JWeqXgJl5VLJ4fq3qbzRpd6BNSb+Bl3mbmZl1M49YtrdbgBUkHVg6IGkLYDawR947ew1ge9KuNf8ABklaQVIfYOcG7tFI1uO5pFfifyiMZC5G0icKGZPvI41M/puOZ2I+Aqwhaet8/vKSBkfEbOBVSVvl8/YsXNMHeCaPfH4VWLbOMy1i5ZWcY2lmZtYsj1i2sYgISaOAUyUdSRqFm0Wak9gLmAoEcEREPAsg6Q+kTMrHgAcauM3VwBWSdqP6Pt/jSa/Aq74Gz3YFTpNUGi08PCKelVQtf7KiiHhL0u7A6blAXo4UuTSTtF/4OZJeA24FXs6X/Qa4UtIXgQkURl0b4RxLMzOz5jnHspv1sFzK60nRRiuS9t9+BXgqIj4q6WfA7RFxUwf6dVhEfLoD958FDC8uFpLUq7T1Yy62146I7zbaZjXOsTQzM2tMrRxLvwrvRoVcylsjYkBEDAJ+RCreWmUEUDFqR1KHRqgj4uPApaS5mp8jFZZH5e9+0mhR2WKfyvFFM4DtgGOXQB/MzMysAheW3aun5VISESdExLqk+YzXRsSNOafyJUlP5vu8lfMo78rxPZvl7MnHJR1caG4VSVdJelDSWZKWyf04M183U9LRZV04XNK9+c/6wBXAKsBQ0kKi5yRtn9uZKGl9SStLOk8pN/OB/JrfzMzMupgLy+7V03IpAcjzPIcDPwSIiONI8y4PzzmVTwOX5VXcE0l7je8ObAX8rNDUlsD/korCAfm5AcbkIfVNgB0kbVK45pWI2BI4Azg1Lx56lBQntC3p99wuxxqtExF/B8YAt+TczB1Jv+dii4WKOZZz5jjH0szMrFkuLNtDW+ZSAkj6AClsfK+ImFfj1PH57+nAPRHxakS8ALyZ8ychZVY+kftyCem5Ab4kaTJpsdFgFs2gvKTwdyl+aCJpJfz2wM9zO1sA9+XvdwWOzBmYt5Je5X+ovMPFHMu+fZ1jaWZm1iwXlt1rJrB5hePdmktJen1cyqW8rtpFeU7oBcAJEfFgjfaLfZnPotmU8wt9K18pFnkHnsOAnSNiE+AaFn3OqPB5Iml+5ZbAtUBf0tzS20tdB76QR22HRcSHIuKhOv03MzOzJrmw7F49KpeSVPC9GRH/18B9G7GlpA/nuZV7AJNI8yVfA16WtBbwybJr9ij8fVf+fA9pgdL8iHiTtGPPN0gFJ6TczENyYYykj9TrmHMszczMmuccy27UA3MpjwX+lV8pl8yOiB0b6EcldwEnkOZY3g5cFRHzJT1AGs19Arij7JoVJN1D+j9BXwaIiHmSngLuzudMzN9Nz/8+hhTpNC0Xl7OAmjFHr79R6y2/mZmZNcI5lj1UM3mYkoaTFvhsV+OcEbQgD1PSGOCL+Z9DWVj8nRcRpzfYxvrAFXmhUJcYNHhoPDhzev0TzczM/svVyrH0iGUPVMjDvCAi9szHhpHyMGsWlnmk9JvU2fObNGdxLrBYYSlpuYh4p5G+5hXkx+Xr5na0OOxo9qaZmZktOZ5j2TN1Og8zIk4gvS5fP383S9Itkl6X9IakhyQ9SIoFalkeZiWSfi/pc4V/l3bUGSnpJkmXUvb6P+dUPpCzMpfLfbpX0jRJB+RzLpH0qcI1l0n6nwr3XxA3NHv2Sx3pupmZmVXgwrJnanUe5lURsRKpmLwj7wj0K1qch9lBW5Hmmg4tHZC0MXA5sE9ETAYOAp7POZdbAN+W9CHS4qT98jX98nfXl9+gGDfUr9+qLey6mZnZfycXlkuXts3D7IS7IuKfhX+vRXr9/+WIKE2G3BXYLy8uuocUO7QBafX9IEmrkYrfeqvfzczMrAU8f61nmkna2aZct+ZhSirmYdabs1mzX5KWLbv3a2XnziHt8PMx4OF8TMC3IuLm8oYlXQTsBeyb/zYzM7Mu5hHLnqmn5WFWM4uFgfGjgGVrnDsP2A3YX9KX8rHrgW+VFvhI2kjSivm784HDSTmcj9TryEorrtDx3puZmdkiPGLZA/XAPMxqfgv8WdIuwA0sumPPYiJirqRPAzdKei1f/yFgSs5Cf55UfBIRT0t6FLi0kY44x9LMzKx5zrHsAZrJrGyw/RF0IrOyWh6mpK8AR5BGIN8h7eF9WETMaUV/G+zbyqTMzE0j4tV65zvH0szMrDG1ciz9KrzNFTIrb42IAXnF9o9Ii1laZQRpi8RK9684qp1HSq8Eflh2/BPAaOCTETEY2IyUhdnK/tYk6ePAQ6Sit25RaWZmZq3hwrL9dTqzMv/7DEn75s+zJB0taXK+ZqCk/sDBdDCzEjg3ItaNiEmFe40BrgD6ANfk1dpHRsR5pXmOuQ+r58/DJd2a26yYiynpM5LuydmVNyntJ46ksZLOy9c/IenQwm/2TeAF4GBJB1X7YYs5lnOcY2lmZtY0F5btr9WZlS9GxGbAmaTX07OAs2hBZmXeZectYPPc1rB8rKaImF/jHpOArSLiI6T5kkcULh0IfBzYEvippOXz8a9HxObAcODQHDtU6b4Lciz7OsfSzMysaS4se662z6yUNDSPgj5eGlGtodo91gGulzSdtMp7cOGaayJiXi5An2fh6/ZDJU0F7gY+SMq2NDMzsy7mwrL9zWRhJE9Rt2ZWAsXMyuvq9HezfN30vDf4dUApBqjYvwV9q3GPXwNn5B14vlH2PMWl3O8Cy+WFSCOBrSNiU9IK+PLfwMzMzLqAC8v219MyK38OnCRpncKxFQufZ7GwUP5CA/foA/w7f/5anT6Wzp8dEa9LGkjaGrIu51iamZk1z4Vlm4uUBzUK2CW/Up4JjAUuJuVSTiUVn0dExLN55K+UWXkRjWSTzuEAACAASURBVGdWjiot3qlyznhSRmbN1+ARcS1wOnCdpAcl3UkaTSzt1X00cJqkifl4vXuMBS7P5zeyF/lfSSOX04BjSK/D63rjTedYmpmZNcs5lj1AO+RYVsusrHDeWOBA0qrs9wITgG/nBTr1+tHQPRohaRYwPCJelHRnRFSMUyoZPGRozJzhHEszM7N6nGPZg7VDjmW1zMoaTslzKwcBQ4Ed6l1QuMdRDd6jYfWKSjMzM2sNF5btb4nnWAL7k0b/JhUyJo/L5xf/jCnr+3tIo5az8/1vzaOS5IzKWfnzvqR5l9NIsUEdeoZ8fDVJN+S8y99SWNwkaW6lH7aYYzn7JedYmpmZNcuFZftr1xzLMYWsyvLMytE5HP0Z4NFcCNezNfC1iNipo8+Qj/0UmJTzLseT9hCvqZhj2W9V51iamZk1y4Vlz9XOOZalV+FrAitL2rOBft0YEY0OG1Z6hu1JBTARcQ15lNTMzMy6jwvL9tfTciwXiIi3Sau0t6/Qt/J+vVb43Nln8Eo0MzOzJciFZfvraTmWC+SFR9sAj+dDs1hYJO9e49LOPMPt5Nf1kj4J9GukjyUrvtc5lmZmZs2qNWJlbSAiQtIo4NS8cvodUhH4DrASMAd4+v+zd+dRdlV1+v/fD6MMAkpQQQhBBGIgoRICCgIdJODQ0BABQXFgjIBCGxsRCV8NKLY/oQERBcHGoIIigxgZBEEiCQgmhFQGBsMQRQFJgEBHCOPn98feJzmp3HvrVNWtSlXlea1Vi6pz99lnnwu9eruHZ5NzLAEkFTmW86ieY3mNpAOA/wU2qVFmEmkKvMpxjuMkfRpYE3gBaJF0FLA68PG8Eef3De4fTupcduQdzgB+IWkGaVnA3yrcs9SSV17tSHEzMzOrwTmWfUgeAbwbuLzYJS6pBXhradNNV58xAVgcEee0ud7hjElJHwHOAv4jIv4haXXS6Tl3RcTDzWhvs+wwdFjMmT1rZTfDzMys13OOZf+xsqKHpgBTgSclzctT75SihwbUae940s7zf+S2vhERlxWdytyGAfn3kZIm59+PkHRh/n2ipAsk3S3pMUlLp9AlfUXSNEmzJJ1Run69pPskzZU0tvNft5mZmXWEp8L7lirRQwOAaZLurFDfwogYIekEUgfwGEkXUxqxlHQ0aTp7vYh4Q9I3gMMlrUfaIb4xcFsaTOXqUuQQwPbAjE696fI2Je2CH0yakr9G0r7ANsAupI1MkyTtGRF3AkdFxHOS1iF9F9dGxLNtK82dzrEAm2327iY008zMbNXmEcv+ocejh3IHchrw6Ro5liuQNDSPgj5ajKh2wPUR8WZEPMCyE4f2zT/3kzqvg0kdTYCTJLWSzgnfonR9Oc6xNDMzay6PWPYtc6m9m7pHo4cklaOHDq9/G3OBEcAdETGbtInnQmCdGu1r27Za7YRl7yrgvyPiR+WCSueejwZ2jYiX8vR6o7rNzMysSTxi2bf0teih/wbOkbR56do6pd/nsyx+6KAKbSu7BThK0voAkt4t6R3AhsDzuVM5GPhAB+s1MzOzTvKIZR9SI3poCalz9iVgfaCVFBLerOihE+uUqRQ9FBE35Y7uzXlH+CJgDqlTCCki6H8lnQbcW6Ft5bpvlfQ+4E95fedi4NOkQPbjJM0CHiZNh7frLWuv1ZHHm5mZWQ2OG+qDJL0LOJ+0jvIVcucyIv7SpPpHAa9GxN11Pq8cPZTji74BbBMRj+Rr44BzgZ0jYnqDeyeTNhXVLVPh+WcCd0bEbY3KDR06LGY7bsjMzKxdjhvqR3KW5a+ByRGxdUQMAU5j2aaWZhhFOjGn1vNPA64FvtaB+mYD5fPCDwYe6GzjOiIivt5ep9LMzMyawx3LvmdlZVmeK+kO0qk8r5KmmYssy2fz/TNLP+NLbb4eOCCXfw8pvmhBqU0XSZqecyfPoIZaZSTtIum6/PsBkl6WtJakt0h6LF+fWM6+NDMzs+7jNZZ9z8rKstwWGJ2zLBeRdoOfT9qBPTkiGm2+eRF4QtIOpA7mVcCRpc/H59zJ1YHbJQ2LiLbz0iuUIcUMDc+f70Fav7kz6b/rdtdsOsfSzMysuTxi2X/0eJZl/v0oqp0f/kvSdPiBpKn8sk8onfF9PylUfUiN+1coExGvA4/kTTy7kNZt7knqZLZ7xGU5x/LtzrE0MzPrMncs+565LIvoKevRLEugnGV5c6MGZ78FPgP8LSJeXNpoaSvgZGDviBgG3Ni2je2UmQJ8FHgNuI3Uwd4dqDJaa2ZmZk3kjmXf09eyLAGIiJeBrwJtT+fZgNRpfUHSO0mdxLYalbmTFLf0p4hYQDpicjCpA25mZmY9yGss+5i+lmXZpu2/rHGtVdL9pI7gY8BdHSxzL2lHfDFCOQt4JjqYo7W2cyzNzMy6zDmW/UhP5lt2JMuyTl0TgGMp7Q4HRkXEoi43dNkzvgRcEhEvtVd26LAdY/as1mY92szMrN9qlGPpEct+opRveXlEHJavtZBG85rSsSTlWy6WtCdwPKVzwiWtkTfTdMR5xc7zbvIl0nR9ux1LMzMz6zp3LPuPmvmWSs4mrUsM4FsRcVUefTw5IvaDlG8JTI+IiZLmA5cD+wNrAoeQptyPI23yWUA6PvEYSR8nRf6slUcx/5LLAGwBbBcRC6u+hKR1gYmkdZIPknaqf4EUo7RDRIzL5Y4F3gdcQDrG8d7cjr+QdqwfA2wG3CFpYUTsVbUNZmZm1jnevNN/VMm3HA2cLWnTCvUtjIgRwEWkDuh84GLSKGNLRBRxPkW+5QeBbwP/GxEtwCmkfMtGncoihH1mDl8HOAF4Pu/+/ibLdsD/EvgPSWvmv49k2frO7UhT3sNImZknRMQFwJPAXvU6lZLG5tD16c89+2yFr8TMzMwaccey/+vN+ZZFJ7Wl1PnbndSJJCLmkDbjEBH/Iu2I30/SYGDNiJid73kiIooNPT/PdbRruRzLjTeucouZmZk14I5l/9FX8y3bqtdeSBFHR7D8aCWkKX4a/G1mZmY9wB3L/qNP5lvWMBX4RG7/EGBo8UFE3Etat/kp4BelewZK2jX//slcR9X2ArD2Wmu2X8jMzMwacseyn8i5jWOAfSQ9KmkuMAG4kjSd3ErqfJ4SEU/n0cUi3/IKqudbjslrIuvFDE0i5WlWybcsr7GcKWkQ8ENgE0mzSIHqs4AXSvf8CrgrIp4vXXsQ+Fy+5+2kdaEAlwA3l9ZvmpmZWTdyjmUf1pO5lR24p26+paRPkzb1rE6aip9G2hi0KO9EH0kaYV0zIpZI2hq4Hdg2Il7NddyQ6789/z0IuCEidujsewIMG7ZjzHKOpZmZWbucY9kP9WRuJbBCx7JWbmU+CWi5fMvSZx8BxgEfjYh/SFod+FxubzkUfV1SRNCapPWWx0fEq5I2Ik3htxadSjMzM+tdPBXed9XMrQSmSjpb0hxJsyUdCmn0MY/2kf++UNIR+ff5ks6QNCPfMziPBB7HsunqPSRNlHRunlo+W9K8vG4TSauRsiN3ioippeeMlzQTuAbYELhR0vi8S/2yiHi49E4nknatrw0cmuODnpV0N3AHsBA4Pdd7hKTrSBFIa0v6bumZF+UYobmSzmjCd21mZmYVeMSy76qSWzkAmCbpzhrl2loYESMknUCanj5G0sXA4uJ0HElHsyy38g1Ji0ijk+eTMjJb2+ZWRsRZwFmSniN1OsvrJRu2gdRRfQjYMyJelzSalJV5UC7fQgpFfwV4WNL389rR8RHxXB4VvV3SsIiY1fZhksYCYwHe/e53V/iKzMzMrBGPWPY/vTm3EgBJQ/Mo6KPFiGqDNmwIXC1pDnAesH2p/O0R8UJELAEeALbM1z8haQZpQ9L2wJBa7Vgux/LtzrE0MzPrKncs+66+lls5FxiR75udT+e5GVinnTZ8E7gjb87Zv027Xyn9/gawhqStSKOde+ep9BtZ8V3NzMysG7hj2Xf1tdzK/wbOkbR56do69QqXbAj8I/9+RIXyG5A6vy9IeifpjPR2reUcSzMzsy7zGss+KiJC0hjg/Lwbewk5boiUI9lKOoHmlIh4GkBSkVs5j+q5lddIOoC0saaWSaQp8IbT4BFxU+7o3pzXPi4C5gC3tNOG7wKXS/oyqTPdUES0SrqfNEL6GHBXO7eYmZlZk/S5HMvuzm7MzxhFB/MbG9Q1ATgWWACsB8wGTo+IB5pQ92bABRFxcDvlbgI+FRGLGpXrZBtGkk66mUfqyD4PfDYi/trk5xwBjIyIL9b4bHFErF/1+6hlxx1borV1ZhNaamZm1r81yrHsU1PhpezGyRGxdUQMAU4jZSE20yhgtzpt6Mwo73kR0RIR2wBXAX8oYnq6IiKerNKJioiPdVOn8lTgWlJncq+8pnEyORKop1X9PszMzKx79KmOJXWyGyNiipKVkt8o6RFJA6q8QERcBdxKOu8aSXtLuj8//zJJa5fa9m1Jf8qZjCMk3ZJ3Uh+XywzKu6WX5jpK+l1uXznXcX7RPkmflTRLUqukn+Vr+0u6N7fjtrw2EUkTcpsmS3pM0klt3uU7EbEly2+i2ZK0xrM4pvGvkp7Iv/8oT4MjabGk/8nf/e2l73NyHgVF0gClE3kKW+T3e1jSN9p+t22+j9UlnZO/11mS6k3lm5mZWZP0tY5lvexGWD6/cTSpA7hphToXRsQI0vnSJ0fEfFLodjHKOCWXK/Ibx5E2qxSny9TMb2zHDGCwpLcAE0lh4ENJa16PL5V7IiJ2BabkcgcDHwDOrFNvC3AoMJTUudui/KGk7YHxwIciYkfgP/NHU4EPRMRw4JekYxcLg4EPA7sA31A6EaeRRaTvsQX4JGlN53vy32+w7HtbD5iRv/s/Ait0FGvYJd/fAhxSdEDrGAtsBQzPI6lXtC0gaWzutE9/9tlnKzzezMzMGulrHctGen1+Y0kRCbQd8HhpfejlpF3chUn5n7OBeyPi/yJiAbBE6YjDturlOhY+BFxTdIIj4rl8fXPgFkmzga+wfFbkjRHxSr7nGeovO7hD0jOkjvaV+drepEikaUqn7+wNvCd/9iZpWQCkjvrudeot+31EPBsRL5P+vTW6ZzRwcXHsZOldlyrnWG68sXMszczMuqqvdSzrZTdC781vrGU48CD129y2bW+y/HTzm3XaukKuY5vPRdpg09b3gQvzqOnnaScrsk5b9yJ1ZOeybERVpLPMW/LPdhExoc79RbvK/77a/rtq2/ZGO8/qvauZmZl1k77WsayZ3Sjp34A76Z35jcuRdBCwL/AL0nGFgyS9N3/8GdJIa3e5nXQqzca5LW/P18tZkZ/rbOV5JPFLwGdz3bcDB0t6R/E8ScUo6mqkqX1I602L88Xns+x/PLTdiLNPrmMd4EAaRwndChxXbLYqvWtNa67p5C0zM7Ou6lMdy0jZSGNIHYxHJc0FJgBPknaLzyLlN/6BnN+YRxeL/MYrqJ7fOKbYvFOnzCRSXmSVafBiI9A84NOkNY4L8pT1kaQjC2eTRiIvblRRV0TEXOAs4I+SWoFz80cTchumAB1ZK1rrGU+ROs1fyJFKpwO3SpoF/B4o1r3+C9he0n2kKfpilPMc4HhJd5POOi+bCvwMmAlcGxHTGzTlx8DfgFn5XT/VlfcyMzOz9vW5HMveIm8cOS8i6nU8m/28bs3vVHOzO29h+bWY7yBtRHp/qcziiFi/E3XXvE/SmcCdEXFbZ9rsHEszM7Nq1CDH0vN/naCU33g8y3Y4d/fzivzOyyPisHythdR5a1Yw/ChgMbBCx1LSGsUmmCoi4sOle9cjbYzq1mzLiPh6d9ZvZmZm7etTU+G9RZHfGBHFukAkjS9lNxY/45v0yJr5ncBU9f7szu8BN0XE7/O9x0qaBjwq6VpJ6+brEyVdJOmOnJn5b0oZmg9KmliusE7+5URJB+ffvy5pWv5eLskdczMzM+tm7lg2SUScVdr9XPyc1aTq6+V39ursTqWzzEcCXytdvi4ids45mg8CR5c+extpveU40jrX80jRR0PzCC1Uy7+8MD9jB2AdYL867VuaY/ncc86xNDMz6yp3LPu2XpvdKendwAWkM8rLkUU7SJqSNysdzvKZmb/NG7RmA/+MiNkR8SYpwqhoZ5X8y72UThKaTeqobl+jzHI5lm9/u3MszczMusody76hXn5nr8zuzFPPlwPfyTvDyyYCX8yZmWdQOzOzam4ntMmqVDrN6IfAwfkZl7Li+5uZmVk3cMeyb6iZ3wk8T+/M7jwZWBIRP6jx2VuBp5SOhuzM5qd6+ZeFohO5UNL6rJiFWZNzLM3MzLrO/9+0D4iIyOsVz8870peQ44ZIWZqtpJG7UyLiaQBJRXbnPKpnd14j6QDgxDplJpGmwNvL7vwW8HelYxwLz0fEXsD/A+4ldX5n035ntq1y/uULpLPRl4qIRZIuzXXPB6Z1sH4zMzPrJOdY9lErI9eys9mdkiYAxwILSpdHRcSiNuU2Ay6IiIPzZp3NIuKmTr5Ch7S0DI+ZM6v0v83MzFZtjXIsPRXeB5VyLSdHxNYRMQQ4jeVDybtqFLBb6ZmnAtcCXyuOSeygYsd58dO2U7lGRDwZEcXUdQvwsVoVdfL5ZmZm1s3cseybejzXEhhM6lh+k2W5lmeVMjtfyfdXzu6UdISkqyX9lnTs46Dc9rVIRzwemus+VNKEnEl5K/DTvK707JxXOUvS53Od6+d8y+J9DujC92xmZmYd4JGfvqlKruUAYJqkOyvUtzAiRkg6gZRreYyki4HFEXEOgKSjWZZr+YakRcALEdEiaV/g8xFxUINnjJP06fx7sd4SYFdgWEQ8lzu0RMSrkr4OjIyIL+bnTyDtjN89Il6WNDY/f2dJawN35U7nE8CYiHgxB7jfI2lS1FjzkesYC7D55ptX+JrMzMysEY9Y9i+9NteS5afC9ypd/31EPFehjQCTIuLl/Pu+wGfzBqF7gY2BbUgRTN+WNAu4DXg3dZYIlHMsN964yiFCZmZm1ohHLPumudSO0enRXEtJ5VzLzp6b/q/2i9QsK+DEiLilXCBP8W8C7BQRr0maj3MszczMeoRHLPumvpZr2RntPf8W4Pich4mkbSWtB2wIPJM7lXsBW1Z52BprrN7V9pqZma3y3LHsg/J6wTHAPpIelTQXmABcScqubCV1Pk+JiKfzqTlFruUVVM+1HFPavFPLJFKOZnvT4LBsI1DxM6id8neQOsMzi01IbfwYeACYIWkO8CPSaOsVwEhJ00mjqA9VaJuZmZk1gXMs+5iVkV/ZoGy7uZZ5w84pwOqkKflppA1Ci+rdszIMbxke9zvH0szMrF3OsewnVkZ+ZZvnr1H6fWmuZYP2fgQYB3w0IrYHRgB312qvJM9Fm5mZ9XHuWPYtPZ5fKWmipHMl3cGy/MpNIuI7wFbAxBzrg6Tx5elu4Brg/oj4R27rGxFxWUQ8XGrD1yVNBQ6RtLWk30m6T9IUSYNzuU0kXZszK6dJ+mC+vr6kn+T2z5J0UL6+r6Q/5Xe7WunMcDMzM+tm3hXet/SW/MrDSdPxo4HWiFgIEBFnAWcVlUt6DvivdtqwJCJ2z+VvB46LiHmS3g/8EPgQ8D3SlPtUSQNJG3feRzp3/IWIGJrvf1vu5J6e2/svSV8FvkwKXF/O8jmWW1T4uszMzKwRdyz7h6X5lcA/JRX5lS+2c185v/LjDcq1za/8DaljWSW/EgBJQ4GfkXZ6nxYRV+WPrsqfr0+agr86zfgDsHb+52jSRp7i+gaS3pqvH1ZcjIjnJe0HDCEFpgOsBfypVpsi4hLgEkhrLKu8h5mZmdXnjmXf0tfyK+eS1lXeERGzgRZJFwLr1Kh7NWBRRLTUqGc1YNdSODqwdM1p2w6hSKHrn2zQLjMzM+sGXmPZt/S1/Mr/Bs6RVD4vcZ1aBSPiReBxSYfk95KkHfPHtwJfLMpKaqlz/W3APcAHJb03X1tX0rbtvA+rO8fSzMysy9yx7EP6Wn5lRNwEXADcLOkBSXeTRkdvqXPL4cDRklpJo50H5OsnkbIpZ0l6gLTBCOBbwNvypqVWYK+IWAAcAfxC6VjHe4DB7b61mZmZdZlzLFcBzc6+bJtf2ZHsywp1T6C0eShfmw+MLDYJ1bnvJuBT+c9PRcQP8/XNgAsiotYSgqWGDx8e99/vHEszM7P2OMdyFdbs7Ms6+ZWjqJB92Z0i4mM5dH0j4ITS9Sfb61SamZlZc7hj2f81NfuStEbyWeCiUvblfwHflvRyzrl8TtLUttmXuY7VJD1SZF92lKTrc87l3BwXVFyfn+v8DrB1nso/W9IgpSMfzczMrJt5V3j/1xPZl//D8tmXE3OdB7SXfVnHOKWjIAublX4/KiKek7RObvO1EfFs6fNTgR2K3eVqcCZ5OcdyC+dYmpmZdZlHLFddS7MvI+KfQJF92Z5y9uWgBuXaZl9+Nv9eJfvyvIhoKX6AJ0ufnZQ36twDbAFsU6HNNUXEJRExMiJGbjxg485WY2ZmZpk7lv3fXGCnGtd7NPuSFNxeZF/e3KjB9eRNQqNJmZY7kna5t22fmZmZrSTuWPZ/fS37spENgecj4iWlc8Q/0Mm2rGD11Z1jaWZm1lXuWPZzfS37sh2/A9bI+ZTfJE2HLyevt7wrb0o6uwvPMjMzsw5yjuUqpNl5ljXqH0WdPMu22ZcV6poAfAPYJiIeydfGAecCO0fE9Ab3TiZtLJpe5FvmKKK6RowYETNmzKjSNDMzs1Wacyyt6XmWdYyiRp5lnezLKmYDh5X+Phh4oCMVlPItzczMrJu5Y7nqaGqepaQzJM3I9xR5lseRooJmStpD0kRJ5wIfJu0m/0kpz/J0Sa/k+2fmn/Ft2nw9+VhHSe8BXgAWlNp0kaTpOdPyjFovXcq3NDMzs27mHMtVR0/kWV7M8nmWRwPbAqNr5Fn+GbghIg5q8IwXgSck7UDqYF4FHFn6fHzOtFwduF3SsIiYVaHt5PYty7HcwjmWZmZmXeURS+vNeZYAvyRNhx9Imsov+4SkGaQNRtsDQyrUt1Q5x3LAAA9qmpmZdZU7lquOvppn+VvgM8DfIuLFpY2WtgJOBvaOiGHAjTXaaGZmZj3IHctVR5/Ms4yIl4GvAme1+WgDUqf1BUnvBD5aoX11rbaa/0/BzMysq7zGchURESFpDHB+3qW9hBw3RMqXbAWCnGcJIKnIs5xH9TzLayQdAJxYp8wk0hR45TzLiPhljWutku4njcQ+BtxVtT4zMzPrHs6x7IdWZl5lhXuXy7PMeZVLN/yUyt0dEbvlZ50cEft1ueENjBw5MqZPrxuNaWZmZplzLFchKzOvMj+/7ih4R/IsI6Jm/WZmZtZ7uWPZ/6y0vEpJdwBnS5pXyqtcTdIjkgZExHciYsuImFpq7x6lupbmWUpaXCqzgaRfS3pA0sW5zqMlnVdq97E5MxNJ10u6L+dbjm3qt2tmZmZ1eY1l/9Pb8ipHA60RsbBO/VOAm2tMhZdHNXchRQn9lXRe+MdJMUSzJJ0SEa+R8i0/n8sflfMt18nveW0+Q3w55RzLgQMHVvgqzMzMrBGPWK46enteZSN/jojHcv2/AHaPiH+RdrrvJ2kwsGZEzM7lT5LUCtwDbAFsU6vSco7lJpts0sUmmpmZmTuW/U9fzatspO0Os+LvHwNHkEYrfwJLNxaNBnaNiB1Ju9mdb2lmZtYD3LHsf/pkXmU7dpG0laTVgEOBqQARcS9pRPJTpJFMgA2B5yPipTyS+YEuPtvMzMwqcseyn4mUHzUG2EfSo5LmAhOAK0mZlK2kzucpEfF0Hl0s8iqvoHpe5Zhi806dMpNI+ZhVpsFPl/T34qfG538CvgPMAR5n+aMdfwXcFRHP579/B6whaRbwTdJ0uJmZmfUA51j2I5IWR8T6eef2bhFxZTc+azvgR8BGwNrAlIgYW/p8ubzKDtY9HxjZYMNPuewN+Tm3d/Q5Zc6xNDMzq6bLOZaSvitpA0lrSrpd0kJJn25uM62JBpGmh7vTBaQOXUtEvA/4fvFBe3mVjbIuq5K0kaS/AC93tVNpZmZmzVF1KnzfiHgR2A/4Oyla5ivd1irrqu8Ae+Sp6nF5XeXZkqZJmiXp87A0w/KPkn4l6S+SviPpcEl/zrmVWzd4xqak/xYAKHZkS3oLsB3wIvB9SXvl69dIWiTpBeD53LZ7ctbkDZJuknRwqf4Ty/mZuY4Jkk7Oz1sEvAp8RdIgSQ9J+nHO6bxC0mhJd+VMzV2a9cWamZlZfVU7lmvmf36MFFnzXDe1x5rjVNLUdEtEnAccDbwQETuTIoaOlbRVLrsj8J/AUOAzwLYRsQtp8029874BzgP+IOnm3HndKF//AkBEDAU+CVyeO5s3AIuBrSLircC3gOfyc48Bdm1T/8KIGAFcBJxc4Z3fC3wPGAYMJo3Y7p7vPa3WDZLGSpouafqCBQsqPMLMzMwaqdqx/K2kh4CRwO15V/GS7muWNdm+wGclzQTuBTZmWbbjtIh4KiJeAR4Fbs3XZ9MgtzIifgK8D7iadMTjPZLWJnXmfpbLPETadb5tvu33pf9Rsjsp+/LNiHgauKPNI6rmZxYej4jZEfEmKXLp9ryRqe57OMfSzMysuSp1LCPiVNKI0sh8yslLwAHd2TBrKgEn5hHMlojYKiKKDuQrpXJvlv5+k3ZOZoqIJyPisog4gJSHuQP18zKhlHXZTrlyu8r5mY0yNzv9HmZmZtYcVTfvrEua4rwoX9qMNHppvVPbnMlbgOMlrQkgaVtJ63XlAZI+UqrvXaRR0H8Ad5KOc0TStsBA4OEaVUwFDsrnfr+TNOrZnvnAiFz3CGCrhqXNzMysR1UdyfkJaUpyt/z330lToDd0R6Osy2YBr+djDSeS1h4OAmZIErAAOLCLz9gX+J6kYknEVyLiaUk/BC6WNJs0wnhERLySHruca0lh7HOAv5Cm6F9o55nXsmxKf1q+z8zMzHqJSjmWkqZHxEhJ90fE8Hytg+J7FAAAIABJREFUNR+ZZzXkUbzzSZtlXiGNtn0pIprSGcpHF74aEXc3oa4JwOKIOCdvtPktMDUizuhq3bn+ycDJETG9zfUid3Nj0ilAH8zrLWvV0QJsFhE3NaNNbTnH0szMrJou51gCr0pah3xGc46heaXxLauuPCr4a2ByRGwdEUNIO5Pf2cTHjGLZCHLb53dqTaGktUijgvc1q1PZjnXy6OMU4Jv1OpVZCymVwMzMzHqpqh3Lb5COyttC0hXA7cAp3daqvm8v4LWIuLi4EBEzgak5T3JOzmc8FJbmSS5dViDpQklH5N/nSzqjnOmYT9Y5DhiX8yD3kDRR0rmS7gDOzvmNm+Q6VpP0iKQBDdq8BvBLYF7erFW05QFJL0l6WdIT+Xk/y/+cKelhSY/nsl/PWZlzJF2iNvPfuR2XS/pWvvQycCPwGnBcXmuJpENyHa2S7swd3jNJZ53PlHSopF0k3S3p/vzP7fK9R0i6TtLv8nfw3Q79mzMzM7NOqzSyFRG/lzQD+ABpN+9/VjlubxW2A2lNalsfJ4287QgMAKZJurNCfQsjYoSkE0hTysdIupg8fQ0g6WhSrM/oiHhD0iLSJprzgdFAazv/zk4BbouIL7W5vntEPJdHrKcBe0fEs8WHkn4F/DH/eWFEnJmv/4wUqP/b/NkapLPI50TEWfnaesA9ETE+dwCPJeVbfh34cET8Q9JGEfGqpK+TUgm+mOvfANgzIl6XNBr4NnBQrrcFGE4aVX9Y0vfzmejLkTQWGAswcODABl+NmZmZVVF1xBLg3cDqwFrAnpI+3j1N6td2JwXMvxER/yR1yHaucF/VTMerI+KN/PtlwGfz70eRNmA1MhXYNe/kLjspbwK6B9iCZfmXSDqFdKTiD/KlvSTdmzfufAjYvlTPj1i+Uwnp5JxipLb8bncBEyUdS/pvrpYNgaslzSGFtZefdXtEvBARS4AHgC1rVeAcSzMzs+aqNGIp6TLSiSZzSbmAkNZbXlf3plXbXODgGtfrZTc2ymeE2pmOtSzNiYyIJyT9U9KHgPeTI4AauBO4HLhZ0h4R8WTeIDQa2DUiXsqbcN4CIGlv4BBgz/z3W4AfkkYVn8gbgsrvcTep4/k/ucMHablAsXts6btFxHGS3g/8OzAzb9xp65vAHRExJi8NmFz6rLz+t73vzMzMzJqk6ojlB/LIzuci4sj8c1S3tqxv+wOwdh5xA0DSzsDzpHWCq+f1j3uSdkP/FRgiaW1JG5JieNrTNquylh8DPwd+VRrJrCsirgXOBn6ndETjhsDzuVM5mLQUAklbkjqRn4iIl/PtRSdyoaT1WbFj/b/ATaRRxoYdPUlbR8S9EfF1YCFppLTt+25Iys0EOKK9dzMzM7PuV7Vj+SdJQ7q1Jf1IHoUbA+wj6VFJc4EJwJWkjMlWUufzlIh4Oq//+1X+7Arg/gqP+S0wpti8U6fMJGB92p8GL7f9YtJI9CTSKOAakmaRRgjvycWOIAWi/zo//6aIWARcSjpC8XrSesy2dZ8LzAB+JqnRf3tn541Kc0gjqa2kIx+HFJt3gO8C/y3pLupPl5uZmVkPqppjuSepI/M0aZpRpP7TsO5tnrVHDfIyJY0EzouIeh3PKvWPonl5mduR1lpuBKwNTImIsR24/whKG3iayTmWZmZm1ahBjmXVtWeXAZ8hjUa92U5Z6yE5zufXwOURcVi+1gK8M2+uOp7211a2ZxSwmLRGsu3z14iI1ztQ1wWkju5v8v1Du9g2MzMz60WqToX/LSImRcTjEfHX4qdbW2ZV1M3LJE1V/x9wkZblZf5Y0gulDMoFkq7Jn/VEXuampONAi7bOzvcdIenC4rqkG/JIKZKOlPQXSX8EPlgqs3/egX6/pNu0LANzgqTLJE2W9Jikk7ryBZuZmVl1VUcsH5J0JWk6fOmO24jwrvCVq6N5mT8H3hUR+0EKYgfK87/dnZd5HvAHSXcDtwI/yWsza5K0KXAGsBPpHPE7WLb+dCppU1lIOoaUw/lf+bPBpE73W0k5lhdFxGs16neOpZmZWRNVHbFch9Sh3BfYP//s112Nsi7rlXmZEfET4H3A1aQp9nskrd3gOe8nHYu5ICJeBa4qfbY5cEvOzPwKy+dY3hgRr+QO7jPUOUrTOZZmZmbNVfXknSO7uyHWKX0uLzMiniR1Ri/Lu753aKdd9XaXfR84NyIm5WnzCTXeo8q7mJmZWZNUGrGU9BZJX5D0w7x+7bIcmm4rV5/Ky5T0EUlr5t/fRVoH+g/STvaWvEZzC2CXfMu9wChJG+f7DilVV86x/FyF9zAzM7NuVnUq/GfAu4APk6ZVNyd1OGwl6oN5mfsCc5SOiLwF+EpEPE06wvFxUurAOaSsSyLiqfw+fwJuK65nE0hh61NIIepmZma2klXNsbw/IoZLmhURw/Lo0S0R8aHub+KqqVE+ZZPqH0Xz8ikvAY4FtomIR/K1ccC5wM4R0esDIp1jaWZmVk2jHMuqI5bFjtpFknYgTUMOakLbrIZSPuXkiNg6IoYAp1FnE0onjQJ2q/P8ymsSJZ0KfAJ4FDis9NHBwAMdaZAkn6BjZmbWh1XtWF4i6W3A6aRpzweA/6/bWmV18yklnS1pTs6aLPIpR0m6oSgr6cJ8Sk2351NGxHdII6tXAgfk8ucAQ4EtgSvyM67Kz58jael/O5IWSzpT0r3ArpL2ztmUs/Na3rVzuZ0l3S2pVdKfJb01ryE9J5edJenEXLZmHWZmZta9OrLG8qOkGJvLgR/Q3NEzW16VfMrRpA7gphXqWxgRI4CLSPmU84GLSafgtETElFyuyKccR9qMU+zwbi+fEuBF4Ik8ov08cCIpI/Nw4GPArsCHcvt3lnRgvm89YE5EvD+XnwgcGhFDSbu5j5e0Filq6D8jonj3l0kZlFsBw/PxoldIekutOmo1WNJYSdMlTV+wYEG7X6KZmZk1VrVj+RvSaNTrpOP9FlOKnLEe0yvzKUt+SZoOP5A0lV/YmWV5lK+TNg7tmT97A7g2/74d8HhpHenludx2wFMRMQ0gIl7M9YwGLi6OlYyI5xrUsQLnWJqZmTVX1bV0m0fER7q1JVbW5/Ips98CZwPTI+LFtFS0YbsBlpQ6s/XKidp5lrWuN3qWmZmZdaOqI5Z3SxrarS2xsj6VT1mIiJeBrwJntfnoXuDfJA3IG3Q+SRptbeshYJCk9+a/P5PLPQRslr8D8vrKNUjHQh5XbDaS9PYGdZiZmVk3qzpiuTtwhKTHSaNfIsUoDuu2lq3C8vnXY4Dz867rJeS4IVJeZCtppO6UnAOJpCKfch7V8ymvkXQAaT1kLZNIU+BVpsGLtv+yxrWnJH2NdNa3gJsi4jc1yi2RdCQpn3INYBppqvvVvFHp+5LWIa2vHE3q+G4LzJL0GnBpRFxYq46q7TczM7POq5pjuWWt6xHx16a3yHpNhqWkkaQNPjWD0SWNZ9lpOENJAeeQ1meOAG6IiGs60K67I2K3vGv9hojYoeq9DeocRdqw1PBse+dYmpmZVdMox7LqWeHuQPaQUobl5RFxWL7WQtqF35SOJSnDcjGwQsdS0hoR8XoeKT2eBmsrI+Is8rS3pMUR0VKqZ2JHGxURNXM1zczMrG+ousbSek6vyLAE/jcitiStr30kr48cn+8p/4xv8C575uzJxyQdnNu0vqTbS206oNT2xW0rkDRI0pRcfoak3UrvPVnSNZIeknRF7pQXZ5I/JGkqKaLJzMzMekDlE1asx1TJsBwATJN0Z4X6FkbECEknkKaEj5F0MbA4Is4BkHQ0yzIs35C0iDRSeT7LZ1guHaGsaFPS+tzBpPWa15DWi47Ju8YHAPdImhT112Q8A+yT119uA/wCKIbfhwPbA0+Szhv/oKTpwKWkzMxHSPmXNUkaS8rCZODAgR14LTMzM6vFI5Z9R2/PsKzl+oh4MyIeYFmgvoBvS5oF3Aa8m8Zh+2sCl0qaDVwNDCl99ueI+HtEvAnMJL3fYFKO5bzcWf15vYqdY2lmZtZcHrHsffpqhmUtr5R+L9p/OLAJsFNEvCZpfo02l40D/kkaqV2NNOJZq/7y+7W/I83MzMyaziOWvU+fzLDsgA2BZ3Knci/SeeLtlX8qj0p+Bli9nfIPAVtJ2jr//ckutdbMzMwqc8eyl8nTt2OAfSQ9KmkuMAG4kpRT2UrqfJ4SEU9HxBNAkWF5BdUzLMcUm3fqlJlEyszs7DR4PVcAI/NayMNJHcFGfgh8TtI9pHWgDY8SjYglpHWTN+bNO040MDMz6yGVciyt+/SWzMoa962QYSlpAqVNP/nafGBk3tzTlXYOoknZlZ3hHEszM7NqGuVYesRyJSplVk6OiK0jYghwGo03s3TUKKBmPmRxFGKN66cC1wJfa2I7mk7peEgzMzPrJdyxXLl6RWZlXrOJpNUkPQL8OCK2jIippWeNb1PXChmWkr6c2zxH0pfytUGSHpR0qaS5km5VOpYRSTtJapX0J+ALpXqOkHRh6e8b8sgrkhZLOlPSvcCukr4uaVp+5iWlLMuTJD0gaZakFY6ZNDMzs+Zzx3LlqpJZOZrUAdy0Qn0LI2IEcBEps3I+6Zzs8yKiJSKm5HJFZuU40gadYtd3ObNyOfmUnbZnbh8CbAapkwgcSdpF/gHgWEnDc7ltgB9ExPbAIuCgfP0nwEkRsWuFdyusB8yJiPfnju+FEbFznkJfByiObjwVGJ7Psz+uVkWSxkqaLmn6ggULOtAEMzMzq8Udy96pN2dWFp3UlnyE45OlNv86Iv4VEYtzW4r1mY/nkdilbcs72DeKiD/m6z9r57mFN0jT9IW9JN2bcy4/RApMh7yZSdKnSZFMK3COpZmZWXO5Y7lyzQV2qnG9RzMrgXJm5c2NGtxAvTaX21Vum6ifN9noPZcUnWJJbyHtGj84IoaSTtwpyv478APS93tfvfWkZmZm1jzuWK5c/Smz8k7gQEnrSlqPFJk0pV7hiFgEvCBp93ypHMI+H2jJaz63AHapU03RiVwoaX1ysLyk1YAtIuIO4BRgI1J0kpmZmXUjj+KsRBERksYA5+ed2EvIcUOkjlAraVTvlIh4GkBSkVk5j+qZlddIOgA4sU6ZSaQp8E5nVkbEDEkTSR1gSBuA7s8biOo5ErhM0kvALaXrdwGPA7OBOcCMOs9cJOnSXG4+MC1/tDrw89z5Fmn6flEnXsvMzMw6wDmWq4D2sjJrZVZ2sP5RdCIrs05dE4BjgQWk/+FzWkRM6mq97XGOpZmZWTXOsVyFtZeV2aTMylF0MCuzHefljUGHkEY0K/136nWUZmZmK5f/H3H/VzMrU8nZwEeBF4F3w9LRx4tJ0/Lk6y8DPyKNJF4O7A+sSer4LSHF+byRd2CfCBwNPAcMB2ZK2g/YLSIW5E7iX4APtHdaT0Q8KOl1YICkyO0amD/+UkTclUc4NyPtgl8o6VbSSUBfzO9zA3BOREzu6BdnZmZmHeOOZf9XJStzADBN0p35s0ciYj9IIezA9IiYmDcZLYyIEZJOIGVlHiPpYkpHPUo6mmVZmW9IWkTanHM+DbIy25L0fuBN0rT4FaSRzKmSBpLWZL4vF90J2D0iXi4C46uQNJZ0rjgDBw5sp7SZmZm1xx3LVdfSrExS3FCRlfliO/eVszI/3qBc26zM35A6llWyMsfl0c//Aw7Nm5xGk3bEF2U2kFTsdp8UES+3U+cKIuIS4BJIayw7er+ZmZktzx3L/m8uOYanjR7NypRUzso8vP5tQBqZPKfNtdWAXdt2IHNH81+lS+2138zMzLqJN+/0f/0lK/NW4Iuld2ipU24+1TIwzczMrMncseznIuVJjQH2kfSopLnABOBKUh5mK6nzeUpEPJ1P4imyMq+gelbmGEkzJdWLLJpEyubsbFbmScBISbMkPUCd879ZPgPzHOpkYJqZmVnzOceyl2kvc7IJ9Y+iezIn1wK+GRG/qFO2S1mZFdpyHPBSRPy0M/c7x9LMzKyaRjmWXmPZi5QyJy+PiMPytRZS5mRTOpakzMnFwAodS0lrRMTrHazvvIg4R9I2pDO5r4mI19rUeypwPO2vrey0cpySmZmZrRyeCu9damZOAlMlnS1pjqTZkg6FNPqYcxrJf19YxO1Imi/pDEkz8j2D8/GKx5F2Xc+UtIekiZLOlXQHcLakeXnNJXmd4iOSBrTX8IiYB7wEvC3f2yLpHkmzSBt2WnJU0GRJ50l6XNISSQ9LWiTpldyG4l2ul3SfpLk5Fqi4vljSWZJac/1F0PsESSfn34+VNC2XuVbSup35l2FmZmYd445l71Ilc3I0qQO4aYX6FkbECOAiUubkfFLI+HkR0RIRU3K5InNyHGmDTTGy2JHMyRHAvIh4Jl/6KfDViBhGWu/4jVLxVyNiK+CrpE0/7wM2ALaRtHEuc1RE7ASMBE4qXV8PuCcidgTuJE3Ft3VdROycyzxICmyv1eaxkqZLmr5gwYL2XtHMzMza4Y5l37A0czIi/gkUmZPtKWdODmpQrm3m5Gfz71UzJx8G7iVtCiLvJt8oIv6Yy1xO2nVeKM7+ng3MjYinIuIV4DFgi/zZSZJagXvytW3y9VeBYpS23nvtIGmKpNmkTvL2tRoeEZdExMiIGLnJJpu085pmZmbWHncse5e5pFNk2urRzElSYHqROXlzowaTRj+3Aw4FfiqpSm5k0a43S78Xf6+RNxiNJuVW7kjamV7U+1os23FW770mAl+MiKHAGTjL0szMrEe4Y9m79NnMyYi4DpgOfC4iXgCeL0UPfYY0ylrVhsDzEfGSpMHABzpwL6T3e0rSmnTjhiEzMzNbnneF9yL56MIxwPl5J/USctwQKQOyFQhy5iSApCJzch7VMyevkXQAcGKdMpNIU+AdzZw8E7hS0qXA54CL88aZx4AjO1DP74Dj8safh0nT4R3x/0hT838lTbe315E2MzOzJnCOZR/Q09mWXcmclDQRuCEirildWxwR6+fnnBwR+3WynZsBF0RErSMqu8Q5lmZmZtU0yrH0VHgvV8q2nBwRW0fEEOA0UrZls4wCdsvPOxW4Fvha/rtHR7UbPS8inuyOTqWZmZk1hzuWvV+PZluSjkS8A/h4KdtyYS4/M/+8IumsrryUpJ0l3S/pPTmD8hJJt5I2AA3Ku7pn5J+i0ztI0pz8+xGSrpP0u5y9+d1S3ftK+lO+92pJ63elrWZmZlaN11j2flWyLQcA0yTdWaG+hRExQtIJpGnpYyRdDCyOiHMAJB3NsmzLNyQtAl6IiPMl7Qt8PiLGd/aFckfx+8ABEfG3NCjLTsDuEfFyXpe5T0QsUTrR5xekPMu2WoDhpOUBD0v6PvAycHpu+78kfRX4Mmn9Z9t2jAXGAgwcOLCzr2NmZmaZRyz7rt6abVlr0W752vuAS4D9I+JvpeuTIuLl/PuawKU5h/JqYEidZ90eES9ExBLgAWBL0g7yIcBdeQT2c/n6io1yjqWZmVlTecSy95sL1FpX2KPZlpLK2ZaNInyeJR/rCCDp7UD55J6ncpuGA0/Weh4wDvgnaTR2NdLu+FrKGZjF+wj4fUR8skEbzczMrBt4xLL362vZlpNzu9bKfx9BWrNZWAT8O/DtvEu8lg2BpyLiTVIG5urttK3sHuCDkt4LIGldSdt24H4zMzPrJI9Y9nJ9LdsyIm6QtBNwn6Q3gEdJm4PKZf4paX/gZklH1ajmh8C1kg4hdUr/VaNMvecvyJuVfiFp7Xz5dKAp0UxmZmZWn3Ms+5nuyrwssi1J4eNLMy+7WOd2wI+AjYC1gSkRMbaTdd0EfCoiFnXmfudYmpmZVdMox9Ijlv1IKfPy8og4LF9rIWVedrpjmUdKjyetrRwNLAZW6FhKWiMiXu9A1ReQgth/k+8f2tk2RsTHOnuvmZmZNYfXWPYv3ZJ5SepQfhj4O8syL5/K+ZHPSXpG0v8Bf8zXNsl1rCbpEUkD6rR301xn0dbZ+b4jJP0mZ1Q+LOkbpTZeL+k+SXNzXFBxfb6kATnr8kFJl+Yyt0pap0vfqpmZmVXijmX/UiXzcjQp9HzTCvUtjIgRwEWkzMv5wMWkUcZNI2Ib0trLPwMbRcQHSRt8il3jo4HWiFi4YtVAmlr/g6SbJY2TtFHps11yPS3AIXkqHuCoiNiJlGt5kqSNa9S7DfCDiNietFnooFoPlzRW0nRJ0xcsWFDh6zAzM7NG3LFcNfTKzMuI+Akp1/Jq0rGS95Q23Pw+Ip7N2ZbX5XeA1JlsJe3+3oLUiWzr8TxS27DtzrE0MzNrLncs+5e5pBNs2urRzEugnHl5c6MG5/O/L4uIA3J7dig+als0xxONBnaNiB1JO97btrnc7iptNzMzsyZxx7J/6VOZl5I+ImnN/Pu7gI2Bf+SP95H09rw+8kDSGeYbAs9HxEuSBpNO2TEzM7NewiM5/Uhfy7wE9gW+J6k4WecrEfF0Pjt8KvAz4L3AlRExPR/xeJykWcDDpOlwMzMz6yXcsewG3ZUlWap/FHWyJCPiSeATNW77Sv5p6yVSp3Nz0rTyPyX9NCIGleqcTloDSX6HYaX7p9Soc0fSpp2HSm2eTNoAtDQsMiK+DHy51juSzguPiNiuVP4V4KO1ChftlbR+m+vn1KnfzMzMmsxT4U1WypKcHBFbR8QQ4DRSlmSzjAJ2q/P8zvyPhfMiogUYAgwF/q2zDcsjpdcCX+tsHWZmZtY3uWPZfN2SJZnvGSxpEMuyJGdK2kPSREnnSrqDFCXUkSzJsrVIo5bP53uPlTRNUqukayWtm69PlHSBpLslPSbp4OJZwEBSgPqpkm6SdLCk8aR4oCtymxdK+nvOmTyj9O4fkfQQcAzwROn6epIuy225P0/DI2l7SX/Odc6SVOwQX905lmZmZj3PHcvm68ksyZaIKKaitwVGR8Q4OpYlCbmTCjwF/KUU1XNdROycd2A/CBxdumdTUgTQfsB3Su84iDTqeQywK0BEnAVMBw7PI6PbRsTmpCn1f5M0TNJbgEuB/YE9gHeVnjUe+ENE7EzquJ8taT1SB/t7uc6RLAtbd46lmZnZSuCOZc/plVmSWTEV/g5gPUmH5es7SJqSN80cDmxfuuf6iHgzIh5g2TT/7rkdb+bNQXfUed4nlE70uT/XOQQYTMqfnBfpAPufl8rvSxoBnQlMJo2qDgT+BJwm6avAljnzEpxjaWZmtlK4Y9l8fS5LsnTfa8DvSHFEABOBL0bEUOCMNm0rZ0WqzT/rkrQVcDKwd0QMA24s1ds2u7Jc/0F5hLYlIgZGxIMRcSXwH8DLwC35fdu2zTmWZmZmPcQdy+brU1mSZXnj0W7Ao/nSW4Gnctbk4XVvXGYqcFBe1/lO8k7yNjYgdYJfyGWKXd4PAVtJ2jr//cnSPbcAJ+b2IWl4/ud7gMci4gJSxFF5t7qZmZn1MHcsmyxP444hBXw/KmkuMAG4kpQX2UrqfJ4SEU/n0cUiS/IKqmdJjik279QpM4kUI9TeNDgsW2M5hzS698N8/f8B9wK/J3X82nMtaZ3jHOBH+d4XygUiopX0jnNJU/Z35etLgLHAjZKmkjrchW+S4odmSZqT/wY4FJiT2z4Y+GmFNpqZmVk3UeoHWW/SjBxMSSNJaydX6Hg2ysHsRFsnAIuLvEhJ60fEYkkbk0ZkP1iEsefPF0fE+rVrW3lGjhwZ06dPb7+gmZnZKk7SfRExstZnXnvWy5RyMC+PiMPytRbSBplKHcucJXk89aevR5EigVboWEpaIyJe73jLl7pB0kak6KJvljuVZmZm1r95Krz36XIOJvB0RGwJ/LyUg/m0pAclPUCK7/m2pKeanINJRIzKO8y/DZyQp+t/JGn1Uhv/J7fp9tJzOpqZqQbfx2RJ10h6SNIVxdpMMzMz617uWPY+3ZWDeSZwVz4J6CzgtIjYtEk5mMuR9D7S+scP5k7mG6X61gNm5Db9EfhGvt6ZzMx638dw0vnoQ4D3AB+s007nWJqZmTWRO5Z9R2/OwWxrb1Lk0rS8sWZvUgcP4E3gqvz7z0nvBZ3LzKz3ffw5Iv4eEW8CM3GOpZmZWY/wGsveZy5wcI3rPZqDKamcg1klaqhtWy+PiCrnhRe7xyYCB0ZEq9KRlqNKZTqamekcSzMzs5XAI5a9T5/NwSy5HThY0jty+98uacv82Wos6zh/ipR9CR3PzLyT2t+HmZmZrSQeyellIiIkjQHOz7u7l5Djhki5lK2kUb5Tih3XkooczHlUz8G8RtIBwIl1ykwiTYFXmQY/XdKXSu+wuaTTgVslrQa8BnyB1An+F7C9pPtIGZeH5tuKzMy/ArNpv+P7a9JZ5Mt9H5IGV2ivmZmZdQPnWPZyzci0bKf+UdTItGyUg9mgrgnAscAClsUN/aIZ7az47KV5mh3lHEszM7NqGuVYeiq8FytlWk6OiK3zju7TWLaBpRlGkY5xLD/3VNIpOqd3or7z8k7wA4Af5altMzMzWwW4Y9m7dTnTMm+EQdL8UqblbEmDJQ0CjiMf6VhkWgLvAB4DDiwyLSWNz2VeyffPlDS+XsMjYh7wEvA2Se/IU99I2lFSSBqY/35U0rqS9pd0r6T7Jd2mdI44kiZIuixnUz4m6aTS+42X9LCk24DtStdrZmKamZlZ9/Iay96tSqblAFKsz50V6lsYESMknQCcHBHHSLqY5Y9kPJplmZZvSFoEHB4RZ0maBnw+Ig5q70GSRgDzIuKZ/PdbJG0A7AFMB/ZQOhP8mYh4Kf/+gbzG9BjgFOC/cnWDSZ3stwIPS7oIGAYcRsqsXAOYUfqurouIS/Nzv0XKxPx+jTaOJZ1PzsCBAyt8fWZmZtaIRyz7pt6caTlO0sOkjTgTStfvJgWV70k6lWdPUiezCGjfHLgl51h+heVzLG+MiFdySPszpKUAewC/joiXIuJF0majQqNMzKWcY2lmZtZc7lj2bnNJQeNt9WimJVDOtLy5UYNJayy3I+32/qmkog1TSJ3BLYHfkEZG8rT0AAAgAElEQVRbdyfFBkEaUbwwIoYCn2/T9nq5lPV2nk0EvpjrOoMVvwczMzPrBu5Y9m59NtMyIq4jTXl/Ll+6E/g0aXr8TeA54GPAXfnzDYF/5N8/R/vuBMZIWkfSW4H9S591NBPTzMzMmsAdy14sUhbUGGCfvMllLml6+UpSbmUrqfN5SkQ8nUcXi0zLK6ieaTmm2LxTp8wkUoZmR492PBP4sqTVImJ+vlaMUE4FFkXE8/nvCcDVkqYA7Z5LHhEzSEdDziTtYJ9S+rjIxPw98FAH22xmZmad5BzLJlpZmZOdrGsC8A1gm4h4JF8bB5wL7BwR00tl62Za5jadHBH7dbVNK5NzLM3MzKpxjmUPWFmZk6Xnd2aH/2zSzurCwcADbeotMi2rnPvda0lafWW3wczMrL9zx7J5VkrmpKRzJd0BnF1kTuY6VpP0iKQBDdp8PSnIHEnvIR2xuKDUpotInc3FwD6l6xMlLZG0GLiaFB00XtIuku7OWZR3S9oul19X0q8kzZJ0Vc6rHFk8Q9J0SXMlnVF6xnckPZDvKaKQ3inp1zmfslXSbvn69ZLuy3WMLdWxWNKZku4lHf+4HElj87OnL1iwoO3HZmZm1kHOsWyeXpM5SZqOHw205oieel4EnpC0A6mDeRVwZOnz8RHxXB7tu13SMOAvpE1BQ4FH8j3r5pzLDYA9I+J1SaNJsUIHAScAz0fEsPysme084++ktaWDc67lRrnsBcAfI2JMLr9+vn5UrmOd/P1eGxHPAusBcyLi67VePiIuAS6BNBXe4HsyMzOzCjxi2f16c+YkwC9J0+EHkqbyyz4haQZpE9D2wBBSWPnjETEvby76ean8hqQNOHOA81iWH7l7fg4RMYe0uajRM14ElgA/lvRx0gk+AB8CLsr1vBERL+TrJ0lqBe4BtgC2ydffIE3jm5mZWQ9wx7J5+mLm5P/P3p3H2z3d+x9/vYnWEENruqolqtogIgg1tAThXr2UXFGUFjW3StOiSktUqaFFifmWqB/looihqCFNghgzoyi5bcWQ1NRcYvz8/lhr53yzs/c++5yzzzl7x/v5eJzH2ec7rO/67vhjWcN7QVoV/i3gbzloPFVaWgs4Gtg+IgYCtxfqWK137xTg/ogYQIr/KV1f8Tuo9oyI+ADYjNQo3A24s1rl8+KhocAWEbEhqYFaeu68euORzMzMrOvcsGyclsycjIh3gB8Dp5adWo7UaH1Tad/unfLxp4G1JK2d/967cE8xi3L/wvEJwDcAJK1HGkav+gxJfYHlI+IO4AekqQQA9wKH52sWz0Pvy5OG2d+W1B/YvL13NjMzs+7hOZYNkucCDgPOzSup55HjhkhzAaeQevqOjYiXASSVMiefpf7MyRsk7Qp8v8o1Y0hD4HVnTkbEtRWOTZE0idQT+zw5yDwi5uUFMrdLmkNqNA7It50JXCnph6SGdsmF+fhU0ntOBd6MiGcrPYPUeL5FadceASPy8aOAS/Pc0g9Jjcw7gcNy2X8hDYebmZlZL3COZYtQnRmZqpE52U75Q2hQRmahzCmk+KJ9gSVyo/RG0taOnyUtBBrczgKjep/1YERUjGKqh3MszczM6qMaOZbusWwB0vyMzCsjYq98bBApI/OZwnXHkXrxOrON4RBSrNBCDUtJffK8x47UeV3SVIutSavhb1faYvFzwEUR8V56rcboSqPSzMzMGsNzLFtDXRmZpNXaawJ9lDMyc77kbEl/U8q/fE/Sfer+jMxvAlcBdwPbRcTgvLhmDAsO+x8j6ZH884Vc/i4563KSpHvy/EskjZR0uaSxkp6XdGSpEKVMTST1lXRv4f12rVZB51iamZk1lhuWraGejMyhpAbgasULIuJUUtbkiRExCJgF3BQRG5Oie47O+3hfTBpCHxQRpX23SxmZI0gLgko9ofVkZO6Zn/t7FlzgU+6tiNgMGEUa6oc0b3PziNiIFFN0bOH6/sC/k1aNn5R7QYvmAcPy+20L/FpVukYj4tLc4B288sor16iimZmZ1cMNy9bWlBmZeTX87Ij4X9JK7o0lfarK5b8v/C7tjvNZ4K7cC3sMbXmYALdHxLu5UfsqC2+ZKeC0vJjnHmD1CteYmZlZN3DDsjW0Wkbm3kB/STOBv5JihXavcm1U+Hw+MCoiNgAOLav/u4XPleq/D7AysEnuoX2Fhd/fzMzMuoEblq2hZTIyJS0G7AEMjIh+EdGPtF1kteHwPQu/H8qfi3mY+9VR96LlgVcj4n1J2wJrdvB+MzMz6ySvCm8BLZaRuTXwYkS8WDg2jtTQXa3C9Z+U9DDpf3JKjc+RpK0hXyTlUq5VR/1LrgZulfQYaU/ypztwr5mZmXWBcywXAfVmXHah/CHAe/mnwxmZZWWNBOZGxK9yAPqtwISIOLkRde0s51iamZnVxzmWi7B6My67aAip0TqAsozMzmRc5vs+QdoL/PHeblSamZlZY3iOZeurK+NS0p6Qeh9LGZf571GS9s+fZ0o6uUrG5SDSnE4VMi6fB2ZJejdfP1nST+vIuOxDihF6NiKOK9Rl35xnOVnSJZIWz8fnSjpV0hRJEyWtKmlZSS+U4oYkLZfrv4SkgyU9mq+/UdLSlSrhHEszM7PGcsOy9XU647KKOR3IuFwnIlYBTgN+m1dhP0L7GZfHAh9ExA9KB5R26tkT2CqX8yFtvaPLABNzwPo44OCI+BcwFvjPfM1ewI0R8T7wh4jYNF//FHBgpUo4x9LMzKyx3LBcdDVlxmU2AdhC0hcLx7YnRSo9Kmly/vvz+dx7QKmXtViv/wYOyJ8PKDx3gKTxOQdzHxbMwTQzM7Nu4jmWrW8GMLzC8R7NuJRUzLhsb6/yccCVwB8lfTUiZuX6XhkRP6lw/fvRtspsfr0i4gFJ/SRtAyweEdPzNaOB3SJiSh7mH9JOfczMzKwB3GPZ+lom47IoIm4EzgLulLQCaYee4ZJWye/waUn1ZFD+jrRrT7GXdFngpTz/sr1GrpmZmTWIG5ZNRtK/SbpW0l8lPSnpjrIh4wXknrxhwA75nhmkHMhrSDmWU0iNz1LG5dqkoeippMzHejMuh+VFNfOjhiSNlBSSvkDKuOwLfJSPVYwhKNw7FniMNPQ+Bnge+Clwd96O8U9APXNCrwY+BfSTNDQf+xnwcC7DOZZmZmY9xDmWTSRHBz1IGhK+OB8bBCxbWDTT1WeMJOdIVjjXoeigXNZ/Af8D3AmcQ/qflRWA/SKiajBkblgeXeuaOuswHNg1Ir7VlXKcY2lmZlafWjmW7rFsLj0VHTSi1PtYiA66n7Ry/Nk8dI6kxeqIDrqZtJ/3jaQ9vt8E5mf3SLooR/rMkFQxr7LSNZK2l3RT4ZodJP0hD+2Pzt/FHNLq9VPyseH52hNz3NB0SZfmBruZmZl1Mzcsm0tvRgcNjYgRpHmSpXmJQ2k/Ougt4FFS7M86wHX5+Hfy6u6vkBbbvA98S9LACmWckP/PZyCwTb7mPmDdUiOXtlXfg4DVI2JARKxEijwqD4IfleOGBgBLATtXqrhzLM3MzBrLDcvW0MzRQZDCzvcCdiPtAgRwec6jvAD4iPTf2rLAehXu/4akJ0jzPdcH1stzR68C9s2Le7YA/kiai/l5SedL+g9Sw7bctpIeznFD21Elbsg5lmZmZo3lhmVzmUHKcizXo9FBQDE66I+1KpzdCnwL+FtEzG/oSVoLOBrYPiIGAreX17Gda64A9gX2JjV+P4iI10k9t2OB75FWoxfLWxK4EBgeERsAl5U/08zMzLqHG5bNpVWjg94BfgycWnZqOVKj9U1JqwI7Vbi96jU533IWabX4aIA833OxHFf0M2DjsvJKjcg5kvpSOePTzMzMuoED0ptIRISkYcC5ko4D5gEzgR+QonymAEFbdBCS/ocUHfQs9UcH3SBpV+D7Va4ZQ+otrGcYvFT3ayscmyJpEqkn9nnggU5cczWwckQ8mf9eHbhCUul/ihYIVI+INyRdBkwjfXeP1vsOZmZm1jWOG2oxkv4NOJc0x/JdcsOzwgKWzpY/hLSV4gER8dV2Lq+nvG+T9gZX/rm8UtRRjftHAZMi4rcV6vleRDyY/z4MeDsifteZejpuyMzMrD614obcY9lCcmzOTaScy73ysUHAqkBDGpakYedNgF0qPL+jOZc7kXpbd4yIWXn+40J5k9XKlfQ4aZj8RxWKHwLMJeV+UoxoMjMzs97hOZatpSdyLgcAbwOjCjmXEyT9C5gl6d18/Ql15Fz+hBRzNCvXdV5EXJafP1bSaZL+DBwlaU1J90qamn+vERGbkLZ9HCdpkqR7JK1aJY9zpKSjc9kH5xzLKZJulLR0Y75+MzMzq8UNy9bSWzmXbwArRMQqwGnAbyPiVNrPuaxW35IVImKbiPg1MAr4XV4ZfjVwXr5mArB5RGxEijU6tkY9S/6Qcyw3BJ4CDqz0cOdYmpmZNZYblouGZs+5rOa6wuctSPubQ8qv/Er+/FngrpxJeQxVMinLDJA0Pt+zT7V7nGNpZmbWWG5YtpZWy7msVt+Fyq2gtKrsfNJOOhuQto6sJ5NyNHBEvufkOu8xMzOzLnLDsrW0Ws7lL4Ez80p2cj2OrHLtg6TdeyD1Mk7In5cHXsyf96uznssCL0lagrbtKc3MzKybuWHZQvI2h8OAHST9VdIMYCRpCHkqKefyPnLOZe5dLOVcXk39OZfDSotiqlwzhpSrWXMYPCLuIG3peE+u6+NU7xk9EjhA0lTSyvGj8vGRwPWSxgPFuZy16vkz4GHgT8DTtepoZmZmjeMcyy7qoVzJ+XmNXSxrJHASsE5EPJePjQDOBjaNiLqCHCUNJi2c6XTOZV7ZfVtEDKhw7r+Bswuh6N3OOZZmZmb1qZVj6R7LLijkSo6NiLUjYj3geFKuZKMMAbas8vzO5JBOo23IGdKWh3U34PKOQDdStuNNI0XEQT3ZqDQzM7PGcMOya3oiV7I8r3G0pLMl3U+KFXo2z6ukjlxJgJuBXfP1nwfeBOZn7UjaOz9/uqQz8rGv5+dPBg4APoqICZJOzHmRr0iaU7pG0lxJD0gaJ+kpSZtK+kOu6y8Kdekj6cqcXXlDKW8yZ1wOzp8PkPSMpD9LukxpJx7y9zC8UO+5hc/H5HpNlXRyXf+SZmZm1mVuWHZNb+VKfhEYGhEjSItoSgtU2suVBHgL+LukAcDeFCJ/JH0GOAPYLtd/U0m7RcSY/PxBpHmcpS0ZR+W8yFVJq8N/lq95DJgQEVvn+t8CfC9/X/tLWjHf/yXg0pxd+Rbw3WJF83d2MrAVsAOwXntfoKQdgXWAzfI7bCJp6yrXOsfSzMysgdyw7B7Nnit5LWk4fDfSUH7JpqRh/dl5i8WrSSvMAZB0LPBORFyQD20r6eGcF7kdC+ZFjsm/pwEzIuKliHgXeB74XD7394h4IH/+f7RlV5Z8uVCf91gw97KaHfPPJOAJoD+pobkQ51iamZk1lvcK75oZpDmK5Xo0VzIPRZdyJeuJ17mVtFXiYxHxVpoqWrPeSNoe2IPc0FTa9/tCYHCuw8iy9ym9y0eFz6W/S+9WvnKs0kqyaqvL5n+Xea7rJwrv8MuIuKTau5iZmVn3cI9l17RariQAEfEO8GPg1LJTDwPbSFpJ0uKkofI/S1qT1Ij8Rr4X2hqRcyT1pXIDuz1rSNoif96btuzKYn2GSFoxZ1LuUTg3k7bw9V2BJfLnu4Dv5DohaXVJq3SibmZmZtZB7rHsgogIScOAc/Nq6XnkuCFSzuMUUo/bsRHxMoCkUq7ks9SfK3mDpF2B71e5ZgxpCLzu7RUj4toKx16S9BPgflLP3x0RcYukk4AVgZty7+asiPiapMtIQ90zgUfrfXbBU8B+ki4hfR8XVajPSOAh4CXS0Pbi+fRlwC2SHgHuJffiRsTdktYFHsp1nQvsC7zaifqZmZlZBzjHsgmoi1mYaidXUo3PwjyYtJJ8SVIj9HsR8VGNe0aTMitv6OKz9ycNvR/RlXIqcY6lmZlZfeQcy+aV5wd2OgtT9eVKDqGxWZjn5NXf6wEbANt0ogwzMzNbxLhh2fu6lIUJfBY4KedKlrIwZ0l6J2dIPgmcAPxMjcvCLPkEqdfy9XzvwTk/coqkG0u5lNnWkh6U9Hwpf1JSX0n3qi27s5Sv2U/S05L+O7//1ZKGknpK/13SZvm6zXKZk/LvL+Xj60t6JL/vVEkVV4WbmZlZY7lh2fu6IwvzM8CPgAdyD+ipwCkNzMIcoRSW/hLwTG4IA/wh51puSJo/eWDhntVIcUI7A6fnY/OAYTm7c1vg12pbov4F4DfAQFJk0Dfz/UeTenQh7QO+dURsBJwInJaPHwb8JveqDgb+UeklnGNpZmbWWG5YNq9mzsIsDYWvAiwjqbRF5ABJ43Ou5T4smGt5c0R8lLdqLA3zCzhN0lTgHmD1wrkXImJanrs5A7g30oTgaYX3Wh64XtJ04JzC8x4Cjpf0Y2DNwkr2BTjH0szMrLHcsOx9M2iLzSnq0SxMoJiF+cdaFS7c9z5wJ20h6qOBIyJiA9KOOZVyLaHt3fYBVgY2yQ3VVwr3lGdfFnMxS+91CnB/RAwAdindGxHXAF8H3gHuyu9lZmZm3cwNy97XklmYuZ4iLQr6az60LPBSzpysJ6h9eeDViHhf0rbAmvU8t+z+F/Pn/Qv1+jzwfEScR4piGtjBcs3MzKwT3LDsZXl4dxiwg6S/SpoBjASuIeVdTiE1Po+NiJdz72IpC/Nq6s/CHFZavFPlmjGk7M16sjBLcyynk3oPL8zHf0YKNf8Taf5je64GBkt6jNQQreeeojOBX0p6gLZ8S4A9gem5jv2B33WwXDMzM+sE51j2oq7mV9ZR/hDqzK9sLwuzcN0U4MmI2LsRdayjXvsDd0fErPz3fwNn57maDeMcSzMzs/o4x7IJdTW/sk5DqCO/ss4sTPKONouRooOWaa/cBtkf+Ezpj4g4qNGNSjMzM2sMNyx7T5fyKyWNyr15FPIrS3mQ/SX1I8XujGgvvzIiTgfWAkaX8islnZDvm/9DGvK+CribtDimVJexkk6T9GfgKElrS5qYMy1/Lmlu4dpj8vGpkk7Ox/opZW5eJmmGpLslLZXzLgcDV+c6LJWfNTjfN1fSqUq5mRMlrZqP7yLp4ZxveU/puJmZmXUvNyx7T3fkV25M2m/76IiYCVxMjgbqaH5lRJya75v/Q4oDug74PVA+FL5CRGwTEb8m5U/+JiI2BWaVLpC0I7AOsFl+x00klVaUrwNcEBHrA28Au+ctIB8D9sl1KI8NWgaYmHMzx5EC1AEmAJvnfMtrgWMrfWHOsTQzM2ssNyybT1PmV+aV6rMj4n+Be4GNJX2qcMl1hc9bANfnz9cUju+YfyYBT5AW1pR2xXmhELTe3juUvAeUenGL93yWFDM0DTiGBfM053OOpZmZWWO5Ydl7Wi2/cm+gv6SZpHih5YDdK5Vbg4BfFnpBvxARvy2rfz3vUPJ+tK0+K95zPjAq52keysLflZmZmXUDNyx7T8vkV0paDNgDGBgR/SKiH7ArCw+Hl0ykrdG5V+H4XcB3JPXN5a4uaZUGvEO5Yr7lfh2818zMzDrJDcte0mL5lVsDL0bEi4Vj40gN3UrzP38A/FDSI6Q9wt/M73x3fr+H8jD1DbTfaBwNXFxavNPOtSUjSVs9jgdq7XluZmZmDdRtOZbdndGYnzGEOnMa6yzv26SFHso/l0fErzpRTj9gy7y1YEfvnRsRfaucG0aaS7luRDxdOH4W8DXgjog4puyerwPr5ZXflcqsK7+yRn33B84i9RAuCVySf96JiFDaR3zviNi1M+UXnjMTGFxaXFQ4PhKYGxG/kvRzYFxE3NPR8p1jaWZmVp9aOZaNzhwsPbCU0XhlROyVjw0iZTQ2rGFJymmcCyzUsJTUJyI+qLcgSTuRetp2jIhZkpYEvtXJevUDvsmCC1c6Va8ye5NWPO9F6pUrORRYOSKK8xRLzxpD6pVcSM6vPJz6tl+s5bqIOELSisBfgL8BJ+b/Dt4gLQzqdhFxYk88x8zMzCrrrqHwihmNETFeSY/mNOYyFpP0XCmnsYKfkGJ6ZuX6zouIy/K9a0u6U9LjksZL6p+Pj5Z0nqQHJT2fcxcBTge+mus1QtL+kq6XdCtwt6S+ku4tvE+7vXl5XuJWwIEU5i1KGkOK3XlY0p5l38EZ+dmj8rWrSrop5z5OIfXurQkcnd9tRj5fyq78UNLLkl5SISeymoj4J/Ac8PccAbQ9MBv4vVJ25Va5HiMlXSXpvvxvdHA+XvW/gewYSY/kny9U+I5Gl/4NJG2a/12m5Os7Ok/TzMzMOqhbeiypntEIC+Y0rgQ8KmlcHWXOiYiNJX2X1AA8SNLF5GFQAEkH0pbT+KGkN0i9cedSltPYwTpfChwWEc9K+jIpKHy7fG41UkRQf1LP4A3AcbmOO+d67U+K4BkYEa8p7U4zLCLeyg3diZLGFFY4V7IbcGdEPCPpNUkbR8QTEfH1PHw+KD9rp7LvYP9CGecBf46IYZIWJ82tBPhOrtdSwKPANhHxT0kBHBwRt0o6k5QT+YtqFZS0Bmk4fGo+9BvSMPuEfO4uYN18biCwOalRPEnS7TXeveStiNhMacrCucDOVerxCVL80Z4R8aik5YDyDEwkHQIcArDGGmvU8XgzMzOrpTcW7zRlTmM1uadwS9JikMmk+YPFBSs3R8RHeZvBWj16f4qI10rFAqdJmgrcQwoeb293mL1JYd/k37X26i5+B0XbkQLUyd//m/n4kbkHcyLwOdqyJavlRJbbU2nx0fOkYPR5+fhQYFT+3sYAyxV6Dm+JiHdyQ/9+Umh6e35f+L1Fjeu+BLwUEY/md32r0vQD51iamZk1Vnf1WM4Ahlc516M5jZKKOY215hKWciXvKzu+GPBGqUewguK8xmrvtkC9cj1WBjaJiPeVFqZUzVpUmru4HTAg9yIuDoSkY6v0ctaTKVkqewipAbhFRLwtaWyhLtVyIsuV5lhuAdwu6Y8R8TLpu9uifMccSQDl9Q7a/28gqnxe6LXaOW9mZmbdoLt6LCtmNErahhRT01Q5jdkvgTOVVrOT63FkRLwFvCBpj3xckjbsYr2WB17NjcptgTXbKW848LuIWDPnSH4OeIHU+9sR95IW65C//+VyXV7Pjcr+pOHpTomIh0h7iR+VD90NHFE6r7SAq2RXSUvmRvMQ0hB8e/8N7Fn4/VCNqjwNfEYpFxRJy+bpB2ZmZtaNuqVhWSOjcRZptXiz5TQSEXcAFwD35Po+TlsP3T7AgXm4eAYpHLyWqcAHeeHIiArnrwYGS3osl/10hWuK9iZ9b0U3klaed8RRwLZKGZKPk7Y6vBPok4flTyENh3fFGcABecj7SNJ7TpX0JGmxVckjwO35eadExKw6/hv4pKSH83tU+l4BiIj3SI3P8/O/2Z/w7jtmZmbdrttyLJuFupjT2B3UzRmfamC+p1JO5LFAv4h4NR+bn7Up6cGI2LITZc5fdNUMnGNpZmZWH9XIsVykd95Rymm8kRQl1BSk+RmfYyNi7YhYDzie9hfvdMQQ0oKjSs/vzJDwHOBHlU50tFFZiYepzczMFg2LdMMyIk7P8xInlI5JOkFtOY2lnxN6sFoVMz6BCWrOfE9Iq+v3lPTp8hOS5hY+H5vrMUXS6fnYwUoZllMk3Shp6YgYSVqIVMzb3Ewpd3JS/v2lfP/Skv4nD6dfJ+nh3Atd/uzhkkbnz7vk6yZJukft5G+amZlZY3zseooi4lTg1F6sQrW8zGbN94S0u9HlpLmNJ1W6QCk/czfgy3khUKkR+odC0PwvSAHv5+dzxTotB2wdER9IGgqcBuwOfJe0uGigpAHA5Dq+kwnA5nlLyYNIQ/kL9bjKOZZmZmYNtUj3WLaYZs/3PA/YLzcAKxkKXBERbwMUMjsHKO1WNI3UmF2/Sp2WJ2WFTgfOKVz3FXJ+Z0RMpy18vZbPAnflZx5T9sz5nGNpZmbWWG5Y9rxSXma5Hs33BIr5nn+sVeF8zxukvc+/W+WSatmRo4EjImID4OSy+hfzNk8B7o+IAcAuhetqZYMWn1cs93xgVH7moXhFuJmZWY9ww7LnVcz4BF6nOfM9i84mNdQqNWDvBr4jaWmAwlD4ssBLkpagdkD98sCL+fP+heMTgG/kMtcDNiice0XSupIWI8VbVSprv3beyczMzBrEDcseViPj8xqaMN+zrO5zSCvaP1nh3J25zMeUtnA8Op/6GfAwKUuyVl7nmcAvJT1A2lmo5EJg5Zyz+WPS91DaivI40paT9wEvFe4ZSRpWH09a0W5mZmY9YJHPsVxUdTULs718z27IwjwYmJ0P3RkRx9V57+LAEhExT9LapN2DvphD0BvGOZZmZmb1qZVj+bFbFb4oKGRhXhkRe+Vjg0hZmO02LHO+5+HUHpoeQloNvlDDUlKfiPigg9U+p1YguqTFqwzJLw3cn4fSBRze6EalmZmZNYaHwltTl7IwSaumT4qICYUszFmS3pH0lNL2iycAP2tgFuZC8rNPlDQB2KNK5uW/gOmkVfJzgQskDS+UUSk7c21Jd0p6PK9I79/xr9jMzMw6yj2Wrak7sjA/k7MwN85ZmCNpbBbmCEn75s8/joi78ud5EfGV/IwVa2RerkaKHupPmst5Q43szEuBwyLiWUlfJs3T3K68Qs6xNDMzayz3WC5amjkL85yIGJR/7iocv67wuVbm5c0R8VFEPEnb9pcLZWdK6kvazvL6vIjoElKjdCHOsTQzM2ss91i2phnA8ArHezQLU1IxC7PWfM1ailmWo4HdImKK0raVQyrUEdres1J25mLAGxExqJP1MTMzs05yj2VrauUszFrqzbwsWSg7MyLeAl6QtEc+JkkbNqBuZmZm1g43LFtQK2dhtqPezEugZnbmPsCBkqaQend3bVD9zMzMrIZFIseyq5mOdT5jCN2T69gHOD4ixnS13E7W4+mYkY4AACAASURBVFigX0S8mo/NjYi+dd5fMwuzcN0PSYtk3gc+ImVR/jgi3q9xz2HA2xHxu3rq0lXOsTQzM6tPrRzLlu+xLGQ6jo2ItSNiPeB42hZ4NMoQ0qKQSnXozFzVc/I8wD2Ay/O2hL1hDvCjjt6UszBvBH7SznWHATsCm+e9uzcFXgWWqnVfRFzcU41KMzMza4yWb1hSJdMxIsbn+XXt5jpKGpUXi5SyFU+W9ES+p7+kfsBhpMichuY6RsRTpMU1K0naRdLDkiZJukfSqrm8kZKuknRffs7BdbzHiTkTcrqkS3MDvJLLSfMyP11+QtK+kh7J73xJnrv5DUlnR8TppL3Df5evXTt/d5OLP8DppFDzN/L7vhcRp+e5kEiaW3jecEmjC+98dP48VtIZuS7PlIbmc33Oyu85VdKh+XhfSfcW/g09FG5mZtYDFoWGZbVMR1gw13EoqQFYMXqmzJyI2Bi4CDg6ImYCF9MWmTM+X1fKdRxBWsRSWnBST64jAEo5ix+RhsUnkHr2NgKuJQ1TlwwE/hPYAjhR0mfaKXpURGwaEQNIvYM7V7luLqlxeVRZvdYF9gS2yj2rH+b3GweUhr6/CvxT0uq0RR2VIoUG5fMRES+09z3UoU9EbAb8ADgpHzsQeDMiNiX1hB4saS1gHjAs/xtuC/y6UsNa0iGSHpP02OzZs8tPm5mZWQctCg3LWpo513FE7tH7FbBnXpDzWeAupRzHY1gwx/GWiHgnN1bvBzZrp/xtc+/nNFI4+Po1rj0P2E/ScoVj2wObkELWJ+e/Px8RLwN9JS0LfI60YGhrUiNy/ILFLhgHJOnfc0/mTEkVpxXUUOnfZEfg27l+DwMrAuvk554maSpwD7A6FaZGOMfSzMyssRaFHMtqmY7Q3LmOlfbOPh84OyLG5MVCIwvnyldZBVXeQ9KSpN1mBud6jWThd2wrKOINSdcA3y0cFmkv8kpzKB8CDgD+QmpMfofUk7rAXM2IeEvS/0laKyJeyMHod+Xh+09UeK+qdaTyv4mA75cFrpOnA6wMbBIR70ua2U7ZZmZm1gCLQo9lxUxHSduQhm1bKddxeeDF/Hm/snO7SlpS0oqkhUSPUv09So2oOUo70VRreBedDRxKW6PtXmC4pFUgZURKWjOfG0eK9hlHii7aFng3It6sUO4vgYskrZDLEQs28l6RtK7S4qVhddSz6C7gcKXcSyR9UdIypO/x1dyo3BZYs1YhZmZm1hgt32MZESFpGHCu0krleeS4IVLDZwtSrmOQcx0BJJVyHZ+l/lzHG/JCkO9XuWYMaQi8s7mOI0lbEb4ITATWKpx7BLgdWAM4JSJmQeX3yD2QlwHTSN/Fo+09OCLmSLoJGJH/flLST4G7c6PvfeB7pMbseNIw+Li8b/jfqZ47eRGwNPCwpHdJczofoO07Pw64Dfg7MJ2Ui1mv/yYNiz+RG6yzSXuHXw3cKukxYHKNupmZmVkDLRI5ls1CdeY61lFOeS7nEsCNEXFc12vZ8EzO0cBtEXFD4VjdWZjNwjmWZmZm9dGinGPZLFRnrmMd5VTK5byX9ofhO2IIjc3kbJekxbujXDMzM2seblg2SM5mXDMiJpSOSTqhPNdR0gntFFUpl/Mw4Ag1eSZnuVy3+/PCoGmS+kmaXjh/dF5YVJoXO1XSQ6X3zMf3lzSqcM9tuccVSRfluKAZkk7Ox7bPQ/ql63eQVFpRbmZmZt2o5edYNrOIOBU4tYO3VcvlLGZyrkSKARpXR3lzImJjSd8lZXIeJOliYG5pVbqkA2nL5PxQ0hukVe3n0oFMzio2AwZExAu5UVvNFcAhEfGgpNPrLPuEiHgt94beK2kgaTHXBZJWjojZpNXrFee8SjqEtNUka6yxRp2PNDMzs2rcY9k6mjWTs9Ik3eKxR9oLSM8rxpctzPm8ptb1Bd+Q9ARpIdD6wHo5D/QqYN9c7hbAHytW3DmWZmZmDeUey+ZTLZezWTM5/wl8an4l09aQxd7N/yt8rlbXau9W9R6lHXaOBjaNiNfzIqJSeVeQVvHPIzWYP6hRvpmZmTWIeyybT8VcTuB1mjOTc2yuVynwfH/SzkCVvAKsImlFSZ8kbzMZEa8D/5K0eb5ur8I9M4FBea7n52jbcWg5UqP1TaU91Xcq3ZCjmGYBPwVGt/OeZmZm1iDusWwy7eRy9qXJMjkj4jZJmwCPS/oQ+CtpcVCla9+X9HPS9osvsGC+5IHAZZL+j9RYLYWtP5CvnUbKuXwilzVF0iRSD+/z+bqiq4GVI+LJWvU3MzOzxnGOZQuokGs5E/hBRDzToPKHUJZr2dlMzrzK+2BSWPmSpN7L70XERzXuGQ3cExH/L/99HLBaRBzVgefeAXwzIt7If48CJkXEb+u53zmWZmZm9XGOZQurkmt5PLBqAx8zhEKuZTGTs5O5ludExCBgPWADYJs67tk4xx9NB74K/KJ4sr0czIj4WqFR+TgwkDSUb2ZmZj3EDcvmVynXcjIwobtyLYH+pIblKbTlWp6qtizOd/P97WVyfoLUa/l6fv7Bkh6VNEXSjZKWLlzbB3ibtP3jFRExuzwHM5dxs6THc3blIYX3nClppfw+SwN/IW31eLekpTryhZuZmVnnuGHZ/OrJtRxKagCuVkd5cyJiY9Ie3kdHxEzgYnIvY0SMz9eVci1HkHr+ZudeyGNJWzhukHM6KxkhaTLwEvBMbggD/CEiNo2IDYGnSPMqS1YjRSrtDBRzLDcj5VWul//+TkRsAgwGjpS0YoXnrwNcEBHrA28Au1eqpKRDcsD6Y7Nnz67yKmZmZlYvNyxbV7PmWkLbUPgqwDKSSqu8B0gaL2kaKcJo/cI9N0fER3mxTXGYvzwH80hJU4CJwOdIjchyLxQas1Xf0zmWZmZmjeWGZfObAWxS4XiP5loCxVzLioHj5SLifeBOUjQSpOifIyJiA+Dksrq9W/hcfLf59ciLjIYCW+Rez0ks/H7lZbX3nmZmZtYgblg2v1bLtZwvLzzakhRBRH7GS5KWoHboejXLA69HxNuS+gObt3eDmZmZ9Rw3LJtc3qJwGLCDpL9KmgGMJG17OJWUa3kfOdcy9y6Wci2vpv5cy2GFxTuVjCHlaLY3DA5tcyynk3oLL8zHf0bKsPwTC2ZY1utOoI+kqaSFRRM7UYaZmZl1E+dYNoHuzqnMzxhCWVZlB++fn2sp6UvAJcAKwCeB8RFxSIV7PgOcFxHDy473Iy0AGtCZuhTKGUJagLRzV8oB51iamZnVq1aOpeee9bJCTuWVEbFXPjaItIClYQ1LUlblXGChhqWkPrX20865lofTNnx9HqmReUs+v0GVMmdRed9zMzMzWwR5KLz3VcypjIjxSrolq1LSaElnS7qftqzKlXMZi0l6TtJKuT6nR8SaETEhP3I1YMdSriVwVf58g6TrJd0K3C2pXw48r0u1nMtc1/MkPSjpeUkLNVYlbSppkqTPS9osXzsp//5S3f8aZmZm1mluWPa+ajmV0PNZlaUeyaHAlIiYU6X8c4B9STmVVwJDcrzQbcAWwH4RsV0d9SzXmZxLJG2Z32/XiHieNH9z64jYCDgROK3Sw5xjaWZm1lhuWDa3psyqjIgrgHWB60lD7BMlfTKf/lNEvFZHHSvpTM7lusClwC4R8bd8bHng+txbek5ZOcX3cI6lmZlZA7lh2fuq5VRCE2dVRsSsiLg8InbN9SktxPm/Gre1ZzQdz7l8CZgHbFQ4dgpwf14ctAuVsy7NzMyswdyw7H0VcyolbQOMowmzKiX9R86iLK1oXxF4sY46tKczOZdvAP8JnJZXiUPqsSzVZ/8G1MvMzMzq4IZlL6uRUzmLtFq8GbMqdwSm560V7wKOiYiX66hD0Zck/aPwswedzLnM0wR2AS6Q9GXgTOCXkh4AFu9gvczMzKyTnGPZy7o7w7Ij+ZXFrMoq50cCcyPiVx14/ljSAqJuDYmslplZL+dYmpmZ1adWjqV7LHtRIcNybESsHRHrAcez4OKUrhpC2lax0vP7FD4fB9wI/KSBz+4xec6nMzPNzMx6kRuWvatihiUwoafzKyPidGAtYHQpv1LSCaWsypxXeRh5PqeksZLOkPSIpGdKw+uSlpJ0raSpkq4DlirUd+9ct+mSzigcnyvp1JxfOVHSqvn4yjnP8tH8s1U+vk2hXpMkLVvMzMyfx+fv4okcR2RmZmbdzA3L3lUtw7Ip8isj4tR836CcU3kxcG/heX0iYjPgB8BJ+djhwNsRMRA4lbziPQ9VnwFsl99tU0m75XuWASbm/MpxQGkh029y3TcFdictLgI4GvhertNXgXfKvodXgR3yd7EnaaeghTjH0szMrLHcsGxOTZlfWefztiY1VomIqaQFRpDqPzYiZuftI6/O1wK8RwpXLy9rKDAq95aOAZaTtCzwAHC2pCOBFSpsR7kEcFnOw7weWK9S5Z1jaWZm1ljeK7x3zaDyXto9ml8pqZhfWW/MT63nVVoRVu2dIE0HKN1TLGsxYIuIKO+RPF3S7cDXSOHsQ0lZliUjgFdIPb6LlZ0zMzOzbuIey95VMcMSeJ0mzK+s0zhy41TSAGBgPv4wsI2klSQtDuxN6omt5W7giNIfkgbl32tHxLSIOAN4DOhfdt/ywEsR8RHwLRw5ZGZm1iPcsOxFNTIsr6E58yvrcRHQV9JU4FhSg5iIeIm04vx+0ns9ERG3tFPWkcDgvBDoSdLiIYAf5AVAU0jzK8t3CboQ2E/SRNJ80q7sBmRmZmZ1co5lE+upjMv8UzW/ss6yRpIakv0i4tV8bG5E9G1APQcD346II6tlaTrH0szMrGfUyrH0HMsmVci4vDIi9srHBpEyLhvSsCRlXG5KWp2+wNxKSX0qLIppzxzgR8CPG1K7LIer12z1RcQsKs9XNTMzsx7iofDm1VMZl4NIczpVyLh8Hpgl6d18/WRJP5X0XCnjsorLSXNDP11+QtLNkh6XNEPSIYXjc3Me5uOS7pG0Wc7IfF7S1yu9G7ChpPuUMjgPztc4x9LMzKyXuWHZvHoz43KdiFgFOA34bc6LfIRCxmUVc0mNy6MqnPtORGwCDAaOlLRiPr4MKYZoE9JCo18AO5Dmnv68ynMGAv8JbAGcmIfBi5xjaWZm1gvcsGw9zZ5xeR5p4cxyZcePzIttJgKfA9bJx98D7syfpwF/joj38+dq9bwlIt7Jjdz7gc3KzjvH0szMrBd4jmXzasmMy4h4Q9I1wHfnVzgtEhpKyqR8W9LYQv2KGZYfleoZER+psJd5+WPa+ds5lmZmZr3APZbNq5UzLs8GDqWtAbs88HpuVPYHNq+znGp2lbRkHk4fAjxadt45lmZmZr3ADcsm1coZl3mI+ibgk/nQnUCfnG15Cmk4vCseAW7P5ZySV4QXOcfSzMysFzjHskn1VIZlRDzYznWDaSfjMmdLHgzMJvVSHh8RYxpdl86QNBq4LSJuqHWdcyzNzMzqUyvH0j2WTaiQYTk2ItaOiPWA40kZlo0yBKgYw1Oa2yjpOOBG0o457Tknrx7fA7hcUl3/beVnVa2LmZmZtQ4v3mlOFTMslZwF7ERasPKLiLgu9/gdHRE7Q8qwBB6LiNGSZgJXAruQVkvvQVrMchjwoaR9ge8DBwKvARsBkyXtDGwZEadLWkzSc6S5kYfmMor+Sd5WMSKekvQBsJKkpUgry1cm9WYeEBF/y72IpWe9BmxVoS7zexlLO/jkxuooYBvgBdL/GF0eETdIOjG/41LAg8Ch4e54MzOzHuUey+bUmxmWQyNiBGnBTmkV+FByhmVEnJrvmf8DlO5H0pdJq7tnkxqBv4uIgaR5n8U8ydKzdq9Sl0r+ixRBtAFwECnHsmRURGwaEQNIjcud2/tSnGNpZmbWWG5YtpZmzrAcIWky8Ctgz9xbuAVpsRHAVbn+lZ5Vr6/k+z6KiJdJGZYl20p6OGdXbges315hzrE0MzNrLA+FN6dWzLA8JyJ+1c41xaHpWiu1579Pnm/6iXy84vtLWpK0EnxwrvdIFv4OzMzMrJu5x7I5tXKGZdGDwF758z7AhDrrMhPYJH/elTQ3lHz/7nnO56qkRT/Q1oicI6kvlRvlZmZm1s3csGxCrZxhWeZI4ICcX/ktKu8hXqkulwHbSHqE1Fta6t28EfgHMB24BHgYeDMi3sj3TANuZuHAdDMzM+sBzrFsQT2VcZl/amZYdqDMKcCTEbF34dho6siYLCunb0TMzbvuPAJsFREvS/oMcF5EdKq30jmWZmZm9amVY+k5li2mkHF5ZUTslY8NImVcNqRhSRpi3pS0On2BuZWS+kTEBx0pTNK6pN7xrSUtExFd2QnnNkkrkOZdnpIblX3y7jseAjczM+tFHgpvPRUzLoEJks6SNF3SNEl7Qup9lHRb6VpJoyTtnz/PlHSypCfyPf0l9SNlXA4izemUpNGSzpb0PDBL0rv5+smSfirpOUkr1ajzN0mrwu8Gvl7pAklfk/S0pAmSzivVWdIyki6X9KikSbQFsZ8J/KekW4G7JfWTND3f00/S+PxeT0hy+LqZmVkPcI9l66kn43Il4FFJ4+oob05EbCzpu6SMy4MkXQzMLa3ylnQgKXdynYj4UNJJpLmN50raEdgo7w9ezZ7ADsCXgCOA3xdP5lXdlwBbR8QLkornTwDui4jv5J7KRyTdk89tAQyMiNdyg7jkVWCHiJgnaZ38vIW67CUdAhwCsMYaa7T7RZmZmVlt7rFcdDRlxmVezT47Iv4XuBfYWNKnyi7rDzwfES/kv4sNyx2B43JG5ljSCvBSK/BPEfFahccuAVyWMy2vB9arVDfnWJqZmTWWeyxbT6tlXO4N9M9bSwIsB+xOijJqr+6lc7tHxF8WOJh2+Kk2V3ME8Aqp93Yx0haWZmZm1s3cY9l6WibjMu/tvQdpuLpfRPQj5VLuXXbp08DnC8PZexbO3QV8Py9aQtJGddR/eeCliPiIFHO0eB33mJmZWRe5YdliWizjcmvgxYh4sXBsHKmhO3+P84h4B/gucKekCaTexjfz6VNIQ9tT8+KcU+qo/4XAfpImkuaGdmUVupmZmdXJOZa9rKcyKSPiwS6WcwKp9xFgA+A5YHXg+Ig4r8o9w4AvRMRZkr4HvBERV+fG4xF5NXvp2r6kAPThwBnAsxFxTll5PwQujIiGD207x9LMzKw+zrFsUj2YSTmXtL1i+fPrzqSMiFOBU/N975Lmav5HRFTbppGIuKnw+YJ2HnEw6b0fJvWqXlLhmh+SFg55zqSZmVkTcsOyd1XMpFRyFrATEMAvIuK63Pt4dETsDCmTEngsIkbnxTFXAruQho73IDXADgM+lLQv8H3gQOA1YCNgsqSdgS0jYnaeE/kMsHk78UHvR8SapT8k7QqMAlYkLRb6W/79PPC3iPiBpF+Qoo3OLdy3eK7zcxExUtKPSHFKHwI35t10FicN9X8OWAUYL+mViBgq6VJgY2Ap4LqI+Hku9x+kOaC75vuHN6oH2MzMzKrzHMveVU8m5VDgrOKcxBrmRMTGwEWkBuhM4GJyqHhEjM/XfREYGhEjSAtwSqu6hwJT2mlUVjIOWCMilgaOBW7PIeZ31LinD2le6LSIGFl27mvAzIjYMCIGkGKFziHlU341Iobm647LXfEbkuacFmOFXomIjUgNzB9WqoCkQyQ9Jumx2bNnd+iFzczMbGFuWDanpsykrGEN0u4300iNuPXruOe3wBMRcUaFc1OB/5B0uqStIuLNCtcA7C3pCeAJYF0WzKts97twjqWZmVljuWHZu2YAm1Q43qOZlEAxk/KPtSpcxQWkXtENSKu7y+tVyQPA9pI+WX4iIp4i7ZQzg9Rbe3z5NXlHnaOA7SJiIHBn2XPr/S7MzMysQdyw7F0tk0nZjuWBF/NipP3qvOdS4B7gWkkLNPwkrU7aUvIq4GzSPEpY8F2Wy3+/lacJ/Hsn6m1mZmYN5IZlL2qxTMpaRpJWt/+ZlEFZVDXPKiLOBJ4ERueFQyUbkvY6n0yas3laPn4pcE/eK/yJfO904DJSD6iZmZn1IudYNoHezrKUNJg0lF2t4Vm8diSpN/FXZccfjIgt8+45W0bENZJ+TBpenxURR3TtLdqt14MRsWVn73eOpZmZWX2cY9nEmiDL8njgUGrv992uQqOuH/BNSZ/OZV4FrFntvkbpSqPSzMzMGsND4b2vYpYlMEHSWZKmS5omaU9IvY+SbitdK2mUpP3z55mSTpb0RL6nf+5BPAwYURoOlzRa0tmS7gdWBt4D/pLLWEzSP/P9kws/J9R6CUlz88fTga8CB5GG1mcDn5F0p6RnJZ1Z4R4kDZc0On/eRdLDkiZJukfSqvn4SEmXSxor6XlJR5aXJamvpHsL38Gudf9LmJmZWZe4x7L31ZNluRJpzuG4OsqbExEbS/ouKcvyIEkXUxi+lnQgbVmWH0p6g9S7eC4py3JsROzeyfc5jgVD3PfP77ERaZj/L5LOz/NFq5lACmkPSQeR5ln+KJ/rT2qML5vLuigi3i/cOw8YFhFvSVoJmChpTFSY8yHpEOAQgDXWWKOTr2tmZmYl7rFsXq2WZVnLvRHxZt7j+0naHxr/LHBXzsU8hgVzMW+PiHdziPurpCkDRQJOkzSVtOp89QrXAM6xNDMzazQ3LHvfopJlWcu7hc/FehV7EYvvcT4wKudiHkrlfMryskr2IQ3vb5J3/3mF+nI1zczMrIvcsOx9i0qWZUeeVfKKpHVz1NCwwvHlgRfz53pzMYv3vhoR70valh5YOGRmZmaJG5a9rEWzLH8q6R+ln7JzU4EPJE2RNKKdco4DbiO930uF4yOB6yWNBzq6b/nVwGBJj5F6L5/u4P1mZmbWSc6xbEK9kWvZkSzLsrK+BFwCrAB8EhgfEYfkZ8xfxNPdnGNpZmbWM5xj2UJ6I9dS0nHA4cA+kvpExAcdKOs8UoP0llzWBg2qY4c4x9LMzKz3eSi8+fR4riUpwudG4BTgrJw3eWohw/LdfH+lLMvVgPnD4RExrfwCSZ+WdLOkqZImShqY8zJnSlqhcN1zklaVtLKkGyU9mn+2yuedY2lmZtbE3GPZfJol1/LNiBgkaUfg0Bq5lucA90l6ELgbuCIi3ii75mRgUkTsllee/y6XfQtpfukVkr4MzIyIVyRdQ+oFnSBpDeAuYN1clnMszczMmpR7LFtHU+ZaRsQVpEbf9aQh9omSPlmh7lfl6+8DVswr2q8D9szX7JX/hhTSPkrSZNKiouUklVaaO8fSzMysSbnHsvnMAIZXON6juZaSirmWNfcRj4hZpMbo5ZKmk3pd26t7AA8BX8hxSrsBv8jnFgO2iIh3FihEKr5PtXcq5li+L2kmzrE0MzPrEe6xbD4tlWsp6T8kLZE//xuwIm0ZlCXjyI3TvFp8TkS8lYenbwLOBp6KiH/m6+8Gjig8Y1Ad71TiHEszM7Ne4h7LJpP3xx4GnJtXa88jxw2RciankHr7jo2IlwEklXItn6X+XMsb8sKW71e5ZgxpCLy9XMsdgd9Impf/PiYiXpbUv3DNSNI8yqnA2ywYen4d8Ciwf+HYkcAF+fo+pIbpYe29VHY1cGvOsZyMcyzNzMx6jHMsW0CL5VqOBm6LiBsKx+ZGRN9G1LXGc8eSFid1KozSOZZmZmb1qZVj6aHwJlfItRwbEWtHxHrA8VRZkNJJQ4D5OZC5p/RG4CeS3KttZmZmdXHDsvm1Wq5lVTm78kJJMyTdJukOScPzuRNzZuV0SZfmBjU5s/IMSY9IeibXD0lLSbo2Z2NeByxVeM5Fkh7Lzzm5o1+4mZmZdY57o5pfq+Va1vJfpMijDYBVgKdIq8kBRkXEz/PzrwJ2Js0FBegTEZtJ+hpwEimO6HDg7YgYKGkg8EThOSdExGuSFgfulTQwIqaWV8Y5lmZmZo3lHsvW1ZS5lqSFRdWOfSWX+1FeeHR/4ZptJT0saRqwHbB+O3XemrRqndxoLDYcvyHpCdJCpvWB9SpW1DmWZmZmDeWGZfObAWxS4XiP5loCxVzLP9a475/Ap+ZXUvo0MKdWnSUtCVwIDI+IDYDLyupdrc6VdtNZCzga2D4iBgK34xxLMzOzHuGGZfNrqVxLYGyu1yfy3/vT1jM5Adg9z7VclbRoCNoafnMk9aVyQHy5YjbmAGBgPr4cqVH8Zn7GTnWUZWZmZg3gOZZNrtVyLSPiNkmbAI9L+hD4K20ZlDeSGrrTgWeAh0lzN9+QdBkwLb/bo3XU+SLasjEnkxrVRMQUSZNIPb3PAw/UUZaZmZk1gHMsFzHdlXlZyrUEfkZZ5mUHy+kbEXMlrUhq+L4LvELqtbwf+F5EfNSAun47Io7MK+IHR8QRte5xjqWZmVl9auVYusdyEVLIvLwyIvbKxwaRMi873bDMPaWHk4aehwJzgYUalpL6RMQH7RR3m6QVgE+QhrMnRMSvJC2W/96GBRf11FvufDkk3a1EMzOzHuY5louWbsm8JDUo/x34B22Zly/lfMvXJL0q6V/An/OxlXMZi0l6TtJKhfoMiYhBOeh9cqHunyD1Wr6e7x0r6TRJfwaOkrRLXjU+SdI9ef4kOQuzlK/5pqT9yt/LzMzMeoYblouWejIvh5JCz1ero7w5EbExaT7j0RExE7iYtNXjahGxDmnu5SPAChGxFWmBzz75/qHAlIiYs3DR842QNBl4CXgmN4RLVoiIbSLi16SFP5tHxEbAtcCxABHxtYgYBBxIWrh0cx3vBaQcyxyk/tjs2bPrvc3MzMyqcMPy46FZMy8hNVIHkQLTl5G0V+HcdYXPnwXuyjmXx1DIucw9olcB34yIN9t53nzOsTQzM2ssNywXLa2WeTlfRLwP3EmKTVqoXOB80u48GwCHluqad9e5Fvh5REyv51lmZmbWPdywXLS0WublfHnh0ZakeKJKlgdezJ/3Kxw/HZgaEdfW8xwzMzPrPm5YLkIiZUcNA3aQ9FdJM4CRwDWkzKgW1gAAIABJREFUXMsppMbnsRHxcu5dLGVeXk39mZfD8mKZr1a5ZgwpY7O9YXBom2M5ndQremGV60YC10saT9tOPpB22dmxsIDn63U808zMzLqBcyw/Jror37JQ/hByvmUp8zIiqjU82ytrJDA3xxDtD9wdEbPauWc0cFtE3NCZZzrH0szMrD7OsfyY6658yzJDgLmStqYt87L0/A7lUJbZn9SbWbNhaWZmZr3PQ+EfD92Sb5nv6S+pHznfEtgL2Bc4SNLZku4n5Vu+m68vDVn/s5hvWYmk4cBg4Op8z1KSTpT0aK7zpbnRXLxne0k3Ff7eQdIfyss2MzOzxnPD8uOhJ/MtB0XE+HzdF4GhOd/yNOC3OVroWGBsO/mW5GHtx4B9crnvkFaGbxoRA4ClgJ3LbrsPWLcU0g4cQJW5ns6xNDMzayw3LD/emjnfsppt8w4804DtKORZwvwFTFcB++atI7egSuSRcyzNzMway3MsPx5mAMMrHO/RfEtJxXzLfarfVpmkJUmrxgfn8kZWqBukRuutwDxS47az8zvNzMysA9xj+fHQsvmWZeWWGpFzJPWlcmOZvIJ8FvBTYHSdzzEzM7Muco/lx0BEhKRhwLmSjiP15M0EfkDKm5wCBDnfEkBSKd/yWerPt7xB0q7A96tcM4bUm9iRYfDRwMWS3iENa18GTMv1f7TGfVcDK0fEkx14lpmZmXWBcyybQE9mTDaovG+TFuAo/1weEb+qcf1o4DbSe3Ul33IIabFQ+YIdJN1B2iv8jfz3KGBSRPy2nrKdY2lmZlYf51g2sZ7MmAQWalh2NGNS0k6kns4dI2JWnvf4rTpu3Q34Kp2YW1mPiPhaoY6Pk+Z3/qg7nmVmZmaVeY5l7+uxjMnSNoySRhcyJs+S9GwpnkfSYpKeq5Ex+RNSr+GsXNd5EXFZvneQpImSpkq6SdKnCvfdHBFrkuZ6Tsr1e1zSlFyv9/Linr/lCKCNJd2ltDXlYYVylstlPynpYkmLFd69VOe/A8sAT0g6pOP/JGZmZtYZblj2vt7OmBxBWlBT6kkcCkypkTFZrb4AvwN+HBEDSfMgTyqezL2bo4E9I2ID0mr1K3K25SxgZESsAYzP1w0HNgd+XihmM1JP5AbA2qTvqdx3ImITUrj6kZJWrFRZ51iamZk1lhuWzaulMibz6vEVIuLP+dCVpFXmRV8CXijMHS2/Zkz+PQ14OCL+FRGzgXk5kxLgkYh4Ptf996TvqdyRkqYAE4HPAetUqrNzLM3MzBrLDcveNwPYpMLxHs2YBIoZkxUDxdupbz2qvVNJqe4fFT6X/i69S/lqswX+zgt8hgJbRMSGpBXtlbIuzczMrMHcsOx9rZYx+UvgzLySnVyPIyPiTeB1SaUV398i9bIWPQ30k/SFGte0ZzNJa+W5lXsCE8rOLw+8HhFvS+pPGko3MzOzHuBV4b2s1TImI+IOSasC9+QV7UEaSgfYj5Q5uTTwPGmf7uK98yQdAFwvqQ8ph/JiOuYh4HTSHMtxpBX1RXcCh0maCvyFNBxuZmZmPcA5lh8z1TIzgeXoQsZkofwhNCgzM2/ZOLdWRmajOMfSzMysPs6xNKBmZuYPgZ1oTMbkEBqUmVlNo8oxMzOzxnLD8uOlYmampMOBM0nD2AH8AvgCaSh7ZeCFfPk7wCURMVrSTNKq7l2AJYA9SMP4hwEfStqXNOx+IPAasBEwWdLOwJb/v707D5OzqtP//75ZZJVNwAE1BCMSwhYDOLIYIgbUEYFIkCD6A2RxRAWjiEBUgv6CIArIMOwyoIIgIJgREQQTSMAAIWRX9qCySIIQJkjY8vn+cU7RTypV1dXd1d1Vlft1XX2l+lnP6eYKn5znOfeJiIX5PcmHgQ/ViDcCQNJkUrG6OzBR0sOktcDfBjwPHBoR/8jRQr/M7b4P+DiwU2fXNzMzs55zYblyqSczc2PSu4//DtxNYQnFvExi0aKIGCbp2HzcUZIuovD4WtKRdGRmvinpRdLI6Ll0nplZboOI2DNfd0NSQRqSjiItMfkNUnbm1Ij4nqRPAlUD0nN4+jEAAwYMqLMJZmZmVo1nhRu0TmbmtYXP7wZulTQH+Cawbd4+nDS7nYi4mTS7viLnWJqZmTWWC8uVS6tlZla9DvBfwPl5BZ8vlrXNM9LMzMz6gQvLlUurZWbWsj7wVP58WGH7XeRJSJI+AWyImZmZ9QkXliuRSNlSo4C9JT0maR4wHrialIs5i1R8nhgRz+bRxVJm5lXUn5k5StLMQlh6uYmkjM4uLx1ZMJ6UhzkFKL6jeRowXNIMYB/grz24h5mZmXWBcywbrFpOZGF97J5efwSNzYk8FdgqIh7N28YCZwO7RESXgx0lHQA8HBHzaxyzMw3IzKyzPQuAnTubIOQcSzMzs/rUyrH0iGUDFXIiJ0fEoIgYApwCvLOBtxkB7Fbl/t2Z5T8HGFP4fjRQtSiswwHAkGo78+pCNwAn9+AeVXXzZ2BmZmYN4MKysSrmRAJTJZ0laa6kOZIOhjT6KOm3pWMlnS/p8Px5gaTTJM3I5wyWNJCUEzm29KhZ0hWSzpY0CThL0iP5PUkkrSLpUUkb12jzTcD++fj3AouBhYU2HZLvP1fSmYXtSyRNkDRL0jRJ75S0G7BfbsdMSYPy1+8lPZAfW98UEVsAR0k6T9I9kv4p6Yl8zkxJT0n6u6TZkk4r3PM7kv4i6Q+SfinphLx9sqTTJd0JHC9pC0l35GUdHwPWrtRxScdImi5p+sKFCysdYmZmZl3gwrKx6smJHEkqvDar43qLImIYcCEpJ3IBaW3tcyJiaERMyceVciLHkibFlFbQqScn8iXgb5K2Aw6hEOkjaXPgTGCv3P5d8qNugHWAaRGxI2nCzNH58fxE4Ju5fY8BlwBfjYidgBOACwr33owUdbQH8GZEDCXlUd4MvCffcydJw/Pj8wNJQeufBsqH4DeIiD0j4sfA+cDPImIH0ruh51XquOOGzMzMGsuFZd9o9pzIa0iPww8gPcov2YX0WH9hXkLxKtKMcYDXgNJoa8X2SVqX9Nj+OkkzgYtJxWTJTRGxLL+PWXpdYJ/89SAwAxgMbEX6Gf4mIl6JiP8jTRIqKmZc7kqakATw83yumZmZ9TK/j9ZY80jvKJbr05xIScWcyHrW//5f4CxgekS8lF4VrdluSI/8SzO/qrVvFeDFPBJZyauFzyr8+YOIuLh4YJ5UVMvLNfZ5hpqZmVkf8IhlY7VkTmREvAJ8C5hQtuteYE9JG0talfSo/M562xcRLwFPSDoI0uQmSTt2cv6twBfyaCeS3iVpU2Aq8ClJa+Z9n6xxjXvomJB0aD7XzMzMeplHLBsor1s9Cjg3z35eSo4bIuU2ziKNnp0YEc8CSCrlRD5C/TmR10vaH/hqlWMmkh6B150TGRHXVNj2jKSTgUmkkcTfRcRvOrnUNcClko4jjd4eClwo6dvA6nn/rBrtuE3SNsCf8sjpEuBzEXG/pIn53CeB6aSJRpUcB1wu6ZukiUhHdNJmMzMzawDnWDapnuRh1pMT2Qt5mEeTirg1SYXolyNiWSf3PyEi9u3CfdaNiCWS1iZNGDomImbkfZcBZ9fKz6zFOZZmZmb1cY5li+lJHmYXciJH0Ng8zHPyu5RDgO2BPbtxjc5ckicBzQBuKBSVq0bEUd0tKs3MzKwxXFg2p27nYUbEGaTH5e/L+xZI+qOkf0l6RdKfJc0HvkFj8zBL3kYatXwhnzs5j6CS39VcUH6CpE1yNuUMSRdLerJ0L0k35QzMeaRCe2hEDAbGSfqepHuBXcvuc2HOp5xXzMGscF/nWJqZmTWQC8vm1Og8zBsjYm1SMXl3HgH9MY3NwxybRxOfIS3pOLOOdpWcCvwxZ3beCAwo7PtCzsDcGThO0jvy9nWAuRHx7xFRPjlnXB6i34E0+WiHSjd1jqWZmVljubBsLc2ch1l6FL4psI6kMZ0cX7QHaVIPEfF78mhndpykWcA0Umj6Vnn7m6RH/pV8RtIM0mSobamxxKSZmZk1jgvL5jQP2KnC9j7NwwSKeZi31Gpw4bzXgd/TEaRebFt5u0oq9itP8BkJ7JpX+HmwcI2llaKUJG1JWuHno3nlnZtr3NfMzMwayIVlc2rJPMzcTpEmBT2WNy2go0iuFB4PKWfyM/n8fYAN8/b1gRci4l+SBgMfqqMJ65EK5MWS3gl8op52m5mZWc+5sGxCeUWbUcDekh7LE1fGk5YpnE3KcvwjOQ8zjy6W8jCvov48zFGlyTtVjplIyt+sJw+z9I7lXNKoaGlN8B8BX5J0D1Bt8s9pwD758fUnSO9p/h9p5HM1SbOB75Meh9cUEbNI/Z9Hepx/dx1tNzMzswZwjmUL6knGZZ3XH0FaC/w1OsnD7MI1ZwHzI+KQCvvWAN6MiDck7QpcWGMZyGrXXwDs3MkEo6qcY2lmZlafWjmWXnmnxRQyLq+MiDF521BSxmVDCktSxuUupNnpy601Lmm1iHijKxfLK+msAgyXtE5ElK/rPQD4laRVSMXs0eXXMDMzs+bnR+Gtp9sZl/n78yUdnj8vkHRazo+cI2mwpIHAf5JijV5Ih72Vcfk48LSkV/PxMyV9u46My88CPwduA/YrtGWypDNJj+/XAb4SEbsA8yT9StJsSddKureQUXlIvvfcfO4KitmXko6p1ijnWJqZmTWWC8vW0+iMy0U5P/JC0hKLC4CLqJxxuVVEbAqcDvw0P66+j84zLg8GrgV+CZQ/Cl8tIj5IWk/91LztWNKknR1I71buBCBpc+BMYK/c110kHVDhftWyL5fjHEszM7PGcmHZPpoy4zLPZl8YEU8CdwDDJG1YOKTS/Yu5lnNJk5Ig9WdyRCzMj+OvoiPWqKha9qWZmZn1IheWrafVMi4PAQbnyTWPkeKADuzk/tX6Um17xwG1sy/NzMysF7mwbD0tk3GZJ+McBOwQEQMjYiCwPys+Di9XzLUcAmyft99LWqJxY0mr5uvcWXZud7IvzczMrAFcWLaYFsu4HA48FRFPFbbdRSp0a73/eQGwSc6v/FZu++KIeAY4GZhE6ueMiPhN2bldzr40MzOzxnCOZZtptYzLPGv76/nbJaTlGKcAq0fEUkmDSO9mvj8iXsvnHA7cFhFP9+TeRc6xNDMzq49zLFcSrZZxKWlf4IvAHhGxSNIw0kjoXsDVklYnvVf5pVJRmR1OWuGn7sKyO/mbZmZm1jV+FN5eWi3j8lvAN0tRRRExg/Ro/fD8L6EbSKOuZ0m6RMloUozQVfkea0n6rqT7c/8uyQV2KSfzdEl3AseX39w5lmZmZo3lwrK9tFrG5bYV2jsdGJI/nx8Ru0TEdsBawL4RcX0+5tDchlcqHVe43gYRsWdE/Lj85s6xNDMzaywXliuHpsy4rKIYKfSRvOrOHNLj8W2rnFPruGu7eH8zMzPrJheW7aXVMi7nV2jvMGC6pDVJs8NHR8T2wKUV2kcdx5WvS25mZma9xIVle2mZjMvsh8CZpSUX80SjUcDFdBSHiyStC4yu0oZax5mZmVkf8qzwNhIRIWkUcK6kk0gjkm/Pf64NvEiaSX1iRDwLIKmUcfkI9WdcXi9pf+CnQKWXEyeSHoHXfAweERPz+t93S1oNeDfwV2AyaZR1Tv56BymCqOQK4KI8R+d20ijlAlIE0u119MHMzMx6gXMs21SeGX0PKXroorxtKPD2wqSbnt5jPLAkIn5Utn1nuphxKemTwM9I738eCKwBfD4iLpU0mTR5qGrQZJ7NvnNEfKWr/QDnWJqZmdWrVo6lH4W3r76KHhpbWqEnRw9NIS3J+LSkR/KjdyStUkf00EER8elIlkbEpYX9B0m6T9LDpdWAyttcaPsmkm7IEUT3S9q9uz9EMzMzq58fhbeveqKHNgbul3RXHddbFBHDJB1LGj08StJFFEYsJR0JLAbWiYg3JZ0KHCppHdIM8XcAt+dH2NdFxIQ62luyWkR8UNJ/AKeSYpOq+QlpxHSqpAHArcA25QcprfpzDMCAAQPq+BGYmZlZLS4sVz5vRQ+RZm+Xoode6uS8YvTQp2scVx499JtckG4P/CIiVhhhrFO90UeQis4huYAFWE/S2yPi/4oHRcQlwCWQHoV3s11mZmaWubBsX/OoPEO6T6OHJBWjhw6tftpbUUl/rLK/3vtD6seuOTzdzMzM+ojfsWxfrRY99APgh5L+Lbd1DUnH1dGGSm4D3prEkyctmZmZWS/ziGWbqhA9tJQUyfM1YF1gFhA0Lnroq1WOqTd66HeS3kl6B1O5bZfX0YZKjgP+W9Js0n/jd5EmGpmZmVkvctxQE8qjdueS3n18lVwQRsTDDbr+COC1iLinAdcaT1nkkKQFpOifRd2JHuoPjhsyMzOrj+OGWkgerbsRmBwRgyJiCHAK8M4G3mYEsFuV+zdsFDuPlN4AnNyoa9Zxz1X76l5mZma2PBeWzae/8ifPljQJOKuL+ZO1XAP8X0RMzdc6QdId+b5L8sSelyUtKmRTri3pV5JmS7pW0r151BNJF0qaLmmepNMKfV4g6buSpgInSZpR2LeVpFoxRmZmZtYgfsey+fRX/uT7gZE5f/JF0gzuc0nRPbMiYlGNe4yV9LnC95vXOHZKRIxXWk3ngYj4Rlk25bHACxGxg6TtgJmFc8dFxD/zqOQdknaIiNl539KI2CP3Z6SkobkgP4K0BOQKnGNpZmbWWB6xbB1v5U9GxD9ISx/uUsd59eY/ludP/n/58xfoZOIN6R3KoaUv0nrk9ajUtj1II51ExFzSZKKSz+TRyAeBbYEhhX3XFj5fBhyRC9CDgasr3TwiLomInSNi5002qbTkuZmZmXWFC8vmU8pzLNen+ZOk8PRS/uQttRpcQ3faVrGfkrYETgA+GhE7ADeXXe/lwucbgE8A+5JGRZ/vVuvNzMysS1xYNp9Wy5+s5R/AppLeIWkNUqHXmanAZwAkDQG2z9vXIxWPi3Ms0SeqXSAilpKWcbyQzkdbzczMrEH8jmWTabX8yU768rqk7wH3Ak8Af6njtAuAK3MG5YOkfi2OiEckPUga0X0cuLuT61xFei/1tu6238zMzLrGOZYtpq8yLvNXt/MnJY0DDsrfbg/MyZ8vj4jzapy3KrB6RCyVNAi4gzSx6GLgjIh4qMp5E4DbI2JS/v4EYP2I+E497XWOpZmZWX1q5Vh6xLKFFDIur4yIMXnbUFLGZUMKS1LG5S6k2enLre0tabWIeKOei0TEBGBCPm9JntRTj7WBSZJWJ71v+aWIeI00u7vW/cYV2nkjMAjYq857mpmZWQP4HcvW0lcZl0NJ73SqkHH5OPC0pFfz8TMlfbs7GZeSfiHpgML3S/KfI4GbgL+SJubMjIhb8r6pkoZKWk3Sz3Mb5iqvJ152zdmk0dzJki7KBbmZmZn1MheWraWejMuRpJDzzeq43qKIGEaa5HJCRCwALqIjPmhKPu79wFYRsSlwOvDTPAJ5H51nXHbVMODLpCihbSR9qGz/TsDGEbF9RGwH/KzCNX4SEbuQHsGvD3y80o0kHZMD16cvXLiwcT0wMzNbSbmwbA/NnHHZVdMi4pl8v5kV2vUosLWkn0j6GLC4wjU+Kuk+0kSnPUmZlytwjqWZmVljubBsLe2ScflWu/JkneK9Xy18XqFdOZNyB1Is0XGkST1vkbQ2cD4wKuddXs6K/TYzM7Ne4MKytbRLxuUCOgrkUcCq9Z6Y+6eIuI60DOSwskPWApYBiyS9HTiwG+0zMzOzbvCs8BbSRhmXFwO/kbQ3KWfy1U6OL3oP8NM8ISeAbxV3RsTzkq4E5pIK63u72UYzMzPrIudYtqi+yrOMiHsq7NuZLmRcShoPHA0sJP1j5pSImNjJ8Usi4kddb/kK17oC+G1EXF/rOOdYmpmZ1adWjqUfhbegQp7l5IgYFBFDgFNIeZaNMgLYrcK9TyKtxX1yF693Tp5JfhBwuST/t2dmZtZm/D/31tRXeZZjc17lh0t5lsDHSLPJ/ye/70jOsyzmW87MK++sICL+TJq8s7GkLSTdIWl2/nNA+fGSjpZ0v6RZkm7Ik3PI7TlP0j2SHpc0Om9X7t98STcDm/bwZ21mZmZ1cmHZmvozz3JkRIwlTd4prcxzH+lx8/b5+KF55Z0VSPp30uSahaTZ2z/Ls7evAiot9fjriNglInYE/gwcWdi3GSlqaV/gjLxtFLA1KcPyaCqMuhba4hxLMzOzBnJh2V6aOc9yrKSZwI+AgyO93LsrcHXe//Pc/nLbSZoiaQ6pkC1mUt4UEcsiYj4drwEMp+Nn8DRpJn1FzrE0MzNrLM8Kb03zgNEVtvdpnqWkYp7lodVPA9LoZ2eTcSrNJLsCOCAiZuXH9yMqtBuW77tnpJmZmfUDj1i2pnbJs7wHGJM/H0oKPS/3duAZSavTefEKcBcwJv8MNiO9j2pmZmZ9wCOWLaiN8iyPI80Q/ybpncsjKhzzHVIW5ZPAHDovdm8E9srHPkx6HcDMzMz6gHMs20R/5Fp2Nc+ycN54upBTKemUiDi9k2M2B86LiEqvCHTKOZZmZmb1cY5lm+uPXMtinqWk3h75PqWzAyLi6e4WlWZmZtYYLizbQ5/nWgKDSYXl90mxRo9ImlDIsSzlWlbMs6xE0k2SHpA0T9IxedsZwFr5mldJOlPSsYVzxkv6hqSBkubmbQPzTPIZ+atq5JCZmZk1jt+xbA/15FpuDNwv6a46rrcoIoblAu6EiDhK0kUUHl9LOpKOXMs3Jb0ILI6IoZL2Ab4YEQd2sR9fiIh/Slort/WGiDhJ0lfyqj1I+gDpkf8F+ZzPAB9n+X8kPQfsHRFLJW0F/BJYYcg+F6/HAAwYsEI2u5mZmXWRRyzbWzPnWlZynKRZwDTgPcBW5QdExIPAppI2l7Qj8EJE/LXssNWBS3P25XXAkEo3c46lmZlZY3nEsj20Yq7l8g1Nk4NGArtGxL8kTa7QrpLrSf39N+CaCvvHAv8gjdSuQpo1b2ZmZr3MI5btoR1yLdcnjT7+S9Jg4EOFfa/nHMuSa0j5l6NJRWalaz0TEcuAzwOrdrEtZmZm1g0uLNtAXh5xFLC3pMckzQPGk5ZLnE3KtfwjOdcyIv4GlHItr6L+XMtRhck7lUwk5WjW8xj825L+XvoCfg+sJmk2aULQtMKxlwCzJV2V+zuPVOQ+FRHPVLj2BcBhkqaR3gN9ucIxZmZm1mDOsexD/ZE12YBrzgLmR8QhdRzbaa5lnn2+c0R8pQtt+B3w2Yh4UdI9EdHwWd7OsTQzM6uPcyybQH9kTZbdv8vv00rahvTfyHBJ63Ry7Fu5ljWO6dY7vRHxHxHxYv7s6CAzM7Mm5cKy7/R51qSkKySdLWkSHVmTm+RrrCLpUUkb12jzZ4GfA7cB++XzNi9kVc6U9KakLYCfAtOBcyTdL2l3SeMkPStpkaSXSMs27gu8R9LvJT0k6dRCH1fIsSz0d+P8eUn+c11JdxR+Bvvn7QMl/VnSpfk6t+X4IjMzM+tlnhXed5ola/JQ0uP4kcCsiFhU4x4HA3sDWwNfIUUXPZ3bi6QvA3tGxJOSriY9Bp8qaQBwa0RskyfdfArYIyJeycXxD/LP41+5vzdHxHQq51g+X6VtS4FREfFSLjqnSZqY920FHBIRRyutkX4gaVLRcpxjaWZm1lgesex/TZk1mWeVL4yIJ4E7gGGSNizs3x04Kl8HUqF6vqSZpEk860kqzSKfGBGvFC7/h4h4Pm/7NelnAHXkWBabCJyeJ/vcDryLjtcKnsijwVDj5+McSzMzs8byiGXfabWsyUOAwZIW5O/XI438XSZpM9Kj7/0iYknevwopg7JYQJJeLV1hVnb5jLHoYo4lue2bADtFxOu5naXjXy0c9ybgR+FmZmZ9wCOWfadlsiYlrQIcBOwQEQMjYiCwP3BIfrT9K+BbZbPZbyM9Li9dY2iNNuwtaaP8yPsA4G5q51hWsj7wXC4qPwJs0cnxZmZm1stcWPaRFsuaHE7KiHyqsO0u0tKIu5Ee1Z9WmMCzOXAcsLOk2ZLmkyYSVTOVNCloJnBDfr+yVo5lUWm086p8v+mk0cu/1LifmZmZ9QHnWPYj9UOuperImqxyrfHA0aSZ3WsCk4Av59Vtqp1zOHBbnvDTY5LeAcyIiIaPTjrH0szMrD5yjmXzkfo+17KYNdnNTMlzImIoaeRye2DPTo4/HNi8G/dZQR4V/RPwo0Zcz8zMzBrPhWX/6fNcS2AwqbD8Ph25lhMKj7RfzeeP66TtbyONWr6Q7z9U0rT8GPxGSRtKGg3sDFyVr72WpDMkzc/H/Si/V/q4kg0kLZM0PF9ziqT3SfqgpHuAm4FFpHc5kXS4pF8r5WE+IumHhZ/NhZKmK+VYntbN34+ZmZl1kWeF959mybVcHBFDJe0DfDEiDqxxj7GSPkeaKHNLIdLnZ8BXI+JOSd8DTo2Ir0n6Sm7LdEkbkd4xHRwRIWmD3IaHSSOgW+afx4cl3Qu8OyIelbQeMDwi3pA0EjidNDud/HP6AOk1gock/Vd+N3VczsNcFbhD0g4RMbu8M3KOpZmZWUN5xLL5NGWuZVZ6FL4psI6kMXnG+gYRcWc+5krS5J9yL5FCzS+T9GlSODrAlHz8cFJw+h6k/t6f968PXCdpLnAOsG3hmndExOKIWArMp2Nm+GckzSBNeNqWVLiuwDmWZmZmjeXCsv/MA3aqsL1Pcy2BYq7lLbUaXDjvddIs7koFZLVz3gA+SHoUf0A+H1Jh+eG873fABqR3Q0ujtN8HJkXEdqQVfIr9Ls+rXE3SlsAJwEcjYgfSI/RaeZhmZmbWIC4s+0/L5FqWyxOPdgMei4jFwAuFeKPPk0ZZl7u/pHWB9SPid8DXyMtCAvfmay3LI48zgS+SCk5II5al2KPD62jeeqTiebGkdwKfqKdPZmZm1nN+x7Kf5PcMRwHn5tnaS8lxQ6ScyVmkzMYTI+JZAKV1r2djE3hfAAAX1ElEQVQDj1B/ruX1kvYHvlrlmImkR+CdPQaHjncsV8/tuCBvPwy4SNLawOPAEXn7FXn7K6QC7zeS1iSNyo4FiIhXJf2NjtzKKaRVf+bk738IXCnp66RivKaImCXpQdKI8OOk8HUzMzPrA86xbCG9kXtZzLWslHvZg+uOpyP3smRERLxY4dgNgM9GxAXl+7pwv8uAsyNifnfOd46lmZlZfZxj2QZ6I/eymGuZN42gkHtZdmy3cy8LXysUldkGwLHduP5bIuKo7haVZmZm1hguLFtHw3Mvgc+QZmsvKuRefkfSKzkb8p+SnpP0OB25l5vka6wi6VFJG3elE5K2lXRfzracLWkr4AxgUN52Vs61rNanyZKul/QXSVflgpu8fef82TmWZmZm/cDvWLaO/si9vCJfc/9C7uWhpMfxI4FZEbGoxj1K72QCvBARHyEVrz+JiKskvQ1YFTgJ2C5HGSHpwBp9+gApQuhp0vuTu5PWHi9yjqWZmVk/8Ihl62v63Mv89ZG87U/AKZK+BWwREa9UOK9Wn+6LiL/nNcpnVmm7cyzNzMz6gQvL1tGyuZdFEXE1sB/wCnBrvla5an2CCtmVy53oHEszM7N+48KydbRs7mWRpPcCj0fEeaSoox0q3PcuKvepHs6xNDMz6yd+x7JFtHjuZckBwMHA5yS9DjwLfC+/D3l3XrbxFuBEYNfyPkka3NkNnWNpZmbWf5xj2aR6I7Oy7Poj6EZmZTH3ssK+WcD8iDikEW3sYrv2A4ZExBndOd85lmZmZvWplWPpEcsmVMisvDIixuRtQ0mZlQ0pLEmZlUuAFQpLSavltb3Lt58EfIk0M7x83zakVyuGS1onIl6ucEzF6zZCREwkjaaamZlZP/E7ls2p4ZmVkmbkcwYXMivH5uzID0u6QtLZkiZRJbMSuCwitoiIqYV7jZM0E5gEvIM0Uebywv7Jkk6XdCdwfL7PhZImSXpc0p6SLpf05xxvVDpvH0l/yu2+Tmmt8Yr9ydsPl3R+/vwpSfdKelDS7fldSzMzM+tlLiybUz2ZlSNJBeBmdVxvUUQMAy4kZVYuAC6iIw5oSj7u/cDIiBhLmqBTGpmsmlkZERNy/uRLpPciDwHWKjtsg4jYMyJ+nL/fENiLtF74/wLnkGKBtpc0VCl0/du5LcOA6cDXq/WnQn+nAh+KiA8A15De2VyBpGNykPr0hQsXVjrEzMzMusCFZWtpyszKPDt9YUQ8CdwBDJO0YeGQa8tO+d9IL/fOAf4REXNyLuW83L4PkbIn786joYcBW3ShP+8mRRnNAb5JKlpX4BxLMzOzxnJh2ZxaLbPyEGCwpAXAY6TInwMrXbesPctYPpdyWW6fgD8UwtWHRMSRXejPfwHnR8T2wBdxjqWZmVmfcGHZnFoms1LSKsBBwA4RMTAiBgL7k4rN7poG7C7pffkea0t6fxfOXx94Kn8+rAftMDMzsy5wYdmE8mPiUcDekh6TNA8YD1xNyqWcRSo+T4yIZ/PoYimz8irqz6wcVZq8U+WYiaSMzFqZlcOBpyLiqcK2u0iFbj3vf64gIhYChwO/lDSbVGh2mmFZMB64TtIUoNZa5mZmZtZAzrFsQ43KwKyWWdndDMwq9xhPmlwzMCKey9uWRERpFvg9EbFbT+/TGedYmpmZ1adWjqVHLNtMIQNzckQMioghwCmkDMyuXOck4Abg5Aq7RwAViz1J3clGXQR8o9KORhWV3WyXmZmZdYELy/bTkAzMvIJNkB7HlzIjz5E0HxgHnC7pFUmX1JOBmSOEqrmc9O7oRuU7JC0pXOcCSfMk/VbS7ySNzvt2knSnpAck3Vp6BF+eodmTH6qZmZl1zqM47aeeDMyNgfsl3VXH9RZFxDBJxwLDImJIfny9JCJ+BJCDzUsZmG9KepGUgXkuNTIwC5aQisvjgVOrHPNpUrTQ9sCmwJ+ByyWtTpoFvn9ELMwF8wRSRBLkDM1KF5R0DHAMwIABAzr9QZiZmVltHrFceTRlBmbBecBhktarsn+PfI9lEfEsaaUfgK1JxfQfcublt0k5liXlGZpvcY6lmZlZY3nEsv3MA0ZX2N6nGZiSihmYK6wtXi4iXpR0NXBslUOqtV/AvIjYtbN2mZmZWe/yiGX7aZkMzArOJgWaVypgpwIH5nct30maQATwELCJpF0BJK0uqeJKO2ZmZta7XFi2mRbLwCxv+yLSjPY1Kuy+Afg7MBe4GLgXWBwRr5FGaM+UNAuYSZUZ62ZmZta7nGPZQ43KjOzkHiNoXG7k1qTCbANSATclIo5pwHVHACdExL6S9gP2BoaWZ2DmY38DbFrj8XW1e6xLKiL3IM1+3z2/b1na3+3MS+dYmpmZ1adWjqXfseyBQmbklRExJm8bSsqMbFhhSXrsuwRYobCUtFpEvNGFa51HCj3/TT5/+4a0cHlDgP2o8G6lpA2AYcASSVtGxBMVjqnWp98C7yWNhH69WFRC4zIvzczMrHv8KLxnKmZGRsQUJXXnRubPCySdVsiNHCxpIPCfwNjSo+ce5kZuRnqkXGrvnHzeQElT8r1nSNqtjvZ+XNJfJE0lxQGVPAv8b0RMLZw3Ls/ang2sRRoxvaiwv9inMyV9UNI9kh7Mf24dESOA7wJTgDGSHpJ0auEapczLdSXdUfg57l/tF2hmZmaN4xHLnqmWGQmNyY08ISKOknQRy+dGHkn3cyPPAf4o6R7gNuB/IuJF4Dlg74hYKmkr4JdAxWHu3IY1gUuBvYBHqRHrAxARE4AJkm4HTgP+AVxfdlixT+sBwyPiDUkjgdOBA/NxHyT97P9F+rneHBHF59hLgVER8VIusKdJmhhl7304x9LMzKyxPGLZe5oyNzIi/gfYBriO9Ih9mqQ1gNWBSyXNyfuGdNLOwcATEfFILth+0cnx5Nnc7wOm5ndQ35C0XZU+rQ9cJ2kuqRguzvT+Q0Q8HxGvkH5ee5TfirQy0GzgduBdVFjS0jmWZmZmjeXCsmfmATtV2denuZFAMTfylhrnERFPR8TlEbF/bs92wFjSKOKOpJHKt9XR3q7O/DoY2BB4QtICUuE8plKfgO8DkyJiO+BTndy3/PtDgU2AnSJiKKlf5T9nMzMzazAXlj1TMTNS0p7AXTRhbmR+L3L1/PnfgHcAT5FGCJ+JiGXA54FV8ynV2vsXYEtJg/L3h9TRj0OAj0fEwIgYSCrKx1Q5dv3cLoDDy/btLWkjSWsBBwB3Vzj3uYh4XdJHgC3qaJuZmZn1kAvLHqiRGfk0abZ4M+ZG7gPMzZmPtwLfzLOrLyAtqTiN9K7jy7mPFdsbEUtJ7yfenCfvPFnrpnkS0gBgWmlbnhH+kqR/r3DKD4EfSLqbjiK3ZCrwc1Jm5Q1l71eS27mzpOmk0cu/1GqbmZmZNYZzLNuEpJ2B80k5mr2SqdngPM3xwInAwIh4Lm9bEhHr9vTaFe7z1sSnapxjaWZmVp9aOZYesWwDkk4irUyzLjA5IgZFxBDgFCpMWumBEVRZ1UZSdxIGFgHf6EmDzMzMrHm4sGwDEXEGcATwz1KmpqRxwBXAf0l6TtIrkp5tojxNSLPZD5a0UfkOSZ+TdF++18WSVs3bl0j6cW7bHYX7HS3pfkmzJN0gae0e/VDNzMysy1xYto/lMjUjYkKeEf190nue65JmfJ8labM6rrcoIoYBF5LyNBeQAs3PiYihETElH1fKnhxLmjxUWm2nszxNSKsJXQ4cX9woaRvSDPLdcx/eLFx3HWBGbtudQCkg/dcRsUtE7Aj8GTiysw5KOkbSdEnTFy5c2NnhZmZm1gkXlu2vKfM0C84jTRpar7Dto6QZ4/fn1Xo+SlrKEWAZHWHsv6Ajw3I7pZWD5pCK0GLuZUXOsTQzM2ssr7zTPuYBoyts79M8TUnFPM0V1govFxEvSroaOLaszVdGxMmdnU9HhuUVwAERMSs/0h9Rx7lmZmbWQB6xbB8VMzWBF2jCPM0yZwNfpKOAvQMYLWnT3I+NJJWyKFeho4D+LCl6iNyuZ3JGZ6cFrZmZmTWeC8s2USNT82qaM0+z2PZFpNzPNfL384FvA7flZRn/AJTeC30Z2FbSA6R1yr+Xt38HuDcf69xKMzOzfuAcyxaRV8k5lybPqMx5mjeQRh8Xkh6xTwK+nFf1qXbeeOrIm+yNrEtwjqWZmVm9nGPZ4iSJNKLX1BmVhTzNO8izx4EhwPbAno1pZtfaZGZmZn3HhWVr+AjweimjEiAiZgJTJZ0laW7Om+zXjMqIOCMitgD+Wtj8HWAYcFG+9nxJD0t6IM/iHlze2WqZlJKuAC7JbTpT0nhJJxTOmytpoKR1JN2cz59b+rmYmZlZ73Jh2RqWy6gs+DQwlJRPOZLmyqgcm6OCvgbcFBFb5xHMZ4BPRsROwAmkNcrL1cqkLLWp1oo9HweejogdI2I74PeVDnKOpZmZWWO5sGxtzZxRWXoUvimwjqQxktYlPW6/LhedF9MxKaeoViZlsU3VzAFGSjpT0ocjYnGlg5xjaWZm1lguLFvDPFJgeLk+zagEihmVt9RqcOG810kjhsNzm17Mo6Klr20qnHYF8JWI2B44raz9Lxc+V+xnntC0E6nA/IGk79bTVjMzM+sZF5atoWUzKvPEo92AxyLiJeAJSQeV9knascJp9WZSLiC9v4mkYcCW+fPmwL8i4hfAj0rHmJmZWe9yYdkCWjSjsvSO5VzSqGjpXcpDgSMlzSKNxO5f4dx6MylvADbK9/kSUIpe2h64L28fB/z/dbTXzMzMesg5li2kv7Msc0blORFRrfAsHjseOJqUZQnw+4g4SdJlwNk5BL3WuZ1mWtYjzyT/bURcX+s451iamZnVp1aOpbMAW0Qhy/LKiBiTtw0lZVk2pLAkZVkuAVYoLCWdQlp2sSvLJZ5TXhxGxFE9aaCZmZk1Lz8Kbx39nWW5CfAa8FC+xiqSns/nzyx8javVCUmT88gnkpZImpDzJqdJWiHwvVampaTzJN0j6XFJo/N25b7Ol3QzaVa6mZmZ9QEXlq2jGbMsJ0fE9mWzvCcU7jG2UHB+rEIb1gGm5bzKu0iPzsvVyrTcjBS5tC9wRt42Ctia9J7l0VRZTQicY2lmZtZoLixbX9NnWeavWyvsfw0ojapWa0etTMubImJZfl+zNNo5nI6fx9OkSU0VOcfSzMyssVxYto6WzbKs4fXomD1WrR1XUD3T8tXC5+LPwTPSzMzM+oELy9bRslmWPVRvpmXJXcCY/PPYjPRuqpmZmfUBzwpvERERkkYB50o6CVhKjhsiZUvOIo3UnRgRzwJIKmVZPkL9WZbXS9of+GqVYyaSHoHXk2XZCKVMyydJK+l0VvjeCOyVj32Y9GqAmZmZ9QHnWLaI/s6wLBzXaZZlzqE8ERgYEc/lbUsiYt1GtLU3OMfSzMysPrVyLP0ovAUUMiwnR8SgiBgCnELHhJVGGEGVGdSSVst/nkRa7ebkOq63CPhGdxqSI4P836aZmVmL8f+8W0N/Z1ieJekR4KcRsQVwj6RHJW0saVxZjuVM4MOkGeQHS9qovDOSvp7bPFfS1/K2gZL+LOkCYAbweUln533HS3o8fx4kaWr+/N2ccTlX0iW5IB0kaUbhXltJqhTTZGZmZg3mwrI1NGOG5ayIWBQRE8pyLIcCU0gr+FwOHF+8saSdgCNIs8o/BBwt6QN599bAzyLiA8CtpAKV/Ofzkt5Filcqte/8nHG5HbAWsG9EPAYsVlqViHyvKyr9EJxjaWZm1lguLFtbM2dYApwHHCZpvbI23xgRL0fEktyWUgH5ZERMA8gTkNaV9HbgPcDVpBnvH6ajsPyIpHtzxuVedGRcXgYcIWlV4OB87gqcY2lmZtZYLixbQ0tmWEbEi6Si7tg62rzc/bI/kUYcHyIVkx8GdgXulrQmcAEwOmdcXkpHP28APkFakeeBiHi+s7aamZlZz7mwbA2tnGF5NvBFOgrYu4ADJK0taR3SEoxTqpx7F3BC/vNB0rumr0bEYjqKyEWS1gVGl06KiKWkR+kX0nexSGZmZis951i2gFbOsIyIRZJuBMbm72dIuoJUAANcFhEP5glE5aaQHoPfFRFvSvob8Jd8nRclXUrKq1wA3F927lWkd1Bvq6edDzzwwBJJD9XbrzawMWnm/spkZeuz+9v+VrY+u7/NY4tqO5xjaXWrJ8OyWUg6AVg/Ir5T5/HTq2VytaOVrb+w8vXZ/W1/K1uf3d/W4BFLq0seKf0S9S2r2K/yCOkg0oQeMzMz6yMuLK0uEXEGcEZxm6RxwEFlh14XERP6rGEVRMSo/ry/mZnZysqFpXVbLiD7tYhsoEv6uwF9bGXrL6x8fXZ/29/K1mf3twX4HUszMzMzawjHDZmZmZlZQ7iwtLYn6eOSHsrrm59UYf8akq7N++8tRh9JOjlvf0jSx/qy3d3V3f7m9dpfKaz7flH5uc2ojv4OlzRD0huSRpftO0zSI/nrsL5rdff1sL9vFn6/E/uu1T1TR5+/Lmm+pNmS7pC0RWFfO/6Oa/W3XX/H/ylpTu7XVElDCvva8e/piv1tib+nI8Jf/mrbL2BV4DHgvcDbSJmfQ8qOORa4KH8eA1ybPw/Jx68BbJmvs2p/96kX+zsQmNvffeiF/g4EdgB+RlqpqbR9I+Dx/OeG+fOG/d2n3upv3rekv/vQS33+CLB2/vylwn/T7fo7rtjfNv8dr1f4vB/w+/y5Xf+ertbfpv972iOW1u4+CDwaEY9HxGvANcD+ZcfsD1yZP18PfFSS8vZrIuLViHgCeDRfr5n1pL+tqNP+RsSCiJgNLCs792PAHyLinxHxAvAH4ON90ege6El/W1U9fZ4UEf/K304D3p0/t+vvuFp/W1U9fX6p8O06pEVBoE3/nq7R36bnwtLa3buAvxW+/3veVvGYiHgDWAy8o85zm01P+guwpaQHJd0pqemD8OnZ76hdf7+1rClpuqRpkg5obNN6TVf7fCRwSzfPbQY96S+08e9Y0pclPQb8EDiuK+c2mZ70F5r872nHDVm7qzQSV/4vv2rH1HNus+lJf58BBkTE85J2Am6StG3Zv5ybTU9+R+36+61lQEQ8Lem9wB8lzYmIxxrUtt5Sd58lfQ7YGdizq+c2kZ70F9r4dxwR/w38t6TPAt8GDqv33CbTk/42/d/THrG0dvd30nrjJe8Gnq52jKTVgPWBf9Z5brPpdn/zo6TnASLiAdI7QO/v9Rb3TE9+R+36+60qIp7Ofz4OTAY+0MjG9ZK6+ixpJDAO2C8iXu3KuU2mJ/1t699xwTVAaTS2bX/HBW/1txX+nnZhae3ufmArSVtKehtpskr5TMmJpH8JAowG/hjpLemJwBilWdRbAlsB9/VRu7ur2/2VtImkVQHyaMdWpMkOzaye/lZzK7CPpA0lbQjsk7c1s273N/dzjfx5Y2B3YH6vtbRxOu2zpA8AF5OKrOcKu9ryd1ytv23+O96q8O0ngUfy57b8e7paf1vi7+n+nj3kL3/19hfwH8DDpH/Zjcvbvkf6SxlgTeA60kvf9wHvLZw7Lp/3EPCJ/u5Lb/YXOBCYR5qhOAP4VH/3pUH93YU0QvAy8Dwwr3DuF/LP4VHgiP7uS2/2F9gNmJN/v3OAI/u7Lw3s8+3AP4CZ+Wtim/+OK/a3zX/HP8l/P80EJgHbFs5tx7+nK/a3Ff6e9so7ZmZmZtYQfhRuZmZmZg3hwtLMzMzMGsKFpZmZmZk1hAtLMzMzM2sIF5ZmZmZm1hAuLM3MrF9Iuqe/22BmjeW4ITMzMzNrCK8VbmZm/ULSkohYV9II4DRS6PdQ4NekgO/jgbWAAyLiMUlXAEuBbYF3Al+PiN/2R9vNrDIXlmZm1gx2BLYB/klaou6yiPigpOOBrwJfy8cNBPYEBgGTJL0vIpb2Q3vNrAK/Y2lmZs3g/oh4JiJeJS1zd1vePodUTJb8KiKWRcQjpAJ0cN8208xqcWFpZmbN4NXC52WF75ex/NO18okBnihg1kRcWJqZWSs5SNIqkgYB7wUe6u8GmVkHv2NpZmat5CHgTtLknf/0+5VmzcVxQ2Zm1hLyrPDfRsT1/d0WM6vMj8LNzMzMrCE8YmlmZmZmDeERSzMzMzNrCBeWZmZmZtYQLizNzMzMrCFcWJqZmZlZQ7iwNDMzM7OGcGFpZmZmZg3x/wDg6RaKQl7DwQAAAABJRU5ErkJggg==\n",
      "text/plain": [
       "<Figure size 595.44x1202.4 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "a4_dims = (8.27,16.7)\n",
    "\n",
    "fig, ax = plt.subplots(figsize=a4_dims)\n",
    "df=pd.DataFrame.from_dict(varimp)\n",
    "df.sort_values(ascending=False,by=[\"imp\"],inplace=True)\n",
    "df=df.dropna()\n",
    "sns.barplot(x=\"imp\",y=\"names\",palette=\"vlag\",data=df,orient=\"h\",ax=ax);"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Getting only top 7 of features importance in the model:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 89,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 1202.4x595.44 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "#7 most important factors that affect crops \n",
    "a4_dims = (16.7, 8.27)\n",
    "\n",
    "fig, ax = plt.subplots(figsize=a4_dims)\n",
    "df=pd.DataFrame.from_dict(varimp)\n",
    "df.sort_values(ascending=False,by=[\"imp\"],inplace=True)\n",
    "df=df.dropna()\n",
    "df=df.nlargest(7, 'imp')\n",
    "sns.barplot(x=\"imp\",y=\"names\",palette=\"vlag\",data=df,orient=\"h\",ax=ax);"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "The crop being potatoes has the highest importance in the decision making for the model, where it's the highest crops in the dataset. Cassava too, then as expected we see the effect of pesticides, where its the third most important feature, and then if the crop is sweet potatoes, we see some of the highest crops in features importance in dataset. \n",
    "\n",
    "If the crop is grown in India, makes sense since Indis has the largest crops sum in the dataset. Then comes rainfall and temprature. Thr first assumption about these features were correct, where they all significanally impact the expected crops yield in the model. "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 90,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 1202.4x595.44 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "#Boxplot that shows yield for each item \n",
    "a4_dims = (16.7, 8.27)\n",
    "\n",
    "fig, ax = plt.subplots(figsize=a4_dims)\n",
    "sns.boxplot(x=\"Item\",y=\"hg/ha_yield\",palette=\"vlag\",data=yield_df,ax=ax);"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 83,
   "metadata": {},
   "outputs": [],
   "source": [
    "import os\n",
    "os.environ[\"PATH\"] += os.pathsep + 'C:/Program Files (x86)/Graphviz2.38/bin/'"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 84,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "C:\\Users\\hajiralmahdi\\AppData\\Local\\Continuum\\anaconda3\\lib\\site-packages\\sklearn\\externals\\six.py:31: DeprecationWarning: The module is deprecated in version 0.21 and will be removed in version 0.23 since we've dropped support for Python 2.7. Please rely on the official version of six (https://pypi.org/project/six/).\n",
      "  \"(https://pypi.org/project/six/).\", DeprecationWarning)\n"
     ]
    },
    {
     "data": {
      "text/plain": [
       "True"
      ]
     },
     "execution_count": 84,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "from sklearn.externals.six import StringIO  \n",
    "from IPython.display import Image  \n",
    "from sklearn.tree import export_graphviz\n",
    "import pydotplus\n",
    "import collections\n",
    "dot_data = export_graphviz(model, out_file=None, max_depth=5,\n",
    "                                feature_names=yield_df_onehot.columns[yield_df_onehot.columns!=\"hg/ha_yield\"])\n",
    "\n",
    "# Draw graph\n",
    "graph = pydotplus.graph_from_dot_data(dot_data)  \n",
    "\n",
    "\n",
    "# Show graph\n",
    "graph.write_pdf(\"model_5_depth.png\")"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 85,
   "metadata": {},
   "outputs": [],
   "source": [
    "data_max=yield_df_onehot.loc[:, yield_df_onehot.columns != 'hg/ha_yield'].max()\n",
    "data_min=yield_df_onehot.loc[:, yield_df_onehot.columns != 'hg/ha_yield'].min()\n",
    "\n",
    "import pickle\n",
    "filename = 'yield_model.sav'\n",
    "pickle.dump(model, open(filename, 'wb'))\n",
    "\n",
    "pickle.dump(data_max, open('max.data', 'wb'))\n",
    "pickle.dump(data_min, open('min.data', 'wb'))"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "References\n",
    "https://towardsdatascience.com/the-mathematics-of-decision-trees-random-forest-and-feature-importance-in-scikit-learn-and-spark-f2861df67e3\n",
    "\n",
    "https://gdcoder.com/decision-tree-regressor-explained-in-depth/\n",
    "\n",
    "http://www.fao.org/home/en/\n",
    "\n",
    "https://data.worldbank.org/\n",
    "\n",
    "https://chrisalbon.com/machine_learning/trees_and_forests/decision_tree_regression/\n",
    "\n"
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.7.3"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 2
}
