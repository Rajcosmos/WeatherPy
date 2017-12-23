

```python
#Dependencies
import json
import pandas as pd
import requests as req
import matplotlib.pyplot as plt
from citipy import citipy
import numpy as np
import time
import datetime
## Installed citipy library
##pip install citipy 
```


```python
### Generate cities list 
## Tried changing longitude range to get different results
lats= np.random.uniform(-90,90,550)
lngs=np.random.uniform(-180,180,550)
city_cordinates=dict(zip(lats,lngs))
```


```python
city_list=[]
city_lat=[]
city_lng=[]
for key,value in city_cordinates.items():
         city=citipy.nearest_city(key,value)
         city_list.append(city.city_name)
         city_lat.append(key)
         city_lng.append(value)
```


```python
## Rounding 
city_lat=[int(round(n,0)) for n in city_lat]
city_lng=[int(round(n,0))for n in city_lng]
```


```python
city_pd=pd.DataFrame({"city":city_list,
                      "lats":city_lat,
                       "lngs":city_lng})
city_pd
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>lats</th>
      <th>lngs</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>hermanus</td>
      <td>-73</td>
      <td>-5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>dawei</td>
      <td>14</td>
      <td>97</td>
    </tr>
    <tr>
      <th>2</th>
      <td>busselton</td>
      <td>-56</td>
      <td>88</td>
    </tr>
    <tr>
      <th>3</th>
      <td>vaitupu</td>
      <td>8</td>
      <td>-179</td>
    </tr>
    <tr>
      <th>4</th>
      <td>san juan</td>
      <td>20</td>
      <td>-66</td>
    </tr>
    <tr>
      <th>5</th>
      <td>leskovik</td>
      <td>40</td>
      <td>21</td>
    </tr>
    <tr>
      <th>6</th>
      <td>longyearbyen</td>
      <td>81</td>
      <td>17</td>
    </tr>
    <tr>
      <th>7</th>
      <td>verkhneuralsk</td>
      <td>54</td>
      <td>59</td>
    </tr>
    <tr>
      <th>8</th>
      <td>quatre cocos</td>
      <td>-16</td>
      <td>71</td>
    </tr>
    <tr>
      <th>9</th>
      <td>bambous virieux</td>
      <td>-42</td>
      <td>83</td>
    </tr>
    <tr>
      <th>10</th>
      <td>savannah bight</td>
      <td>18</td>
      <td>-85</td>
    </tr>
    <tr>
      <th>11</th>
      <td>new norfolk</td>
      <td>-70</td>
      <td>127</td>
    </tr>
    <tr>
      <th>12</th>
      <td>port alfred</td>
      <td>-73</td>
      <td>42</td>
    </tr>
    <tr>
      <th>13</th>
      <td>marawi</td>
      <td>18</td>
      <td>30</td>
    </tr>
    <tr>
      <th>14</th>
      <td>dikson</td>
      <td>90</td>
      <td>69</td>
    </tr>
    <tr>
      <th>15</th>
      <td>san cristobal</td>
      <td>-4</td>
      <td>-88</td>
    </tr>
    <tr>
      <th>16</th>
      <td>jamestown</td>
      <td>-41</td>
      <td>-8</td>
    </tr>
    <tr>
      <th>17</th>
      <td>trelew</td>
      <td>-42</td>
      <td>-67</td>
    </tr>
    <tr>
      <th>18</th>
      <td>ushuaia</td>
      <td>-75</td>
      <td>-62</td>
    </tr>
    <tr>
      <th>19</th>
      <td>naruto</td>
      <td>34</td>
      <td>135</td>
    </tr>
    <tr>
      <th>20</th>
      <td>hirata</td>
      <td>35</td>
      <td>133</td>
    </tr>
    <tr>
      <th>21</th>
      <td>evensk</td>
      <td>61</td>
      <td>158</td>
    </tr>
    <tr>
      <th>22</th>
      <td>jamestown</td>
      <td>-50</td>
      <td>-14</td>
    </tr>
    <tr>
      <th>23</th>
      <td>ushuaia</td>
      <td>-80</td>
      <td>-50</td>
    </tr>
    <tr>
      <th>24</th>
      <td>riyadh</td>
      <td>21</td>
      <td>48</td>
    </tr>
    <tr>
      <th>25</th>
      <td>ushuaia</td>
      <td>-79</td>
      <td>-80</td>
    </tr>
    <tr>
      <th>26</th>
      <td>airai</td>
      <td>19</td>
      <td>143</td>
    </tr>
    <tr>
      <th>27</th>
      <td>maceio</td>
      <td>-16</td>
      <td>-30</td>
    </tr>
    <tr>
      <th>28</th>
      <td>busselton</td>
      <td>-45</td>
      <td>92</td>
    </tr>
    <tr>
      <th>29</th>
      <td>penzance</td>
      <td>51</td>
      <td>-5</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>520</th>
      <td>la primavera</td>
      <td>5</td>
      <td>-70</td>
    </tr>
    <tr>
      <th>521</th>
      <td>bluff</td>
      <td>-72</td>
      <td>164</td>
    </tr>
    <tr>
      <th>522</th>
      <td>cape town</td>
      <td>-56</td>
      <td>4</td>
    </tr>
    <tr>
      <th>523</th>
      <td>lavrentiya</td>
      <td>73</td>
      <td>-172</td>
    </tr>
    <tr>
      <th>524</th>
      <td>bluff</td>
      <td>-70</td>
      <td>170</td>
    </tr>
    <tr>
      <th>525</th>
      <td>nicosia</td>
      <td>38</td>
      <td>14</td>
    </tr>
    <tr>
      <th>526</th>
      <td>loandjili</td>
      <td>-5</td>
      <td>11</td>
    </tr>
    <tr>
      <th>527</th>
      <td>ushuaia</td>
      <td>-78</td>
      <td>-30</td>
    </tr>
    <tr>
      <th>528</th>
      <td>castro</td>
      <td>-50</td>
      <td>-97</td>
    </tr>
    <tr>
      <th>529</th>
      <td>punta arenas</td>
      <td>-64</td>
      <td>-96</td>
    </tr>
    <tr>
      <th>530</th>
      <td>kozhva</td>
      <td>66</td>
      <td>56</td>
    </tr>
    <tr>
      <th>531</th>
      <td>punta arenas</td>
      <td>-53</td>
      <td>-80</td>
    </tr>
    <tr>
      <th>532</th>
      <td>bredasdorp</td>
      <td>-51</td>
      <td>17</td>
    </tr>
    <tr>
      <th>533</th>
      <td>palmer</td>
      <td>60</td>
      <td>-147</td>
    </tr>
    <tr>
      <th>534</th>
      <td>bambous virieux</td>
      <td>-31</td>
      <td>78</td>
    </tr>
    <tr>
      <th>535</th>
      <td>bluff</td>
      <td>-78</td>
      <td>173</td>
    </tr>
    <tr>
      <th>536</th>
      <td>paso de los toros</td>
      <td>-33</td>
      <td>-56</td>
    </tr>
    <tr>
      <th>537</th>
      <td>hithadhoo</td>
      <td>-4</td>
      <td>69</td>
    </tr>
    <tr>
      <th>538</th>
      <td>tasiilaq</td>
      <td>70</td>
      <td>-39</td>
    </tr>
    <tr>
      <th>539</th>
      <td>east london</td>
      <td>-55</td>
      <td>48</td>
    </tr>
    <tr>
      <th>540</th>
      <td>buraydah</td>
      <td>28</td>
      <td>43</td>
    </tr>
    <tr>
      <th>541</th>
      <td>tyukalinsk</td>
      <td>56</td>
      <td>73</td>
    </tr>
    <tr>
      <th>542</th>
      <td>marawi</td>
      <td>22</td>
      <td>25</td>
    </tr>
    <tr>
      <th>543</th>
      <td>geraldton</td>
      <td>52</td>
      <td>-87</td>
    </tr>
    <tr>
      <th>544</th>
      <td>pierre</td>
      <td>43</td>
      <td>-100</td>
    </tr>
    <tr>
      <th>545</th>
      <td>amderma</td>
      <td>78</td>
      <td>67</td>
    </tr>
    <tr>
      <th>546</th>
      <td>kovdor</td>
      <td>68</td>
      <td>31</td>
    </tr>
    <tr>
      <th>547</th>
      <td>butaritari</td>
      <td>17</td>
      <td>180</td>
    </tr>
    <tr>
      <th>548</th>
      <td>tarakan</td>
      <td>2</td>
      <td>117</td>
    </tr>
    <tr>
      <th>549</th>
      <td>tasiilaq</td>
      <td>80</td>
      <td>-37</td>
    </tr>
  </tbody>
</table>
<p>550 rows × 3 columns</p>
</div>




```python
# Dropping duplicates
city_pd=city_pd.drop_duplicates()
len(city_pd)
```




    549




```python
# Randomly select 500 cities
selected_cities = city_pd.sample(n=510)

