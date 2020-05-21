---
layout: post
title: Building a $2,300 Deep Learning Server
---

![](/images/build-server/all-parts.jpg)

![](/images/build-server/buzz.gif)

Sometimes I have to wonder if Buzz was talking to me too.  When working on my deep learning projects in the past, I’ve used AWS’s P2 GPU instance and then a machine at The University of Nottingham while doing my dissertation. Now that I’ve concluded my dissertation, I either needed to revert to feeding Bezos’ pockets, or invest in my very own deep learning box. The AWS GPU instance always seemed quite throttled, so I decided to go the latter route. It was my first time ever building a computer, so in a way it felt like a right of passage. I’ll take you through the process, but first, let’s get the equipment overview out of the way.

### Overview
![](/images/build-server/price-breakdown.png)

Bear in mind, these were all purchased NEW, so it doesn’t have to be this expensive if you’re willing to hunt for some deals on Ebay, etc.

As for operating system(s), I’ve dual booted Windows and Linux, giving Windows about 200GB in its partition, the rest for deep learning on Linux. Running a benchmark test on UserBenchmark.com witnessed the following results:

UserBenchmarks: Game 131%, Desk 127%, Work 108%
CPU: Intel Core i7-6850K – 95%
GPU: Nvidia GTX 1080 Ti – 163%
SSD: Samsung 960 Evo NVMe PCIe M.2 1TB – 253.2%
RAM: Crucial BLS16G4D240FSC.16FB 2x16GB – 74.3%
MBD: MSI X99A WORKSTATION (MS-7A54)

It’s blowing everything out of the water, which is fun to look at I guess. Let’s dive into the reason for picking each particular part in the order in which I picked them.

NB: I used PCPartPicker to ensure compatibility among all components. I always filter for only 4 & 5 star results, sort by price, then look which items are getting the most reviews for a metric of reliability of the rating.

### GPU – EVGA GEFORCE GTX 1080 TI SC2
![](/images/build-server/gpu-pic.jpg)

This is THE most important piece of equipment for a deeplearning box. If you’re investing in building one of these, this should be the biggest expense. Why is this? Well GPUs are designed to process tons of tiny triangles when rendering game graphics, and they have to be able to do this very quickly. One triangle does not depend on any other triangle to be rendered first, so wouldn’t it be great if they could be rendered in parallel? Well yes, that would be great! And it’s exactly what GPUs do best.

DL involves the calculation of millions if not billions of derivatives calculations when performing gradient descent, a process you can read up on in my overview of Deep Neural Nets.  These calculations benefit tremendously from being parallelized, as opposed to being fed through the CPU one at a time.

Another important component of the GPU is the amount of RAM it has. As background, DL benefits from being able to run its calculations over multiple data points at a time, called a batch. The more data points one can fit in a batch, the more it can process in a given timeframe. If using a CPU, the largest batch size you can use is 1. Depending on the GPU, you can process as many as 256, a greater than 25,000% improvement. From Jeremy Howard in Lesson 8 of Fast.ai:

> More RAM helps more than people who discuss this stuff online quite appreciate. 12G RAM means twice as big batch sizes, which means half as many steps necessary to get through an epoch, means more stable gradients, means higher learning rates. More RAM is often under-appreciated.

I think a lot of this answer can be intuited by browsing through Tim Dettmers’ excellent blog post on Which GPU’s to Get for Deep Learning. In it, he shows various benchmarks comparing the performance of GPUs for DL tasks and at the end of the day, the 1080Ti is simply the greatest bang for the buck, and by quite a large margin.

As for RAM, the “best” GPU, the Titan X, has 12GB. The 1080 Ti has 11GB. The next highest I’ve seen from Nvidia is the 1080 at 8GB. The 1GB of RAM difference will be negligible compared to how empty your pockets would feel after splurging on a Titan X, so in the end, this was the obvious choice.

### CPU – INTEL CORE I7-6850K
Alright! Next up on the chopping block: the CPU. This one can be tricky. In fact, I purchased the wrong CPU and consequent motherboard the first time around, so BEWARE! There seems to be an ongoing debate about the number of PCIe lanes in the CPU for deep learning applications, and no tests have been done on this that I am aware of. Allow me to explain.

