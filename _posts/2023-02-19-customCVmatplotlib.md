---
layout: post
title: "Putting the \"graphic\" back in \"biographic\": Make your CV using matplotlib"
tags: CV matplotlib jupyter
---

In general, I've had issue with expressing myself through my CV. This week I took the time to create a CV that's more funky than average. Here's the code, jupyter notebook style, to make it from scratch using python, a dash of numpy, pandas and, most importantly, matplotlib.


```python
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
%matplotlib inline
```

The most important question a CV should answer, as a biographic note, is where you are coming from. So, first thing is to prep an object that contains this information, and take advantage of the smooth co-operation between pandas and matplotlib.

I use monthly frequency in the `date_range` objects, noone should need more granularity in a CV. Columns are used according to the purposes of a graph, and to not lose track of parallel activities. Extra dates in the end are used for graph padding.


```python
history_df = pd.DataFrame()

date_range = pd.date_range(start="2011-08", end='2023-03', freq='m')
history_df['Date'] = date_range
history_df.set_index('Date', inplace=True)
history_df['Education'] = ""
history_df['Army'] = ""
history_df['Occupation'] = ""

# N.B. date_range stops a month earlier, so e.g. where it would end 2016-10 I put 2016-11
ranges = {
    'BSc in Physics': pd.date_range(start="2011-09", end='2016-08', freq='m'),
    'MSc in Physics': pd.date_range(start="2016-09", end='2017-08', freq='m'),
    'Hellenic Air Force': pd.date_range(start="2017-09", end='2018-09', freq='m'),
    'PhD in Physics': pd.date_range(start="2017-11", end='2022-06', freq='m'),
    'IT Business Analyst': pd.date_range(start="2021-11", end='2022-12', freq='m'),
}

history_df.loc[ranges['BSc in Physics'], 'Education'] = "BSc in Physics"
history_df.loc[ranges['MSc in Physics'], 'Education'] = "MSc in Physics"
history_df.loc[ranges['Hellenic Air Force'], 'Army'] = "Hellenic Air Force"
history_df.loc[ranges['PhD in Physics'], 'Education'] = "PhD in Physics"
history_df.loc[ranges['IT Business Analyst'], 'Occupation'] = "IT Business Analyst"

history_df
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
      <th>Date</th>
      <th>Education</th>
      <th>Army</th>
      <th>Occupation</th>
    </tr>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr style="text-align: right;">
      <th>2011-08-31</th>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr style="text-align: right;">
      <th>2011-09-30</th>
      <td>BSc in Physics</td>
      <td></td>
      <td></td>
    </tr>
    <tr style="text-align: right;">
      <th>2011-10-31</th>
      <td>BSc in Physics</td>
      <td></td>
      <td></td>
    </tr>
    <tr style="text-align: right;">
      <th>2011-11-30</th>
      <td>BSc in Physics</td>
      <td></td>
      <td></td>
    </tr>
    <tr style="text-align: right;">
      <th>2011-12-31</th>
      <td>BSc in Physics</td>
      <td></td>
      <td></td>
    </tr>
    <tr style="text-align: right;">
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr style="text-align: right;">
      <th>2022-10-31</th>
      <td></td>
      <td></td>
      <td>IT Business Analyst</td>
    </tr>
    <tr style="text-align: right;">
      <th>2022-11-30</th>
      <td></td>
      <td></td>
      <td>IT Business Analyst</td>
    </tr>
    <tr style="text-align: right;">
      <th>2022-12-31</th>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr style="text-align: right;">
      <th>2023-01-31</th>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr style="text-align: right;">
      <th>2023-02-28</th>
      <td></td>
      <td></td>
      <td></td>
    </tr>
  </tbody>
</table>
<p>139 rows × 3 columns</p>
</div>



## A4 Arrangement

If you stopped to think about how one can use code to make a CV with graphs, you may have thought that one could generate some pictures that could then be put in a photo editing software or an online canvas to continue. But why not use matplotlib for the whole thing?

First, think of how you'd layer the information in a A4 sheet of paper. Afterwards, matplotlib's `add_gridspec` allows you to create a custom grid of objects to your liking.

Notice I used fewer inches for the A4 page size. In fact, one of the things that I couldn't quite tune is the page margins that push the graphs towards the center of the page. This tweak allows me to "print" the page on second step to get a bit more margin space.


```python
# gridspec A4 matplotlib
# see also https://stackoverflow.com/questions/56824062/matplotlib-gridspec-plots-and-images-on-a4-page
fig = plt.figure(dpi=300, tight_layout=True)
fig.set_size_inches(8, 11, forward=True)