# Visualize
selected_cities
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>lats</th>
      <th>lngs</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>128</th>
      <td>ribeira grande</td>
      <td>33</td>
      <td>-32</td>
    </tr>
    <tr>
      <th>185</th>
      <td>leningradskiy</td>
      <td>81</td>
      <td>177</td>
    </tr>
    <tr>
      <th>75</th>
      <td>khatanga</td>
      <td>69</td>
      <td>99</td>
    </tr>
    <tr>
      <th>179</th>
      <td>half moon bay</td>
      <td>35</td>
      <td>-129</td>
    </tr>
    <tr>
      <th>264</th>
      <td>qaanaaq</td>
      <td>78</td>
      <td>-84</td>
    </tr>
    <tr>
      <th>299</th>
      <td>ushuaia</td>
      <td>-80</td>
      <td>-35</td>
    </tr>
    <tr>
      <th>28</th>
      <td>busselton</td>
      <td>-45</td>
      <td>92</td>
    </tr>
    <tr>
      <th>296</th>
      <td>tukrah</td>
      <td>34</td>
      <td>21</td>
    </tr>
    <tr>
      <th>503</th>
      <td>nikolskoye</td>
      <td>48</td>
      <td>165</td>
    </tr>
    <tr>
      <th>448</th>
      <td>port alfred</td>
      <td>-67</td>
      <td>41</td>
    </tr>
    <tr>
      <th>98</th>
      <td>hermanus</td>
      <td>-80</td>
      <td>-4</td>
    </tr>
    <tr>
      <th>261</th>
      <td>auki</td>
      <td>-6</td>
      <td>163</td>
    </tr>
    <tr>
      <th>318</th>
      <td>los llanos de aridane</td>
      <td>26</td>
      <td>-20</td>
    </tr>
    <tr>
      <th>2</th>
      <td>busselton</td>
      <td>-56</td>
      <td>88</td>
    </tr>
    <tr>
      <th>537</th>
      <td>hithadhoo</td>
      <td>-4</td>
      <td>69</td>
    </tr>
    <tr>
      <th>352</th>
      <td>geraldton</td>
      <td>50</td>
      <td>-89</td>
    </tr>
    <tr>
      <th>469</th>
      <td>honiara</td>
      <td>-10</td>
      <td>158</td>
    </tr>
    <tr>
      <th>392</th>
      <td>lewiston</td>
      <td>46</td>
      <td>-117</td>
    </tr>
    <tr>
      <th>176</th>
      <td>airai</td>
      <td>14</td>
      <td>144</td>
    </tr>
    <tr>
      <th>443</th>
      <td>novyy urengoy</td>
      <td>68</td>
      <td>77</td>
    </tr>
    <tr>
      <th>271</th>
      <td>kupang</td>
      <td>-13</td>
      <td>122</td>
    </tr>
    <tr>
      <th>199</th>
      <td>albany</td>
      <td>-83</td>
      <td>94</td>
    </tr>
    <tr>
      <th>518</th>
      <td>chokurdakh</td>
      <td>86</td>
      <td>153</td>
    </tr>
    <tr>
      <th>540</th>
      <td>buraydah</td>
      <td>28</td>
      <td>43</td>
    </tr>
    <tr>
      <th>480</th>
      <td>iki-burul</td>
      <td>45</td>
      <td>45</td>
    </tr>
    <tr>
      <th>453</th>
      <td>vaini</td>
      <td>-87</td>
      <td>-171</td>
    </tr>
    <tr>
      <th>76</th>
      <td>hobart</td>
      <td>-87</td>
      <td>145</td>
    </tr>
    <tr>
      <th>96</th>
      <td>benguela</td>
      <td>-13</td>
      <td>11</td>
    </tr>
    <tr>
      <th>238</th>
      <td>west linton</td>
      <td>56</td>
      <td>-3</td>
    </tr>
    <tr>
      <th>60</th>
      <td>manaus</td>
      <td>-3</td>
      <td>-60</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>485</th>
      <td>port elizabeth</td>
      <td>-89</td>
      <td>37</td>
    </tr>
    <tr>
      <th>431</th>
      <td>guajara-mirim</td>
      <td>-10</td>
      <td>-64</td>
    </tr>
    <tr>
      <th>196</th>
      <td>luderitz</td>
      <td>-29</td>
      <td>1</td>
    </tr>
    <tr>
      <th>504</th>
      <td>denpasar</td>
      <td>-14</td>
      <td>113</td>
    </tr>
    <tr>
      <th>506</th>
      <td>ushuaia</td>
      <td>-72</td>
      <td>-70</td>
    </tr>
    <tr>
      <th>165</th>
      <td>punta arenas</td>
      <td>-59</td>
      <td>-77</td>
    </tr>
    <tr>
      <th>89</th>
      <td>saint-philippe</td>
      <td>-53</td>
      <td>67</td>
    </tr>
    <tr>
      <th>418</th>
      <td>barrow</td>
      <td>78</td>
      <td>-154</td>
    </tr>
    <tr>
      <th>446</th>
      <td>georgetown</td>
      <td>-2</td>
      <td>-12</td>
    </tr>
    <tr>
      <th>281</th>
      <td>kropotkin</td>
      <td>59</td>
      <td>115</td>
    </tr>
    <tr>
      <th>187</th>
      <td>claremore</td>
      <td>36</td>
      <td>-95</td>
    </tr>
    <tr>
      <th>322</th>
      <td>nadvoitsy</td>
      <td>64</td>
      <td>35</td>
    </tr>
    <tr>
      <th>251</th>
      <td>hobart</td>
      <td>-72</td>
      <td>145</td>
    </tr>
    <tr>
      <th>217</th>
      <td>malanje</td>
      <td>-10</td>
      <td>17</td>
    </tr>
    <tr>
      <th>219</th>
      <td>hamilton</td>
      <td>45</td>
      <td>-115</td>
    </tr>
    <tr>
      <th>252</th>
      <td>jamestown</td>
      <td>-28</td>
      <td>-19</td>
    </tr>
    <tr>
      <th>298</th>
      <td>harper</td>
      <td>5</td>
      <td>-8</td>
    </tr>
    <tr>
      <th>83</th>
      <td>taolanaro</td>
      <td>-27</td>
      <td>50</td>
    </tr>
    <tr>
      <th>457</th>
      <td>neiafu</td>
      <td>-18</td>
      <td>-174</td>
    </tr>
    <tr>
      <th>233</th>
      <td>itarema</td>
      <td>1</td>
      <td>-39</td>
    </tr>
    <tr>
      <th>507</th>
      <td>aklavik</td>
      <td>70</td>
      <td>-140</td>
    </tr>
    <tr>
      <th>56</th>
      <td>dikson</td>
      <td>84</td>
      <td>90</td>
    </tr>
    <tr>
      <th>22</th>
      <td>jamestown</td>
      <td>-50</td>
      <td>-14</td>
    </tr>
    <tr>
      <th>67</th>
      <td>carnarvon</td>
      <td>-26</td>
      <td>114</td>
    </tr>
    <tr>
      <th>317</th>
      <td>dingle</td>
      <td>53</td>
      <td>-14</td>
    </tr>
    <tr>
      <th>405</th>
      <td>busselton</td>
      <td>-87</td>
      <td>74</td>
    </tr>
    <tr>
      <th>366</th>
      <td>aloleng</td>
      <td>15</td>
      <td>116</td>
    </tr>
    <tr>
      <th>513</th>
      <td>hasaki</td>
      <td>22</td>
      <td>158</td>
    </tr>
    <tr>
      <th>139</th>
      <td>samusu</td>
      <td>-11</td>
      <td>-165</td>
    </tr>
    <tr>
      <th>476</th>
      <td>provideniya</td>
      <td>60</td>
      <td>-172</td>
    </tr>
  </tbody>
</table>
<p>510 rows × 3 columns</p>
</div>




```python
# Weather API Key
api_key = "62e6c158794571605e5f2b3046aa6eac"
```


