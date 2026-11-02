---
layout: page
title: "HW5: Bigfoot Sighting Reports"
permalink: /hw5/
---

<script src="https://cdn.jsdelivr.net/npm/vega@5"></script>
<script src="https://cdn.jsdelivr.net/npm/vega-lite@5"></script>
<script src="https://cdn.jsdelivr.net/npm/vega-embed@6"></script>

<a href="https://raw.githubusercontent.com/UIUC-iSchool-DataViz/is445_data/main/bfro_reports_fall2022.csv"><button>The Data</button></a>
<a href="https://github.com/truptireddy23/Jekyll-Webpage/blob/main/python_notebooks/hw5_bigfoot.ipynb"><button>The Analysis</button></a>

For this homework I used the Bigfoot Field Researchers Organization (BFRO) reports dataset. Each row is one reported sighting, with the date, season, state, coordinates, and a classification: Class A means the person says they clearly saw something, and Class B means they heard or found something but didn't get a clear look.

## Plot 1: Reports per year, Class A vs Class B

<div id="vis1"></div>

This stacked bar chart shows how many Bigfoot reports were filed each year from 1960 onward, split into Class A and Class B. The year is encoded on the x-axis as a temporal (T) variable, the count of reports is on the y-axis as a quantitative (Q) variable, and classification is mapped to color as a nominal (N) variable. Since classification has only two unordered categories, I picked two clearly different colors (green and brown) instead of a sequential scheme, which would wrongly suggest one class is "more" than the other. The earthy colors also fit the woods theme. In my notebook, I converted the `date` column to a pandas timestamp and pulled out the year. I dropped the roughly 30 Class C reports so the comparison is Class A vs Class B only, then grouped by year and classification to count reports. That aggregation means the chart uses about 120 rows instead of almost 5,000. The chart shows reports climbing through the late 1990s and peaking around 2005, which lines up with the BFRO website taking off, before dropping again.

## Plot 2: Where sightings happen, by season

<div id="vis2"></div>

This map plots every report that has coordinates, using longitude and latitude as quantitative (Q) encodings on an `albersUsa` projection with US state outlines as the background. Season is a nominal (N) variable mapped to color. I chose a custom four-color palette that matches how people think about the seasons: green for spring, yellow for summer, orange for fall, and blue for winter. That makes the dropdown easier to read without checking the legend. On the analysis side, I dropped rows with missing coordinates, removed reports with an "Unknown" season, and filtered out a few points that were geocoded far outside the US.

## Interactivity

Both plots are interactive beyond pan and zoom. In Plot 1, clicking Class A or Class B in the legend highlights that class and fades the other one, so you can see each class's trend over time without the stacking getting in the way. In Plot 2, a **Season** dropdown highlights only the reports from that season and grays out the rest. Switching between seasons shows that summer reports are heavily concentrated in the Pacific Northwest (Washington and Oregon), while winter reports thin out up north and shift south, with Florida and Texas near the top. That pattern is hard to see when all 3,700 points are colored at once. Both charts also have tooltips, so you can hover over a bar or a point to see the exact details.

<script type="text/javascript">
  vegaEmbed('#vis1', "../assets/json/chart1.json");
  vegaEmbed('#vis2', "../assets/json/chart2.json");
</script>
