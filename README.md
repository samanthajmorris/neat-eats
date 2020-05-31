# Neat-Eats by The Bluenosers
### Challenge: Food for Thought

## The Motivation

On March 22, 2020 the province of Nova Scotia in Canada announced a state of emergency in response to the COVID-19 global pandemic. Local boutiques closed their doors, parks locked the gates, and restaurants shut down their kitchens. Additionally, borders were closed, making exporting goods all that more difficult. As a consequence, local farmers and producers have lots on of their main sources of revenue, and many industries are suffering. Fisheries is one of the main resources provided by our home province, and our largest market is Asian countries. Before COVID-19 began, 2020 was shaping up to be one of the best times in the lobster industry ever. Now, our main industry is facing its largest struggle in decades- fisherman are laid off, prices have dropped, and nobody is buying. 
  
Today it is May 30th, 2020 and three days ago our provincial government, Nova Scotia, announced that on June 5th they would be allowing restaurants to re-open their doors to dine in, patios and take out. This would mean a huge increase in revenue back to our local farmers. However, Nova Scotians are hesitant to venture out of their homes after two months of social isolation. They are concerned about businesses ability to adhere to social distancing and sanitation guidelines, and they are worried that opening up with cause a second wave of exposure. The inspiration for our project came from us trying to find a way to help Nova Scotians feel more comfortable venturing back out into the world, because our farmers and producers need us to. 

## A High Level Summary

With the closures of restaurants, local producers have experienced a severe decline in profits. We’re supporting the reopening of local food establishments in a sustainably safe way to provide local producers a revenue stream again. We’ll provide a device which relays a count of customers inside establishments to a constantly refreshing app. The app shows the current capacity of the establishment, customer reviews on social distancing and sanitization, and the location of the establishment on the SEDAC Global COVID-19 Viewer. This provides a relationship between business location, guideline adherence, and virus hotspots, allowing consumers to make decisions regarding their visit. 

## The Technology

Due to the ubiquity of WIFI and Bluetooth connections on both low-price and high-end consumer electronics over the past decade, wireless mid and short-range networking constitutes an opportunity to uniquely count individuals in any given area. This technology was used in the mid-2010’s by retail stores to uniquely identify shoppers though logging their Medium Access Control (MAC) addresses as their devices searched for WIFI and Bluetooth connections in stores . In response, manufacturers made it such that their devices MAC addresses became randomized. This removed the ability for individuals to uniquely track customers through simple monitoring of airwaves. However, as the research, testing, and development of the Bluenosers team showed, the ability to estimate the total number of users in each area still exists.

Over the course of the hackathon, a working prototype of a discreet and small dual WIFI/Bluetooth traffic analytic device was created. By running several open-source applications and python based data-management/processing programs on a Raspberry Pi4, a packet capture device with the option for advanced filtering will allow businesses, governments, and individuals to estimate the number of individuals in an area by analyzing key metrics of packets. 

The device uses Kismet, an open source device detector and packet sniffer, the Raspberry Pi was configured to capture only the MAC addresses, signal strength, and timestamp of unique devices. These metrics were chosen as they do not require the logging the actual data in the packets, due to privacy concerns. From these metrics two unique streams emerged from testing, a stream of MAC addresses having legitimate manufacturing numbers and a stream of MAC addresses with fully randomized data. The unique identifiers pertained to devices such as access points and older devices whereas the randomized data were newer mobile devices. 

To process this data, first devices are filtered based on a minimal WIFI/Bluetooth signal strength to be “inside the building”. This value is uniquely calculated given a layout of the building and the placement of the Raspberry Pi and could be calibrated or uncalibrated if needed. The MAC addresses from known vendors are then counted immediately as users and exist as users for as long as they continue to send signals within a set period . The unknown addresses are handled differently. It was discovered through testing that after an initial startup point, new random MAC addresses are detected at a range of regular intervals. By turning on and off WIFI-enabled devices the rate of newly detected devices change. This can be seen in Trendline Figure below where mock data was used to highlight the trend. Therefore, since the rate of new unknown devices correlates with the number of true active devices, an estimate of how many devices are sending these packets can be made. This number is added to the vendor MAC users and a baseline of total users representing devices such as access points and employee devices from the start of the day is subtracted. This gives an accurate estimate of the number of users in a timeframe, which is sent to the server for further processing and visualization.

Due to its ability to monitor wireless frequencies, the Pi Zero W can be easily used to cut costs to ~5USD per unit without issue. Moreover, it can be implemented in any place with minimal speed internet access and unlike other solutions, this monitoring does not require generating intrusive probe requests, creating illegitimate access points, or doing unethical deep packet analytics as seen in other research.


### An Overview
![The System.](resources/network-diagram-2.png "The System.")

## The Algorithm
![The System.](resources/RaspberryPi-Flowchart-2.png "The Algorithm.")

## The App
### Screenshot 1
![Iphone-1.](resources/iphone-1.png "Iphone1")
### Screenshot 2
![Iphone-2.](resources/iphone-2.png "Iphone2")


### Citations

Wanhoef, M. (n.d.). Why MAC Address Randomization is not Enough: An Analysis of Wi-Fi Network Discovery Mechanisms. Retrieved May 31, 2020, from https://papers.mathyvanhoef.com/asiaccs2016.pdf

Matte, C., Cunche, M., Rousseau, F., & Vanhoef, M. (2016). Defeating MAC Address Randomization Through Timing Attacks. Proceedings of the 9th ACM Conference on Security & Privacy in Wireless and Mobile Networks - WiSec 16. doi: 10.1145/2939918.2939930

Oliveira, L., Schneider, D., Souza, J. D., & Shen, W. (2019). Mobile Device Detection Through WiFi Probe Request Analysis. IEEE Access, 7, 98579–98588. doi: 10.1109/access.2019.2925406
 
Martin, J., Mayberry, T., Donahue, C., Foppe, L., Brown, L., Riggins, C., … Brown, D. (2017). A Study of MAC Address Randomization in Mobile Devices and When it Fails. Proceedings on Privacy Enhancing Technologies, 2017(4), 365–383. doi: 10.1515/popets-2017-0054



