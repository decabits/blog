---
layout: post
title:  "Data visualization using victory in ReactJS"
date:   2020-09-21 13:28:30 +0530
categories: ReactJS
---
<h3>What Is Victory?</h3>

Victory is a ReactJs Library. It is a collection of composable and reusable components for building interactive data visualizations.

<h3>Why Use Victory?</h3>

One of the main benefits of using Victory is its customizability. The components can be altered, wrapped, or created from scratch, proving to be very beneficial to developers.


Compared to other popular data visualization libraries like Plotly and D3, Victory has user-friendly and intuitive documentation. Even a person with a minimal programming background can easily use it. As far as its UI is concerned, it will immediately catch your eye with its stylishness, interactiveness, and smooth animations.

One of its drawbacks is being limited to only React, unlike Plotly which can be integrated with Python, React, MATLAB, Jupyter, etc.

<h3>Getting Started</h3>

To get started, Victory needs to be added to your project. 
<br>
<img src="/assets/images/a.jpg" height="200px" width="200px" alt="There was supposed to be an image here">
<h3>Creating A Graph</h3>

Now that you have added Victory, you can import it in your project.
Victory has a wide variety of charts and graphs. For this blog, we are going to use bar graphs to provide an effective introduction.

<img src="/assets/images/b.jpg" height="350px" width="350px" alt="There was supposed to be an image here">


With the above code,  you will get the following bar chart on your page, after starting the npm server.

<img src="/assets/images/1.jpg" height="350px" width="300px" alt="There was supposed to be an image here">

You will notice 2 things:

Even though no data was provided you still get a bar chart with values. This is because Victory uses some dummy placeholder values. Think of it as Loren Ipsum for charts and graphs.
You did not need to wrap the VictoryPie component inside VictoryChart. This is because it provides graphed data along with the graph axes but VictoryBar just provides the graphed data.

<h3>Providing Custom Data</h3> 

If you want to actually feed the charts and graphs with your own data, you will need to pass a data property with properly formatted data based on the chart or graph you’re using.
<br>
<img src="/assets/images/c.jpg" height="350px" width="350px" alt="There was supposed to be an image here">

With the above code,  you will get the following bar chart on your page.

<img src="/assets/images/2.jpg" height="320px" width="350px" alt="There was supposed to be an image here">


In the above data, the x-axis is referred to as quarter and y-axis as earnings. You can skip this part and keep it x and y for simplicity.



<h3>Naming Axes</h3>

Let’s take advantage of the VictoryAxis component to display what each axis on the chart is referencing. One axis will display the label “Earnings” while another will display the label “Quarter”.
<br>
<img src="/assets/images/d.jpg" height="400px" width="380px" alt="There was supposed to be an image here">


Using VictoryAxis you can label the axes, as needed. You can also provide tick values format and custom styling to each axis. Using the ‘domainPadding property’ of VictoryChart you can shift the bars that were earlier overlapping with the Y-axis.

With the above code,  you will get the following bar chart on your page.
<br>
<img src="/assets/images/3.jpg" height="350px" width="350px" alt="There was supposed to be an image here">

<h3>Styling Charts</h3>

Victory charts come with a default ‘grayscale’ theme so that all components look clean and consistent. Let’s switch it up with the Victory provided ‘material’ theme. We can do that by importing VictoryTheme and adding a theme property to VictoryChart. Themes should always be applied to the outermost wrapper component in a chart.

theme={VictoryTheme.material} 
<br>
<img src="/assets/images/4.jpg" height="350px" width="350px" alt="There was supposed to be an image here">


Other properties like borders and colors can also be customized using style property. Default is set to ‘grayscale’ theme.

<img src="/assets/images/e.jpg" height="500px" width="500px" alt="There was supposed to be an image here">
<br>
<img src="/assets/images/5.jpg" height="350px" width="350px" alt="There was supposed to be an image here">


Many more properties like ‘barWidth’, ‘alignment’, ‘barRatio’, ‘cornerRadius’  can also be altered.


<h3>Scales</h3>

VictoryBar uses standard scale property. Options for scale include ‘linear’, ‘time’, ‘log’, ‘sqrt’, and the D3-scale functions that correspond to these options. The default scale is set to linear.


<h3>Animation</h3> 

VictoryAnimation is able to animate changes in properties using D3-interpolate. Victory components define their animations via the animate property. 
Duration, delay, easing and onEnd functions may all be specified via the animate property.

<h3>Stacked Bar Graphs</h3>

VictoryStack can be used to stack multiple bar graphs on each other in a single chart.
<br>
<img src="/assets/images/f.jpg" height="500px" width="500px" alt="There was supposed to be an image here">


It is to be noted that the naming of X and Y axes in all the 4 data should be the same. 

<h3>Conclusion</h3>

The above discussed are just a few properties for customizing and making your own Victory Chart.
Victory offers not just bar graphs but also pie Charts, polar graphs, scatter charts, line charts etc.

You can also club multiple types of graphs in a single chart to make your visualized data more interesting and readable.

For a further description of properties and charts, refer to Victory | Getting Started 


Signing off,
<br>
Vaibhav Sethia
<br>
Github Handle: VaibhavSethia
