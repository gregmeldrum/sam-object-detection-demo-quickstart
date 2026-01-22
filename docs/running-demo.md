---
sidebar_position: 3
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Running the Demo

Now that you have Solace Agent Mesh running with the agents installed, let's run a demo that showcases the power of multi-agent collaboration.

## Recommended Model

This demo works best with **frontier models** (latest Claude Sonnet or preferably Opus) due to the complexity of the operations and workflow. Free-tier models may struggle with the multi-step coordination required.

## Demo Prompt

The demo pulls images from traffic cameras, uses object detection to count vehicles, crops an interesting vehicle, and creates an HTML page to display the results.

Choose a location based on the current time of day - **select a location that has sunlight** since the object detection works more accurately in good lighting conditions.

<Tabs>
  <TabItem value="ottawa" label="Ottawa, Canada" default>

Best during **Eastern Time daytime hours** (approx. 7 AM - 5 PM ET).

```
Get images from https://traffic.ottawa.ca/camera?id=222 and https://traffic.ottawa.ca/camera?id=330 in parallel, then count the number of cars, buses, trucks, etc.... Also, take an image of the vehicle in the lowest/rightmost area and create an html page that captures this information and host it.
```

  </TabItem>
  <TabItem value="australia" label="Australia">

Best during **Australian Eastern Time daytime hours** (approx. 7 AM - 5 PM AEST).

```
Get images from https://webcams.transport.nsw.gov.au/livetraffic-webcams/cameras/ryde_bridge_ryde.jpeg and https://www.transport.tas.gov.au/__traffic_updates/204_Tasman_Bridge.jpeg in parallel, then count the number of cars, buses, trucks, etc.... Also, take an image of the vehicle in the lowest/rightmost area and create an html page that captures this information and host it.
```

  </TabItem>
</Tabs>

## What Happens

When you run the demo, multiple agents collaborate:

1. **Web Agent** fetches the traffic camera images from the URLs
2. **Object Detection Agent** analyzes the images and counts vehicles by type
3. **ImageMagick Agent** crops an image of the specified vehicle
4. **Artifact Host Agent** creates and hosts an HTML page with the results

## Agents Explained

| Agent | Description |
|-------|-------------|
| **Web Agent** | Pulls information from the web and performs web searches |
| **ImageMagick Agent** | Resizes, crops images and adds text overlays |
| **Object Detection Agent** | Uses a YOLO object detection model pre-tuned to detect certain objects. These models can be fine-tuned for specific use cases. |
| **Artifact Host Agent** | Starts a web server to host HTML and images created by the system |

## First Run Note

:::caution First Run Delay
The first time you run the demo, the **Object Detection Agent** needs to download the YOLO model, which is approximately 40 MB. This may cause a delay in the workflow or it may fail on the first attempt. Subsequent runs will not be impacted.
:::

## Viewing Results

After the demo completes, the Artifact Host Agent will provide a URL where you can view the generated HTML page with the traffic analysis results.