gs = fig.add_gridspec(
    3, 2, width_ratios=[1, 1], height_ratios=[0.5, 0.65, 0.3],
)

ax = np.zeros(9, dtype=object)
ax[0] = fig.add_subplot(gs[0, :])
ax[1] = fig.add_subplot(gs[1, 0])
ax[2] = fig.add_subplot(gs[2, 0])
ax[3] = fig.add_subplot(gs[1:3, 1:3])

```


    
![png]({{site.baseurl}}/assets/img/CV-dashboard-post_files/CV-dashboard-post_5_0.png)
    


## Career Timeline

To put the "graphic" back in "biographic", let's make the career timeline portion of our CV more easily readable to the reader. After experimenting and receiving some feedback, I understand that a custom timeline plot would be ideal for this job.

Using the date ranges of the information given in the pandas dataframe, we can set up a quick timeline that the eye can follow both horizontally and vertically. Details of each portion are given as annotations, and the beginning and end of a timeline arrow are shown with custom markers.

```python
# use A4
ax = fig.axes[0]

year_xticks = pd.date_range(start='2015-01-01', end='2024-01-01', freq='m')

# will annotate BSc towards the end, so keep only 17 last points, and all points for the rest
bsc_years = pd.date_range(start=ranges['BSc in Physics'][-17:][0], end=ranges['BSc in Physics'][-1], freq='m') 
msc_years = pd.date_range(start=ranges['MSc in Physics'][0], end=ranges['MSc in Physics'][-1], freq='m')
phd_years = pd.date_range(start=ranges['PhD in Physics'][0], end=ranges['PhD in Physics'][-1], freq='m')
haf_years = pd.date_range(start=ranges['Hellenic Air Force'][0], end=ranges['Hellenic Air Force'][-1], freq='m')
it_years = pd.date_range(start=ranges['IT Business Analyst'][0], end=ranges['IT Business Analyst'][-1], freq='m')

ax.plot(bsc_years, np.linspace(3,3, len(bsc_years)), markerfacecolor='white',   linewidth=3, c="#567189")
ax.plot(bsc_years[0], [3],  marker="", c="#567189", markersize=4) # no marker to indicate it was on-going
ax.plot(bsc_years[-1], [3], marker=9, c="#567189", markersize=6)
ax.annotate(f'BSc in Physics', xy=(bsc_years[0], 3), xytext=(bsc_years[0], 3.3), bbox=dict(facecolor='black', alpha=0.75), color='white',)

ax.plot(msc_years, np.linspace(2,2, len(msc_years)), markerfacecolor='white',   linewidth=3, c='#7B8FA1')
ax.plot(msc_years[0], [2],  marker="o", c="#7B8FA1", markersize=4)
ax.plot(msc_years[-1], [2], marker=9, c="#7B8FA1", markersize=6)
ax.annotate(f'MSc in Physics', xy=(msc_years[0], 2), xytext=(msc_years[0], 2.3), bbox=dict(facecolor='black', alpha=0.75), color='white',)

ax.plot(haf_years, np.linspace(1,1, len(haf_years)), markerfacecolor='white', linewidth=3, c='#CFB997')
ax.plot(haf_years[0], [1],  marker="o", c="#CFB997", markersize=4)
ax.plot(haf_years[-1], [1], marker=9, c="#CFB997", markersize=6)
ax.annotate(f'Mandatory Army Service (HAF)', xy=(haf_years[0], 1), xytext=(haf_years[0], 1.3), bbox=dict(facecolor='black', alpha=0.75), color='white',)

ax.plot(phd_years, np.linspace(-1,-1, len(phd_years)), markerfacecolor='white', linewidth=3, c='teal')
ax.plot(phd_years[0], [-1],  marker="o", c="teal", markersize=4)
ax.plot(phd_years[-1], [-1], marker=9, c="teal", markersize=6)
ax.annotate(f'PhD in Physics', xy=(phd_years[0], -1), xytext=(phd_years[0], -0.7), bbox=dict(facecolor='black', alpha=0.75), color='white',)