```python
# Create blank columns for necessary fields
selected_cities["temp"] = ""
selected_cities["humidity%"] = ""
selected_cities["cloudiness%"] = ""
selected_cities["windspeed"] = ""

# Counter
row_count = 0

# Loop through and grab the lat/lng 

for index, row in selected_cities.iterrows():
   #target_url = "http://api.openweathermap.org/data/2.5/history?q=%s&units=IMPERIAL&mode=json&APPID=%s" %(selected_cities["city"],api_key)
   #target_url = "http://api.openweathermap.org/data/2.5/weather?lat=%s&lon=%s&units=IMPERIAL&mode=json&APPID=%s" %(row["lats"],row["lngs"],api_key)
    
    target_url = "http://api.openweathermap.org/data/2.5/weather?q=%s&units=IMPERIAL&mode=json&APPID=%s" %(row["city"],api_key)
  # Print log to ensure loop is working correctly
    print("Now retrieving city #"+ str(row_count)+" City Name"+row["city"])
    print(target_url)
    row_count+=1
    
    # Run requests to grab the JSON at the requested URL
    city_weather = req.get(target_url).json()
    # Append the lat/lng to the appropriate columns
    # Use try / except to skip any cities with errors
    try: 
        city_temp = city_weather["main"]["temp_max"]
        city_humidity=city_weather["main"]["humidity"]
        city_clouds=city_weather["clouds"]["all"]
        city_wind=city_weather["wind"]["speed"]
        
        selected_cities.set_value(index, "temp", city_temp)
        selected_cities.set_value(index, "humidity%", city_humidity)
        selected_cities.set_value(index, "cloudiness%", city_clouds)
        selected_cities.set_value(index, "windspeed", city_wind)
        
    except:
        print("Error with city data. Skipping")
        continue
```

    Now retrieving city #0 City Nameribeira grande
    http://api.openweathermap.org/data/2.5/weather?q=ribeira grande&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #1 City Nameleningradskiy
    http://api.openweathermap.org/data/2.5/weather?q=leningradskiy&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #2 City Namekhatanga
    http://api.openweathermap.org/data/2.5/weather?q=khatanga&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #3 City Namehalf moon bay
    http://api.openweathermap.org/data/2.5/weather?q=half moon bay&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #4 City Nameqaanaaq
    http://api.openweathermap.org/data/2.5/weather?q=qaanaaq&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #5 City Nameushuaia
    http://api.openweathermap.org/data/2.5/weather?q=ushuaia&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #6 City Namebusselton
    http://api.openweathermap.org/data/2.5/weather?q=busselton&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #7 City Nametukrah
    http://api.openweathermap.org/data/2.5/weather?q=tukrah&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #8 City Namenikolskoye
    http://api.openweathermap.org/data/2.5/weather?q=nikolskoye&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #9 City Nameport alfred
    http://api.openweathermap.org/data/2.5/weather?q=port alfred&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #10 City Namehermanus
    http://api.openweathermap.org/data/2.5/weather?q=hermanus&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #11 City Nameauki
    http://api.openweathermap.org/data/2.5/weather?q=auki&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #12 City Namelos llanos de aridane
    http://api.openweathermap.org/data/2.5/weather?q=los llanos de aridane&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #13 City Namebusselton
    http://api.openweathermap.org/data/2.5/weather?q=busselton&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #14 City Namehithadhoo
    http://api.openweathermap.org/data/2.5/weather?q=hithadhoo&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #15 City Namegeraldton
    http://api.openweathermap.org/data/2.5/weather?q=geraldton&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #16 City Namehoniara
    http://api.openweathermap.org/data/2.5/weather?q=honiara&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #17 City Namelewiston
    http://api.openweathermap.org/data/2.5/weather?q=lewiston&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #18 City Nameairai
    http://api.openweathermap.org/data/2.5/weather?q=airai&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #19 City Namenovyy urengoy
    http://api.openweathermap.org/data/2.5/weather?q=novyy urengoy&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #20 City Namekupang
    http://api.openweathermap.org/data/2.5/weather?q=kupang&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #21 City Namealbany
    http://api.openweathermap.org/data/2.5/weather?q=albany&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #22 City Namechokurdakh
    http://api.openweathermap.org/data/2.5/weather?q=chokurdakh&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #23 City Nameburaydah
    http://api.openweathermap.org/data/2.5/weather?q=buraydah&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #24 City Nameiki-burul
    http://api.openweathermap.org/data/2.5/weather?q=iki-burul&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #25 City Namevaini
    http://api.openweathermap.org/data/2.5/weather?q=vaini&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #26 City Namehobart
    http://api.openweathermap.org/data/2.5/weather?q=hobart&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #27 City Namebenguela
    http://api.openweathermap.org/data/2.5/weather?q=benguela&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #28 City Namewest linton
    http://api.openweathermap.org/data/2.5/weather?q=west linton&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #29 City Namemanaus
    http://api.openweathermap.org/data/2.5/weather?q=manaus&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #30 City Nameriyadh
    http://api.openweathermap.org/data/2.5/weather?q=riyadh&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #31 City Namehermanus
    http://api.openweathermap.org/data/2.5/weather?q=hermanus&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #32 City Namecastro
    http://api.openweathermap.org/data/2.5/weather?q=castro&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #33 City Namelebu
    http://api.openweathermap.org/data/2.5/weather?q=lebu&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #34 City Namebredasdorp
    http://api.openweathermap.org/data/2.5/weather?q=bredasdorp&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #35 City Namesan juan
    http://api.openweathermap.org/data/2.5/weather?q=san juan&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #36 City Nameushuaia
    http://api.openweathermap.org/data/2.5/weather?q=ushuaia&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #37 City Namehilo
    http://api.openweathermap.org/data/2.5/weather?q=hilo&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #38 City Namecape town
    http://api.openweathermap.org/data/2.5/weather?q=cape town&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #39 City Namerikitea
    http://api.openweathermap.org/data/2.5/weather?q=rikitea&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #40 City Namequatre cocos
    http://api.openweathermap.org/data/2.5/weather?q=quatre cocos&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #41 City Nameangoche
    http://api.openweathermap.org/data/2.5/weather?q=angoche&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #42 City Namechokurdakh
    http://api.openweathermap.org/data/2.5/weather?q=chokurdakh&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #43 City Nameribeira grande
    http://api.openweathermap.org/data/2.5/weather?q=ribeira grande&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #44 City Nametouros
    http://api.openweathermap.org/data/2.5/weather?q=touros&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #45 City Namecape town
    http://api.openweathermap.org/data/2.5/weather?q=cape town&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #46 City Namerio gallegos
    http://api.openweathermap.org/data/2.5/weather?q=rio gallegos&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #47 City Namefaanui
    http://api.openweathermap.org/data/2.5/weather?q=faanui&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #48 City Namebyron bay
    http://api.openweathermap.org/data/2.5/weather?q=byron bay&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #49 City Namethiers
    http://api.openweathermap.org/data/2.5/weather?q=thiers&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #50 City Namemeulaboh
    http://api.openweathermap.org/data/2.5/weather?q=meulaboh&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #51 City Namearraial do cabo
    http://api.openweathermap.org/data/2.5/weather?q=arraial do cabo&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #52 City Namehobart
    http://api.openweathermap.org/data/2.5/weather?q=hobart&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #53 City Nameleningradskiy
    http://api.openweathermap.org/data/2.5/weather?q=leningradskiy&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #54 City Nameport hawkesbury
    http://api.openweathermap.org/data/2.5/weather?q=port hawkesbury&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #55 City Namewindhoek
    http://api.openweathermap.org/data/2.5/weather?q=windhoek&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #56 City Namethompson
    http://api.openweathermap.org/data/2.5/weather?q=thompson&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #57 City Namemahebourg
    http://api.openweathermap.org/data/2.5/weather?q=mahebourg&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #58 City Nameviransehir
    http://api.openweathermap.org/data/2.5/weather?q=viransehir&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #59 City Namekahului
    http://api.openweathermap.org/data/2.5/weather?q=kahului&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #60 City Namemys shmidta
    http://api.openweathermap.org/data/2.5/weather?q=mys shmidta&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #61 City Namehermanus
    http://api.openweathermap.org/data/2.5/weather?q=hermanus&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #62 City Nameancud
    http://api.openweathermap.org/data/2.5/weather?q=ancud&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #63 City Namekasama
    http://api.openweathermap.org/data/2.5/weather?q=kasama&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #64 City Nameport lincoln
    http://api.openweathermap.org/data/2.5/weather?q=port lincoln&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #65 City Namealbany
    http://api.openweathermap.org/data/2.5/weather?q=albany&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #66 City Namebusselton
    http://api.openweathermap.org/data/2.5/weather?q=busselton&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #67 City Namealbany
    http://api.openweathermap.org/data/2.5/weather?q=albany&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #68 City Namemataura
    http://api.openweathermap.org/data/2.5/weather?q=mataura&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #69 City Namesaldanha
    http://api.openweathermap.org/data/2.5/weather?q=saldanha&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #70 City Namerikitea
    http://api.openweathermap.org/data/2.5/weather?q=rikitea&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #71 City Nameport alfred
    http://api.openweathermap.org/data/2.5/weather?q=port alfred&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #72 City Namela baule-escoublac
    http://api.openweathermap.org/data/2.5/weather?q=la baule-escoublac&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #73 City Nameglubokiy
    http://api.openweathermap.org/data/2.5/weather?q=glubokiy&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #74 City Nameprovideniya
    http://api.openweathermap.org/data/2.5/weather?q=provideniya&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #75 City Nameayer itam
    http://api.openweathermap.org/data/2.5/weather?q=ayer itam&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #76 City Nameinayawan
    http://api.openweathermap.org/data/2.5/weather?q=inayawan&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #77 City Namemataura
    http://api.openweathermap.org/data/2.5/weather?q=mataura&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #78 City Nameklaksvik
    http://api.openweathermap.org/data/2.5/weather?q=klaksvik&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #79 City Namewerda
    http://api.openweathermap.org/data/2.5/weather?q=werda&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #80 City Namearraial do cabo
    http://api.openweathermap.org/data/2.5/weather?q=arraial do cabo&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #81 City Namekasongo-lunda
    http://api.openweathermap.org/data/2.5/weather?q=kasongo-lunda&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #82 City Nameatuona
    http://api.openweathermap.org/data/2.5/weather?q=atuona&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #83 City Nameocos
    http://api.openweathermap.org/data/2.5/weather?q=ocos&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #84 City Namekapaa
    http://api.openweathermap.org/data/2.5/weather?q=kapaa&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #85 City Nameconceicao da barra
    http://api.openweathermap.org/data/2.5/weather?q=conceicao da barra&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #86 City Namedikson
    http://api.openweathermap.org/data/2.5/weather?q=dikson&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #87 City Namerikitea
    http://api.openweathermap.org/data/2.5/weather?q=rikitea&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #88 City Nameamderma
    http://api.openweathermap.org/data/2.5/weather?q=amderma&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #89 City Nameawjilah
    http://api.openweathermap.org/data/2.5/weather?q=awjilah&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #90 City Namevaitupu
    http://api.openweathermap.org/data/2.5/weather?q=vaitupu&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #91 City Namehasaki
    http://api.openweathermap.org/data/2.5/weather?q=hasaki&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #92 City Namedemyansk
    http://api.openweathermap.org/data/2.5/weather?q=demyansk&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #93 City Nametupik
    http://api.openweathermap.org/data/2.5/weather?q=tupik&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #94 City Namemataura
    http://api.openweathermap.org/data/2.5/weather?q=mataura&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #95 City Namewinslow
    http://api.openweathermap.org/data/2.5/weather?q=winslow&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #96 City Nametasiilaq
    http://api.openweathermap.org/data/2.5/weather?q=tasiilaq&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #97 City Namecap malheureux
    http://api.openweathermap.org/data/2.5/weather?q=cap malheureux&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #98 City Namelima
    http://api.openweathermap.org/data/2.5/weather?q=lima&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #99 City Namenovikovo
    http://api.openweathermap.org/data/2.5/weather?q=novikovo&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #100 City Namekinsale
    http://api.openweathermap.org/data/2.5/weather?q=kinsale&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #101 City Namegurupi
    http://api.openweathermap.org/data/2.5/weather?q=gurupi&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #102 City Namebutaritari
    http://api.openweathermap.org/data/2.5/weather?q=butaritari&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #103 City Namelompoc
    http://api.openweathermap.org/data/2.5/weather?q=lompoc&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #104 City Namemaceio
    http://api.openweathermap.org/data/2.5/weather?q=maceio&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #105 City Nametarakan
    http://api.openweathermap.org/data/2.5/weather?q=tarakan&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #106 City Namesaleaula
    http://api.openweathermap.org/data/2.5/weather?q=saleaula&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #107 City Namedesaguadero
    http://api.openweathermap.org/data/2.5/weather?q=desaguadero&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #108 City Namemahebourg
    http://api.openweathermap.org/data/2.5/weather?q=mahebourg&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #109 City Namevestmannaeyjar
    http://api.openweathermap.org/data/2.5/weather?q=vestmannaeyjar&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #110 City Namecape town
    http://api.openweathermap.org/data/2.5/weather?q=cape town&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #111 City Namecape town
    http://api.openweathermap.org/data/2.5/weather?q=cape town&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #112 City Namesamusu
    http://api.openweathermap.org/data/2.5/weather?q=samusu&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #113 City Namerikitea
    http://api.openweathermap.org/data/2.5/weather?q=rikitea&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #114 City Nameilo
    http://api.openweathermap.org/data/2.5/weather?q=ilo&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #115 City Namerikitea
    http://api.openweathermap.org/data/2.5/weather?q=rikitea&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #116 City Namesitka
    http://api.openweathermap.org/data/2.5/weather?q=sitka&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #117 City Namebambous virieux
    http://api.openweathermap.org/data/2.5/weather?q=bambous virieux&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #118 City Nametaolanaro
    http://api.openweathermap.org/data/2.5/weather?q=taolanaro&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #119 City Namebarentsburg
    http://api.openweathermap.org/data/2.5/weather?q=barentsburg&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #120 City Namepekan
    http://api.openweathermap.org/data/2.5/weather?q=pekan&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #121 City Namekudahuvadhoo
    http://api.openweathermap.org/data/2.5/weather?q=kudahuvadhoo&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #122 City Nameavarua
    http://api.openweathermap.org/data/2.5/weather?q=avarua&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #123 City Nameilloqqortoormiut
    http://api.openweathermap.org/data/2.5/weather?q=illoqqortoormiut&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #124 City Namehilo
    http://api.openweathermap.org/data/2.5/weather?q=hilo&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #125 City Namekarratha
    http://api.openweathermap.org/data/2.5/weather?q=karratha&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #126 City Namepunta arenas
    http://api.openweathermap.org/data/2.5/weather?q=punta arenas&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #127 City Nameroad town
    http://api.openweathermap.org/data/2.5/weather?q=road town&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #128 City Namearraial do cabo
    http://api.openweathermap.org/data/2.5/weather?q=arraial do cabo&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #129 City Nameaktash
    http://api.openweathermap.org/data/2.5/weather?q=aktash&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #130 City Nameluderitz
    http://api.openweathermap.org/data/2.5/weather?q=luderitz&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #131 City Namecastro
    http://api.openweathermap.org/data/2.5/weather?q=castro&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #132 City Namepuerto del rosario
    http://api.openweathermap.org/data/2.5/weather?q=puerto del rosario&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #133 City Namekailua
    http://api.openweathermap.org/data/2.5/weather?q=kailua&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #134 City Namebutaritari
    http://api.openweathermap.org/data/2.5/weather?q=butaritari&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #135 City Nameqaanaaq
    http://api.openweathermap.org/data/2.5/weather?q=qaanaaq&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #136 City Namesao joao da barra
    http://api.openweathermap.org/data/2.5/weather?q=sao joao da barra&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #137 City Namequatre cocos
    http://api.openweathermap.org/data/2.5/weather?q=quatre cocos&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #138 City Nameushuaia
    http://api.openweathermap.org/data/2.5/weather?q=ushuaia&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #139 City Namehirata
    http://api.openweathermap.org/data/2.5/weather?q=hirata&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #140 City Namerosetta
    http://api.openweathermap.org/data/2.5/weather?q=rosetta&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #141 City Namesaskylakh
    http://api.openweathermap.org/data/2.5/weather?q=saskylakh&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #142 City Namebundaberg
    http://api.openweathermap.org/data/2.5/weather?q=bundaberg&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #143 City Namebarrow
    http://api.openweathermap.org/data/2.5/weather?q=barrow&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #144 City Namesouillac
    http://api.openweathermap.org/data/2.5/weather?q=souillac&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #145 City Namesharan
    http://api.openweathermap.org/data/2.5/weather?q=sharan&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #146 City Namedebre birhan
    http://api.openweathermap.org/data/2.5/weather?q=debre birhan&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #147 City Namemehamn
    http://api.openweathermap.org/data/2.5/weather?q=mehamn&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #148 City Namealbany
    http://api.openweathermap.org/data/2.5/weather?q=albany&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #149 City Nameborogontsy
    http://api.openweathermap.org/data/2.5/weather?q=borogontsy&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #150 City Namemar del plata
    http://api.openweathermap.org/data/2.5/weather?q=mar del plata&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #151 City Nameushuaia
    http://api.openweathermap.org/data/2.5/weather?q=ushuaia&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #152 City Nameqingdao
    http://api.openweathermap.org/data/2.5/weather?q=qingdao&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #153 City Nameport lincoln
    http://api.openweathermap.org/data/2.5/weather?q=port lincoln&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #154 City Namecollege
    http://api.openweathermap.org/data/2.5/weather?q=college&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #155 City Namebroome
    http://api.openweathermap.org/data/2.5/weather?q=broome&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #156 City Namearbroath
    http://api.openweathermap.org/data/2.5/weather?q=arbroath&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #157 City Namehermanus
    http://api.openweathermap.org/data/2.5/weather?q=hermanus&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #158 City Nametasiilaq
    http://api.openweathermap.org/data/2.5/weather?q=tasiilaq&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #159 City Namepierre
    http://api.openweathermap.org/data/2.5/weather?q=pierre&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #160 City Namequatre cocos
    http://api.openweathermap.org/data/2.5/weather?q=quatre cocos&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #161 City Nametiksi
    http://api.openweathermap.org/data/2.5/weather?q=tiksi&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #162 City Namebilma
    http://api.openweathermap.org/data/2.5/weather?q=bilma&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #163 City Namebaruun-urt
    http://api.openweathermap.org/data/2.5/weather?q=baruun-urt&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #164 City Namebarrow
    http://api.openweathermap.org/data/2.5/weather?q=barrow&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #165 City Namehilo
    http://api.openweathermap.org/data/2.5/weather?q=hilo&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #166 City Namepuerto del rosario
    http://api.openweathermap.org/data/2.5/weather?q=puerto del rosario&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #167 City Namebluff
    http://api.openweathermap.org/data/2.5/weather?q=bluff&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #168 City Namesevero-kurilsk
    http://api.openweathermap.org/data/2.5/weather?q=severo-kurilsk&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #169 City Namemar del plata
    http://api.openweathermap.org/data/2.5/weather?q=mar del plata&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #170 City Namesaint george
    http://api.openweathermap.org/data/2.5/weather?q=saint george&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #171 City Namehusavik
    http://api.openweathermap.org/data/2.5/weather?q=husavik&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #172 City Namevanderhoof
    http://api.openweathermap.org/data/2.5/weather?q=vanderhoof&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #173 City Namethompson
    http://api.openweathermap.org/data/2.5/weather?q=thompson&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #174 City Nameushuaia
    http://api.openweathermap.org/data/2.5/weather?q=ushuaia&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #175 City Nametakoradi
    http://api.openweathermap.org/data/2.5/weather?q=takoradi&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #176 City Namela primavera
    http://api.openweathermap.org/data/2.5/weather?q=la primavera&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #177 City Namefairbanks
    http://api.openweathermap.org/data/2.5/weather?q=fairbanks&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #178 City Nameairai
    http://api.openweathermap.org/data/2.5/weather?q=airai&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #179 City Namegeraldton
    http://api.openweathermap.org/data/2.5/weather?q=geraldton&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #180 City Namekavaratti
    http://api.openweathermap.org/data/2.5/weather?q=kavaratti&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #181 City Nameiqaluit
    http://api.openweathermap.org/data/2.5/weather?q=iqaluit&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #182 City Nameqaanaaq
    http://api.openweathermap.org/data/2.5/weather?q=qaanaaq&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #183 City Namekaitangata
    http://api.openweathermap.org/data/2.5/weather?q=kaitangata&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #184 City Namemataura
    http://api.openweathermap.org/data/2.5/weather?q=mataura&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #185 City Namepunta arenas
    http://api.openweathermap.org/data/2.5/weather?q=punta arenas&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #186 City Nametaolanaro
    http://api.openweathermap.org/data/2.5/weather?q=taolanaro&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #187 City Nameguiren
    http://api.openweathermap.org/data/2.5/weather?q=guiren&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #188 City Namenew norfolk
    http://api.openweathermap.org/data/2.5/weather?q=new norfolk&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #189 City Namebayburt
    http://api.openweathermap.org/data/2.5/weather?q=bayburt&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #190 City Nameoranjestad
    http://api.openweathermap.org/data/2.5/weather?q=oranjestad&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #191 City Namemalokakhovka
    http://api.openweathermap.org/data/2.5/weather?q=malokakhovka&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #192 City Nameponta do sol
    http://api.openweathermap.org/data/2.5/weather?q=ponta do sol&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #193 City Namemataura
    http://api.openweathermap.org/data/2.5/weather?q=mataura&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #194 City Namebarrow
    http://api.openweathermap.org/data/2.5/weather?q=barrow&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #195 City Namelakes entrance
    http://api.openweathermap.org/data/2.5/weather?q=lakes entrance&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #196 City Nameraudeberg
    http://api.openweathermap.org/data/2.5/weather?q=raudeberg&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #197 City Namealbany
    http://api.openweathermap.org/data/2.5/weather?q=albany&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #198 City Namesexsmith
    http://api.openweathermap.org/data/2.5/weather?q=sexsmith&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #199 City Namealbany
    http://api.openweathermap.org/data/2.5/weather?q=albany&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #200 City Namebarentsburg
    http://api.openweathermap.org/data/2.5/weather?q=barentsburg&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #201 City Namegat
    http://api.openweathermap.org/data/2.5/weather?q=gat&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #202 City Namemawlaik
    http://api.openweathermap.org/data/2.5/weather?q=mawlaik&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #203 City Namesaint-philippe
    http://api.openweathermap.org/data/2.5/weather?q=saint-philippe&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #204 City Namenogliki
    http://api.openweathermap.org/data/2.5/weather?q=nogliki&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #205 City Namesavannah bight
    http://api.openweathermap.org/data/2.5/weather?q=savannah bight&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #206 City Nametaolanaro
    http://api.openweathermap.org/data/2.5/weather?q=taolanaro&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #207 City Nameeast london
    http://api.openweathermap.org/data/2.5/weather?q=east london&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #208 City Namebethel
    http://api.openweathermap.org/data/2.5/weather?q=bethel&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #209 City Namenew norfolk
    http://api.openweathermap.org/data/2.5/weather?q=new norfolk&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #210 City Nametasbuget
    http://api.openweathermap.org/data/2.5/weather?q=tasbuget&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #211 City Namelebu
    http://api.openweathermap.org/data/2.5/weather?q=lebu&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #212 City Nameolafsvik
    http://api.openweathermap.org/data/2.5/weather?q=olafsvik&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #213 City Namejamestown
    http://api.openweathermap.org/data/2.5/weather?q=jamestown&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #214 City Namerikitea
    http://api.openweathermap.org/data/2.5/weather?q=rikitea&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #215 City Namewajima
    http://api.openweathermap.org/data/2.5/weather?q=wajima&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #216 City Namekamaishi
    http://api.openweathermap.org/data/2.5/weather?q=kamaishi&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #217 City Namekaitangata
    http://api.openweathermap.org/data/2.5/weather?q=kaitangata&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #218 City Namelagoa
    http://api.openweathermap.org/data/2.5/weather?q=lagoa&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #219 City Namejinchang
    http://api.openweathermap.org/data/2.5/weather?q=jinchang&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #220 City Nameushuaia
    http://api.openweathermap.org/data/2.5/weather?q=ushuaia&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #221 City Nameloandjili
    http://api.openweathermap.org/data/2.5/weather?q=loandjili&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #222 City Namefevralsk
    http://api.openweathermap.org/data/2.5/weather?q=fevralsk&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #223 City Namemys shmidta
    http://api.openweathermap.org/data/2.5/weather?q=mys shmidta&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #224 City Nametasiilaq
    http://api.openweathermap.org/data/2.5/weather?q=tasiilaq&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #225 City Namehusavik
    http://api.openweathermap.org/data/2.5/weather?q=husavik&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #226 City Namelongyearbyen
    http://api.openweathermap.org/data/2.5/weather?q=longyearbyen&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #227 City Nameyanahuanca
    http://api.openweathermap.org/data/2.5/weather?q=yanahuanca&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #228 City Namebroome
    http://api.openweathermap.org/data/2.5/weather?q=broome&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #229 City Namecastro
    http://api.openweathermap.org/data/2.5/weather?q=castro&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #230 City Namemar del plata
    http://api.openweathermap.org/data/2.5/weather?q=mar del plata&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #231 City Namenandura
    http://api.openweathermap.org/data/2.5/weather?q=nandura&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #232 City Namefreetown
    http://api.openweathermap.org/data/2.5/weather?q=freetown&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #233 City Namearraial do cabo
    http://api.openweathermap.org/data/2.5/weather?q=arraial do cabo&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #234 City Namealbany
    http://api.openweathermap.org/data/2.5/weather?q=albany&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #235 City Namerikitea
    http://api.openweathermap.org/data/2.5/weather?q=rikitea&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #236 City Namevardo
    http://api.openweathermap.org/data/2.5/weather?q=vardo&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #237 City Nameaklavik
    http://api.openweathermap.org/data/2.5/weather?q=aklavik&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #238 City Nametaoudenni
    http://api.openweathermap.org/data/2.5/weather?q=taoudenni&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #239 City Namebusselton
    http://api.openweathermap.org/data/2.5/weather?q=busselton&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #240 City Namekruisfontein
    http://api.openweathermap.org/data/2.5/weather?q=kruisfontein&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #241 City Nameport alfred
    http://api.openweathermap.org/data/2.5/weather?q=port alfred&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #242 City Namethompson
    http://api.openweathermap.org/data/2.5/weather?q=thompson&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #243 City Namebusselton
    http://api.openweathermap.org/data/2.5/weather?q=busselton&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #244 City Nameushuaia
    http://api.openweathermap.org/data/2.5/weather?q=ushuaia&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #245 City Nameilloqqortoormiut
    http://api.openweathermap.org/data/2.5/weather?q=illoqqortoormiut&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #246 City Namecazaje
    http://api.openweathermap.org/data/2.5/weather?q=cazaje&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #247 City Namepunta arenas
    http://api.openweathermap.org/data/2.5/weather?q=punta arenas&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #248 City Nametrelew
    http://api.openweathermap.org/data/2.5/weather?q=trelew&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #249 City Nameport elizabeth
    http://api.openweathermap.org/data/2.5/weather?q=port elizabeth&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #250 City Namelamesa
    http://api.openweathermap.org/data/2.5/weather?q=lamesa&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #251 City Namefarmington
    http://api.openweathermap.org/data/2.5/weather?q=farmington&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #252 City Namerock sound
    http://api.openweathermap.org/data/2.5/weather?q=rock sound&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #253 City Namethompson
    http://api.openweathermap.org/data/2.5/weather?q=thompson&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #254 City Namedikson
    http://api.openweathermap.org/data/2.5/weather?q=dikson&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #255 City Namerikitea
    http://api.openweathermap.org/data/2.5/weather?q=rikitea&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #256 City Namehobart
    http://api.openweathermap.org/data/2.5/weather?q=hobart&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #257 City Namelavrentiya
    http://api.openweathermap.org/data/2.5/weather?q=lavrentiya&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #258 City Namenikolskoye
    http://api.openweathermap.org/data/2.5/weather?q=nikolskoye&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #259 City Namecape town
    http://api.openweathermap.org/data/2.5/weather?q=cape town&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #260 City Namelos llanos de aridane
    http://api.openweathermap.org/data/2.5/weather?q=los llanos de aridane&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #261 City Namepangoa
    http://api.openweathermap.org/data/2.5/weather?q=pangoa&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #262 City Namepunta arenas
    http://api.openweathermap.org/data/2.5/weather?q=punta arenas&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #263 City Nameponta do sol
    http://api.openweathermap.org/data/2.5/weather?q=ponta do sol&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #264 City Nameyanchukan
    http://api.openweathermap.org/data/2.5/weather?q=yanchukan&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #265 City Nameyerbogachen
    http://api.openweathermap.org/data/2.5/weather?q=yerbogachen&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #266 City Namecape town
    http://api.openweathermap.org/data/2.5/weather?q=cape town&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #267 City Namevictoria
    http://api.openweathermap.org/data/2.5/weather?q=victoria&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #268 City Namebathsheba
    http://api.openweathermap.org/data/2.5/weather?q=bathsheba&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #269 City Nameushuaia
    http://api.openweathermap.org/data/2.5/weather?q=ushuaia&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #270 City Namehenties bay
    http://api.openweathermap.org/data/2.5/weather?q=henties bay&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #271 City Namedikson
    http://api.openweathermap.org/data/2.5/weather?q=dikson&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #272 City Nameulagan
    http://api.openweathermap.org/data/2.5/weather?q=ulagan&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #273 City Namelebu
    http://api.openweathermap.org/data/2.5/weather?q=lebu&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #274 City Nameqaanaaq
    http://api.openweathermap.org/data/2.5/weather?q=qaanaaq&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #275 City Namepuerto ayora
    http://api.openweathermap.org/data/2.5/weather?q=puerto ayora&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #276 City Namenew norfolk
    http://api.openweathermap.org/data/2.5/weather?q=new norfolk&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #277 City Namealbany
    http://api.openweathermap.org/data/2.5/weather?q=albany&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #278 City Namehofn
    http://api.openweathermap.org/data/2.5/weather?q=hofn&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #279 City Namegeorgetown
    http://api.openweathermap.org/data/2.5/weather?q=georgetown&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #280 City Namemar del plata
    http://api.openweathermap.org/data/2.5/weather?q=mar del plata&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #281 City Namebengkulu
    http://api.openweathermap.org/data/2.5/weather?q=bengkulu&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #282 City Namedikson
    http://api.openweathermap.org/data/2.5/weather?q=dikson&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #283 City Nameport macquarie
    http://api.openweathermap.org/data/2.5/weather?q=port macquarie&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #284 City Namevaini
    http://api.openweathermap.org/data/2.5/weather?q=vaini&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #285 City Nameroebourne
    http://api.openweathermap.org/data/2.5/weather?q=roebourne&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #286 City Namemataura
    http://api.openweathermap.org/data/2.5/weather?q=mataura&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #287 City Nameashdod
    http://api.openweathermap.org/data/2.5/weather?q=ashdod&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #288 City Namenew norfolk
    http://api.openweathermap.org/data/2.5/weather?q=new norfolk&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #289 City Nameamderma
    http://api.openweathermap.org/data/2.5/weather?q=amderma&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #290 City Namerikitea
    http://api.openweathermap.org/data/2.5/weather?q=rikitea&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #291 City Namedali
    http://api.openweathermap.org/data/2.5/weather?q=dali&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #292 City Namecape town
    http://api.openweathermap.org/data/2.5/weather?q=cape town&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #293 City Nameguanica
    http://api.openweathermap.org/data/2.5/weather?q=guanica&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #294 City Nameatbasar
    http://api.openweathermap.org/data/2.5/weather?q=atbasar&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #295 City Namedikson
    http://api.openweathermap.org/data/2.5/weather?q=dikson&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #296 City Namevictoria
    http://api.openweathermap.org/data/2.5/weather?q=victoria&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #297 City Namehassleholm
    http://api.openweathermap.org/data/2.5/weather?q=hassleholm&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #298 City Namefochville
    http://api.openweathermap.org/data/2.5/weather?q=fochville&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #299 City Namesrednekolymsk
    http://api.openweathermap.org/data/2.5/weather?q=srednekolymsk&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #300 City Nameeast london
    http://api.openweathermap.org/data/2.5/weather?q=east london&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #301 City Namecarutapera
    http://api.openweathermap.org/data/2.5/weather?q=carutapera&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #302 City Nametommot
    http://api.openweathermap.org/data/2.5/weather?q=tommot&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #303 City Nameport hardy
    http://api.openweathermap.org/data/2.5/weather?q=port hardy&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #304 City Namebajo baudo
    http://api.openweathermap.org/data/2.5/weather?q=bajo baudo&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #305 City Namemale
    http://api.openweathermap.org/data/2.5/weather?q=male&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #306 City Namekodiak
    http://api.openweathermap.org/data/2.5/weather?q=kodiak&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #307 City Namefrederick
    http://api.openweathermap.org/data/2.5/weather?q=frederick&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #308 City Namebusselton
    http://api.openweathermap.org/data/2.5/weather?q=busselton&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #309 City Namemataura
    http://api.openweathermap.org/data/2.5/weather?q=mataura&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #310 City Nameverkhneuralsk
    http://api.openweathermap.org/data/2.5/weather?q=verkhneuralsk&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #311 City Namenizhneyansk
    http://api.openweathermap.org/data/2.5/weather?q=nizhneyansk&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #312 City Nameberingovskiy
    http://api.openweathermap.org/data/2.5/weather?q=beringovskiy&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #313 City Nameushuaia
    http://api.openweathermap.org/data/2.5/weather?q=ushuaia&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #314 City Nameqaanaaq
    http://api.openweathermap.org/data/2.5/weather?q=qaanaaq&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #315 City Namedikson
    http://api.openweathermap.org/data/2.5/weather?q=dikson&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #316 City Nameprince rupert
    http://api.openweathermap.org/data/2.5/weather?q=prince rupert&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #317 City Namebluff
    http://api.openweathermap.org/data/2.5/weather?q=bluff&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #318 City Namehaibowan
    http://api.openweathermap.org/data/2.5/weather?q=haibowan&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #319 City Namemarienburg
    http://api.openweathermap.org/data/2.5/weather?q=marienburg&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #320 City Namemarystown
    http://api.openweathermap.org/data/2.5/weather?q=marystown&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #321 City Namejambi
    http://api.openweathermap.org/data/2.5/weather?q=jambi&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #322 City Nameairai
    http://api.openweathermap.org/data/2.5/weather?q=airai&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #323 City Namecherskiy
    http://api.openweathermap.org/data/2.5/weather?q=cherskiy&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #324 City Namemildura
    http://api.openweathermap.org/data/2.5/weather?q=mildura&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #325 City Namejuneau
    http://api.openweathermap.org/data/2.5/weather?q=juneau&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #326 City Namelebu
    http://api.openweathermap.org/data/2.5/weather?q=lebu&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #327 City Nameport alfred
    http://api.openweathermap.org/data/2.5/weather?q=port alfred&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #328 City Namegeorgetown
    http://api.openweathermap.org/data/2.5/weather?q=georgetown&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #329 City Namekrasnyy oktyabr
    http://api.openweathermap.org/data/2.5/weather?q=krasnyy oktyabr&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #330 City Namehamilton
    http://api.openweathermap.org/data/2.5/weather?q=hamilton&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #331 City Nameesil
    http://api.openweathermap.org/data/2.5/weather?q=esil&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #332 City Namepangnirtung
    http://api.openweathermap.org/data/2.5/weather?q=pangnirtung&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #333 City Namemarawi
    http://api.openweathermap.org/data/2.5/weather?q=marawi&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #334 City Namepenzance
    http://api.openweathermap.org/data/2.5/weather?q=penzance&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #335 City Namemonterey
    http://api.openweathermap.org/data/2.5/weather?q=monterey&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #336 City Namepisco
    http://api.openweathermap.org/data/2.5/weather?q=pisco&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #337 City Namehobart
    http://api.openweathermap.org/data/2.5/weather?q=hobart&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #338 City Nameeast london
    http://api.openweathermap.org/data/2.5/weather?q=east london&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #339 City Nameport elizabeth
    http://api.openweathermap.org/data/2.5/weather?q=port elizabeth&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #340 City Namebarao de melgaco
    http://api.openweathermap.org/data/2.5/weather?q=barao de melgaco&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #341 City Nametuktoyaktuk
    http://api.openweathermap.org/data/2.5/weather?q=tuktoyaktuk&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #342 City Namearraial do cabo
    http://api.openweathermap.org/data/2.5/weather?q=arraial do cabo&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #343 City Namekodiak
    http://api.openweathermap.org/data/2.5/weather?q=kodiak&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #344 City Namebusselton
    http://api.openweathermap.org/data/2.5/weather?q=busselton&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #345 City Namepuerto el triunfo
    http://api.openweathermap.org/data/2.5/weather?q=puerto el triunfo&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #346 City Namevaitupu
    http://api.openweathermap.org/data/2.5/weather?q=vaitupu&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #347 City Namemayo
    http://api.openweathermap.org/data/2.5/weather?q=mayo&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #348 City Namekatsuura
    http://api.openweathermap.org/data/2.5/weather?q=katsuura&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #349 City Namehithadhoo
    http://api.openweathermap.org/data/2.5/weather?q=hithadhoo&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #350 City Namekrasnoselkup
    http://api.openweathermap.org/data/2.5/weather?q=krasnoselkup&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #351 City Namechuy
    http://api.openweathermap.org/data/2.5/weather?q=chuy&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #352 City Namekhatanga
    http://api.openweathermap.org/data/2.5/weather?q=khatanga&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #353 City Nametura
    http://api.openweathermap.org/data/2.5/weather?q=tura&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #354 City Namebarahona
    http://api.openweathermap.org/data/2.5/weather?q=barahona&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #355 City Namepuerto ayora
    http://api.openweathermap.org/data/2.5/weather?q=puerto ayora&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #356 City Namesola
    http://api.openweathermap.org/data/2.5/weather?q=sola&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #357 City Nameushuaia
    http://api.openweathermap.org/data/2.5/weather?q=ushuaia&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #358 City Namehusavik
    http://api.openweathermap.org/data/2.5/weather?q=husavik&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #359 City Namebethel
    http://api.openweathermap.org/data/2.5/weather?q=bethel&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #360 City Namepinhao
    http://api.openweathermap.org/data/2.5/weather?q=pinhao&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #361 City Namelongyearbyen
    http://api.openweathermap.org/data/2.5/weather?q=longyearbyen&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #362 City Nametorbay
    http://api.openweathermap.org/data/2.5/weather?q=torbay&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #363 City Nametongliao
    http://api.openweathermap.org/data/2.5/weather?q=tongliao&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #364 City Namepaso de los toros
    http://api.openweathermap.org/data/2.5/weather?q=paso de los toros&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #365 City Namepalmer
    http://api.openweathermap.org/data/2.5/weather?q=palmer&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #366 City Namebeira
    http://api.openweathermap.org/data/2.5/weather?q=beira&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #367 City Namealbany
    http://api.openweathermap.org/data/2.5/weather?q=albany&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #368 City Nameroma
    http://api.openweathermap.org/data/2.5/weather?q=roma&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #369 City Namebandarbeyla
    http://api.openweathermap.org/data/2.5/weather?q=bandarbeyla&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #370 City Namesaint george
    http://api.openweathermap.org/data/2.5/weather?q=saint george&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #371 City Namenanortalik
    http://api.openweathermap.org/data/2.5/weather?q=nanortalik&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #372 City Namenome
    http://api.openweathermap.org/data/2.5/weather?q=nome&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #373 City Nameketchikan
    http://api.openweathermap.org/data/2.5/weather?q=ketchikan&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #374 City Namekapaa
    http://api.openweathermap.org/data/2.5/weather?q=kapaa&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #375 City Nameitupiranga
    http://api.openweathermap.org/data/2.5/weather?q=itupiranga&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #376 City Nameotane
    http://api.openweathermap.org/data/2.5/weather?q=otane&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #377 City Namemataura
    http://api.openweathermap.org/data/2.5/weather?q=mataura&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #378 City Namepunta arenas
    http://api.openweathermap.org/data/2.5/weather?q=punta arenas&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #379 City Namegeorgetown
    http://api.openweathermap.org/data/2.5/weather?q=georgetown&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #380 City Namepunta arenas
    http://api.openweathermap.org/data/2.5/weather?q=punta arenas&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #381 City Nameburica
    http://api.openweathermap.org/data/2.5/weather?q=burica&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #382 City Namehermanus
    http://api.openweathermap.org/data/2.5/weather?q=hermanus&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #383 City Nameqaanaaq
    http://api.openweathermap.org/data/2.5/weather?q=qaanaaq&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #384 City Namebusselton
    http://api.openweathermap.org/data/2.5/weather?q=busselton&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #385 City Nameyar-sale
    http://api.openweathermap.org/data/2.5/weather?q=yar-sale&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #386 City Nameatuona
    http://api.openweathermap.org/data/2.5/weather?q=atuona&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #387 City Namembanza-ngungu
    http://api.openweathermap.org/data/2.5/weather?q=mbanza-ngungu&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #388 City Namesatitoa
    http://api.openweathermap.org/data/2.5/weather?q=satitoa&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #389 City Nameaguimes
    http://api.openweathermap.org/data/2.5/weather?q=aguimes&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #390 City Nameleskovik
    http://api.openweathermap.org/data/2.5/weather?q=leskovik&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #391 City Namevaitupu
    http://api.openweathermap.org/data/2.5/weather?q=vaitupu&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #392 City Namehermanus
    http://api.openweathermap.org/data/2.5/weather?q=hermanus&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #393 City Namehermanus
    http://api.openweathermap.org/data/2.5/weather?q=hermanus&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #394 City Namepunta arenas
    http://api.openweathermap.org/data/2.5/weather?q=punta arenas&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #395 City Namegeorgetown
    http://api.openweathermap.org/data/2.5/weather?q=georgetown&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #396 City Nameperth
    http://api.openweathermap.org/data/2.5/weather?q=perth&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #397 City Namehendijan
    http://api.openweathermap.org/data/2.5/weather?q=hendijan&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #398 City Nameyellowknife
    http://api.openweathermap.org/data/2.5/weather?q=yellowknife&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #399 City Nameyellowknife
    http://api.openweathermap.org/data/2.5/weather?q=yellowknife&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #400 City Nametuktoyaktuk
    http://api.openweathermap.org/data/2.5/weather?q=tuktoyaktuk&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #401 City Namesaskylakh
    http://api.openweathermap.org/data/2.5/weather?q=saskylakh&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #402 City Namemataura
    http://api.openweathermap.org/data/2.5/weather?q=mataura&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #403 City Nametyukalinsk
    http://api.openweathermap.org/data/2.5/weather?q=tyukalinsk&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #404 City Nametiksi
    http://api.openweathermap.org/data/2.5/weather?q=tiksi&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #405 City Namemarawi
    http://api.openweathermap.org/data/2.5/weather?q=marawi&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #406 City Namediamantino
    http://api.openweathermap.org/data/2.5/weather?q=diamantino&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #407 City Nameilloqqortoormiut
    http://api.openweathermap.org/data/2.5/weather?q=illoqqortoormiut&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #408 City Namekapaa
    http://api.openweathermap.org/data/2.5/weather?q=kapaa&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #409 City Namehermanus
    http://api.openweathermap.org/data/2.5/weather?q=hermanus&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #410 City Namedikson
    http://api.openweathermap.org/data/2.5/weather?q=dikson&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #411 City Namepevek
    http://api.openweathermap.org/data/2.5/weather?q=pevek&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #412 City Namehobart
    http://api.openweathermap.org/data/2.5/weather?q=hobart&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #413 City Nameushuaia
    http://api.openweathermap.org/data/2.5/weather?q=ushuaia&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #414 City Namenew norfolk
    http://api.openweathermap.org/data/2.5/weather?q=new norfolk&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #415 City Namenicosia
    http://api.openweathermap.org/data/2.5/weather?q=nicosia&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #416 City Namenguruka
    http://api.openweathermap.org/data/2.5/weather?q=nguruka&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #417 City Namearraial do cabo
    http://api.openweathermap.org/data/2.5/weather?q=arraial do cabo&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #418 City Namebredasdorp
    http://api.openweathermap.org/data/2.5/weather?q=bredasdorp&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #419 City Nameeast london
    http://api.openweathermap.org/data/2.5/weather?q=east london&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #420 City Nameskjervoy
    http://api.openweathermap.org/data/2.5/weather?q=skjervoy&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #421 City Namefort nelson
    http://api.openweathermap.org/data/2.5/weather?q=fort nelson&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #422 City Namebusselton
    http://api.openweathermap.org/data/2.5/weather?q=busselton&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #423 City Namealbany
    http://api.openweathermap.org/data/2.5/weather?q=albany&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #424 City Namecap-aux-meules
    http://api.openweathermap.org/data/2.5/weather?q=cap-aux-meules&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #425 City Namecamacha
    http://api.openweathermap.org/data/2.5/weather?q=camacha&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #426 City Namecodrington
    http://api.openweathermap.org/data/2.5/weather?q=codrington&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #427 City Namejamestown
    http://api.openweathermap.org/data/2.5/weather?q=jamestown&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #428 City Namespringbok
    http://api.openweathermap.org/data/2.5/weather?q=springbok&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #429 City Namebluff
    http://api.openweathermap.org/data/2.5/weather?q=bluff&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #430 City Nametasiilaq
    http://api.openweathermap.org/data/2.5/weather?q=tasiilaq&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #431 City Namebahawalpur
    http://api.openweathermap.org/data/2.5/weather?q=bahawalpur&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #432 City Nameevensk
    http://api.openweathermap.org/data/2.5/weather?q=evensk&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #433 City Nameavarua
    http://api.openweathermap.org/data/2.5/weather?q=avarua&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #434 City Nameribeira grande
    http://api.openweathermap.org/data/2.5/weather?q=ribeira grande&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #435 City Namecidreira
    http://api.openweathermap.org/data/2.5/weather?q=cidreira&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #436 City Namekayerkan
    http://api.openweathermap.org/data/2.5/weather?q=kayerkan&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #437 City Namenew norfolk
    http://api.openweathermap.org/data/2.5/weather?q=new norfolk&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #438 City Nameosa
    http://api.openweathermap.org/data/2.5/weather?q=osa&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #439 City Namepunta arenas
    http://api.openweathermap.org/data/2.5/weather?q=punta arenas&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #440 City Namerikitea
    http://api.openweathermap.org/data/2.5/weather?q=rikitea&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #441 City Namerikitea
    http://api.openweathermap.org/data/2.5/weather?q=rikitea&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #442 City Namebluff
    http://api.openweathermap.org/data/2.5/weather?q=bluff&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #443 City Namedzhusaly
    http://api.openweathermap.org/data/2.5/weather?q=dzhusaly&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #444 City Namezaysan
    http://api.openweathermap.org/data/2.5/weather?q=zaysan&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #445 City Namemount gambier
    http://api.openweathermap.org/data/2.5/weather?q=mount gambier&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #446 City Namepunta arenas
    http://api.openweathermap.org/data/2.5/weather?q=punta arenas&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #447 City Nametemaraia
    http://api.openweathermap.org/data/2.5/weather?q=temaraia&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #448 City Namepuerto ayora
    http://api.openweathermap.org/data/2.5/weather?q=puerto ayora&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #449 City Nameqaanaaq
    http://api.openweathermap.org/data/2.5/weather?q=qaanaaq&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #450 City Namegeorgetown
    http://api.openweathermap.org/data/2.5/weather?q=georgetown&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #451 City Namesan cristobal
    http://api.openweathermap.org/data/2.5/weather?q=san cristobal&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #452 City Nameilloqqortoormiut
    http://api.openweathermap.org/data/2.5/weather?q=illoqqortoormiut&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #453 City Nametsihombe
    http://api.openweathermap.org/data/2.5/weather?q=tsihombe&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #454 City Namemataura
    http://api.openweathermap.org/data/2.5/weather?q=mataura&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #455 City Nameushuaia
    http://api.openweathermap.org/data/2.5/weather?q=ushuaia&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #456 City Namepisco
    http://api.openweathermap.org/data/2.5/weather?q=pisco&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #457 City Namemys shmidta
    http://api.openweathermap.org/data/2.5/weather?q=mys shmidta&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #458 City Namerikitea
    http://api.openweathermap.org/data/2.5/weather?q=rikitea&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #459 City Nameportland
    http://api.openweathermap.org/data/2.5/weather?q=portland&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #460 City Namepacific grove
    http://api.openweathermap.org/data/2.5/weather?q=pacific grove&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #461 City Nameribeira grande
    http://api.openweathermap.org/data/2.5/weather?q=ribeira grande&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #462 City Nameumzimvubu
    http://api.openweathermap.org/data/2.5/weather?q=umzimvubu&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #463 City Namepemangkat
    http://api.openweathermap.org/data/2.5/weather?q=pemangkat&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #464 City Namesan jose
    http://api.openweathermap.org/data/2.5/weather?q=san jose&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #465 City Namebluff
    http://api.openweathermap.org/data/2.5/weather?q=bluff&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #466 City Namealofi
    http://api.openweathermap.org/data/2.5/weather?q=alofi&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #467 City Namepevek
    http://api.openweathermap.org/data/2.5/weather?q=pevek&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #468 City Namekavieng
    http://api.openweathermap.org/data/2.5/weather?q=kavieng&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #469 City Namehobart
    http://api.openweathermap.org/data/2.5/weather?q=hobart&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #470 City Namenew norfolk
    http://api.openweathermap.org/data/2.5/weather?q=new norfolk&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #471 City Nametaolanaro
    http://api.openweathermap.org/data/2.5/weather?q=taolanaro&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #472 City Namehilo
    http://api.openweathermap.org/data/2.5/weather?q=hilo&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #473 City Namedole
    http://api.openweathermap.org/data/2.5/weather?q=dole&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #474 City Namecarnarvon
    http://api.openweathermap.org/data/2.5/weather?q=carnarvon&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #475 City Nameushuaia
    http://api.openweathermap.org/data/2.5/weather?q=ushuaia&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #476 City Namebambous virieux
    http://api.openweathermap.org/data/2.5/weather?q=bambous virieux&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #477 City Namegrafton
    http://api.openweathermap.org/data/2.5/weather?q=grafton&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #478 City Namecidreira
    http://api.openweathermap.org/data/2.5/weather?q=cidreira&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #479 City Nameport alfred
    http://api.openweathermap.org/data/2.5/weather?q=port alfred&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #480 City Nameport elizabeth
    http://api.openweathermap.org/data/2.5/weather?q=port elizabeth&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #481 City Nameguajara-mirim
    http://api.openweathermap.org/data/2.5/weather?q=guajara-mirim&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #482 City Nameluderitz
    http://api.openweathermap.org/data/2.5/weather?q=luderitz&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #483 City Namedenpasar
    http://api.openweathermap.org/data/2.5/weather?q=denpasar&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #484 City Nameushuaia
    http://api.openweathermap.org/data/2.5/weather?q=ushuaia&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #485 City Namepunta arenas
    http://api.openweathermap.org/data/2.5/weather?q=punta arenas&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #486 City Namesaint-philippe
    http://api.openweathermap.org/data/2.5/weather?q=saint-philippe&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #487 City Namebarrow
    http://api.openweathermap.org/data/2.5/weather?q=barrow&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #488 City Namegeorgetown
    http://api.openweathermap.org/data/2.5/weather?q=georgetown&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #489 City Namekropotkin
    http://api.openweathermap.org/data/2.5/weather?q=kropotkin&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #490 City Nameclaremore
    http://api.openweathermap.org/data/2.5/weather?q=claremore&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #491 City Namenadvoitsy
    http://api.openweathermap.org/data/2.5/weather?q=nadvoitsy&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #492 City Namehobart
    http://api.openweathermap.org/data/2.5/weather?q=hobart&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #493 City Namemalanje
    http://api.openweathermap.org/data/2.5/weather?q=malanje&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #494 City Namehamilton
    http://api.openweathermap.org/data/2.5/weather?q=hamilton&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #495 City Namejamestown
    http://api.openweathermap.org/data/2.5/weather?q=jamestown&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #496 City Nameharper
    http://api.openweathermap.org/data/2.5/weather?q=harper&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #497 City Nametaolanaro
    http://api.openweathermap.org/data/2.5/weather?q=taolanaro&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #498 City Nameneiafu
    http://api.openweathermap.org/data/2.5/weather?q=neiafu&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #499 City Nameitarema
    http://api.openweathermap.org/data/2.5/weather?q=itarema&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #500 City Nameaklavik
    http://api.openweathermap.org/data/2.5/weather?q=aklavik&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #501 City Namedikson
    http://api.openweathermap.org/data/2.5/weather?q=dikson&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #502 City Namejamestown
    http://api.openweathermap.org/data/2.5/weather?q=jamestown&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #503 City Namecarnarvon
    http://api.openweathermap.org/data/2.5/weather?q=carnarvon&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #504 City Namedingle
    http://api.openweathermap.org/data/2.5/weather?q=dingle&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #505 City Namebusselton
    http://api.openweathermap.org/data/2.5/weather?q=busselton&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #506 City Namealoleng
    http://api.openweathermap.org/data/2.5/weather?q=aloleng&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #507 City Namehasaki
    http://api.openweathermap.org/data/2.5/weather?q=hasaki&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Now retrieving city #508 City Namesamusu
    http://api.openweathermap.org/data/2.5/weather?q=samusu&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    Error with city data. Skipping
    Now retrieving city #509 City Nameprovideniya
    http://api.openweathermap.org/data/2.5/weather?q=provideniya&units=IMPERIAL&mode=json&APPID=62e6c158794571605e5f2b3046aa6eac
    