In ELI5 terms (since that’s about the extent of my understanding anyways), PCIe lanes carry information to and from the GPU and CPU. Each GPU can use up to 16 PCIe lanes to exchange this information. That said, processors only support up to a certain amount of maximum PCIe lanes, the most common number you’ll find being 16. This is perfectly fine for a single GPU, but if you ever wanted to expand to a second GPU, you’d run into a potential bottleneck where each GPU can only utilize 8 PCIe lanes each. Does this matter? Nobody really knows for sure, but I didn’t want to take the chance so I spent an extra $150 or so on an X99 chip/mobo just in case.

However, according to Linus Tech Tips, there doesn’t seem to be much impact as far as gaming is concerned:

<iframe width="420" height="315" src="https://youtu.be/rctaLgK5stA" frameborder="0" allowfullscreen></iframe>

Now, I’m not sure how this translates to deep learning. Take the chance if you’re so inclined, but I played it safe with a slightly more expensive, beefier CPU that supported a maximum of 40 PCIe lanes. If you want to find out which chips support 40 PCIe lanes on pcpartpicker, filter check the LGA2011-3 filter under the Socket category.

### CPU COOLER – COOLER MASTER HYPER 212
This may have been a mistake, given the power of the CPU. I didn’t really think very hard about it, just saw how cheap and how many reviews this cooler had, but may well look into getting a better cooling unit in the future. Literally only saying this because of the price. So really I have no idea.

### NVME DRIVE – SAMSUNG 1TB PCIE NVME
NVMe Drives are awesome. They’re a kind of SSD drive that can retrieve data at RAM-like speeds. I knew I wanted 1TB, so I grabbed the cheapest one I could with good reviews. Easy as that.

NB: When I first ran my benchmarks, the NVMe was underperforming. Installing the Samsung official drivers boosted performance considerably.

### HDD – TOSHIBA 3TB
Basically decided I wanted 3TB (this is the age of big data we’re talking about here), and I’ve had good experiences with Toshiba drives in the past. Cheapest one at the time.

### RAM – BALLISTIX SPORT LT 32GB KIT (16GBX2)
The more RAM, the more data you can pre-load to pass to the model. This is crucially important. If you’re going to be working with large datasets, having sufficient RAM is a necessity. I went with 32GB to start, but the mobo can support up to 128GB. Just going to see how this goes for now, and look at upping to 64 if need be. Just went with the cheapest option with good reviews.

### MOTHERBOARD – MSI INTEL X99 LGA 2011 (X99A WORKSTATION)
After going through all these other components, I again filtered by star rating, sorted by price, and picked an option that was on the cheaper end with lots of positive reviews. This mobo usually goes for \>$350, so at \<$200, couldn’t pass it up.

BUT: beware potential incompatibilities with particular CPU architectures. Some mobos, such as those by ASRock, do not allow you to update the BIOS to support certain architectures without putting a supported (older) generation CPU in first. MSI and a few others allow you to update the BIOS using a USB stick, therefore circumventing the need to also buy an older CPU just so you can use your particular architecture. If you don’t have a spare CPU lying around, it would be wise to check for this before picking a mobo.

### POWER SUPPLY – EVGA SUPERNOVA 850 P2
Now we’ve got to power all this craziness! PCPartPicker will tell you how much wattage your machine will be using, on which you can make a decision as to how beefy a power supply you need to buy. If you think you may ever want to add a second GPU, make sure you add a second one to your configuration to see how it raises the wattage and buy accordingly. Gold and Platinum energy efficiency models were no more than $5 difference on amazon, so I went with the higher efficiency model.

### CASE – DEEPCOOL TX MID TOWER TESSERACT SW
Just found something that would fit the motherboard, had good reviews and cheap. Couldn’t really care less what it looked like.

And that’s everything! Simply plug it all in and let it rip. Consult as many manuals as necessary to make sure things are going in the right places, but this should leave you set.

![](/images/build-server/assembled-pic.jpg)

### NOTES ON INSTALLATION
When installing some parts, you may not be comfortable with how hard you have to press some of the pieces into their slots, as Slav Ivanov discussed in his excellent blog post for his deep learning machine. I’m glad I went into this project knowing this, as the CPU lever, RAM, and NVMe drive all required a little more force than I’d have otherwise been comfortable with.