ax.plot(it_years, np.linspace(-2,-2, len(it_years)), markerfacecolor='white',   linewidth=3, c='olive')
ax.plot(it_years[0], [-2],  marker="o", c="olive", markersize=4)
ax.plot(it_years[-1], [-2], marker=9, c="olive", markersize=6)
ax.annotate(f'IT Business Analyst', xy=(it_years[0], -2), xytext=(it_years[0], -1.7), bbox=dict(facecolor='black', alpha=0.75), color='white',)

ax.set_xticks(year_xticks, year_xticks)
ax.set_ylim(-3,4)
ax.set_xlim(16500)

# hide axis spines
ax.spines[["left", "top", "right"]].set_visible(False)
ax.set_ylabel("Career Evolution", fontsize=14, fontweight='semibold', family='monospace', color = 'grey')
ax.xaxis.set_tick_params(labelsize='large')
ax.set_facecolor("lightyellow")

# hide ticks and tick labels
# https://stackoverflow.com/questions/29988241/python-hide-ticks-but-show-tick-labels
ax.set_yticks([])
ax.set_yticklabels([])

for tick in ax.get_xticklabels():
    tick.set_fontname("monospace")
    
# # Turn grid on for both major and minor ticks and style minor slightly
# # differently.
ax.grid(which='major', color='#CCCCCC', linestyle='--')
ax.grid(which='minor', color='#CCCCCC', linestyle=':')

# use advanced mpl ticks
# https://stackoverflow.com/questions/45704366/how-to-change-the-datetime-tick-label-frequency-for-matplotlib-plots
import matplotlib.dates as mdates     # v 3.3.2
# Create custom ticks using matplotlib date tick locator and formatter
# https://stackoverflow.com/questions/75466013/matplotlib-major-and-minor-ticks-misaligned-when-using-pandas-date-range?noredirect=1#comment133152201_75466013
loc_minor = mdates.MonthLocator(interval=1)
loc_major = mdates.YearLocator()
ax.xaxis.set_major_locator(loc_major)
ax.xaxis.set_minor_locator(loc_minor) # for some reason I can't have 12 minor ticks correctly

# fmt = mdates.DateFormatter('%Y-%m')
fmt = mdates.DateFormatter('%Y')
ax.xaxis.set_major_formatter(fmt)
fig
```




    
![png]({{site.baseurl}}/assets/img/CV-dashboard-post_files/CV-dashboard-post_7_0.png)
    



## Technical Experience

On thinking how to provide a visual quantitative gauge illustrating the experience in technical skills, I decided to first go with a color-connected nested pie chart. The way this is implemented is that one can add/remove what is desired to be showcased in a way that keeps the overall consistency of the visual design. Each parent takes up a desired percentage of the arc, to measure the experience level, and is underlined by several child features. Those follow the arc of the parent, and one can omit children features where they are not needed.

The labels in the nested slices are the only ones that can't quite align with the symmetry axis of the slice, as this is not how matplotlib handles it by default. They still look good, though.

```python
ax = fig.axes[1]

def make_Ramp(ramp_colors):
    """https://stackoverflow.com/questions/16834861/create-own-colormap-using-matplotlib-and-plot-color-scale"""
    from colour import Color
    from matplotlib.colors import LinearSegmentedColormap

    color_ramp = LinearSegmentedColormap.from_list(
        'my_list', [Color(c1).rgb for c1 in ramp_colors])
    return color_ramp

cmap = make_Ramp(['#567189',
                  '#CFB997',
                  '#FAD6A5'])

# outer pie chart
skills = {
    'Python':   {'c': cmap([0]),   'p': 35,     'explode': 0.0,     'details': ['numpy', 'pandas', 'pyplot', 'scipy', 'PySpark']},
    'R':        {'c': cmap([50]),  'p': 12.5,   'explode': 0.0,     'details': ['dplyr', 'ggplot']},
    'Web Dev.': {'c': cmap([100]), 'p': 12.5,   'explode': 0.0,     'details': ['Tailwind', 'Jekyll', 'REST API']},
    'Machine\nLearning':       {'c': cmap([150]),  'p': 25, 'explode': 0.0, 'details': ['sk-learn', 'Keras', 'PyTorch']},
    'C++':      {'c': cmap([200]), 'p': 5,      'explode': 0.0,     'details': ['Cpp.hide']},
    'SQL':      {'c': cmap([250]), 'p': 10,     'explode': 0.0,     'details': ['SQL.hide']},
}

