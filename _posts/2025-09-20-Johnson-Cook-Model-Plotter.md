---
#layout: posts
permalink: /posts/jc-plotter/
title: "A tool for plotting Johnson-Cook Model curves"
categories: Posts
toc: true
toc_sticky: true

header:
  overlay_image: /assets/images/posts/jc-plotter/light-1.png
  overlay_filter: 0.4
  caption: "A screenshot showing the web app in action!"
---

_In this post, I will present a project I worked on over the last few months. Months ago, when I was looking for a tool capable of plotting Johnson-Cook model curves based on Johnson-Cook parameters, I couldn't find one, so... I made one! Hopefully, my web app will come in handy for anyone who finds themselves in the same situation in the future! <br> Disclaimer: This is a niche application in the field of materials science engineering! But keep reading!_
{: .notice--primary}

<p style="text-align:center;"><img src="{{ "/assets/images/posts/jc-plotter/jc-plotter-logo.png" | absolute_url }}" width="30%" hspace="5"></p>

<i class="far fa-file-alt"></i> Logo and favicon of the web app resembling a stress-strain curve! 
{: .notice--info}
{: .text-justify}

## The App
[Click here to head to the web app: **Johnson-Cook Model Plotter**!][1]
{: .notice--primary}

## The Background
A few months ago, I was working on modeling the behavior of metals, specifically titanium alloys, under extreme conditions.
One model used for this purpose in the literature is the **Johnson-Cook model**.

The Johnson-Cook model is a widely used constitutive material model that describes the flow stress of metals as a function of strain, strain rate, and temperature. It is especially valuable for simulating the behavior of materials under high strain rates and elevated temperatures, such as in machining, impact, or explosive events.

A typical plot of the Johnson-Cook model shows flow stress versus plastic strain at various strain rates and temperatures. This illustrates how a material's strength evolves during deformation under different conditions.

While searching the internet for websites offering plots of Johnson-Cook curves based on given parameters, I could not find one.
For that reason, I decided to create one myself and make it available to anyone, so that someone in my position in the future can take advantage of this resource.

## The Tools I used
This project was also an opportunity for me to experiment with a tool that I had been interested in trying out for a while. This project was the perfect application, so I jumped in and started experimenting.

The entire web application is written in **Python** and uses the [Panel][2] library (by HoloViz) for the dashboard and GUI. Panel makes it very easy to code and build good-looking dashboards, plotters, and other visualization tools. I can't recommend this enough!
The other two key tools I used are [Matplotlib][3] (for creating the plots) and [NumPy][4] (for numerical computations).

## The Deploy
Deploying the app and making it accessible on the Internet is the second phase of the project.
Considering how lightweight and resource-efficient the web app is, I was hoping to find an easy hosting solution.

Starting out, I looked into free options to host the demo while researching better solutions (like self-hosting?).
I considered [Render.com][5], but ultimately landed on [Koyeb.com][6]. These tools make it easy to deploy from a GitHub repository, but, as expected, the free plans are limited in terms of performance and fluidity.
I will look into better (paid) options, but for now, I'm okay with having the demo app hosted there.

## The Future
I plan to release the web app as an open-source project with a public repository on GitHub. Until then, I'll continue working on it and preparing it for release.

Feel free to contact me if you find this tool useful or if you have any suggestions!


<!-------------------------------- FOOTER --------------------------------->

[1]: https://johnson-cook-model-plotter.koyeb.app/
[2]: https://panel.holoviz.org/
[3]: https://matplotlib.org/
[4]: https://numpy.org/
[5]: https://render.com/
[6]: https://www.koyeb.com/