```python
############Below is to understand what is required to get the data from Dictionary, You can ignore###
#city_weather["main"]["temp"]
#city_weather["main"]["humidity"]
#city_weather["clouds"]["all"]
#city_weather["wind"]["speed"]
```


```python
# Visualize
selected_cities.replace('',np.nan,inplace=True)
selected_cities
selected_cities.dropna(axis=0,how='any')
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>lats</th>
      <th>lngs</th>
      <th>temp</th>
      <th>humidity%</th>
      <th>cloudiness%</th>
      <th>windspeed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>128</th>
      <td>ribeira grande</td>
      <td>33</td>
      <td>-32</td>
      <td>64.40</td>
      <td>88.0</td>
      <td>40.0</td>
      <td>12.75</td>
    </tr>
    <tr>
      <th>185</th>
      <td>leningradskiy</td>
      <td>81</td>
      <td>177</td>
      <td>8.71</td>
      <td>100.0</td>
      <td>88.0</td>
      <td>3.71</td>
    </tr>
    <tr>
      <th>75</th>
      <td>khatanga</td>
      <td>69</td>
      <td>99</td>
      <td>-34.45</td>
      <td>64.0</td>
      <td>0.0</td>
      <td>3.49</td>
    </tr>
    <tr>
      <th>179</th>
      <td>half moon bay</td>
      <td>35</td>
      <td>-129</td>
      <td>48.20</td>
      <td>66.0</td>
      <td>75.0</td>
      <td>4.70</td>
    </tr>
    <tr>
      <th>264</th>
      <td>qaanaaq</td>
      <td>78</td>
      <td>-84</td>
      <td>-11.46</td>
      <td>100.0</td>
      <td>0.0</td>
      <td>9.53</td>
    </tr>
    <tr>
      <th>299</th>
      <td>ushuaia</td>
      <td>-80</td>
      <td>-35</td>
      <td>53.60</td>
      <td>58.0</td>
      <td>75.0</td>
      <td>13.87</td>
    </tr>
    <tr>
      <th>28</th>
      <td>busselton</td>
      <td>-45</td>
      <td>92</td>
      <td>67.61</td>
      <td>100.0</td>
      <td>0.0</td>
      <td>18.21</td>
    </tr>
    <tr>
      <th>503</th>
      <td>nikolskoye</td>
      <td>48</td>
      <td>165</td>
      <td>30.20</td>
      <td>92.0</td>
      <td>90.0</td>
      <td>8.95</td>
    </tr>
    <tr>
      <th>448</th>
      <td>port alfred</td>
      <td>-67</td>
      <td>41</td>
      <td>68.60</td>
      <td>91.0</td>
      <td>88.0</td>
      <td>9.64</td>
    </tr>
    <tr>
      <th>98</th>
      <td>hermanus</td>
      <td>-80</td>
      <td>-4</td>
      <td>64.19</td>
      <td>70.0</td>
      <td>0.0</td>
      <td>2.59</td>
    </tr>
    <tr>
      <th>261</th>
      <td>auki</td>
      <td>-6</td>
      <td>163</td>
      <td>81.20</td>
      <td>30.0</td>
      <td>0.0</td>
      <td>10.42</td>
    </tr>
    <tr>
      <th>318</th>
      <td>los llanos de aridane</td>
      <td>26</td>
      <td>-20</td>
      <td>64.40</td>
      <td>59.0</td>
      <td>20.0</td>
      <td>8.05</td>
    </tr>
    <tr>
      <th>2</th>
      <td>busselton</td>
      <td>-56</td>
      <td>88</td>
      <td>67.61</td>
      <td>100.0</td>
      <td>0.0</td>
      <td>18.21</td>
    </tr>
    <tr>
      <th>537</th>
      <td>hithadhoo</td>
      <td>-4</td>
      <td>69</td>
      <td>82.78</td>
      <td>100.0</td>
      <td>68.0</td>
      <td>4.72</td>
    </tr>
    <tr>
      <th>352</th>
      <td>geraldton</td>
      <td>50</td>
      <td>-89</td>
      <td>6.80</td>
      <td>60.0</td>
      <td>75.0</td>
      <td>9.17</td>
    </tr>
    <tr>
      <th>469</th>
      <td>honiara</td>
      <td>-10</td>
      <td>158</td>
      <td>73.40</td>
      <td>88.0</td>
      <td>20.0</td>
      <td>3.36</td>
    </tr>
    <tr>
      <th>392</th>
      <td>lewiston</td>
      <td>46</td>
      <td>-117</td>
      <td>24.80</td>
      <td>85.0</td>
      <td>1.0</td>
      <td>6.93</td>
    </tr>
    <tr>
      <th>176</th>
      <td>airai</td>
      <td>14</td>
      <td>144</td>
      <td>69.10</td>
      <td>94.0</td>
      <td>68.0</td>
      <td>1.59</td>
    </tr>
    <tr>
      <th>443</th>
      <td>novyy urengoy</td>
      <td>68</td>
      <td>77</td>
      <td>17.71</td>
      <td>87.0</td>
      <td>80.0</td>
      <td>12.06</td>
    </tr>
    <tr>
      <th>271</th>
      <td>kupang</td>
      <td>-13</td>
      <td>122</td>
      <td>80.26</td>
      <td>100.0</td>
      <td>88.0</td>
      <td>5.91</td>
    </tr>
    <tr>
      <th>199</th>
      <td>albany</td>
      <td>-83</td>
      <td>94</td>
      <td>39.20</td>
      <td>86.0</td>
      <td>90.0</td>
      <td>6.93</td>
    </tr>
    <tr>
      <th>518</th>
      <td>chokurdakh</td>
      <td>86</td>
      <td>153</td>
      <td>-3.90</td>
      <td>78.0</td>
      <td>68.0</td>
      <td>14.12</td>
    </tr>
    <tr>
      <th>540</th>
      <td>buraydah</td>
      <td>28</td>
      <td>43</td>
      <td>60.80</td>
      <td>44.0</td>
      <td>20.0</td>
      <td>4.70</td>
    </tr>
    <tr>
      <th>480</th>
      <td>iki-burul</td>
      <td>45</td>
      <td>45</td>
      <td>26.60</td>
      <td>100.0</td>
      <td>92.0</td>
      <td>4.47</td>
    </tr>
    <tr>
      <th>453</th>
      <td>vaini</td>
      <td>-87</td>
      <td>-171</td>
      <td>64.01</td>
      <td>64.0</td>
      <td>0.0</td>
      <td>3.89</td>
    </tr>
    <tr>
      <th>76</th>
      <td>hobart</td>
      <td>-87</td>
      <td>145</td>
      <td>51.80</td>
      <td>71.0</td>
      <td>75.0</td>
      <td>10.29</td>
    </tr>
    <tr>
      <th>96</th>
      <td>benguela</td>
      <td>-13</td>
      <td>11</td>
      <td>75.31</td>
      <td>97.0</td>
      <td>48.0</td>
      <td>5.23</td>
    </tr>
    <tr>
      <th>238</th>
      <td>west linton</td>
      <td>56</td>
      <td>-3</td>
      <td>53.60</td>
      <td>93.0</td>
      <td>90.0</td>
      <td>21.92</td>
    </tr>
    <tr>
      <th>60</th>
      <td>manaus</td>
      <td>-3</td>
      <td>-60</td>
      <td>75.20</td>
      <td>94.0</td>
      <td>75.0</td>
      <td>4.70</td>
    </tr>
    <tr>
      <th>24</th>
      <td>riyadh</td>
      <td>21</td>
      <td>48</td>
      <td>62.60</td>
      <td>23.0</td>
      <td>0.0</td>
      <td>3.36</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>194</th>
      <td>grafton</td>
      <td>-30</td>
      <td>152</td>
      <td>65.63</td>
      <td>98.0</td>
      <td>0.0</td>
      <td>2.21</td>
    </tr>
    <tr>
      <th>334</th>
      <td>cidreira</td>
      <td>-38</td>
      <td>-41</td>
      <td>73.15</td>
      <td>100.0</td>
      <td>92.0</td>
      <td>5.73</td>
    </tr>
    <tr>
      <th>12</th>
      <td>port alfred</td>
      <td>-73</td>
      <td>42</td>
      <td>68.60</td>
      <td>91.0</td>
      <td>88.0</td>
      <td>9.64</td>
    </tr>
    <tr>
      <th>485</th>
      <td>port elizabeth</td>
      <td>-89</td>
      <td>37</td>
      <td>59.00</td>
      <td>82.0</td>
      <td>75.0</td>
      <td>8.05</td>
    </tr>
    <tr>
      <th>196</th>
      <td>luderitz</td>
      <td>-29</td>
      <td>1</td>
      <td>64.40</td>
      <td>68.0</td>
      <td>0.0</td>
      <td>24.16</td>
    </tr>
    <tr>
      <th>504</th>
      <td>denpasar</td>
      <td>-14</td>
      <td>113</td>
      <td>80.60</td>
      <td>83.0</td>
      <td>75.0</td>
      <td>14.99</td>
    </tr>
    <tr>
      <th>506</th>
      <td>ushuaia</td>
      <td>-72</td>
      <td>-70</td>
      <td>53.60</td>
      <td>58.0</td>
      <td>75.0</td>
      <td>13.87</td>
    </tr>
    <tr>
      <th>165</th>
      <td>punta arenas</td>
      <td>-59</td>
      <td>-77</td>
      <td>53.60</td>
      <td>54.0</td>
      <td>75.0</td>
      <td>34.45</td>
    </tr>
    <tr>
      <th>89</th>
      <td>saint-philippe</td>
      <td>-53</td>
      <td>67</td>
      <td>30.20</td>
      <td>92.0</td>
      <td>90.0</td>
      <td>11.41</td>
    </tr>
    <tr>
      <th>418</th>
      <td>barrow</td>
      <td>78</td>
      <td>-154</td>
      <td>67.97</td>
      <td>45.0</td>
      <td>0.0</td>
      <td>16.35</td>
    </tr>
    <tr>
      <th>446</th>
      <td>georgetown</td>
      <td>-2</td>
      <td>-12</td>
      <td>86.00</td>
      <td>55.0</td>
      <td>75.0</td>
      <td>16.11</td>
    </tr>
    <tr>
      <th>281</th>
      <td>kropotkin</td>
      <td>59</td>
      <td>115</td>
      <td>29.81</td>
      <td>95.0</td>
      <td>92.0</td>
      <td>5.91</td>
    </tr>
    <tr>
      <th>187</th>
      <td>claremore</td>
      <td>36</td>
      <td>-95</td>
      <td>37.40</td>
      <td>88.0</td>
      <td>75.0</td>
      <td>3.36</td>
    </tr>
    <tr>
      <th>322</th>
      <td>nadvoitsy</td>
      <td>64</td>
      <td>35</td>
      <td>20.36</td>
      <td>88.0</td>
      <td>88.0</td>
      <td>11.61</td>
    </tr>
    <tr>
      <th>251</th>
      <td>hobart</td>
      <td>-72</td>
      <td>145</td>
      <td>51.80</td>
      <td>71.0</td>
      <td>75.0</td>
      <td>10.29</td>
    </tr>
    <tr>
      <th>217</th>
      <td>malanje</td>
      <td>-10</td>
      <td>17</td>
      <td>70.90</td>
      <td>69.0</td>
      <td>12.0</td>
      <td>6.58</td>
    </tr>
    <tr>
      <th>219</th>
      <td>hamilton</td>
      <td>45</td>
      <td>-115</td>
      <td>71.60</td>
      <td>64.0</td>
      <td>75.0</td>
      <td>11.41</td>
    </tr>
    <tr>
      <th>252</th>
      <td>jamestown</td>
      <td>-28</td>
      <td>-19</td>
      <td>65.86</td>
      <td>45.0</td>
      <td>8.0</td>
      <td>8.63</td>
    </tr>
    <tr>
      <th>298</th>
      <td>harper</td>
      <td>5</td>
      <td>-8</td>
      <td>53.60</td>
      <td>40.0</td>
      <td>1.0</td>
      <td>4.56</td>
    </tr>
    <tr>
      <th>457</th>
      <td>neiafu</td>
      <td>-18</td>
      <td>-174</td>
      <td>77.00</td>
      <td>94.0</td>
      <td>75.0</td>
      <td>4.70</td>
    </tr>
    <tr>
      <th>233</th>
      <td>itarema</td>
      <td>1</td>
      <td>-39</td>
      <td>85.21</td>
      <td>66.0</td>
      <td>76.0</td>
      <td>15.79</td>
    </tr>
    <tr>
      <th>507</th>
      <td>aklavik</td>
      <td>70</td>
      <td>-140</td>
      <td>15.80</td>
      <td>85.0</td>
      <td>75.0</td>
      <td>9.17</td>
    </tr>
    <tr>
      <th>56</th>
      <td>dikson</td>
      <td>84</td>
      <td>90</td>
      <td>-1.51</td>
      <td>100.0</td>
      <td>76.0</td>
      <td>27.16</td>
    </tr>
    <tr>
      <th>22</th>
      <td>jamestown</td>
      <td>-50</td>
      <td>-14</td>
      <td>65.86</td>
      <td>45.0</td>
      <td>8.0</td>
      <td>8.63</td>
    </tr>
    <tr>
      <th>67</th>
      <td>carnarvon</td>
      <td>-26</td>
      <td>114</td>
      <td>70.49</td>
      <td>12.0</td>
      <td>0.0</td>
      <td>8.25</td>
    </tr>
    <tr>
      <th>317</th>
      <td>dingle</td>
      <td>53</td>
      <td>-14</td>
      <td>75.89</td>
      <td>96.0</td>
      <td>56.0</td>
      <td>5.39</td>
    </tr>
    <tr>
      <th>405</th>
      <td>busselton</td>
      <td>-87</td>
      <td>74</td>
      <td>67.61</td>
      <td>100.0</td>
      <td>0.0</td>
      <td>18.21</td>
    </tr>
    <tr>
      <th>366</th>
      <td>aloleng</td>
      <td>15</td>
      <td>116</td>
      <td>79.67</td>
      <td>92.0</td>
      <td>8.0</td>
      <td>3.89</td>
    </tr>
    <tr>
      <th>513</th>
      <td>hasaki</td>
      <td>22</td>
      <td>158</td>
      <td>32.00</td>
      <td>100.0</td>
      <td>75.0</td>
      <td>1.12</td>
    </tr>
    <tr>
      <th>476</th>
      <td>provideniya</td>
      <td>60</td>
      <td>-172</td>
      <td>30.44</td>
      <td>100.0</td>
      <td>88.0</td>
      <td>11.16</td>
    </tr>
  </tbody>
</table>
<p>464 rows × 7 columns</p>
</div>




```python
#