# inner pie chart
details = {
    # python
    'numpy':        {'c': cmap([10]),      'p': skills['Python']['p']*0.2},
    'pandas':       {'c': cmap([20]),      'p': skills['Python']['p']*0.2},
    'pyplot':       {'c': cmap([30]),      'p': skills['Python']['p']*0.2},
    'scipy':        {'c': cmap([40]),      'p': skills['Python']['p']*0.2},
    'PySpark':      {'c': cmap([45]),      'p': skills['Python']['p']*0.2},

    # R
    'dplyr':        {'c': cmap([70]),     'p': skills['R']['p']*0.5},
    'ggplot':       {'c': cmap([80]),     'p': skills['R']['p']*0.5},

    # Web Dev
    'Tailwind':     {'c': cmap([115]),    'p': skills['Web Dev.']['p']*0.3333},
    'Jekyll':       {'c': cmap([125]),    'p': skills['Web Dev.']['p']*0.3333},
    'REST API':     {'c': cmap([130]),    'p': skills['Web Dev.']['p']*0.3333},

    # ML
    'sk-learn':     {'c': cmap([160]),   'p': skills['Machine\nLearning']['p']*0.3333},
    'Keras':        {'c': cmap([165]),    'p': skills['Machine\nLearning']['p']*0.3333},
    'PyTorch':      {'c': cmap([170]),    'p': skills['Machine\nLearning']['p']*0.3333},

    # C++
    # no details
    'Cpp.hide':     {'c': 'white', 'p': skills['C++']['p']*1.0},

    # SQL
    # no details
    'SQL.hide':     {'c': 'white', 'p': skills['SQL']['p']*1.0},
}

ax.pie(
    [j["p"] for _, j in skills.items()],
    labels=list(skills.keys()),
    colors=[j["c"] for _, j in skills.items()],
    startangle=297,
    # shadow=True,
    explode=[j["explode"] for _, j in skills.items()],
    # autopct='%1.1f%%'
    radius=1,
    wedgeprops=dict(width=0.25, edgecolor='w'),
    textprops=dict(fontsize=12, family='monospace', fontweight='semibold', )
)

ax.pie(
    [details[j]['p'] for i in skills.keys() for j in skills[i]['details']],
    labels=[j if '.hide' not in j else " " for i in skills.keys()
            for j in skills[i]['details']],
    labeldistance=0.525,
    textprops={'fontsize': 5.5, 'family': 'monospace', 'fontweight': 'light'},
    rotatelabels=True,

    colors=[details[j]['c'] for i in skills.keys()
            for j in skills[i]['details']],
    startangle=297,
    # shadow=True,
    # autopct='%1.1f%%'
    radius=0.8,
    wedgeprops=dict(width=0.5, edgecolor='w')
)

fig.text(0.05, 0.58, 'Experience', fontsize=14, fontweight='semibold', color = 'grey', family='monospace')
fig

```




    
![png]({{site.baseurl}}/assets/img/CV-dashboard-post_files/CV-dashboard-post_9_0.png)
    



## Competence Graph

There may still be essential features to give in a CV. For example, auxiliary skills or linguistic competences still are useful to be mentioned. No report is complete without a bar chart, and why should a visually guided CV be the exception? To spice things up, I customised the design a bit by including a second y-axis, along with a modified x-axis to have the 100% peak in the middle of the graph.

One of the issues with gridspec is that after adding more stuff to the grid, the sizes of the grid elements may shift a bit. At least, they did for me! For example, look at the position of the "Career Evolution" y-label in the timeline plot and compare it with the previous image.

```python
ax = fig.axes[2]

import matplotlib.ticker as ticker
ax.set_xticks([-100,-50,0,50,100], ["0", "50", "100", "50", "0"])

l_names = ["Git", "Bash", "PlantUML", "Confluence", "MS Office"]
l_widths = [75, 65, 60, 60, 60]
l_y = [4,5,6,7,8][::-1]

