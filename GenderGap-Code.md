
# GLOBAL GENDER GAP RANKING - 2006-2016

The analysis below is being prepared by the dataset provided by 1 Million Women to Tech at https://github.com/1mwtt-wod1/gender-gap-datathon.

The dataset is compiled and/or recorded by World Economic Forum (WEF) to measure Global Gender Gap in countries (http://www3.weforum.org/docs/WEF_GenderGap_Report_2006.pdf). The dataset has four subindexes; Global Gender Gap Economic Participation and Opportunity, Global Gender Gap Educational Attainment, Global Gender Gap Health and Survival and Global Gender Gap Political Empowerment in addition to Overall Global Gender Gap index. In 2016, a new subindex measuring Wage equality between women and men for similar work is also added to the dataset. 

In 2016, a new methodology was added in the second Global Gender Gap Report to capture the size of the gap more efficiently. Here is a short excerpt from that report that we would like to include in this report: 

<i>"One particular societal and economic challenge is the persistent gap between women and men in their access to resources and opportunities.This gap not only undermines the quality of life of one half of the world’s population but also poses a significant risk to the long-term growth and well-being of nations: countries that do not capitalize on the full potential of one half of their human resources may compromise their competitive potential.(http://www3.weforum.org/docs/WEF_GenderGap_Report_2006.pdf)</i>

There are many positive steps taken by many entities around the world. In 2010, United Nations General Assembly founded UN Women to address issues that women are facing. In 2014, UN Women launched He for She, a global campaing to include men in the gender equality dicsussions, as well. For UN Women, please go to http://www.unwomen.org/en/about-us/about-un-women and for the He for She website please go to https://www.heforshe.org/en. 

In this report, we will focus on improvements and positive changes in the ranking of countries between the years 2006 and 2016. After providing some information about the ranking in the world, we will look at countries who improved their rank significantly. We will define improving rank concept in three different ways: The first one compares overall gender gap ranks between 2006 and 2016 only. After creating a dataframe, we will look at the top three countries who improved their ranking the most.

Looking at the difference in ranks between 2006 and 2016 is very useful to determine the countries who improved their ranking. However, a quick examination of the dataset shows that ranks of many countries fluctuated a lot during the years 2006 to 2016. A countries rank might be improved significantly but then rank might get worse during recent years. So, to find the factors influencing the ranking, we will look at the maximum positive difference occurred between successsive years during 2006-2016. We will create a new column by comparing ranks of successive years and then recording the max positive difference between successive years in a new column. In addition, the years when the max difference occured are also coded in another newly created column. After sorting the dataset according to the max difference column, we will look at Top 3 countries who impoved their overall rank the most according to this criteria.

Lastly, we will look at how many times a country improved their rank or preserved their rank between 2006-2016. This might give us information about countries' effort in improving or preserving their ranks and whether these changes were temporary or have long-lasting effects.

Among the research problems explored are

<ol>
<li> Are there any differences in the general trend in the overall ranking between recent years and the years when WEF started measuring and publishing their findings?</li> 
<li> What are the similarities and differences in the Top 20 countries in 2016? </li>
<li> When we compare overall ranks of countries in 2006 and 2016, which countries improved their rank the most? What are the factors influencing these improvements in the Top 3 countries when the dataset is sorted according to this criteria?</li>
<li> When we compare overall ranks of countries in successive years, which countries improved their rank the most and when does that improvement happened? What are the factors influencing these improvements in the Top 3 countries when the dataset is sorted according to this criteria?</li>
<li> Which countries improved their overall rank or preserved their rank the most between 2006-2016? What are the factors influencing these improvements in the Top 3 countries when the dataset is sorted according to this criteria?</li>
</ol>




```python
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
import plotly
import plotly.graph_objs as go
from plotly.offline import init_notebook_mode, plot, iplot
from plotly import tools

init_notebook_mode(connected=True)  #to start offline plotly

gender=pd.read_csv('globalgendergap2016.csv')
gender1=gender[gender["Subindicator Type"]=="Rank"]
ranking=gender1[gender1["Indicator"]=="Overall Global Gender Gap Index"]

ranking.head()
```


<script>requirejs.config({paths: { 'plotly': ['https://cdn.plot.ly/plotly-latest.min']},});if(!window.Plotly) {{require(['plotly'],function(plotly) {window.Plotly=plotly;});}}</script>





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Country ISO3</th>
      <th>Country Name</th>
      <th>Indicator</th>
      <th>Subindicator Type</th>
      <th>2006</th>
      <th>2007</th>
      <th>2008</th>
      <th>2009</th>
      <th>2010</th>
      <th>2011</th>
      <th>2012</th>
      <th>2013</th>
      <th>2014</th>
      <th>2015</th>
      <th>2016</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>9</th>
      <td>AGO</td>
      <td>Angola</td>
      <td>Overall Global Gender Gap Index</td>
      <td>Rank</td>
      <td>96.0</td>
      <td>110.0</td>
      <td>114.0</td>
      <td>106.0</td>
      <td>81.0</td>
      <td>87.0</td>
      <td>NaN</td>
      <td>92.0</td>
      <td>121.0</td>
      <td>126.0</td>
      <td>117.0</td>
    </tr>
    <tr>
      <th>22</th>
      <td>ALB</td>
      <td>Albania</td>
      <td>Overall Global Gender Gap Index</td>
      <td>Rank</td>
      <td>61.0</td>
      <td>66.0</td>
      <td>87.0</td>
      <td>91.0</td>
      <td>78.0</td>
      <td>78.0</td>
      <td>91.0</td>
      <td>108.0</td>
      <td>83.0</td>
      <td>70.0</td>
      <td>62.0</td>
    </tr>
    <tr>
      <th>35</th>
      <td>ARE</td>
      <td>United Arab Emirates</td>
      <td>Overall Global Gender Gap Index</td>
      <td>Rank</td>
      <td>101.0</td>
      <td>105.0</td>
      <td>105.0</td>
      <td>112.0</td>
      <td>103.0</td>
      <td>103.0</td>
      <td>107.0</td>
      <td>109.0</td>
      <td>115.0</td>
      <td>119.0</td>
      <td>124.0</td>
    </tr>
    <tr>
      <th>48</th>
      <td>ARG</td>
      <td>Argentina</td>
      <td>Overall Global Gender Gap Index</td>
      <td>Rank</td>
      <td>41.0</td>
      <td>33.0</td>
      <td>24.0</td>
      <td>24.0</td>
      <td>29.0</td>
      <td>28.0</td>
      <td>32.0</td>
      <td>34.0</td>
      <td>31.0</td>
      <td>35.0</td>
      <td>33.0</td>
    </tr>
    <tr>
      <th>61</th>
      <td>ARM</td>
      <td>Armenia</td>
      <td>Overall Global Gender Gap Index</td>
      <td>Rank</td>
      <td>NaN</td>
      <td>71.0</td>
      <td>78.0</td>
      <td>90.0</td>
      <td>84.0</td>
      <td>84.0</td>
      <td>92.0</td>
      <td>94.0</td>
      <td>103.0</td>
      <td>105.0</td>
      <td>102.0</td>
    </tr>
  </tbody>
</table>
</div>



From now on, we will be working with this dataset including overall rankings only. This report is organized as follows: In Section 1, we will be looking at some general ... about the ranking of all countries. In Section 2, we will try to answer some specific questions. For this, we will create new datasets with some new comparison tools. After that, we will focus on countries that are on top of those lists and try to find out more about their ranking and factors influencing their ranking. We will try to support our findings with external .... In Section 3, some conclusions will be stated in addition to the problems and issues that we encountered in this analysis. Future directions and interesting related topics will be explored, as well.


# Section 1: General Information

## Comparison of data related to different years

In the plots below, we will compare the ranking of countries in 2016(the last year in the dataset) with the ranking in 2006 to explore the differences between two datasets. We believe that this would provide a general overview of the ranking of countries.


```python
colors=['red','darkred','green','darkgreen']
years=['2006','2007','2014','2015']

f=tools.make_subplots(rows=2,cols=2,
                      subplot_titles=('2006 vs 2016','2007 vs 2016','2014 vs 2016','2015 vs 2016'))

for i in range(0,4):
    if i<2:
        scatter=go.Scatter(dict(x=ranking[years[i]], 
                   y=ranking['2016'], 
                   marker=dict(color=colors[i]),
                   text=ranking['Country Name'],
                   name=years[i]+' vs 2016', 
                   mode='markers'))
        f.append_trace(scatter,1,i+1)
    if 2<=i<4:
        scatter=go.Scatter(dict(x=ranking[years[i]], 
                   y=ranking['2016'], 
                   marker=dict(color=colors[i]),
                   text=ranking['Country Name'],
                   name=years[i]+' vs 2016', 
                   mode='markers'))
        f.append_trace(scatter,2,i-1)


f['layout'].update(dict(title='Overall Global Gender Gap Rank'),showlegend=False)
iplot(f)


```

    This is the format of your plot grid:
    [ (1,1) x1,y1 ]  [ (1,2) x2,y2 ]
    [ (2,1) x3,y3 ]  [ (2,2) x4,y4 ]
    
    


<div id="2107ee0f-5a92-46dc-924a-1f7f2c7daa18" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("2107ee0f-5a92-46dc-924a-1f7f2c7daa18", [{"type": "scatter", "x": [96.0, 61.0, 101.0, 41.0, null, 15.0, 27.0, null, null, 20.0, 110.0, 104.0, 91.0, 37.0, 102.0, null, null, null, null, 87.0, 67.0, null, null, null, 34.0, 14.0, 26.0, 78.0, 63.0, null, 103.0, 22.0, null, 30.0, null, 83.0, 53.0, 5.0, 8.0, 59.0, 97.0, 82.0, 109.0, 11.0, 29.0, 100.0, 3.0, null, 70.0, 9.0, 54.0, 58.0, null, 80.0, 69.0, 95.0, null, 74.0, 16.0, 55.0, 68.0, 98.0, 10.0, 108.0, 4.0, 35.0, 77.0, 25.0, 93.0, 79.0, 32.0, 73.0, 52.0, 89.0, 92.0, 86.0, null, null, null, 13.0, 43.0, 21.0, 56.0, 19.0, 107.0, 17.0, 84.0, null, 75.0, 28.0, 99.0, 71.0, null, 42.0, null, 106.0, 88.0, 81.0, 72.0, 38.0, 94.0, 62.0, 12.0, 2.0, 111.0, 7.0, null, 112.0, 31.0, 60.0, 6.0, 44.0, 33.0, 64.0, null, 46.0, 49.0, null, 114.0, null, 65.0, 39.0, null, null, 50.0, 51.0, 1.0, null, null, 113.0, 40.0, null, null, 45.0, 90.0, 105.0, 24.0, 47.0, 48.0, 66.0, 23.0, 36.0, 57.0, null, 115.0, 18.0, 85.0, 76.0], "y": [117.0, 62.0, 124.0, 33.0, 102.0, 46.0, 52.0, 86.0, 12.0, 24.0, 127.0, 123.0, 72.0, 41.0, 131.0, 37.0, 83.0, 30.0, 98.0, 23.0, 79.0, 28.0, 103.0, 121.0, 54.0, 35.0, 11.0, 70.0, 99.0, 136.0, 85.0, 39.0, 36.0, 32.0, 27.0, 84.0, 77.0, 13.0, 19.0, 97.0, 120.0, 40.0, 132.0, 29.0, 22.0, 109.0, 2.0, null, 17.0, 20.0, 90.0, 59.0, 122.0, 104.0, 92.0, 105.0, null, 78.0, 68.0, 101.0, 88.0, 87.0, 6.0, 139.0, 1.0, 49.0, 50.0, 42.0, 134.0, 111.0, 51.0, 63.0, 81.0, 112.0, 116.0, 128.0, 43.0, 135.0, 114.0, 100.0, 57.0, 25.0, 34.0, 18.0, 137.0, 26.0, 60.0, 115.0, 66.0, 73.0, 138.0, 108.0, 89.0, 58.0, 21.0, 129.0, 113.0, 67.0, 106.0, 14.0, 118.0, 10.0, 16.0, 3.0, 110.0, 9.0, 133.0, 143.0, 47.0, 80.0, 7.0, 38.0, 31.0, 96.0, 119.0, 76.0, 75.0, 5.0, 141.0, 82.0, 55.0, 64.0, 48.0, 95.0, 94.0, 8.0, 4.0, 107.0, 142.0, 140.0, 71.0, 93.0, 125.0, 44.0, 126.0, 130.0, 53.0, 61.0, 69.0, 91.0, 45.0, null, 74.0, 65.0, 144.0, 15.0, null, 56.0], "marker": {"color": "red"}, "text": ["Angola", "Albania", "United Arab Emirates", "Argentina", "Armenia", "Australia", "Austria", "Azerbaijan", "Burundi", "Belgium", "Benin", "Burkina Faso", "Bangladesh", "Bulgaria", "Bahrain", "Bahamas, The", "Bosnia and Herzegovina", "Belarus", "Belize", "Bolivia", "Brazil", "Barbados", "Brunei Darussalam", "Bhutan", "Botswana", "Canada", "Switzerland", "Chile", "China", "Cote d'Ivoire", "Cameroon", "Colombia", "Cabo Verde", "Costa Rica", "Cuba", "Cyprus", "Czech Republic", "Germany", "Denmark", "Dominican Republic", "Algeria", "Ecuador", "Egypt, Arab Rep.", "Spain", "Estonia", "Ethiopia", "Finland", "Fiji", "France", "United Kingdom", "Georgia", "Ghana", "Guinea", "Gambia, The", "Greece", "Guatemala", "Guyana", "Honduras", "Croatia", "Hungary", "Indonesia", "India", "Ireland", "Iran, Islamic Rep.", "Iceland", "Israel", "Italy", "Jamaica", "Jordan", "Japan", "Kazakhstan", "Kenya", "Kyrgyz Republic", "Cambodia", "Korea, Rep.", "Kuwait", "Lao PDR", "Lebanon", "Liberia", "Sri Lanka", "Lesotho", "Lithuania", "Luxembourg", "Latvia", "Morocco", "Moldova", "Madagascar", "Maldives", "Mexico", "Macedonia, FYR", "Mali", "Malta", "Montenegro", "Mongolia", "Mozambique", "Mauritania", "Mauritius", "Malawi", "Malaysia", "Namibia", "Nigeria", "Nicaragua", "Netherlands", "Norway", "Nepal", "New Zealand", "Oman", "Pakistan", "Panama", "Peru", "Philippines", "Poland", "Portugal", "Paraguay", "Qatar", "Romania", "Russian Federation", "Rwanda", "Saudi Arabia", "Senegal", "Singapore", "El Salvador", "Serbia", "Suriname", "Slovak Republic", "Slovenia", "Sweden", "Swaziland", "Syrian Arab Republic", "Chad", "Thailand", "Tajikistan", "Timor-Leste", "Trinidad and Tobago", "Tunisia", "Turkey", "Tanzania", "Uganda", "Ukraine", "Uruguay", "United States", "Uzbekistan", "Venezuela, RB", "Vietnam", "Yemen, Rep.", "South Africa", "Zambia", "Zimbabwe"], "name": "2006 vs 2016", "mode": "markers", "xaxis": "x1", "yaxis": "y1"}, {"type": "scatter", "x": [110.0, 66.0, 105.0, 33.0, 71.0, 17.0, 27.0, 59.0, null, 19.0, 123.0, 117.0, 100.0, 25.0, 115.0, null, null, 23.0, 94.0, 80.0, 74.0, null, null, null, 53.0, 18.0, 40.0, 86.0, 73.0, null, 116.0, 24.0, null, 28.0, 22.0, 82.0, 64.0, 7.0, 8.0, 65.0, 108.0, 44.0, 120.0, 10.0, 30.0, 113.0, 3.0, null, 51.0, 11.0, 67.0, 63.0, null, 95.0, 72.0, 106.0, null, 68.0, 16.0, 61.0, 81.0, 114.0, 9.0, 118.0, 4.0, 36.0, 84.0, 39.0, 104.0, 91.0, 32.0, 83.0, 70.0, 98.0, 97.0, 96.0, null, null, null, 15.0, 26.0, 14.0, 58.0, 13.0, 122.0, 21.0, 89.0, 99.0, 93.0, 35.0, 112.0, 76.0, null, 62.0, 43.0, 111.0, 85.0, 87.0, 92.0, 29.0, 107.0, 90.0, 12.0, 2.0, 125.0, 5.0, 119.0, 126.0, 38.0, 75.0, 6.0, 60.0, 37.0, 69.0, 109.0, 47.0, 45.0, null, 124.0, null, 77.0, 48.0, null, 56.0, 54.0, 49.0, 1.0, null, 103.0, 127.0, 52.0, 79.0, null, 46.0, 102.0, 121.0, 34.0, 50.0, 57.0, 78.0, 31.0, 41.0, 55.0, 42.0, 128.0, 20.0, 101.0, 88.0], "y": [117.0, 62.0, 124.0, 33.0, 102.0, 46.0, 52.0, 86.0, 12.0, 24.0, 127.0, 123.0, 72.0, 41.0, 131.0, 37.0, 83.0, 30.0, 98.0, 23.0, 79.0, 28.0, 103.0, 121.0, 54.0, 35.0, 11.0, 70.0, 99.0, 136.0, 85.0, 39.0, 36.0, 32.0, 27.0, 84.0, 77.0, 13.0, 19.0, 97.0, 120.0, 40.0, 132.0, 29.0, 22.0, 109.0, 2.0, null, 17.0, 20.0, 90.0, 59.0, 122.0, 104.0, 92.0, 105.0, null, 78.0, 68.0, 101.0, 88.0, 87.0, 6.0, 139.0, 1.0, 49.0, 50.0, 42.0, 134.0, 111.0, 51.0, 63.0, 81.0, 112.0, 116.0, 128.0, 43.0, 135.0, 114.0, 100.0, 57.0, 25.0, 34.0, 18.0, 137.0, 26.0, 60.0, 115.0, 66.0, 73.0, 138.0, 108.0, 89.0, 58.0, 21.0, 129.0, 113.0, 67.0, 106.0, 14.0, 118.0, 10.0, 16.0, 3.0, 110.0, 9.0, 133.0, 143.0, 47.0, 80.0, 7.0, 38.0, 31.0, 96.0, 119.0, 76.0, 75.0, 5.0, 141.0, 82.0, 55.0, 64.0, 48.0, 95.0, 94.0, 8.0, 4.0, 107.0, 142.0, 140.0, 71.0, 93.0, 125.0, 44.0, 126.0, 130.0, 53.0, 61.0, 69.0, 91.0, 45.0, null, 74.0, 65.0, 144.0, 15.0, null, 56.0], "marker": {"color": "darkred"}, "text": ["Angola", "Albania", "United Arab Emirates", "Argentina", "Armenia", "Australia", "Austria", "Azerbaijan", "Burundi", "Belgium", "Benin", "Burkina Faso", "Bangladesh", "Bulgaria", "Bahrain", "Bahamas, The", "Bosnia and Herzegovina", "Belarus", "Belize", "Bolivia", "Brazil", "Barbados", "Brunei Darussalam", "Bhutan", "Botswana", "Canada", "Switzerland", "Chile", "China", "Cote d'Ivoire", "Cameroon", "Colombia", "Cabo Verde", "Costa Rica", "Cuba", "Cyprus", "Czech Republic", "Germany", "Denmark", "Dominican Republic", "Algeria", "Ecuador", "Egypt, Arab Rep.", "Spain", "Estonia", "Ethiopia", "Finland", "Fiji", "France", "United Kingdom", "Georgia", "Ghana", "Guinea", "Gambia, The", "Greece", "Guatemala", "Guyana", "Honduras", "Croatia", "Hungary", "Indonesia", "India", "Ireland", "Iran, Islamic Rep.", "Iceland", "Israel", "Italy", "Jamaica", "Jordan", "Japan", "Kazakhstan", "Kenya", "Kyrgyz Republic", "Cambodia", "Korea, Rep.", "Kuwait", "Lao PDR", "Lebanon", "Liberia", "Sri Lanka", "Lesotho", "Lithuania", "Luxembourg", "Latvia", "Morocco", "Moldova", "Madagascar", "Maldives", "Mexico", "Macedonia, FYR", "Mali", "Malta", "Montenegro", "Mongolia", "Mozambique", "Mauritania", "Mauritius", "Malawi", "Malaysia", "Namibia", "Nigeria", "Nicaragua", "Netherlands", "Norway", "Nepal", "New Zealand", "Oman", "Pakistan", "Panama", "Peru", "Philippines", "Poland", "Portugal", "Paraguay", "Qatar", "Romania", "Russian Federation", "Rwanda", "Saudi Arabia", "Senegal", "Singapore", "El Salvador", "Serbia", "Suriname", "Slovak Republic", "Slovenia", "Sweden", "Swaziland", "Syrian Arab Republic", "Chad", "Thailand", "Tajikistan", "Timor-Leste", "Trinidad and Tobago", "Tunisia", "Turkey", "Tanzania", "Uganda", "Ukraine", "Uruguay", "United States", "Uzbekistan", "Venezuela, RB", "Vietnam", "Yemen, Rep.", "South Africa", "Zambia", "Zimbabwe"], "name": "2007 vs 2016", "mode": "markers", "xaxis": "x2", "yaxis": "y2"}, {"type": "scatter", "x": [121.0, 83.0, 115.0, 31.0, 103.0, 24.0, 36.0, 94.0, 17.0, 10.0, null, 110.0, 68.0, 22.0, 124.0, 35.0, null, 32.0, 100.0, 58.0, 71.0, 33.0, 98.0, 120.0, 51.0, 19.0, 11.0, 66.0, 87.0, 136.0, null, 53.0, 50.0, 48.0, 30.0, 95.0, 96.0, 12.0, 5.0, 78.0, 126.0, 21.0, 129.0, 29.0, 62.0, 127.0, 2.0, 122.0, 16.0, 26.0, 85.0, 101.0, 132.0, null, 91.0, 89.0, 64.0, 73.0, 55.0, 93.0, 97.0, 114.0, 8.0, 137.0, 1.0, 65.0, 69.0, 52.0, 134.0, 104.0, 43.0, 37.0, 67.0, 108.0, 117.0, 113.0, 60.0, 135.0, 111.0, 79.0, 38.0, 44.0, 28.0, 15.0, 133.0, 25.0, 41.0, 105.0, 80.0, 70.0, 138.0, 99.0, 74.0, 42.0, 27.0, 131.0, 106.0, 34.0, 107.0, 40.0, 118.0, 6.0, 14.0, 3.0, 112.0, 13.0, 128.0, 141.0, 46.0, 45.0, 9.0, 57.0, 39.0, 81.0, 116.0, 72.0, 75.0, 7.0, 130.0, 77.0, 59.0, 84.0, 54.0, 109.0, 90.0, 23.0, 4.0, 92.0, 139.0, 140.0, 61.0, 102.0, null, 49.0, 123.0, 125.0, 47.0, 88.0, 56.0, 82.0, 20.0, null, 86.0, 76.0, 142.0, 18.0, 119.0, 63.0], "y": [117.0, 62.0, 124.0, 33.0, 102.0, 46.0, 52.0, 86.0, 12.0, 24.0, 127.0, 123.0, 72.0, 41.0, 131.0, 37.0, 83.0, 30.0, 98.0, 23.0, 79.0, 28.0, 103.0, 121.0, 54.0, 35.0, 11.0, 70.0, 99.0, 136.0, 85.0, 39.0, 36.0, 32.0, 27.0, 84.0, 77.0, 13.0, 19.0, 97.0, 120.0, 40.0, 132.0, 29.0, 22.0, 109.0, 2.0, null, 17.0, 20.0, 90.0, 59.0, 122.0, 104.0, 92.0, 105.0, null, 78.0, 68.0, 101.0, 88.0, 87.0, 6.0, 139.0, 1.0, 49.0, 50.0, 42.0, 134.0, 111.0, 51.0, 63.0, 81.0, 112.0, 116.0, 128.0, 43.0, 135.0, 114.0, 100.0, 57.0, 25.0, 34.0, 18.0, 137.0, 26.0, 60.0, 115.0, 66.0, 73.0, 138.0, 108.0, 89.0, 58.0, 21.0, 129.0, 113.0, 67.0, 106.0, 14.0, 118.0, 10.0, 16.0, 3.0, 110.0, 9.0, 133.0, 143.0, 47.0, 80.0, 7.0, 38.0, 31.0, 96.0, 119.0, 76.0, 75.0, 5.0, 141.0, 82.0, 55.0, 64.0, 48.0, 95.0, 94.0, 8.0, 4.0, 107.0, 142.0, 140.0, 71.0, 93.0, 125.0, 44.0, 126.0, 130.0, 53.0, 61.0, 69.0, 91.0, 45.0, null, 74.0, 65.0, 144.0, 15.0, null, 56.0], "marker": {"color": "green"}, "text": ["Angola", "Albania", "United Arab Emirates", "Argentina", "Armenia", "Australia", "Austria", "Azerbaijan", "Burundi", "Belgium", "Benin", "Burkina Faso", "Bangladesh", "Bulgaria", "Bahrain", "Bahamas, The", "Bosnia and Herzegovina", "Belarus", "Belize", "Bolivia", "Brazil", "Barbados", "Brunei Darussalam", "Bhutan", "Botswana", "Canada", "Switzerland", "Chile", "China", "Cote d'Ivoire", "Cameroon", "Colombia", "Cabo Verde", "Costa Rica", "Cuba", "Cyprus", "Czech Republic", "Germany", "Denmark", "Dominican Republic", "Algeria", "Ecuador", "Egypt, Arab Rep.", "Spain", "Estonia", "Ethiopia", "Finland", "Fiji", "France", "United Kingdom", "Georgia", "Ghana", "Guinea", "Gambia, The", "Greece", "Guatemala", "Guyana", "Honduras", "Croatia", "Hungary", "Indonesia", "India", "Ireland", "Iran, Islamic Rep.", "Iceland", "Israel", "Italy", "Jamaica", "Jordan", "Japan", "Kazakhstan", "Kenya", "Kyrgyz Republic", "Cambodia", "Korea, Rep.", "Kuwait", "Lao PDR", "Lebanon", "Liberia", "Sri Lanka", "Lesotho", "Lithuania", "Luxembourg", "Latvia", "Morocco", "Moldova", "Madagascar", "Maldives", "Mexico", "Macedonia, FYR", "Mali", "Malta", "Montenegro", "Mongolia", "Mozambique", "Mauritania", "Mauritius", "Malawi", "Malaysia", "Namibia", "Nigeria", "Nicaragua", "Netherlands", "Norway", "Nepal", "New Zealand", "Oman", "Pakistan", "Panama", "Peru", "Philippines", "Poland", "Portugal", "Paraguay", "Qatar", "Romania", "Russian Federation", "Rwanda", "Saudi Arabia", "Senegal", "Singapore", "El Salvador", "Serbia", "Suriname", "Slovak Republic", "Slovenia", "Sweden", "Swaziland", "Syrian Arab Republic", "Chad", "Thailand", "Tajikistan", "Timor-Leste", "Trinidad and Tobago", "Tunisia", "Turkey", "Tanzania", "Uganda", "Ukraine", "Uruguay", "United States", "Uzbekistan", "Venezuela, RB", "Vietnam", "Yemen, Rep.", "South Africa", "Zambia", "Zimbabwe"], "name": "2014 vs 2016", "mode": "markers", "xaxis": "x3", "yaxis": "y3"}, {"type": "scatter", "x": [126.0, 70.0, 119.0, 35.0, 105.0, 36.0, 37.0, 96.0, 23.0, 19.0, 129.0, 114.0, 64.0, 43.0, 123.0, 40.0, null, 34.0, 103.0, 22.0, 85.0, 24.0, 88.0, 118.0, 55.0, 30.0, 8.0, 73.0, 91.0, 133.0, 90.0, 42.0, 50.0, 38.0, 29.0, 100.0, 81.0, 11.0, 14.0, 86.0, 128.0, 33.0, 136.0, 25.0, 21.0, 124.0, 3.0, 121.0, 15.0, 18.0, 82.0, 63.0, 131.0, 98.0, 87.0, 106.0, 66.0, 80.0, 59.0, 99.0, 92.0, 108.0, 5.0, 141.0, 1.0, 53.0, 41.0, 65.0, 140.0, 101.0, 47.0, 48.0, 76.0, 109.0, 115.0, 117.0, 52.0, 138.0, 112.0, 84.0, 61.0, 31.0, 32.0, 20.0, 139.0, 26.0, 74.0, 113.0, 71.0, 69.0, 137.0, 104.0, 79.0, 56.0, 27.0, 132.0, 120.0, 68.0, 111.0, 16.0, 125.0, 12.0, 13.0, 2.0, 110.0, 10.0, 135.0, 144.0, 44.0, 89.0, 7.0, 51.0, 39.0, 107.0, 122.0, 77.0, 75.0, 6.0, 134.0, 72.0, 54.0, 62.0, 45.0, 94.0, 97.0, 9.0, 4.0, 102.0, 143.0, 142.0, 60.0, 95.0, null, 46.0, 127.0, 130.0, 49.0, 58.0, 67.0, 93.0, 28.0, null, 78.0, 83.0, 145.0, 17.0, 116.0, 57.0], "y": [117.0, 62.0, 124.0, 33.0, 102.0, 46.0, 52.0, 86.0, 12.0, 24.0, 127.0, 123.0, 72.0, 41.0, 131.0, 37.0, 83.0, 30.0, 98.0, 23.0, 79.0, 28.0, 103.0, 121.0, 54.0, 35.0, 11.0, 70.0, 99.0, 136.0, 85.0, 39.0, 36.0, 32.0, 27.0, 84.0, 77.0, 13.0, 19.0, 97.0, 120.0, 40.0, 132.0, 29.0, 22.0, 109.0, 2.0, null, 17.0, 20.0, 90.0, 59.0, 122.0, 104.0, 92.0, 105.0, null, 78.0, 68.0, 101.0, 88.0, 87.0, 6.0, 139.0, 1.0, 49.0, 50.0, 42.0, 134.0, 111.0, 51.0, 63.0, 81.0, 112.0, 116.0, 128.0, 43.0, 135.0, 114.0, 100.0, 57.0, 25.0, 34.0, 18.0, 137.0, 26.0, 60.0, 115.0, 66.0, 73.0, 138.0, 108.0, 89.0, 58.0, 21.0, 129.0, 113.0, 67.0, 106.0, 14.0, 118.0, 10.0, 16.0, 3.0, 110.0, 9.0, 133.0, 143.0, 47.0, 80.0, 7.0, 38.0, 31.0, 96.0, 119.0, 76.0, 75.0, 5.0, 141.0, 82.0, 55.0, 64.0, 48.0, 95.0, 94.0, 8.0, 4.0, 107.0, 142.0, 140.0, 71.0, 93.0, 125.0, 44.0, 126.0, 130.0, 53.0, 61.0, 69.0, 91.0, 45.0, null, 74.0, 65.0, 144.0, 15.0, null, 56.0], "marker": {"color": "darkgreen"}, "text": ["Angola", "Albania", "United Arab Emirates", "Argentina", "Armenia", "Australia", "Austria", "Azerbaijan", "Burundi", "Belgium", "Benin", "Burkina Faso", "Bangladesh", "Bulgaria", "Bahrain", "Bahamas, The", "Bosnia and Herzegovina", "Belarus", "Belize", "Bolivia", "Brazil", "Barbados", "Brunei Darussalam", "Bhutan", "Botswana", "Canada", "Switzerland", "Chile", "China", "Cote d'Ivoire", "Cameroon", "Colombia", "Cabo Verde", "Costa Rica", "Cuba", "Cyprus", "Czech Republic", "Germany", "Denmark", "Dominican Republic", "Algeria", "Ecuador", "Egypt, Arab Rep.", "Spain", "Estonia", "Ethiopia", "Finland", "Fiji", "France", "United Kingdom", "Georgia", "Ghana", "Guinea", "Gambia, The", "Greece", "Guatemala", "Guyana", "Honduras", "Croatia", "Hungary", "Indonesia", "India", "Ireland", "Iran, Islamic Rep.", "Iceland", "Israel", "Italy", "Jamaica", "Jordan", "Japan", "Kazakhstan", "Kenya", "Kyrgyz Republic", "Cambodia", "Korea, Rep.", "Kuwait", "Lao PDR", "Lebanon", "Liberia", "Sri Lanka", "Lesotho", "Lithuania", "Luxembourg", "Latvia", "Morocco", "Moldova", "Madagascar", "Maldives", "Mexico", "Macedonia, FYR", "Mali", "Malta", "Montenegro", "Mongolia", "Mozambique", "Mauritania", "Mauritius", "Malawi", "Malaysia", "Namibia", "Nigeria", "Nicaragua", "Netherlands", "Norway", "Nepal", "New Zealand", "Oman", "Pakistan", "Panama", "Peru", "Philippines", "Poland", "Portugal", "Paraguay", "Qatar", "Romania", "Russian Federation", "Rwanda", "Saudi Arabia", "Senegal", "Singapore", "El Salvador", "Serbia", "Suriname", "Slovak Republic", "Slovenia", "Sweden", "Swaziland", "Syrian Arab Republic", "Chad", "Thailand", "Tajikistan", "Timor-Leste", "Trinidad and Tobago", "Tunisia", "Turkey", "Tanzania", "Uganda", "Ukraine", "Uruguay", "United States", "Uzbekistan", "Venezuela, RB", "Vietnam", "Yemen, Rep.", "South Africa", "Zambia", "Zimbabwe"], "name": "2015 vs 2016", "mode": "markers", "xaxis": "x4", "yaxis": "y4"}], {"xaxis1": {"domain": [0.0, 0.45], "anchor": "y1"}, "yaxis1": {"domain": [0.625, 1.0], "anchor": "x1"}, "xaxis2": {"domain": [0.55, 1.0], "anchor": "y2"}, "yaxis2": {"domain": [0.625, 1.0], "anchor": "x2"}, "xaxis3": {"domain": [0.0, 0.45], "anchor": "y3"}, "yaxis3": {"domain": [0.0, 0.375], "anchor": "x3"}, "xaxis4": {"domain": [0.55, 1.0], "anchor": "y4"}, "yaxis4": {"domain": [0.0, 0.375], "anchor": "x4"}, "annotations": [{"y": 1.0, "xref": "paper", "x": 0.225, "yref": "paper", "text": "2006 vs 2016", "showarrow": false, "font": {"size": 16}, "xanchor": "center", "yanchor": "bottom"}, {"y": 1.0, "xref": "paper", "x": 0.775, "yref": "paper", "text": "2007 vs 2016", "showarrow": false, "font": {"size": 16}, "xanchor": "center", "yanchor": "bottom"}, {"y": 0.375, "xref": "paper", "x": 0.225, "yref": "paper", "text": "2014 vs 2016", "showarrow": false, "font": {"size": 16}, "xanchor": "center", "yanchor": "bottom"}, {"y": 0.375, "xref": "paper", "x": 0.775, "yref": "paper", "text": "2015 vs 2016", "showarrow": false, "font": {"size": 16}, "xanchor": "center", "yanchor": "bottom"}], "title": "Overall Global Gender Gap Rank", "showlegend": false}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>


As it can be seen from these scatterplots, the plots 2006 vs 2016 and 2007 vs 2016 looks very different than 2014 vs 2016 and 2015 vs 2016. The last plot (2015 vs 2016) shows that ranking of countries is becoming more stable, i.e., new ranks in 2016 are close to that of 2015. The reason of the data becoming more stable might be due to the fact that countries are getting used to their rating. It might be the case that when WEF started measuring the gap for the first time in 2005, the ranking created awareness and many countries took concrete steps in decreasing gap parity between women and men. That may explain the difference in plots between the early years (2006 and 2007) and later years (2015 and 2016).

## Average Overall Global Gender Rank across years 2006-2016

Since a lot of changes and fluctuations are observed in the dataset, we decided to look at the average rank to capture any interesting patterns in the data. The starting point is getting a general idea of the global ranking of countries. For this purpose, we first create a new column, Average Rank, and then look at the world map.


```python
overall=ranking.copy()

years=[]
for i in range(2006,2017):
    years.append(str(i))

overall['Average Rank']=overall[years].mean(numeric_only=True,axis=1).astype(int)

overall.sort_values(by='Average Rank', ascending=True).head(10)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Country ISO3</th>
      <th>Country Name</th>
      <th>Indicator</th>
      <th>Subindicator Type</th>
      <th>2006</th>
      <th>2007</th>
      <th>2008</th>
      <th>2009</th>
      <th>2010</th>
      <th>2011</th>
      <th>2012</th>
      <th>2013</th>
      <th>2014</th>
      <th>2015</th>
      <th>2016</th>
      <th>Average Rank</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>820</th>
      <td>ISL</td>
      <td>Iceland</td>
      <td>Overall Global Gender Gap Index</td>
      <td>Rank</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>595</th>
      <td>FIN</td>
      <td>Finland</td>
      <td>Overall Global Gender Gap Index</td>
      <td>Rank</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1324</th>
      <td>NOR</td>
      <td>Norway</td>
      <td>Overall Global Gender Gap Index</td>
      <td>Rank</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1620</th>
      <td>SWE</td>
      <td>Sweden</td>
      <td>Overall Global Gender Gap Index</td>
      <td>Rank</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1506</th>
      <td>RWA</td>
      <td>Rwanda</td>
      <td>Overall Global Gender Gap Index</td>
      <td>Rank</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>7.0</td>
      <td>6.0</td>
      <td>5.0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>794</th>
      <td>IRL</td>
      <td>Ireland</td>
      <td>Overall Global Gender Gap Index</td>
      <td>Rank</td>
      <td>10.0</td>
      <td>9.0</td>
      <td>8.0</td>
      <td>8.0</td>
      <td>6.0</td>
      <td>5.0</td>
      <td>5.0</td>
      <td>6.0</td>
      <td>8.0</td>
      <td>5.0</td>
      <td>6.0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>1415</th>
      <td>PHL</td>
      <td>Philippines</td>
      <td>Overall Global Gender Gap Index</td>
      <td>Rank</td>
      <td>6.0</td>
      <td>6.0</td>
      <td>6.0</td>
      <td>9.0</td>
      <td>9.0</td>
      <td>8.0</td>
      <td>8.0</td>
      <td>5.0</td>
      <td>9.0</td>
      <td>7.0</td>
      <td>7.0</td>
      <td>7</td>
    </tr>
    <tr>
      <th>1350</th>
      <td>NZL</td>
      <td>New Zealand</td>
      <td>Overall Global Gender Gap Index</td>
      <td>Rank</td>
      <td>7.0</td>
      <td>5.0</td>
      <td>5.0</td>
      <td>5.0</td>
      <td>5.0</td>
      <td>6.0</td>
      <td>6.0</td>
      <td>7.0</td>
      <td>13.0</td>
      <td>10.0</td>
      <td>9.0</td>
      <td>7</td>
    </tr>
    <tr>
      <th>491</th>
      <td>DNK</td>
      <td>Denmark</td>
      <td>Overall Global Gender Gap Index</td>
      <td>Rank</td>
      <td>8.0</td>
      <td>8.0</td>
      <td>7.0</td>
      <td>7.0</td>
      <td>7.0</td>
      <td>7.0</td>
      <td>7.0</td>
      <td>8.0</td>
      <td>5.0</td>
      <td>14.0</td>
      <td>19.0</td>
      <td>8</td>
    </tr>
    <tr>
      <th>478</th>
      <td>DEU</td>
      <td>Germany</td>
      <td>Overall Global Gender Gap Index</td>
      <td>Rank</td>
      <td>5.0</td>
      <td>7.0</td>
      <td>11.0</td>
      <td>12.0</td>
      <td>13.0</td>
      <td>11.0</td>
      <td>13.0</td>
      <td>14.0</td>
      <td>12.0</td>
      <td>11.0</td>
      <td>13.0</td>
      <td>11</td>
    </tr>
  </tbody>
</table>
</div>



The dataset shows that when we sort the data according to the average overall rank, the first seven countries are the first seven countries in 2015 and 2016. Denmark's overall average rank is eight even though their overall rank gradually decreased in 2015 and 2016. 


```python
def world_rank_map(rank):
    color_scale=[[0.40,'rgb(75, 75, 0)'],[0.30,'rgb(75, 38, 255)'],[0.60,'rgb(0,0,0)'],[0.90,'rgb(255, 238, 255)']]
    data=[dict(type='choropleth',
          text=overall['Country Name'],
          locations=overall['Country ISO3'],
          z=overall[rank].astype(float),
          marker=dict(line=dict(color='rgb(180,180,180)',width=0.5)),
          autocolorscale=False,
          reversescale=True,
          colorbar={'title':'Rank'})]
    #Now, let's plot the values:
    fig={'data': data,'layout':{'title':'Overall Global Gender Gap Index - '+ rank, 
                            'geo':{'scope':'world', 'projection':{'type': 'equirectangular'}},
                            'showlegend':True}}
    return iplot(fig)

world_rank_map('Average Rank')
```


<div id="e27d6e2c-5276-457b-92d2-d63489041813" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("e27d6e2c-5276-457b-92d2-d63489041813", [{"type": "choropleth", "text": ["Angola", "Albania", "United Arab Emirates", "Argentina", "Armenia", "Australia", "Austria", "Azerbaijan", "Burundi", "Belgium", "Benin", "Burkina Faso", "Bangladesh", "Bulgaria", "Bahrain", "Bahamas, The", "Bosnia and Herzegovina", "Belarus", "Belize", "Bolivia", "Brazil", "Barbados", "Brunei Darussalam", "Bhutan", "Botswana", "Canada", "Switzerland", "Chile", "China", "Cote d'Ivoire", "Cameroon", "Colombia", "Cabo Verde", "Costa Rica", "Cuba", "Cyprus", "Czech Republic", "Germany", "Denmark", "Dominican Republic", "Algeria", "Ecuador", "Egypt, Arab Rep.", "Spain", "Estonia", "Ethiopia", "Finland", "Fiji", "France", "United Kingdom", "Georgia", "Ghana", "Guinea", "Gambia, The", "Greece", "Guatemala", "Guyana", "Honduras", "Croatia", "Hungary", "Indonesia", "India", "Ireland", "Iran, Islamic Rep.", "Iceland", "Israel", "Italy", "Jamaica", "Jordan", "Japan", "Kazakhstan", "Kenya", "Kyrgyz Republic", "Cambodia", "Korea, Rep.", "Kuwait", "Lao PDR", "Lebanon", "Liberia", "Sri Lanka", "Lesotho", "Lithuania", "Luxembourg", "Latvia", "Morocco", "Moldova", "Madagascar", "Maldives", "Mexico", "Macedonia, FYR", "Mali", "Malta", "Montenegro", "Mongolia", "Mozambique", "Mauritania", "Mauritius", "Malawi", "Malaysia", "Namibia", "Nigeria", "Nicaragua", "Netherlands", "Norway", "Nepal", "New Zealand", "Oman", "Pakistan", "Panama", "Peru", "Philippines", "Poland", "Portugal", "Paraguay", "Qatar", "Romania", "Russian Federation", "Rwanda", "Saudi Arabia", "Senegal", "Singapore", "El Salvador", "Serbia", "Suriname", "Slovak Republic", "Slovenia", "Sweden", "Swaziland", "Syrian Arab Republic", "Chad", "Thailand", "Tajikistan", "Timor-Leste", "Trinidad and Tobago", "Tunisia", "Turkey", "Tanzania", "Uganda", "Ukraine", "Uruguay", "United States", "Uzbekistan", "Venezuela, RB", "Vietnam", "Yemen, Rep.", "South Africa", "Zambia", "Zimbabwe"], "locations": ["AGO", "ALB", "ARE", "ARG", "ARM", "AUS", "AUT", "AZE", "BDI", "BEL", "BEN", "BFA", "BGD", "BGR", "BHR", "BHS", "BIH", "BLR", "BLZ", "BOL", "BRA", "BRB", "BRN", "BTN", "BWA", "CAN", "CHE", "CHL", "CHN", "CIV", "CMR", "COL", "CPV", "CRI", "CUB", "CYP", "CZE", "DEU", "DNK", "DOM", "DZA", "ECU", "EGY", "ESP", "EST", "ETH", "FIN", "FJI", "FRA", "GBR", "GEO", "GHA", "GIN", "GMB", "GRC", "GTM", "GUY", "HND", "HRV", "HUN", "IDN", "IND", "IRL", "IRN", "ISL", "ISR", "ITA", "JAM", "JOR", "JPN", "KAZ", "KEN", "KGZ", "KHM", "KOR", "KWT", "LAO", "LBN", "LBR", "LKA", "LSO", "LTU", "LUX", "LVA", "MAR", "MDA", "MDG", "MDV", "MEX", "MKD", "MLI", "MLT", "MNE", "MNG", "MOZ", "MRT", "MUS", "MWI", "MYS", "NAM", "NGA", "NIC", "NLD", "NOR", "NPL", "NZL", "OMN", "PAK", "PAN", "PER", "PHL", "POL", "PRT", "PRY", "QAT", "ROU", "RUS", "RWA", "SAU", "SEN", "SGP", "SLV", "SRB", "SUR", "SVK", "SVN", "SWE", "SWZ", "SYR", "TCD", "THA", "TJK", "TLS", "TTO", "TUN", "TUR", "TZA", "UGA", "UKR", "URY", "USA", "UZB", "VEN", "VNM", "YEM", "ZAF", "ZMB", "ZWE"], "z": [105.0, 79.0, 109.0, 31.0, 90.0, 24.0, 32.0, 87.0, 20.0, 18.0, 124.0, 112.0, 80.0, 39.0, 115.0, 34.0, 83.0, 31.0, 97.0, 57.0, 74.0, 28.0, 88.0, 113.0, 58.0, 22.0, 14.0, 70.0, 71.0, 132.0, 107.0, 47.0, 42.0, 31.0, 24.0, 85.0, 73.0, 11.0, 8.0, 76.0, 117.0, 38.0, 125.0, 19.0, 41.0, 117.0, 2.0, 113.0, 36.0, 16.0, 80.0, 71.0, 128.0, 86.0, 77.0, 106.0, 47.0, 67.0, 46.0, 78.0, 89.0, 107.0, 6.0, 126.0, 1.0, 50.0, 69.0, 45.0, 118.0, 98.0, 40.0, 75.0, 58.0, 101.0, 108.0, 107.0, 53.0, 126.0, 112.0, 41.0, 27.0, 29.0, 39.0, 15.0, 127.0, 31.0, 69.0, 101.0, 82.0, 54.0, 125.0, 87.0, 80.0, 42.0, 25.0, 119.0, 99.0, 63.0, 98.0, 31.0, 111.0, 34.0, 13.0, 2.0, 116.0, 7.0, 125.0, 132.0, 39.0, 66.0, 7.0, 49.0, 39.0, 81.0, 116.0, 66.0, 56.0, 6.0, 129.0, 85.0, 64.0, 71.0, 47.0, 93.0, 73.0, 36.0, 3.0, 100.0, 126.0, 132.0, 58.0, 91.0, 96.0, 35.0, 110.0, 123.0, 50.0, 47.0, 61.0, 71.0, 26.0, 47.0, 63.0, 69.0, 134.0, 15.0, 107.0, 78.0], "marker": {"line": {"color": "rgb(180,180,180)", "width": 0.5}}, "autocolorscale": false, "reversescale": true, "colorbar": {"title": "Rank"}}], {"title": "Overall Global Gender Gap Index - Average Rank", "geo": {"scope": "world", "projection": {"type": "equirectangular"}}, "showlegend": true}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>


<b>Average Ranking and Continents:</b>

<ul>
<li> Most African countries have ranks greater than 100 except few counties in Southern parts of Africa. There are only two countries with rank less than 20 in Africa: Rwanda (the only country in Top 10 with rank=6) and South Africa(rank=15). Note that there are many countries with no records in the Central Africa. </li> 
<li> According to Quartz Africa, one third of all world's population would be living in Africa by 2100. (https://qz.com/africa/1099546/population-growth-africans-will-be-a-third-of-all-people-on-earth-by-2100/). This is another reason why it is imperative to improve the gender gap in the African countries with high ranks. </li>

<li> Only  Philippines rank is in Top 10 in Asia.</li>

<li> The map shows that most Western European countries have high ranking while most Eastern European counties have average ranks between 50-100.    </li>

<li> Both United States and Canada's overall ranks increased in 2015 and then again in 2016 but their average ranks are still less than 30. Even though Mexico's average overall rank is 82, they decreased their overall global gender rank in both 2015 and 2016. </li>

<li> Average rank of all countries in South America are less than 100. Argentina has the highest rank (31) while Suriname has the lowest average rank (93). </li>
</ul>

Next, we look at the Top 20 countries in year 2016.


## Top 20 in the year 2016

Next, let's explore Top 20 ranking in the year 2016.


```python
overall_ranked=overall.sort_values(by="2016", ascending=True)
overall_ranked_top20=overall_ranked[:20]
overall_ranked_top20=overall_ranked_top20.reset_index()

overall_ranked_top20.head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>index</th>
      <th>Country ISO3</th>
      <th>Country Name</th>
      <th>Indicator</th>
      <th>Subindicator Type</th>
      <th>2006</th>
      <th>2007</th>
      <th>2008</th>
      <th>2009</th>
      <th>2010</th>
      <th>2011</th>
      <th>2012</th>
      <th>2013</th>
      <th>2014</th>
      <th>2015</th>
      <th>2016</th>
      <th>Average Rank</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>820</td>
      <td>ISL</td>
      <td>Iceland</td>
      <td>Overall Global Gender Gap Index</td>
      <td>Rank</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>595</td>
      <td>FIN</td>
      <td>Finland</td>
      <td>Overall Global Gender Gap Index</td>
      <td>Rank</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1324</td>
      <td>NOR</td>
      <td>Norway</td>
      <td>Overall Global Gender Gap Index</td>
      <td>Rank</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1620</td>
      <td>SWE</td>
      <td>Sweden</td>
      <td>Overall Global Gender Gap Index</td>
      <td>Rank</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1506</td>
      <td>RWA</td>
      <td>Rwanda</td>
      <td>Overall Global Gender Gap Index</td>
      <td>Rank</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>7.0</td>
      <td>6.0</td>
      <td>5.0</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
</div>




```python
bar2015=go.Bar(x=overall_ranked_top20['Country Name'], 
               y=overall_ranked_top20['Average Rank'], 
               marker=dict(color='darkblue'),
               opacity=0.5,
              name='Average Rank')

bar2016=go.Bar(x=overall_ranked_top20['Country Name'], 
               y=overall_ranked_top20['2016'], 
               marker=dict(color='darkred'),
              name='2016')

bars=[bar2015,bar2016]

fig={'data': bars,'layout':{'title':'Top 20 Ranked Countries in 2016', 
                            'xaxis':{'title':'Country'},
                            'yaxis':{'title':'Rank'}}}

iplot(fig)
```


<div id="e3a43592-254b-4d10-ac1b-18efd7d6bbf5" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("e3a43592-254b-4d10-ac1b-18efd7d6bbf5", [{"type": "bar", "x": ["Iceland", "Finland", "Norway", "Sweden", "Rwanda", "Ireland", "Philippines", "Slovenia", "New Zealand", "Nicaragua", "Switzerland", "Burundi", "Germany", "Namibia", "South Africa", "Netherlands", "France", "Latvia", "Denmark", "United Kingdom"], "y": [1, 2, 2, 3, 6, 6, 7, 36, 7, 34, 14, 20, 11, 31, 15, 13, 36, 15, 8, 16], "marker": {"color": "darkblue"}, "opacity": 0.5, "name": "Average Rank"}, {"type": "bar", "x": ["Iceland", "Finland", "Norway", "Sweden", "Rwanda", "Ireland", "Philippines", "Slovenia", "New Zealand", "Nicaragua", "Switzerland", "Burundi", "Germany", "Namibia", "South Africa", "Netherlands", "France", "Latvia", "Denmark", "United Kingdom"], "y": [1.0, 2.0, 3.0, 4.0, 5.0, 6.0, 7.0, 8.0, 9.0, 10.0, 11.0, 12.0, 13.0, 14.0, 15.0, 16.0, 17.0, 18.0, 19.0, 20.0], "marker": {"color": "darkred"}, "name": "2016"}], {"title": "Top 20 Ranked Countries in 2016", "xaxis": {"title": "Country"}, "yaxis": {"title": "Rank"}}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>


<b> What are the similarities and differences in the Top 20 countries in 2016?</b>

This dataframe and following barplot shows the ranking sorted in an ascending order according to their 2016 ranking. In addition, the barplot includes average rank of countries with ranks in Top 20. Note that the newly created column Average Rank provides average rank of each country over the years 2006 and 2016. A high average rank means that that country's rank was very high at some time in the past and improved significantly later so that the country was in Top 20 list in 2016. 

In 2016, Iceland has rank 1 which is followed by other Nordic countries Finland, Norway and Sweden. Since 2006, these four countries always had ranks between 1 and 4. In 2006 and 2007, Sweden's rank was number one but later increased to four while Iceland's ranking was initially four and decreased to one and stays the same from 2009 to 2016. Rwanda's records were available from 2014 onwards and gradually decreased to rank five.

When we look at the countries in Top 20 in 2016, we see that there are thirteen countries in Europe, four in Africa, one in Asia, one in Ocenia and one in North America. 

It is worth noting that while rank of Nicaragua, the only North American country in Top 20, was 62 in 2006, its rank decreased to 10 in 2016 (it was even 6 in 2014 and its average rank is 34).

Another notable example is Slovenia (rank=8 in 2016 and average rank=36) who improved their rank significantly. According to UN Women, Slovenia committed to improve the gender gap in their country and took several positive steps including a call for support from men and boys to support policies and activities regarding gender gap issues (http://www.unwomen.org/en/get-involved/step-it-up/commitments/slovenia)

In addition to Nicaragua and Slovenia, Namibia(rank=14 in 2016 and average rank=31) and France (rank=17 in 2016 and average rank=36) also took many positive steps to increase their ranking. According to a report published by the European Parliement http://www.europarl.europa.eu/RegData/etudes/IDAN/2015/510024/IPOL_IDA(2015)510024_EN.pdf ......


# Section 2: Which countries improved their ranking the most? What are the factors influencing these positive changes?

There are several ways to find out which countries improved their ranking the most. Below, each one is explained in detail. 

After creating a new column according to each critera, we will look at Top 3 countries in detail by using their subindexes measuring economic participation, educational attainments, health and survival and political empowerment. To get more information about the factors influencing these positive changes in these countries, we will provide two different types of plots.

The following two functions are defined to plot data related to subindexes. The first function helps us to see the change in each subindex by using a line graph. Note that the plots still uses ranks rather than indexes because it is more clear to show how the overall ranking depend on subindexes. However, this does not capture all information about the subindexes. Some steep increases or decreases might be due to other factors, such as several countries sharing the same rank. Therefore, a boxplot will be provided to get a better picture of the ranking and to support the information presented in the line graph. 


```python
def country_scatterplot(country):
    index_list=['Economic Participation', 'Education', 'Health', 'Political','Overall', 'Wage Equality']
    gender_country=gender[(gender['Country Name']==country) & (gender['Subindicator Type']=='Rank')]
    gender_country.index=index_list
    scatters_list=[]
    colors=['red','blue','green','brown','purple','orange']
    for i in range(0,len(index_list)):
        scat=go.Scatter(x=years, 
               y=gender_country.loc[index_list[i],years], 
               marker=dict(color=colors[i]),
               name=index_list[i],
               mode='lines')
        scatters_list.append(scat)
    fig={'data': scatters_list,'layout':{'title':country, 
                            'xaxis':{'title':'Years'},
                            'yaxis':{'title':'Rank'}}}
    return iplot(fig)

def country_boxplot(country):
    index_list=['Economic Participation', 'Education', 'Health', 'Political','Overall','Wage Equality']
    gender_country=gender[(gender['Country Name']==country) & (gender['Subindicator Type']=='Rank')]
    gender_country.index=index_list
    box_list=[]
    colors=['red','blue','green','black','purple','orange']
    for i in range(0,len(index_list)):
        boxp=go.Box(y=gender_country.loc[index_list[i],years], 
                    boxpoints='all',
                    marker=dict(color=colors[i]),
                    name=index_list[i])
        box_list.append(boxp)
    fig={'data': box_list,'layout':{'title':country,
                            #'xaxis':{'title':'Subindexes'},
                            'yaxis':{'title':'Rank'}}}
    return iplot(fig)
```

### 1.Comparison of overall ranks in 2006 and 2016

One way is finding a rough estimate by using data related to the years 2006 and 2006. For this, two columns are created by using two newly defined functions: One columns gives information whether a country improved their ranking in 2016. If 2006 rank is greater than 2016 rank, the change is positive, otherwise it is negative. Unfortunately, there is no report for some countries in 2006, or 2016 or both. These are recorded as missing 2006, missing 2016 and missing both.


```python
def changed(row):
    if pd.isna(row["2006"])==True & pd.notna(row["2016"])==True:
        return "missing 2006"
    elif pd.notna(row["2006"])==True & pd.isna(row["2016"])==True:
        return "missing 2016"                                                   
    elif row["2006"]>row["2016"]:
        return "positive"
    elif row["2006"]<row["2016"]:
        return "negative"

def change_val(row):
    if pd.isna(row["2006"])==True & pd.notna(row["2016"])==True:
        return np.nan
    elif pd.notna(row["2006"])==True & pd.isna(row["2016"])==True:
        return np.nan
    else:
        return row["2006"]-row["2016"]    

def change_val2(row):
    if pd.isna(row["2015"])==True & pd.notna(row["2016"])==True:
        return np.nan
    elif pd.notna(row["2015"])==True & pd.isna(row["2016"])==True:
        return np.nan
    else:
        return row["2015"]-row["2016"]   

overall["Change 2006-2016"]=overall.apply(lambda row: changed(row),axis=1)                                                   
overall["Numerical Change 2006-2016"]=overall.apply(lambda row: change_val(row),axis=1)
overall=overall.sort_values(by="Numerical Change 2006-2016",ascending=False)

overall_count=overall.groupby('Change 2006-2016').count()
overall_mean=overall.groupby('Change 2006-2016').mean()

overall.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Country ISO3</th>
      <th>Country Name</th>
      <th>Indicator</th>
      <th>Subindicator Type</th>
      <th>2006</th>
      <th>2007</th>
      <th>2008</th>
      <th>2009</th>
      <th>2010</th>
      <th>2011</th>
      <th>2012</th>
      <th>2013</th>
      <th>2014</th>
      <th>2015</th>
      <th>2016</th>
      <th>Average Rank</th>
      <th>Change 2006-2016</th>
      <th>Numerical Change 2006-2016</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>247</th>
      <td>BOL</td>
      <td>Bolivia</td>
      <td>Overall Global Gender Gap Index</td>
      <td>Rank</td>
      <td>87.0</td>
      <td>80.0</td>
      <td>80.0</td>
      <td>82.0</td>
      <td>76.0</td>
      <td>62.0</td>
      <td>30.0</td>
      <td>27.0</td>
      <td>58.0</td>
      <td>22.0</td>
      <td>23.0</td>
      <td>57</td>
      <td>positive</td>
      <td>64.0</td>
    </tr>
    <tr>
      <th>618</th>
      <td>FRA</td>
      <td>France</td>
      <td>Overall Global Gender Gap Index</td>
      <td>Rank</td>
      <td>70.0</td>
      <td>51.0</td>
      <td>15.0</td>
      <td>18.0</td>
      <td>46.0</td>
      <td>48.0</td>
      <td>57.0</td>
      <td>45.0</td>
      <td>16.0</td>
      <td>15.0</td>
      <td>17.0</td>
      <td>36</td>
      <td>positive</td>
      <td>53.0</td>
    </tr>
    <tr>
      <th>1298</th>
      <td>NIC</td>
      <td>Nicaragua</td>
      <td>Overall Global Gender Gap Index</td>
      <td>Rank</td>
      <td>62.0</td>
      <td>90.0</td>
      <td>71.0</td>
      <td>49.0</td>
      <td>30.0</td>
      <td>27.0</td>
      <td>9.0</td>
      <td>10.0</td>
      <td>6.0</td>
      <td>12.0</td>
      <td>10.0</td>
      <td>34</td>
      <td>positive</td>
      <td>52.0</td>
    </tr>
    <tr>
      <th>1607</th>
      <td>SVN</td>
      <td>Slovenia</td>
      <td>Overall Global Gender Gap Index</td>
      <td>Rank</td>
      <td>51.0</td>
      <td>49.0</td>
      <td>51.0</td>
      <td>52.0</td>
      <td>42.0</td>
      <td>41.0</td>
      <td>38.0</td>
      <td>38.0</td>
      <td>23.0</td>
      <td>9.0</td>
      <td>8.0</td>
      <td>36</td>
      <td>positive</td>
      <td>43.0</td>
    </tr>
    <tr>
      <th>530</th>
      <td>ECU</td>
      <td>Ecuador</td>
      <td>Overall Global Gender Gap Index</td>
      <td>Rank</td>
      <td>82.0</td>
      <td>44.0</td>
      <td>35.0</td>
      <td>23.0</td>
      <td>40.0</td>
      <td>45.0</td>
      <td>33.0</td>
      <td>25.0</td>
      <td>21.0</td>
      <td>33.0</td>
      <td>40.0</td>
      <td>38</td>
      <td>positive</td>
      <td>42.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
world_rank_map('Numerical Change 2006-2016')
```


<div id="2a82dc68-4271-4bcd-9a5c-5c34085ffe02" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("2a82dc68-4271-4bcd-9a5c-5c34085ffe02", [{"type": "choropleth", "text": ["Bolivia", "France", "Nicaragua", "Slovenia", "Ecuador", "Italy", "Madagascar", "Namibia", "Luxembourg", "Zimbabwe", "Bangladesh", "Cameroon", "Switzerland", "Malawi", "India", "Singapore", "Kenya", "Mexico", "Argentina", "Chile", "Estonia", "Poland", "Ireland", "Iceland", "South Africa", "Portugal", "Nepal", "Finland", "Trinidad and Tobago", "Latvia", "Albania", "Cyprus", "Norway", "Philippines", "Ghana", "Costa Rica", "New Zealand", "Sweden", "Honduras", "Netherlands", "Lithuania", "Bulgaria", "Belgium", "Germany", "Moldova", "Ethiopia", "Guatemala", "United Kingdom", "Denmark", "Brazil", "Uganda", "Israel", "Lesotho", "Panama", "Mongolia", "Benin", "Venezuela, RB", "Colombia", "Jamaica", "Spain", "Kazakhstan", "Burkina Faso", "Botswana", "Indonesia", "Peru", "Ukraine", "Angola", "Canada", "United States", "Cambodia", "United Arab Emirates", "Algeria", "Greece", "Mauritania", "Egypt, Arab Rep.", "Nigeria", "Czech Republic", "Gambia, The", "Korea, Rep.", "El Salvador", "Austria", "Turkey", "Mauritius", "Uruguay", "Russian Federation", "Chad", "Saudi Arabia", "Kyrgyz Republic", "Tanzania", "Yemen, Rep.", "Bahrain", "Morocco", "Romania", "Thailand", "Australia", "Iran, Islamic Rep.", "Pakistan", "Japan", "Paraguay", "Malaysia", "China", "Georgia", "Tunisia", "Malta", "Dominican Republic", "Mali", "Jordan", "Kuwait", "Slovak Republic", "Macedonia, FYR", "Hungary", "Croatia", "Sri Lanka", "Armenia", "Azerbaijan", "Burundi", "Bahamas, The", "Bosnia and Herzegovina", "Belarus", "Belize", "Barbados", "Brunei Darussalam", "Bhutan", "Cote d'Ivoire", "Cabo Verde", "Cuba", "Fiji", "Guinea", "Guyana", "Lao PDR", "Lebanon", "Liberia", "Maldives", "Montenegro", "Mozambique", "Oman", "Qatar", "Rwanda", "Senegal", "Serbia", "Suriname", "Swaziland", "Syrian Arab Republic", "Tajikistan", "Timor-Leste", "Uzbekistan", "Vietnam", "Zambia"], "locations": ["BOL", "FRA", "NIC", "SVN", "ECU", "ITA", "MDG", "NAM", "LUX", "ZWE", "BGD", "CMR", "CHE", "MWI", "IND", "SGP", "KEN", "MEX", "ARG", "CHL", "EST", "POL", "IRL", "ISL", "ZAF", "PRT", "NPL", "FIN", "TTO", "LVA", "ALB", "CYP", "NOR", "PHL", "GHA", "CRI", "NZL", "SWE", "HND", "NLD", "LTU", "BGR", "BEL", "DEU", "MDA", "ETH", "GTM", "GBR", "DNK", "BRA", "UGA", "ISR", "LSO", "PAN", "MNG", "BEN", "VEN", "COL", "JAM", "ESP", "KAZ", "BFA", "BWA", "IDN", "PER", "UKR", "AGO", "CAN", "USA", "KHM", "ARE", "DZA", "GRC", "MRT", "EGY", "NGA", "CZE", "GMB", "KOR", "SLV", "AUT", "TUR", "MUS", "URY", "RUS", "TCD", "SAU", "KGZ", "TZA", "YEM", "BHR", "MAR", "ROU", "THA", "AUS", "IRN", "PAK", "JPN", "PRY", "MYS", "CHN", "GEO", "TUN", "MLT", "DOM", "MLI", "JOR", "KWT", "SVK", "MKD", "HUN", "HRV", "LKA", "ARM", "AZE", "BDI", "BHS", "BIH", "BLR", "BLZ", "BRB", "BRN", "BTN", "CIV", "CPV", "CUB", "FJI", "GIN", "GUY", "LAO", "LBN", "LBR", "MDV", "MNE", "MOZ", "OMN", "QAT", "RWA", "SEN", "SRB", "SUR", "SWZ", "SYR", "TJK", "TLS", "UZB", "VNM", "ZMB"], "z": [64.0, 53.0, 52.0, 43.0, 42.0, 27.0, 24.0, 24.0, 22.0, 20.0, 19.0, 18.0, 15.0, 14.0, 11.0, 10.0, 10.0, 9.0, 8.0, 8.0, 7.0, 6.0, 4.0, 3.0, 3.0, 2.0, 1.0, 1.0, 1.0, 1.0, -1.0, -1.0, -1.0, -1.0, -1.0, -2.0, -2.0, -3.0, -4.0, -4.0, -4.0, -4.0, -4.0, -8.0, -9.0, -9.0, -10.0, -11.0, -11.0, -12.0, -14.0, -14.0, -14.0, -16.0, -16.0, -17.0, -17.0, -17.0, -17.0, -18.0, -19.0, -19.0, -20.0, -20.0, -20.0, -21.0, -21.0, -21.0, -22.0, -23.0, -23.0, -23.0, -23.0, -23.0, -23.0, -24.0, -24.0, -24.0, -24.0, -25.0, -25.0, -25.0, -25.0, -25.0, -26.0, -27.0, -27.0, -29.0, -29.0, -29.0, -29.0, -30.0, -30.0, -31.0, -31.0, -31.0, -31.0, -32.0, -32.0, -34.0, -36.0, -36.0, -36.0, -37.0, -38.0, -39.0, -41.0, -42.0, -44.0, -45.0, -46.0, -52.0, -87.0, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null], "marker": {"line": {"color": "rgb(180,180,180)", "width": 0.5}}, "autocolorscale": false, "reversescale": true, "colorbar": {"title": "Rank"}}], {"title": "Overall Global Gender Gap Index - Numerical Change 2006-2016", "geo": {"scope": "world", "projection": {"type": "equirectangular"}}, "showlegend": true}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>


The world map provides a more clear picture about the overall change in the world. For example, when we look at the difference between years 2006 and 2016, we see that Bolivia is the country that improved their ranking the most followed by France and Nicaragua. The world map also shows that many countries increased their ranks (brownish colors). [We defined change positive if their 2016 rank is less than their 2006 rank.]


```python
overall_stat=overall_mean.copy()
overall_stat=overall_stat[['2016','Average Rank','Numerical Change 2006-2016']]
overall_stat=overall_stat.rename(columns={'2016':'mean 2016','Average Rank':'mean of Average Rank', 'Numerical Change 2006-2016':'mean change'})
overall_stat['count']=overall_count['Country Name']

overall_stat

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>mean 2016</th>
      <th>mean of Average Rank</th>
      <th>mean change</th>
      <th>count</th>
    </tr>
    <tr>
      <th>Change 2006-2016</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>missing 2006</th>
      <td>82.322581</td>
      <td>78.967742</td>
      <td>NaN</td>
      <td>31</td>
    </tr>
    <tr>
      <th>missing 2016</th>
      <td>NaN</td>
      <td>77.000000</td>
      <td>NaN</td>
      <td>2</td>
    </tr>
    <tr>
      <th>negative</th>
      <td>80.481928</td>
      <td>70.698795</td>
      <td>-22.421687</td>
      <td>83</td>
    </tr>
    <tr>
      <th>positive</th>
      <td>40.266667</td>
      <td>49.966667</td>
      <td>17.400000</td>
      <td>30</td>
    </tr>
  </tbody>
</table>
</div>



Statistics table above confirms our observation: There are 83 countries whose ranks got worse while there are 30 countries whose ranks got better. The mean change in rank for the countries who changed their rank positively is 17.4 while the mean change in rank of the countries whose rank changed negatively is -22.42. 

Next, we look at the Top 3 countries who decreased their ranking the most in detail and try to find the factors contributing to the positive change in their ranking.

### Bolivia


```python
country_scatterplot('Bolivia')
country_boxplot('Bolivia')
```


<div id="7d722553-d62b-48f0-afc2-5baf8f5abb0f" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("7d722553-d62b-48f0-afc2-5baf8f5abb0f", [{"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [77.0, 77.0, 88.0, 94.0, 91.0, 72.0, 79.0, 57.0, 92.0, 96.0, 98.0], "marker": {"color": "red"}, "name": "Economic Participation", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [89.0, 85.0, 90.0, 91.0, 97.0, 95.0, 98.0, 99.0, 99.0, 101.0, 98.0], "marker": {"color": "blue"}, "name": "Education", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [79.0, 107.0, 108.0, 112.0, 82.0, 84.0, 84.0, 84.0, 56.0, 1.0, 1.0], "marker": {"color": "green"}, "name": "Health", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [71.0, 79.0, 51.0, 56.0, 46.0, 45.0, 20.0, 23.0, 40.0, 10.0, 11.0], "marker": {"color": "brown"}, "name": "Political", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [87.0, 80.0, 80.0, 82.0, 76.0, 62.0, 30.0, 27.0, 58.0, 22.0, 23.0], "marker": {"color": "purple"}, "name": "Overall", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [null, null, null, null, null, null, null, null, null, null, 132.0], "marker": {"color": "orange"}, "name": "Wage Equality", "mode": "lines"}], {"title": "Bolivia", "xaxis": {"title": "Years"}, "yaxis": {"title": "Rank"}}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>



<div id="47382490-ba8e-44df-8e77-7dad776128bd" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("47382490-ba8e-44df-8e77-7dad776128bd", [{"type": "box", "y": [77.0, 77.0, 88.0, 94.0, 91.0, 72.0, 79.0, 57.0, 92.0, 96.0, 98.0], "boxpoints": "all", "marker": {"color": "red"}, "name": "Economic Participation"}, {"type": "box", "y": [89.0, 85.0, 90.0, 91.0, 97.0, 95.0, 98.0, 99.0, 99.0, 101.0, 98.0], "boxpoints": "all", "marker": {"color": "blue"}, "name": "Education"}, {"type": "box", "y": [79.0, 107.0, 108.0, 112.0, 82.0, 84.0, 84.0, 84.0, 56.0, 1.0, 1.0], "boxpoints": "all", "marker": {"color": "green"}, "name": "Health"}, {"type": "box", "y": [71.0, 79.0, 51.0, 56.0, 46.0, 45.0, 20.0, 23.0, 40.0, 10.0, 11.0], "boxpoints": "all", "marker": {"color": "black"}, "name": "Political"}, {"type": "box", "y": [87.0, 80.0, 80.0, 82.0, 76.0, 62.0, 30.0, 27.0, 58.0, 22.0, 23.0], "boxpoints": "all", "marker": {"color": "purple"}, "name": "Overall"}, {"type": "box", "y": [null, null, null, null, null, null, null, null, null, null, 132.0], "boxpoints": "all", "marker": {"color": "orange"}, "name": "Wage Equality"}], {"title": "Bolivia", "yaxis": {"title": "Rank"}}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>


For Bolivia, we see that the overall ranking (purple color) change more like the changes in their political empowerment subindex(brown). This is more clear between the years 2011 and 2012. Note that only political empowerment ranking improved while all other subindexes were either increased or stayed the same. Accordingly, overall rank got better. As for other years, this trends continues. The other subindex affecting the overall rank is economic participation. 

### France


```python
country_scatterplot('France')
country_boxplot('France')
```


<div id="9148abdf-bb39-4867-b1b5-7dfe5f3806d9" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("9148abdf-bb39-4867-b1b5-7dfe5f3806d9", [{"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [88.0, 61.0, 53.0, 61.0, 60.0, 61.0, 62.0, 67.0, 57.0, 56.0, 64.0], "marker": {"color": "red"}, "name": "Economic Participation", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0], "marker": {"color": "blue"}, "name": "Education", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0], "marker": {"color": "green"}, "name": "Health", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [60.0, 67.0, 18.0, 16.0, 47.0, 46.0, 63.0, 45.0, 20.0, 19.0, 19.0], "marker": {"color": "brown"}, "name": "Political", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [70.0, 51.0, 15.0, 18.0, 46.0, 48.0, 57.0, 45.0, 16.0, 15.0, 17.0], "marker": {"color": "purple"}, "name": "Overall", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [null, null, null, null, null, null, null, null, null, null, 134.0], "marker": {"color": "orange"}, "name": "Wage Equality", "mode": "lines"}], {"title": "France", "xaxis": {"title": "Years"}, "yaxis": {"title": "Rank"}}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>



<div id="fe5ec7f5-f9d7-441d-bc50-0db2735b61bb" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("fe5ec7f5-f9d7-441d-bc50-0db2735b61bb", [{"type": "box", "y": [88.0, 61.0, 53.0, 61.0, 60.0, 61.0, 62.0, 67.0, 57.0, 56.0, 64.0], "boxpoints": "all", "marker": {"color": "red"}, "name": "Economic Participation"}, {"type": "box", "y": [1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0], "boxpoints": "all", "marker": {"color": "blue"}, "name": "Education"}, {"type": "box", "y": [1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0], "boxpoints": "all", "marker": {"color": "green"}, "name": "Health"}, {"type": "box", "y": [60.0, 67.0, 18.0, 16.0, 47.0, 46.0, 63.0, 45.0, 20.0, 19.0, 19.0], "boxpoints": "all", "marker": {"color": "black"}, "name": "Political"}, {"type": "box", "y": [70.0, 51.0, 15.0, 18.0, 46.0, 48.0, 57.0, 45.0, 16.0, 15.0, 17.0], "boxpoints": "all", "marker": {"color": "purple"}, "name": "Overall"}, {"type": "box", "y": [null, null, null, null, null, null, null, null, null, null, 134.0], "boxpoints": "all", "marker": {"color": "orange"}, "name": "Wage Equality"}], {"title": "France", "yaxis": {"title": "Rank"}}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>


The second country who improved their rank the most is France. Line plot clearly shows that their health and education parity is excellent (rank=1) over all years. The line plot clearly shows that overall ranking closely follows political empowerment subindex. For more information about France's progress, please look at the report at http://www.europarl.europa.eu/RegData/etudes/IDAN/2015/510024/IPOL_IDA(2015)510024_EN.pdf.

### Nicaragua


```python
country_scatterplot('Nicaragua')
country_boxplot('Nicaragua')
```


<div id="ce3c6ea3-b351-4f5e-802c-77266c6b05c8" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("ce3c6ea3-b351-4f5e-802c-77266c6b05c8", [{"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [101.0, 117.0, 117.0, 104.0, 94.0, 79.0, 88.0, 91.0, 95.0, 100.0, 92.0], "marker": {"color": "red"}, "name": "Economic Participation", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [39.0, 51.0, 1.0, 1.0, 24.0, 25.0, 23.0, 28.0, 33.0, 1.0, 1.0], "marker": {"color": "blue"}, "name": "Education", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [50.0, 60.0, 62.0, 65.0, 57.0, 58.0, 58.0, 55.0, 1.0, 1.0, 1.0], "marker": {"color": "green"}, "name": "Health", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [25.0, 28.0, 23.0, 25.0, 19.0, 21.0, 5.0, 5.0, 4.0, 4.0, 4.0], "marker": {"color": "brown"}, "name": "Political", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [62.0, 90.0, 71.0, 49.0, 30.0, 27.0, 9.0, 10.0, 6.0, 12.0, 10.0], "marker": {"color": "purple"}, "name": "Overall", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [null, null, null, null, null, null, null, null, null, null, 104.0], "marker": {"color": "orange"}, "name": "Wage Equality", "mode": "lines"}], {"title": "Nicaragua", "xaxis": {"title": "Years"}, "yaxis": {"title": "Rank"}}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>



<div id="83f48795-cf7a-4b51-a52b-0497f576bce2" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("83f48795-cf7a-4b51-a52b-0497f576bce2", [{"type": "box", "y": [101.0, 117.0, 117.0, 104.0, 94.0, 79.0, 88.0, 91.0, 95.0, 100.0, 92.0], "boxpoints": "all", "marker": {"color": "red"}, "name": "Economic Participation"}, {"type": "box", "y": [39.0, 51.0, 1.0, 1.0, 24.0, 25.0, 23.0, 28.0, 33.0, 1.0, 1.0], "boxpoints": "all", "marker": {"color": "blue"}, "name": "Education"}, {"type": "box", "y": [50.0, 60.0, 62.0, 65.0, 57.0, 58.0, 58.0, 55.0, 1.0, 1.0, 1.0], "boxpoints": "all", "marker": {"color": "green"}, "name": "Health"}, {"type": "box", "y": [25.0, 28.0, 23.0, 25.0, 19.0, 21.0, 5.0, 5.0, 4.0, 4.0, 4.0], "boxpoints": "all", "marker": {"color": "black"}, "name": "Political"}, {"type": "box", "y": [62.0, 90.0, 71.0, 49.0, 30.0, 27.0, 9.0, 10.0, 6.0, 12.0, 10.0], "boxpoints": "all", "marker": {"color": "purple"}, "name": "Overall"}, {"type": "box", "y": [null, null, null, null, null, null, null, null, null, null, 104.0], "boxpoints": "all", "marker": {"color": "orange"}, "name": "Wage Equality"}], {"title": "Nicaragua", "yaxis": {"title": "Rank"}}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>


In Nicaragua, the line plot is very complicated than Bolivia and France. It seems like the improvement in their overall ranking is a result of improvements in health and political empowerment. Educational attainment ranking fluctuates a lot but it may also have some positive effect on the overall ranking. Nicaragua's overall ranking decreased and stayed around 10 even though economic participation ranking increased between the years 2011 and 2015. It seems like the increase in their rank from 2014 to 2015 was due to the increase in the economic participation subindex.

## 2. Maximum positive difference in the ranking

So far, we focused on changes between the years 2006 and 2016 and looked at the factors leading up to that change in top 3 counties in that list. However, this gives us a rough information about the ranking. As we can see from the dataset, there might be some fluctations over the years, i.e., a country's ranking might change significantly from year to year. A possible reason contributing to this change could be the change in ranking of other countries. It might also be due to a significant event or a policy change in that country. To explore sudden changes in ranks over the years, we will create a new column, max difference, which gives us the max positive change observed during the years 2006 and 2016. In addition, we create a new column showing the years to find out whether the change occurred is more recent or not.


```python
df_max_diff=ranking.copy()

lst=[]
lst2=[]

for index,row in df_max_diff.iterrows():
    max_difference=0
    year='2006'
    for i in range(4,14):
        if pd.notna(row[i])==True and pd.notna(row[i+1])==True:
            if row[i]>row[i+1]:
                x=row[i]-row[i+1]
                if max_difference<x:
                        max_difference=x
                        year=(df_max_diff.columns[i]+'-'+df_max_diff.columns[i+1])
                else:
                   continue                     
            else:
                max_difference=max_difference
    lst.append(max_difference)
    lst2.append(year)
    
df_max_diff["max difference"]=lst
df_max_diff["max difference-years"]=lst2

df_max_diff.sort_values(by='max difference', ascending=False).head()

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Country ISO3</th>
      <th>Country Name</th>
      <th>Indicator</th>
      <th>Subindicator Type</th>
      <th>2006</th>
      <th>2007</th>
      <th>2008</th>
      <th>2009</th>
      <th>2010</th>
      <th>2011</th>
      <th>2012</th>
      <th>2013</th>
      <th>2014</th>
      <th>2015</th>
      <th>2016</th>
      <th>max difference</th>
      <th>max difference-years</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>911</th>
      <td>KEN</td>
      <td>Kenya</td>
      <td>Overall Global Gender Gap Index</td>
      <td>Rank</td>
      <td>73.0</td>
      <td>83.0</td>
      <td>88.0</td>
      <td>97.0</td>
      <td>96.0</td>
      <td>99.0</td>
      <td>72.0</td>
      <td>78.0</td>
      <td>37.0</td>
      <td>48.0</td>
      <td>63.0</td>
      <td>41.0</td>
      <td>2013-2014</td>
    </tr>
    <tr>
      <th>569</th>
      <td>EST</td>
      <td>Estonia</td>
      <td>Overall Global Gender Gap Index</td>
      <td>Rank</td>
      <td>29.0</td>
      <td>30.0</td>
      <td>37.0</td>
      <td>37.0</td>
      <td>47.0</td>
      <td>52.0</td>
      <td>60.0</td>
      <td>59.0</td>
      <td>62.0</td>
      <td>21.0</td>
      <td>22.0</td>
      <td>41.0</td>
      <td>2014-2015</td>
    </tr>
    <tr>
      <th>657</th>
      <td>GHA</td>
      <td>Ghana</td>
      <td>Overall Global Gender Gap Index</td>
      <td>Rank</td>
      <td>58.0</td>
      <td>63.0</td>
      <td>77.0</td>
      <td>80.0</td>
      <td>70.0</td>
      <td>70.0</td>
      <td>71.0</td>
      <td>76.0</td>
      <td>101.0</td>
      <td>63.0</td>
      <td>59.0</td>
      <td>38.0</td>
      <td>2014-2015</td>
    </tr>
    <tr>
      <th>530</th>
      <td>ECU</td>
      <td>Ecuador</td>
      <td>Overall Global Gender Gap Index</td>
      <td>Rank</td>
      <td>82.0</td>
      <td>44.0</td>
      <td>35.0</td>
      <td>23.0</td>
      <td>40.0</td>
      <td>45.0</td>
      <td>33.0</td>
      <td>25.0</td>
      <td>21.0</td>
      <td>33.0</td>
      <td>40.0</td>
      <td>38.0</td>
      <td>2006-2007</td>
    </tr>
    <tr>
      <th>1054</th>
      <td>LUX</td>
      <td>Luxembourg</td>
      <td>Overall Global Gender Gap Index</td>
      <td>Rank</td>
      <td>56.0</td>
      <td>58.0</td>
      <td>66.0</td>
      <td>63.0</td>
      <td>26.0</td>
      <td>30.0</td>
      <td>17.0</td>
      <td>21.0</td>
      <td>28.0</td>
      <td>32.0</td>
      <td>34.0</td>
      <td>37.0</td>
      <td>2009-2010</td>
    </tr>
  </tbody>
</table>
</div>



### Kenya


```python
country_scatterplot('Kenya')
country_boxplot('Kenya')
```


<div id="ac0a7fc6-ef9b-449a-99aa-a7c2b4a3e37c" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("ac0a7fc6-ef9b-449a-99aa-a7c2b4a3e37c", [{"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [40.0, 59.0, 41.0, 50.0, 82.0, 83.0, 35.0, 44.0, 9.0, 25.0, 48.0], "marker": {"color": "red"}, "name": "Economic Participation", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [88.0, 97.0, 102.0, 106.0, 102.0, 101.0, 106.0, 107.0, 115.0, 113.0, 116.0], "marker": {"color": "blue"}, "name": "Education", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [96.0, 104.0, 105.0, 110.0, 101.0, 102.0, 103.0, 102.0, 80.0, 85.0, 83.0], "marker": {"color": "green"}, "name": "Health", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [93.0, 104.0, 121.0, 122.0, 98.0, 100.0, 103.0, 85.0, 48.0, 62.0, 64.0], "marker": {"color": "brown"}, "name": "Political", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [73.0, 83.0, 88.0, 97.0, 96.0, 99.0, 72.0, 78.0, 37.0, 48.0, 63.0], "marker": {"color": "purple"}, "name": "Overall", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [null, null, null, null, null, null, null, null, null, null, 67.0], "marker": {"color": "orange"}, "name": "Wage Equality", "mode": "lines"}], {"title": "Kenya", "xaxis": {"title": "Years"}, "yaxis": {"title": "Rank"}}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>



<div id="f409c4c7-f40e-4871-8b2f-bc39c5edb3dd" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("f409c4c7-f40e-4871-8b2f-bc39c5edb3dd", [{"type": "box", "y": [40.0, 59.0, 41.0, 50.0, 82.0, 83.0, 35.0, 44.0, 9.0, 25.0, 48.0], "boxpoints": "all", "marker": {"color": "red"}, "name": "Economic Participation"}, {"type": "box", "y": [88.0, 97.0, 102.0, 106.0, 102.0, 101.0, 106.0, 107.0, 115.0, 113.0, 116.0], "boxpoints": "all", "marker": {"color": "blue"}, "name": "Education"}, {"type": "box", "y": [96.0, 104.0, 105.0, 110.0, 101.0, 102.0, 103.0, 102.0, 80.0, 85.0, 83.0], "boxpoints": "all", "marker": {"color": "green"}, "name": "Health"}, {"type": "box", "y": [93.0, 104.0, 121.0, 122.0, 98.0, 100.0, 103.0, 85.0, 48.0, 62.0, 64.0], "boxpoints": "all", "marker": {"color": "black"}, "name": "Political"}, {"type": "box", "y": [73.0, 83.0, 88.0, 97.0, 96.0, 99.0, 72.0, 78.0, 37.0, 48.0, 63.0], "boxpoints": "all", "marker": {"color": "purple"}, "name": "Overall"}, {"type": "box", "y": [null, null, null, null, null, null, null, null, null, null, 67.0], "boxpoints": "all", "marker": {"color": "orange"}, "name": "Wage Equality"}], {"title": "Kenya", "yaxis": {"title": "Rank"}}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>


When the overall ranks are sorted according to the newly created maximum difference column, we see that Kenya and Estonia decreased their ranks by 41 points (Kenya in 2013-2014 and Estonia in 2014-2015). Over the years since 2006, we see that Kenya's overall rank got worse until 2011 (when its rank=99). After 2011, their overall rank got better mainly due to the decrease in economic participation rank. After 2011, political empowerment and economic participation rank graphs follow a similar trend. Accordingly, graph for their overall rank also follows a similar pattern. After 2014, their rank started to increase again and it was 63 in 2016.

### Estonia


```python
country_scatterplot('Estonia')
country_boxplot('Estonia')

```


<div id="420a99cd-d74d-4518-8313-1c9fea171475" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("420a99cd-d74d-4518-8313-1c9fea171475", [{"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [27.0, 34.0, 33.0, 36.0, 35.0, 35.0, 40.0, 41.0, 56.0, 47.0, 50.0], "marker": {"color": "red"}, "name": "Economic Participation", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [16.0, 20.0, 48.0, 37.0, 38.0, 38.0, 58.0, 59.0, 1.0, 39.0, 53.0], "marker": {"color": "blue"}, "name": "Education", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [36.0, 37.0, 38.0, 41.0, 50.0, 51.0, 34.0, 34.0, 37.0, 1.0, 1.0], "marker": {"color": "green"}, "name": "Health", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [51.0, 51.0, 48.0, 50.0, 74.0, 87.0, 87.0, 88.0, 88.0, 30.0, 30.0], "marker": {"color": "brown"}, "name": "Political", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [29.0, 30.0, 37.0, 37.0, 47.0, 52.0, 60.0, 59.0, 62.0, 21.0, 22.0], "marker": {"color": "purple"}, "name": "Overall", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [null, null, null, null, null, null, null, null, null, null, 73.0], "marker": {"color": "orange"}, "name": "Wage Equality", "mode": "lines"}], {"title": "Estonia", "xaxis": {"title": "Years"}, "yaxis": {"title": "Rank"}}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>



<div id="b0cc85f9-c5c3-42fc-818f-af58593dc671" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("b0cc85f9-c5c3-42fc-818f-af58593dc671", [{"type": "box", "y": [27.0, 34.0, 33.0, 36.0, 35.0, 35.0, 40.0, 41.0, 56.0, 47.0, 50.0], "boxpoints": "all", "marker": {"color": "red"}, "name": "Economic Participation"}, {"type": "box", "y": [16.0, 20.0, 48.0, 37.0, 38.0, 38.0, 58.0, 59.0, 1.0, 39.0, 53.0], "boxpoints": "all", "marker": {"color": "blue"}, "name": "Education"}, {"type": "box", "y": [36.0, 37.0, 38.0, 41.0, 50.0, 51.0, 34.0, 34.0, 37.0, 1.0, 1.0], "boxpoints": "all", "marker": {"color": "green"}, "name": "Health"}, {"type": "box", "y": [51.0, 51.0, 48.0, 50.0, 74.0, 87.0, 87.0, 88.0, 88.0, 30.0, 30.0], "boxpoints": "all", "marker": {"color": "black"}, "name": "Political"}, {"type": "box", "y": [29.0, 30.0, 37.0, 37.0, 47.0, 52.0, 60.0, 59.0, 62.0, 21.0, 22.0], "boxpoints": "all", "marker": {"color": "purple"}, "name": "Overall"}, {"type": "box", "y": [null, null, null, null, null, null, null, null, null, null, 73.0], "boxpoints": "all", "marker": {"color": "orange"}, "name": "Wage Equality"}], {"title": "Estonia", "yaxis": {"title": "Rank"}}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>


Estonia's overall rank decreased from 62 to 21 in 2015, which was the maximum drop in any given successive years. This improvement might be due to their commitment to achieving gender equality by promoting women's rights, taking measures to reduce and prevent violence agaist women and increasing their efforts in closing the gender pay gap (http://www.unwomen.org/en/get-involved/step-it-up/commitments/estonia). The fact that their rank was still around 21 in 2016 might be an indication that they are working on addressing these issues but more data is needed to support this guess.

### Ghana


```python
country_scatterplot('Ghana')
country_boxplot('Ghana')
```


<div id="c41fdc66-4bff-46a8-9d9c-bd6187ec4d37" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("c41fdc66-4bff-46a8-9d9c-bd6187ec4d37", [{"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [5.0, 3.0, 14.0, 13.0, 15.0, 17.0, 26.0, 24.0, 64.0, 13.0, 10.0], "marker": {"color": "red"}, "name": "Economic Participation", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [94.0, 106.0, 110.0, 112.0, 111.0, 111.0, 113.0, 111.0, 117.0, 119.0, 119.0], "marker": {"color": "blue"}, "name": "Education", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [89.0, 105.0, 106.0, 111.0, 103.0, 104.0, 105.0, 104.0, 116.0, 87.0, 85.0], "marker": {"color": "green"}, "name": "Health", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [80.0, 91.0, 94.0, 101.0, 88.0, 91.0, 100.0, 95.0, 97.0, 96.0, 95.0], "marker": {"color": "brown"}, "name": "Political", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [58.0, 63.0, 77.0, 80.0, 70.0, 70.0, 71.0, 76.0, 101.0, 63.0, 59.0], "marker": {"color": "purple"}, "name": "Overall", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [null, null, null, null, null, null, null, null, null, null, 26.0], "marker": {"color": "orange"}, "name": "Wage Equality", "mode": "lines"}], {"title": "Ghana", "xaxis": {"title": "Years"}, "yaxis": {"title": "Rank"}}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>



<div id="be6c9409-835d-454b-9b8f-d0ebcb8f8a2f" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("be6c9409-835d-454b-9b8f-d0ebcb8f8a2f", [{"type": "box", "y": [5.0, 3.0, 14.0, 13.0, 15.0, 17.0, 26.0, 24.0, 64.0, 13.0, 10.0], "boxpoints": "all", "marker": {"color": "red"}, "name": "Economic Participation"}, {"type": "box", "y": [94.0, 106.0, 110.0, 112.0, 111.0, 111.0, 113.0, 111.0, 117.0, 119.0, 119.0], "boxpoints": "all", "marker": {"color": "blue"}, "name": "Education"}, {"type": "box", "y": [89.0, 105.0, 106.0, 111.0, 103.0, 104.0, 105.0, 104.0, 116.0, 87.0, 85.0], "boxpoints": "all", "marker": {"color": "green"}, "name": "Health"}, {"type": "box", "y": [80.0, 91.0, 94.0, 101.0, 88.0, 91.0, 100.0, 95.0, 97.0, 96.0, 95.0], "boxpoints": "all", "marker": {"color": "black"}, "name": "Political"}, {"type": "box", "y": [58.0, 63.0, 77.0, 80.0, 70.0, 70.0, 71.0, 76.0, 101.0, 63.0, 59.0], "boxpoints": "all", "marker": {"color": "purple"}, "name": "Overall"}, {"type": "box", "y": [null, null, null, null, null, null, null, null, null, null, 26.0], "boxpoints": "all", "marker": {"color": "orange"}, "name": "Wage Equality"}], {"title": "Ghana", "yaxis": {"title": "Rank"}}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>


In Ghana, the line plots shows that the overall rank is affected by the economic participation and health and survival subindexes more than the other subindexes.  In 2014, all of its subindexes got worse, economic participation subindex increased to 64 from 24 and overall rank increased to 101 from 76. However, after 2014, their index gradually improved to 38 in 2016. Their rank in 2016 was better than all other ranks in years 2006-2015.

## 3. Which countries improved their ranking or preserved it multiple times between years 2006 and 2016?


```python
df_pos_count=ranking.copy()

dict_ch2={}

for index,row in df_pos_count.iterrows():
    count=0
    for i in range(2006,2016):
        if pd.notna(row[str(i)])==True and pd.notna(row[str(i+1)])==True:
            if row[str(i)]>=row[str(i+1)]:
                count+=1
            else:
                count=count
    dict_ch2[index]=count

df_pos_count["count_positive"]=dict_ch2.values()

df_pos_count_sorted=df_pos_count.sort_values(by='count_positive',ascending=False)

df_pos_count_sorted.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Country ISO3</th>
      <th>Country Name</th>
      <th>Indicator</th>
      <th>Subindicator Type</th>
      <th>2006</th>
      <th>2007</th>
      <th>2008</th>
      <th>2009</th>
      <th>2010</th>
      <th>2011</th>
      <th>2012</th>
      <th>2013</th>
      <th>2014</th>
      <th>2015</th>
      <th>2016</th>
      <th>count_positive</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>820</th>
      <td>ISL</td>
      <td>Iceland</td>
      <td>Overall Global Gender Gap Index</td>
      <td>Rank</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>10</td>
    </tr>
    <tr>
      <th>1415</th>
      <td>PHL</td>
      <td>Philippines</td>
      <td>Overall Global Gender Gap Index</td>
      <td>Rank</td>
      <td>6.0</td>
      <td>6.0</td>
      <td>6.0</td>
      <td>9.0</td>
      <td>9.0</td>
      <td>8.0</td>
      <td>8.0</td>
      <td>5.0</td>
      <td>9.0</td>
      <td>7.0</td>
      <td>7.0</td>
      <td>8</td>
    </tr>
    <tr>
      <th>595</th>
      <td>FIN</td>
      <td>Finland</td>
      <td>Overall Global Gender Gap Index</td>
      <td>Rank</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>8</td>
    </tr>
    <tr>
      <th>1620</th>
      <td>SWE</td>
      <td>Sweden</td>
      <td>Overall Global Gender Gap Index</td>
      <td>Rank</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>8</td>
    </tr>
    <tr>
      <th>1607</th>
      <td>SVN</td>
      <td>Slovenia</td>
      <td>Overall Global Gender Gap Index</td>
      <td>Rank</td>
      <td>51.0</td>
      <td>49.0</td>
      <td>51.0</td>
      <td>52.0</td>
      <td>42.0</td>
      <td>41.0</td>
      <td>38.0</td>
      <td>38.0</td>
      <td>23.0</td>
      <td>9.0</td>
      <td>8.0</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>



### Iceland


```python
country_scatterplot('Iceland')
country_boxplot('Iceland')
```


<div id="a74d79e0-2b84-4535-a4e1-65fe96c86730" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("a74d79e0-2b84-4535-a4e1-65fe96c86730", [{"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [17.0, 23.0, 20.0, 16.0, 18.0, 24.0, 27.0, 22.0, 7.0, 5.0, 9.0], "marker": {"color": "red"}, "name": "Economic Participation", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [49.0, 67.0, 61.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0], "marker": {"color": "blue"}, "name": "Education", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [92.0, 95.0, 96.0, 101.0, 96.0, 96.0, 98.0, 97.0, 128.0, 105.0, 104.0], "marker": {"color": "green"}, "name": "Health", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [4.0, 4.0, 3.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0], "marker": {"color": "brown"}, "name": "Political", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [4.0, 4.0, 4.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0], "marker": {"color": "purple"}, "name": "Overall", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [null, null, null, null, null, null, null, null, null, null, 11.0], "marker": {"color": "orange"}, "name": "Wage Equality", "mode": "lines"}], {"title": "Iceland", "xaxis": {"title": "Years"}, "yaxis": {"title": "Rank"}}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>



<div id="08b452ca-c277-4500-8f31-991ea2780861" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("08b452ca-c277-4500-8f31-991ea2780861", [{"type": "box", "y": [17.0, 23.0, 20.0, 16.0, 18.0, 24.0, 27.0, 22.0, 7.0, 5.0, 9.0], "boxpoints": "all", "marker": {"color": "red"}, "name": "Economic Participation"}, {"type": "box", "y": [49.0, 67.0, 61.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0], "boxpoints": "all", "marker": {"color": "blue"}, "name": "Education"}, {"type": "box", "y": [92.0, 95.0, 96.0, 101.0, 96.0, 96.0, 98.0, 97.0, 128.0, 105.0, 104.0], "boxpoints": "all", "marker": {"color": "green"}, "name": "Health"}, {"type": "box", "y": [4.0, 4.0, 3.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0], "boxpoints": "all", "marker": {"color": "black"}, "name": "Political"}, {"type": "box", "y": [4.0, 4.0, 4.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0], "boxpoints": "all", "marker": {"color": "purple"}, "name": "Overall"}, {"type": "box", "y": [null, null, null, null, null, null, null, null, null, null, 11.0], "boxpoints": "all", "marker": {"color": "orange"}, "name": "Wage Equality"}], {"title": "Iceland", "yaxis": {"title": "Rank"}}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>


For the last 8 years, Iceland has the highest global overall rank. From the line graph above, we see that once they improved their educational attainment rank, they were able to preserve their rank as number one. 

According to President Johannesson's statement, gender pay gap in Iceland is around 5.7-18.3% (https://www.heforshe.org/en/impact). This shows that even in the number one country, the gender gap is around 10% on average. For more details, please look at https://www.weforum.org/agenda/2017/11/why-iceland-ranks-first-gender-equality/. 

### Philippines


```python
country_scatterplot('Philippines')
country_boxplot('Philippines')
```


<div id="2bc93a3f-9f67-4368-bef4-295695faf687" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("2bc93a3f-9f67-4368-bef4-295695faf687", [{"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [4.0, 2.0, 8.0, 11.0, 13.0, 15.0, 17.0, 16.0, 24.0, 16.0, 21.0], "marker": {"color": "red"}, "name": "Economic Participation", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 34.0, 1.0], "marker": {"color": "blue"}, "name": "Education", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0], "marker": {"color": "green"}, "name": "Health", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [16.0, 14.0, 22.0, 19.0, 17.0, 16.0, 14.0, 10.0, 17.0, 17.0, 17.0], "marker": {"color": "brown"}, "name": "Political", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [6.0, 6.0, 6.0, 9.0, 9.0, 8.0, 8.0, 5.0, 9.0, 7.0, 7.0], "marker": {"color": "purple"}, "name": "Overall", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [null, null, null, null, null, null, null, null, null, null, 7.0], "marker": {"color": "orange"}, "name": "Wage Equality", "mode": "lines"}], {"title": "Philippines", "xaxis": {"title": "Years"}, "yaxis": {"title": "Rank"}}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>



<div id="18e1b06f-b877-4a9e-af70-fab8a17cc3f0" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("18e1b06f-b877-4a9e-af70-fab8a17cc3f0", [{"type": "box", "y": [4.0, 2.0, 8.0, 11.0, 13.0, 15.0, 17.0, 16.0, 24.0, 16.0, 21.0], "boxpoints": "all", "marker": {"color": "red"}, "name": "Economic Participation"}, {"type": "box", "y": [1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 34.0, 1.0], "boxpoints": "all", "marker": {"color": "blue"}, "name": "Education"}, {"type": "box", "y": [1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0], "boxpoints": "all", "marker": {"color": "green"}, "name": "Health"}, {"type": "box", "y": [16.0, 14.0, 22.0, 19.0, 17.0, 16.0, 14.0, 10.0, 17.0, 17.0, 17.0], "boxpoints": "all", "marker": {"color": "black"}, "name": "Political"}, {"type": "box", "y": [6.0, 6.0, 6.0, 9.0, 9.0, 8.0, 8.0, 5.0, 9.0, 7.0, 7.0], "boxpoints": "all", "marker": {"color": "purple"}, "name": "Overall"}, {"type": "box", "y": [null, null, null, null, null, null, null, null, null, null, 7.0], "boxpoints": "all", "marker": {"color": "orange"}, "name": "Wage Equality"}], {"title": "Philippines", "yaxis": {"title": "Rank"}}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>


Philippines was always in Top 10 since 2006 in the overall ranking. Between 2006 and 2016, their overall rank got worse only two times in 2009 and in 2014. According to the line graph above, we see that Philippines overall rank graph is very similar to their political empowerment rank graph. Another factor contributing to their overall rank would be economic participation. 

Note that their overall rank increased by 2 points in 2015 even though their educational attainment rank dropped by 34 points in 2015. It seems like the improvement in their overall rank is due to the improvement in their economic participation rank (from 24 to 16) since political empowerment and health and survival ranks stayed the same in that year.

For more details about their efforts, we refer to the State of Filipino Women Report at (https://pcw.gov.ph/sites/default/files/documents/resources/ESTADO%20NI%20JUANA_THE%20STATE%20OF%20FILIPINO%20WOMEN%20REPORT.pdf)

### Finland


```python
country_scatterplot('Finland')
country_boxplot('Finland')

```


<div id="7abe4605-c55c-428f-b50a-550551c6933c" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("7abe4605-c55c-428f-b50a-550551c6933c", [{"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [8.0, 22.0, 19.0, 15.0, 16.0, 12.0, 14.0, 19.0, 21.0, 8.0, 16.0], "marker": {"color": "red"}, "name": "Economic Participation", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [17.0, 21.0, 1.0, 1.0, 28.0, 26.0, 1.0, 1.0, 1.0, 1.0, 1.0], "marker": {"color": "blue"}, "name": "Education", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 52.0, 1.0, 1.0], "marker": {"color": "green"}, "name": "Health", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [3.0, 2.0, 1.0, 2.0, 2.0, 2.0, 2.0, 2.0, 2.0, 2.0, 2.0], "marker": {"color": "brown"}, "name": "Political", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [3.0, 3.0, 2.0, 2.0, 3.0, 3.0, 2.0, 2.0, 2.0, 3.0, 2.0], "marker": {"color": "purple"}, "name": "Overall", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [null, null, null, null, null, null, null, null, null, null, 6.0], "marker": {"color": "orange"}, "name": "Wage Equality", "mode": "lines"}], {"title": "Finland", "xaxis": {"title": "Years"}, "yaxis": {"title": "Rank"}}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>



<div id="b6f81631-23ad-469d-8892-3c759848f01d" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("b6f81631-23ad-469d-8892-3c759848f01d", [{"type": "box", "y": [8.0, 22.0, 19.0, 15.0, 16.0, 12.0, 14.0, 19.0, 21.0, 8.0, 16.0], "boxpoints": "all", "marker": {"color": "red"}, "name": "Economic Participation"}, {"type": "box", "y": [17.0, 21.0, 1.0, 1.0, 28.0, 26.0, 1.0, 1.0, 1.0, 1.0, 1.0], "boxpoints": "all", "marker": {"color": "blue"}, "name": "Education"}, {"type": "box", "y": [1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 52.0, 1.0, 1.0], "boxpoints": "all", "marker": {"color": "green"}, "name": "Health"}, {"type": "box", "y": [3.0, 2.0, 1.0, 2.0, 2.0, 2.0, 2.0, 2.0, 2.0, 2.0, 2.0], "boxpoints": "all", "marker": {"color": "black"}, "name": "Political"}, {"type": "box", "y": [3.0, 3.0, 2.0, 2.0, 3.0, 3.0, 2.0, 2.0, 2.0, 3.0, 2.0], "boxpoints": "all", "marker": {"color": "purple"}, "name": "Overall"}, {"type": "box", "y": [null, null, null, null, null, null, null, null, null, null, 6.0], "boxpoints": "all", "marker": {"color": "orange"}, "name": "Wage Equality"}], {"title": "Finland", "yaxis": {"title": "Rank"}}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>


Finland is one of the counties that are always in Top 3 in overall ranking. It seems like their overall rank is more dependent on their political empowerment rank since overall rank didn't get affected by their educational attainment rank, which varied a lot between years 2006 and 2016, and their economic participation rank,which was always between 8 and 22. For more information, we refer the reader to http://www.stat.fi/tup/tasaarvo/index_en.html.



```python
country_scatterplot('United States')
country_boxplot('United States')
```


<div id="6d64d94b-401a-4394-9058-da3dff0ebefd" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("6d64d94b-401a-4394-9058-da3dff0ebefd", [{"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [3.0, 14.0, 12.0, 17.0, 6.0, 6.0, 8.0, 6.0, 4.0, 6.0, 26.0], "marker": {"color": "red"}, "name": "Economic Participation", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [66.0, 76.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 39.0, 40.0, 1.0], "marker": {"color": "blue"}, "name": "Education", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [1.0, 36.0, 37.0, 40.0, 38.0, 39.0, 33.0, 33.0, 62.0, 64.0, 62.0], "marker": {"color": "green"}, "name": "Health", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [66.0, 69.0, 56.0, 61.0, 40.0, 39.0, 55.0, 60.0, 54.0, 72.0, 73.0], "marker": {"color": "brown"}, "name": "Political", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [23.0, 31.0, 27.0, 31.0, 19.0, 17.0, 22.0, 23.0, 20.0, 28.0, 45.0], "marker": {"color": "purple"}, "name": "Overall", "mode": "lines"}, {"type": "scatter", "x": ["2006", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"], "y": [null, null, null, null, null, null, null, null, null, null, 66.0], "marker": {"color": "orange"}, "name": "Wage Equality", "mode": "lines"}], {"title": "United States", "xaxis": {"title": "Years"}, "yaxis": {"title": "Rank"}}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>



<div id="f41c3427-1dc1-4a2e-9392-07312bd4ef92" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("f41c3427-1dc1-4a2e-9392-07312bd4ef92", [{"type": "box", "y": [3.0, 14.0, 12.0, 17.0, 6.0, 6.0, 8.0, 6.0, 4.0, 6.0, 26.0], "boxpoints": "all", "marker": {"color": "red"}, "name": "Economic Participation"}, {"type": "box", "y": [66.0, 76.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 39.0, 40.0, 1.0], "boxpoints": "all", "marker": {"color": "blue"}, "name": "Education"}, {"type": "box", "y": [1.0, 36.0, 37.0, 40.0, 38.0, 39.0, 33.0, 33.0, 62.0, 64.0, 62.0], "boxpoints": "all", "marker": {"color": "green"}, "name": "Health"}, {"type": "box", "y": [66.0, 69.0, 56.0, 61.0, 40.0, 39.0, 55.0, 60.0, 54.0, 72.0, 73.0], "boxpoints": "all", "marker": {"color": "black"}, "name": "Political"}, {"type": "box", "y": [23.0, 31.0, 27.0, 31.0, 19.0, 17.0, 22.0, 23.0, 20.0, 28.0, 45.0], "boxpoints": "all", "marker": {"color": "purple"}, "name": "Overall"}, {"type": "box", "y": [null, null, null, null, null, null, null, null, null, null, 66.0], "boxpoints": "all", "marker": {"color": "orange"}, "name": "Wage Equality"}], {"title": "United States", "yaxis": {"title": "Rank"}}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>


Overall Global Gender Gap rank of United States was 45 in 2016, which was 22 points less than the Overall Rank in 2006. United States' overall rank got worse in 2015 and 2016 even though there was improvement several times between 2006-2016. Overall rank line graph above looks more similar to the line graph for the economic participation but its values were not as low as economic participation ranking values. It seems like high political empowerment ranking also affected overall gender gap ranking. However, more data is needed to support this claim as the political empowerment ranking fluctuates a lot.


```python
overall[overall["Country Name"]=='United States']
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Country ISO3</th>
      <th>Country Name</th>
      <th>Indicator</th>
      <th>Subindicator Type</th>
      <th>2006</th>
      <th>2007</th>
      <th>2008</th>
      <th>2009</th>
      <th>2010</th>
      <th>2011</th>
      <th>2012</th>
      <th>2013</th>
      <th>2014</th>
      <th>2015</th>
      <th>2016</th>
      <th>Average Rank</th>
      <th>Change 2006-2016</th>
      <th>Numerical Change 2006-2016</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1796</th>
      <td>USA</td>
      <td>United States</td>
      <td>Overall Global Gender Gap Index</td>
      <td>Rank</td>
      <td>23.0</td>
      <td>31.0</td>
      <td>27.0</td>
      <td>31.0</td>
      <td>19.0</td>
      <td>17.0</td>
      <td>22.0</td>
      <td>23.0</td>
      <td>20.0</td>
      <td>28.0</td>
      <td>45.0</td>
      <td>26</td>
      <td>negative</td>
      <td>-22.0</td>
    </tr>
  </tbody>
</table>
</div>



# CONCLUSION

In this report, we focused on positive changes and improvements and explored some factors influencing these changes. A similar study can be done by exploring the countries who decreased their ranking and explore and the events leading up to the decrease in their ranks.

Since WEF started publishing their reports for the first time in 2005, there are many positive steps taken in many countries to decrease the gap in their countries as well as on a global level. However, even in Iceland, #1 in the last 8 years, the gender gap is around 5.7-18.3% (https://www.heforshe.org/en/impact). 


