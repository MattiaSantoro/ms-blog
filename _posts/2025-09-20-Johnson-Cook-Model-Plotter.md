---
#layout: posts
permalink: /posts/jc-plotter/
title: "I created a tool for plotting Johnson-Cook Model curves"
categories: Posts
toc: true
toc_sticky: true

header:
  overlay_image: /assets/images/posts/jc-plotter/jc-screenshot1.png
  overlay_filter: 0.4
  caption: "A screenshot showing the web app in action!"
  teaser: /assets/images/posts/jc-plotter/jc-screenshot1.png

galleryLight:
  - url: /assets/images/posts/jc-plotter/jc-screenshot1.png
    image_path: /assets/images/posts/jc-plotter/jc-screenshot1.png
    alt: "Light Mode"
  - url: /assets/images/posts/jc-plotter/jc-screenshot2.png
    image_path: /assets/images/posts/jc-plotter/jc-screenshot2.png
    alt: "Light Mode"

galleryDark:
  - url: /assets/images/posts/jc-plotter/dark-1.png
    image_path: /assets/images/posts/jc-plotter/dark-1.png
    alt: "Dark Mode"
  - url: /assets/images/posts/jc-plotter/dark-2.png
    image_path: /assets/images/posts/jc-plotter/dark-2.png
    alt: "Dark Mode"
---

_In this post, I will present a project I worked on over the last few months. Months ago, when I was looking for a tool capable of plotting Johnson-Cook model curves based on Johnson-Cook parameters, I couldn't find one, so... I made one! Hopefully, my web app will come in handy for anyone who finds themselves in the same situation in the future! <br> Disclaimer: This is a niche application in the field of materials science engineering! But keep reading!_
{: .notice--primary}

<p style="text-align:center;"><img src="{{ "/assets/images/posts/jc-plotter/jc-plotter-logo.png" | absolute_url }}" width="30%" hspace="5"></p>

<i class="far fa-file-alt"></i> Logo and favicon of the web app resembling a stress-strain curve! 
{: .notice--info}
{: .text-justify}

## App
[Click here to head to the Johnson-Cook Model Plotter: **jc-plotter.matsan.it**][1]
<br> _It may take up to 10-20 seconds to load the app after clicking the link._
{: .notice--primary}

## Background
A few months ago, I was working on modeling the behavior of metals, specifically titanium alloys, under extreme conditions.
One model used for this purpose in the literature is the **Johnson-Cook model**.

The Johnson-Cook model is a widely used constitutive material model that describes the flow stress of metals as a function of strain, strain rate, and temperature. It is especially valuable for simulating the behavior of materials under high strain rates and elevated temperatures, such as in machining, impact, or explosive events.

A typical plot of the Johnson-Cook model shows flow stress versus plastic strain at various strain rates and temperatures. This illustrates how a material's strength evolves during deformation under different conditions.

While searching the internet for websites offering plots of Johnson-Cook curves based on given parameters, I could not find one.
For that reason, I decided to create one myself and make it available to anyone, so that someone in my position in the future can take advantage of this resource.

## Tools
This project was also an opportunity for me to experiment with a tool that I had been interested in trying out for a while. This project was the perfect application, so I jumped in and started experimenting.

The entire web application is written in **Python** and uses the [Panel][2] library (by HoloViz) for the dashboard and GUI. Panel makes it very easy to code and build good-looking dashboards, plotters, and other visualization tools. I can't recommend this enough!
The other two key tools I used are [Matplotlib][3] (for creating the plots) and [NumPy][4] (for numerical computations).

## Deploy
Deploying the app and making it accessible on the Internet is the second phase of the project.
Considering how lightweight and resource-efficient the web app is, I was hoping to find an easy hosting solution.

Starting out, I looked into free options to host the demo while researching better solutions (like self-hosting?).
I considered [Render.com][5], but ultimately landed on [Koyeb.com][6]. These tools make it easy to deploy from a GitHub repository, but, as expected, the free plans are limited in terms of performance and fluidity.
I will look into better (paid) options, but for now, I'm okay with having the demo app hosted there.

**Update!**<br>
<br>
I moved the Johnson-Cook Model Plotter from traditional server-side hosting (like Koyeb, which I was using before) to a Client-Side WebAssembly architecture. Previously, every time a user performed a calculation on the website, the app had to send a request to a remote Linux server to perform the calculations, resulting in lags and limitations on the free plan, which degraded usability. <br>I migrated to [Cloudflare Pages][7] and [Pyodide][8], shifting the computations to the user's browser. Now, after an initial download on the first visit, the application downloads the necessary Python engine, allowing all the computations to remain on the user's device. Essentially, I moved to a Serverless Static Web App so that after the first download, the performance is the best possible without even needing external server access! <br>I am really happy that I took the time to find this elegant solution, which solved the negative points I had with the previous solution!
{: .notice--success}

## Gallery
Below, you can find some screenshots showing the app and its features. The app has both light and dark modes, which can be activated in the top right corner.

Using the sidebar on the left, the parameters can be adjusted. The plotting mode can be changed by selecting which quantity (temperature or strain rate) stays constant and which quantity varies.

The main section has three panels. The actual plot takes center stage. Below, there is a brief summary of the Johnson-Cook model, along with its equation. The last section serves as an acknowledgment and disclaimer, mentioning the tools used.

### Screenshots
{% include gallery id="galleryLight" %}

<!--
<i class="far fa-file-alt"></i> Light Mode! 
{: .notice--info}
{: .text-justify}


### Dark Mode
{% include gallery id="galleryDark" %}

<i class="far fa-file-alt"></i> Light Dark! 
{: .notice--info}
{: .text-justify}
-->

## Future
I plan to release the web app as an open-source project with a public repository on GitHub. Until then, I'll continue working on it and preparing it for release.

Feel free to contact me if you find this tool useful or if you have any suggestions!

*Ciao!*

<!-------------------------------- FOOTER --------------------------------->

[1]: https://jc-plotter.matsan.it/
[2]: https://panel.holoviz.org/
[3]: https://matplotlib.org/
[4]: https://numpy.org/
[5]: https://render.com/
[6]: https://www.koyeb.com/
[7]: https://pages.cloudflare.com/
[8]: https://pyodide.org/en/stable/