r_names = ["Greek", "English", "German"]
r_widths = [100,100,50]
r_y = [1,2,3][::-1]

ax2 = ax.twinx()

ax.set_xlim(-100,100)
ax.set_ylim(0, 10)
ax2.set_ylim(0, 10)
ax.set_xlabel("% Confidence")

ax.xaxis.set_minor_locator(ticker.AutoMinorLocator())
ax.tick_params(axis='both', which='major', labelsize=8)
ax2.tick_params(axis='both', which='major', labelsize=8)
ax.set_yticks(l_y, l_names)
ax2.set_yticks(r_y, r_names)

ax.hlines(y=l_y, xmin=-100, xmax=[-100+i for i in l_widths], color='#FAD6A5', alpha=0.9, linewidth=2, linestyles='dashdot')
ax2.hlines(y=r_y, xmin=[100-i for i in r_widths], xmax=100, color='#FAD6A5', alpha=0.9,  linewidth=2, linestyles='dashdot')

for i,j in zip(l_y, l_widths):
    ax.plot([-100+j], [i], "o", markersize=4, color='#007ACC', alpha=0.6)
for i,j in zip(r_y, r_widths):
    ax2.plot([100-j], [i], "o", markersize=4, color='#007ACC', alpha=0.6)

# change the style of the axis spines
ax.spines['top'].set_visible(False)
ax2.spines['top'].set_visible(False)

ax.spines['right'].set_visible(False)
ax.spines['left'].set_bounds([l_y[0], l_y[-1]])

ax2.spines['left'].set_visible(False)
ax2.spines['right'].set_bounds([r_y[0], r_y[-1]])

ax.spines['left'].set_position(('outward', 8))
ax.spines['bottom'].set_position(('outward', 5))

ax2.spines['right'].set_position(('outward', 8))
ax2.spines['bottom'].set_position(('outward', 5))

fig.text(0.05, 0.25, 'Competence', fontsize=14, fontweight='semibold', color = 'grey', family='monospace')
fig

```




    
![png]({{site.baseurl}}/assets/img/CV-dashboard-post_files/CV-dashboard-post_11_0.png)
    



## Personal Information

What's left is personal information. Using matplotlib for this is kind of wonky, especially the handling of large bodies of text such as a small personal statement contained in some CVs. However, it can still be implemented with user-defined line breaking with triple quotes. Also, text elements can also be made into links.

And that's pretty much it! Let me know what you think!


```python
ax = fig.axes[3]
ax.axis('off')

ax.text(0.1, 0.7, "Ioannis Karkanias", family='monospace', fontsize=18, fontweight="bold")
ax.text(0.11, 0.67, "Data Scientist, PhD", family='monospace', fontsize=10, fontweight="semibold", color="grey")
ax.text(0.11, 0.60, "Website:", fontsize=8, family='monospace', fontweight="semibold", color="grey")
ax.text(0.3, 0.60, "iokarkan.github.io", 
            url='https://iokarkan.github.io',
            bbox=dict(color='w', alpha=1e-6, url='https://iokarkan.github.io'),
            family='monospace', fontsize=8, fontweight="semibold", color="royalblue"
            )
ax.text(0.11, 0.57, "Email:", fontsize=8, family='monospace', fontweight="semibold", color="grey")
ax.text(0.3, 0.57, "ioannis.karkanias@gmail.com", 
            url='mailto:ioannis.karkanias@gmail.com',
            bbox=dict(color='w', alpha=1e-6, url='mailto:ioannis.karkanias@gmail.com'),
            family='monospace', fontsize=8, fontweight="semibold", color="royalblue"
            )

ax.text(0.125, 0.225, """Combining a theoretical and 
experimental background,
I employ a physicist's approach
in the world of data.

Alongside my main expertise in
designing and applying
data analysis, statistical 
computation and 
visualization pipelines,
my passions extend to web and
software development.""", 
        family='monospace', fontsize=10, fontweight="semibold",
        bbox=dict(facecolor='black', alpha=0.7), color='white'
        )
fig

```




    
![png]({{site.baseurl}}/assets/img/CV-dashboard-post_files/CV-dashboard-post_13_0.png)
    













