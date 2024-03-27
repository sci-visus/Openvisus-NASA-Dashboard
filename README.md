# Openvisus-NASA-Dashboard
---

## Publicly Deployed Dashboards
Publicly available dashboards for different purposed can be available from the links below. 

-  NASA Petascale Climate Data Exploration
[```http://chpc3.nationalsciencedatafabric.org:11957/```](http://chpc3.nationalsciencedatafabric.org:11957/)

- NASA Coupled Dashboard for studying relationships between oceanic and atmospheric variables
[```http://chpc3.nationalsciencedatafabric.org:11857/run```](http://chpc3.nationalsciencedatafabric.org:11857/run)

---
## Instructions to launch dashboard using NASA LLC2160 dataset from your machine


### Basic Pre-requirements
- Download [Python](https://www.python.org/downloads/) version > 3.8 and version< 3.12 depending on your  OS
- Install and setup latest version of [Git](https://git-scm.com/downloads) 


**1. Clone this repository**
- Open the terminal or git bash from your machine and run the following command:
``` git clone  https://github.com/sci-visus/Openvisus-NASA-Dashboard.git```

**2. Run the script**
- After cloning, go inside the repository using `cd Openvisus-NASA-Dashboard` from your terminal.

- If you are using Windows, you can go the folder containing the files, and double-click it. It should open a shell and start running the script.

- If you are using Linux or Mac, you can do `sh setup.sh` to run the script.

- This code uses port `8989` by default. If this port is already in use, please feel free to change it in the first line in the [`setup.sh`](setup.sh) file and run again.

- Once the installation completes, you should see something like this: 
![Installation Terminal](./images/installation.png)

It is basically cloning a repo, setting up the environment and installing required dependencies to run the dashboard properly. It could take upto 3 minutes but your internet speed can affect this time.

**3. Visit the Dashboard**
- Once the script runs successfully, you can visit the url [localhost:8989](http://localhost:8989) or [0.0.0.0:8989](http://0.0.0.0:8989) in your browser and start exploring.
- By default, you can see the dashboard that looks like this:
![Dashboard](./images/dashboard_homepage.png)

**4. Interactivity**
There are several interactive options available within the dashboard. 

- *Dataset*: you can click dropdown option called `scene` at the topmost left and get a list of dataset available
- *Time*: You can change the timeslider called `Time` to get any timesteps. There are more than 10000 timesteps available from the original simulation.
- *Offset*: You can change the depth of the ocean by changing the `offset` slider. Since this is ocean data, `0` means the sea surface. The depth increases as the offset increases. Total 90 depths available from the original simulation.
- *Resolution*: It lets the users select the quality of the data they want. Lower resolution means coarser data, with low data movement, higher resolution means finer and more detailed data which can be slower.
- *Direction*: This is useful to see the vertical slicing, horizontal slicing or the surface visualization based on user's needs.
- *Play*: There is a `Play` button available that lets the users browse through time. 
- *Speed*: It is the number of timesteps users want to see at a time while `playing`. `1` means every single timestep, `2` means every other timestep and so on.
- *Frame delay*: This allows the users to manually slow down the rate at which data are updated.
- *Palette*: Users can choose from a list of high quality perceptually accurate color palettes depending on their needs. 
- *Range*: This lets the users decide if they want to keep the same range across entire data or dynamically change the range as new timestep or depths comes in. Users can manually set their own range by change the dropdown option to `user` and changing `min` and `max` values in the following boxes.

**5. Subregion Extraction**
We understand that extracting a region from this huge dataset can be extremely useful for certain usecases. So, we have used the bokeh widgets along with Javascript to allow selection of regions within the dashboard. Right next to the colormap, you can see a bokeh toolbar that looks like this:

<img src='./images/bokeh_widgets.png' alt = 'Bokeh Widgets' style= "float:left; margin-right: 20px">
<p> 

- *Pan*: The top option is called `pan` and its selected by default. You can move the image around while this is clicked. 

- *Selection*: The second option is a `selection` box. After clicking this, you can draw a bounding box on the image anywhere, and this will show the detailed view of that selection region, which is described in the next section below.

- *Zoom*: The third option is the `zoom` button. Its on by default and, users can use their mouse cursor to zoom into a region or zoom out as per their needs.

- *Reset*: If the viewing region is changed at any point because of the use of the buttons above, clicking this will reset the zoom and pan to default.  
</p>

**6. Region of Interest Detailed View**
 When a selection box is clicked from bokeh toolbar and a bounding box is drawn on the image, it queries for the higher resolution data in that selection region. We limit the size to be either 20MB or highest resolution possible without going over this limit. The detailed view looks like this:

 ![Detailed Window](./images/detailed_window.png)

 Some of the features available in this window are mentioned below:
 - *Download the numpy array*: Users have the option to save the selected data into their local machine as a numpy array. It captures both the data and their relative position in the data nad save it as a `.npz` file which can then  be loaded with `numpy` and can be used anywhere numpy is supported.

 - *Download the python script*: In case the data is large and users dont want to download the data immediately, it lets the users download the python script that can query for the exact region and save them locally in their machine. 

 - *Replace Existing Range*: If the range of the seleted data is different and users think this is more appropriate for the whole dashboard, they can click ` Replace Existing Range` to replace the min/max value in the original dashbaord. For example, if the original dashboard colormap has the range forom `-4` to `4`, and the selected region has range from `-1` to `1` which they believe is more appropriate, clicking this will change the original colormap in the dashboard to `-1`to `1`.

 - *Add This Range*: In other cases where the original dashboard is showing range thats not including the range in detailed view or if users changed the range previously and wants to manually manipulate the range, clicking `Add This Range` will change the min/max in the orginal dashboard ensuring that the new range is included. For example, if the main dashboard is showing range from `-1` to `1`, and users selected a region that had values ranging `-2` to `1.5`, clicking this will update the color range in main dashboard to include highest minima and maxima values, i.e. `-2` to `1.5` in this case.

 - *Detailed Stats*: The detailed view also shows the minimum and amximum value for the selected region. If users want to download the data locally, it also shows the approximate file size. Again, this is set to a 20 MB max so that users don't accidentally download large chunk of data in their local machine without being aware of.