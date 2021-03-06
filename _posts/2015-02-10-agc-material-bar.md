---
layout: post
title: Angular-Google-Chart with Material Design Bar Charts
description: A short how-to of using the Google Charts API's new Material Design versions of Bar and Line charts.
category: AngularJS
tags: [google-visualization, AngularJS, charts]
date: 2015-02-10 23:41
last_modified_at: 2016-05-20 00:14:22 2016 -0400
author: Nicholas Bering
---

If you're not familiar with Material Design, have you been living under a rock?!  Just kidding.  Material Design is a pretty recent initiative from Google to unify design principles across all of their public-facing technologies.  Material Design is coming in some incarnation or other to <a class="tracked" href="https://developer.android.com/design/material/index.html">Android</a>, <a class="tracked" href="https://material.angularjs.org/">AngularJS</a>, and even the Google Charts API.  In this article I will cover how to use the two new charts with <a class="tracked" href="https://github.com/angular-google-chart/angular-google-chart/">Angular-Google-Chart</a>.

### Material Design Comes to Google Charts

Material Design is a pretty big initiative, so it may not surprise you that it is coming to the Google Charts API a little at a time.  To start out, the Google Charts team has added two new chart classes:  `google.charts.Bar` and `google.charts.Line`.  If you are already familiar with the Charts API, you may have noticed that the naming convention is different with these two new charts (the old chart classes for these two chart types were `google.visualization.BarChart` and `google.visualization.LineChart`).

Along with the name change is a pair of new packages.  Optional package loading in Angular-Google-Chart is handled by setting the content of an angular value, which is used to call the Google Api Loader.  Check out the code snippet below to see an example of how to load both the new bar and line chart packages.

```js
angular.module('myApp')
  .value('googleChartApiConfig', {
    version: '1.1',
    optionalSettings: {
      packages: ['line', 'bar'],
      language: 'en'
    }
  });
```

### ChartWrapper and the New Charts

Angular-Google-Chart makes use of google.visualization.ChartWrapper to handle the drawing of any type of chart that the Charts API supports without having to do anything from the directive's end to handle the switching.  On the API's end of things they somehow select a JavaScript object to handle building and drawing your chart using the value passed as the chart type.  In the existing charts this would mean if you pass `"Bar"` as the chart type the underlying chart will be a `google.visualization.BarChart`.  If you want the Material Design version, you'll need to set this value to `"google.charts.Bar"`.  Not nearly as pretty, but the API for Material Design is not yet completely baked (my speculation would be that later on we will be using `google.charts.ChartWrapper` instead of `google.visualization.ChartWrapper`, but that's just a guess).

p. So to create an Angular-Google-Chart with the Material Design Bar Chart, our object looks something like:

```js
angular.module('myApp')
  .controller('MainController', function($scope){
    $scope.myChart = {
      type: 'google.charts.Bar', // This is the important line.
      options: {}, // Set up your chart
      data: {} // Fill in your own data
    };
  });
```

For details on the options available for the new charts visit the API Documentation for <a class="tracked" href="https://developers.google.com/chart/interactive/docs/gallery/barchart#Material">Bar Charts</a> and <a class="tracked" href="https://developers.google.com/chart/interactive/docs/gallery/linechart#Material">Line Charts</a>.

### Full Examples

To see all this in action, check out the plunks below.

<iframe src="http://embed.plnkr.co/x9ttq50KYzuFSULNIX2L/preview" width="100%" height="250"></iframe>

<iframe src="http://embed.plnkr.co/gb39c964GGNn8IRDoWSl/preview" width="100%" height="250"></iframe>

### Words of Caution

This works right now.  I have no idea how fixed the API is, ad this stuff is pretty cutting edge.  Using Material Design with ChartWrapper isn't even in the documentation yet.  I personally treat this as something that could just stop working at any time, but it's far enough along that if they do make breaking changes it should be easy enough to find a way to fix it.

So basically, don't go using this for medical applications or to view readouts on a nuclear reactor.  But if you just want some pretty charts, have at it!  Let me know in the comments how this works out for you.