# Build a scatter plot for each data type
plt.scatter(selected_cities["lats"], selected_cities["temp"], color='b',edgecolor="black", linewidths=1, marker="o",s=100, alpha=1, label='City')
# Or we can use below syntax
#plt.plot('lats','temp',data=selected_cities,linestyle='none',marker='o')

# Incorporate the other graph properties
plt.title("Temperature(F) vs.Latitude - Data Analyzed on %s" %(time.strftime("%x")))
plt.ylabel("Temperature")
plt.xlabel("Latitude")
plt.grid(True)
plt.xlim([-90, 90])
plt.ylim([-20, 130])
plt.legend()

# Annotate with text + Arrow
plt.annotate(
# Label and coordinate
'Equator', xy=(0,0 ), xytext=(100, 80),
 
# Custom arrow
arrowprops=dict(facecolor='black', shrink=0.05
               )
)


# Save the figure
plt.savefig("city_weather_equator_temp.png")

# Show plot
plt.show()
```


![png](README_files/README_11_0.png)



```python
# Build a scatter plot for each data type
plt.scatter(selected_cities["lats"], selected_cities["humidity%"], color='b',edgecolor="black", linewidths=1, marker="o",s=100, alpha=1, label='City')

# Incorporate the other graph properties
plt.title("Humidity(Percent) vs.Latitude by City - Data Analyzed on %s" %(time.strftime("%x")))
plt.ylabel("Humidity(%)")
plt.xlabel("Latitude")
plt.grid(True)
plt.xlim([-90, 90])
plt.ylim([0,120])
plt.legend()

# Save the figure
plt.savefig("city_weather_equator_hum.png")

# Show plot
plt.show()
```


![png](README_files/README_12_0.png)



```python
# Build a scatter plot for each data type
plt.scatter(selected_cities["lats"], 
            selected_cities["cloudiness%"], color='b',
            edgecolor="black", linewidths=1, marker="o",s=100, alpha=1, label='City')

# Incorporate the other graph properties
plt.title("Cloudiness(Percent) vs.Latitude by City- Data Analyzed on %s" %(time.strftime("%x")))
plt.ylabel("Cloudiness(%)")
plt.xlabel("Latitude")
plt.grid(True)
plt.xlim([-90, 90])
plt.ylim([0, 105])
plt.legend()

# Save the figure
plt.savefig("city_weather_equator_cloud.png")

# Show plot
plt.show()
```


![png](README_files/README_13_0.png)



```python
# Build a scatter plot for each data type
plt.scatter(selected_cities["lats"], 
            selected_cities["windspeed"], color='b',
            edgecolor="black", linewidths=1, marker="o",s=100, alpha=1, label='City')

# Incorporate the other graph properties
plt.title("Wind Speed(mph) vs.Latitude by City - Data Analyzed on %s" %(time.strftime("%x")))
plt.ylabel("Wind Speed(mph)")
plt.xlabel("Latitude")
plt.grid(True)
plt.xlim([-90, 90])
plt.ylim([-10, 50])
plt.legend()

# Save the figure
plt.savefig("city_weather_equator_windspeed.png")

# Show plot
plt.show()
```


![png](README_files/README_14_0.png)



```python



```
