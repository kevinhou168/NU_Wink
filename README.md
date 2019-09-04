# NU Wink
![NU Wink](https://i.imgur.com/VoqoDVR.png)
## Our Problem
- Students (especially freshmen) may have difficulty navigating the campus
- Prospective students and families visiting campus could get lost without a guide
- Due to shape of certain buildings on campus, determining whether you're at the right building on Google Maps is difficult
## Our Solution
- Build a smartphone app to help guide people!
- App displays names and information about buildings on campus to help
- Activate by opening app and viewing building/landmark through camera
## How it works
- Connects to database with important buildings on campus  with details such as location, descriptions, and photos
- Uses compass and GPS data to figure out what building you are looking at
- Displays the correct title, picture, and description for the building
### Tech Stack
![Tech Stack](https://i.imgur.com/uvL61MD.png)
#### Tech Stack: Data Pipeline
![Data Pipeline](https://i.imgur.com/vqUpeYd.png)
### UX Flow
![UX Flow Onboarding](https://i.imgur.com/EmxlXkd.png)
![UX Flow](https://i.imgur.com/UsjcOtC.png)
### Building Algorithm
#### Psuedocode
For each building in buildings:
Check if it is sufficiently close to you and within your FOV
If so, calculate its cost. If it’s cost is lower than that of current most likely candidate building, set it as the most likely candidate.
*Because this algorithm only loops once through (n) buildings and only calls functions that are O(1), it runs in linear time, O(n).*
#### Visualization
![BuildingAlgo](https://i.imgur.com/OdxVwrW.png)
#### Cost Function
- Each building that we run the cost function on has a distance and bearing under some acceptable limits, maxdistance and maxbearing. 
- We normalize distance and bearing so we can adequately compare them, and square the results so both are required to be quite close.
![CostFunction](https://i.imgur.com/Y9SUU4G.png)
### User Location + GPS
One would expect getting a user’s whereabouts to be simple, and that to find a user’s distance from a building, one can simply subtract lat and long. However, to do so is to assume the world is flat... the actual calculation is a little more complicated, requiring some non-euclidean geometry:
![Userlocation](https://i.imgur.com/7sZlce5.png)
- Finding and making sense of the direction a user is facing was also more complicated than anticipated
- The compass API gives us the user’s heading with respect to the magnetic north pole, so we had to find a way to convert that to their heading with respect to an individual building:
![Conversion](https://i.imgur.com/sOs7sqe.png)
### Bearing and Distance
![BearingDistance](https://i.imgur.com/nYRJjbP.png)
### Building Data
- Another hurdle was finding the data for the buildings on campus, as inputting that by hand would be extremely time-consuming
- We needed the latitude, longitude, name, and an image and description for each building.
- We managed to find an API for that included all we needed, except for images and descriptions. However, note the field “nu_maps_link”- where could that lead?
![API](https://i.imgur.com/fiY6hT2.png)
- The site maps.northwestern.edu has a picture and description for many buildings on campus, but no API or public database.
- What to do now?
- Web scraping to the rescue!
![NUSite](https://i.imgur.com/z7yNS2h.png)
![Scraping](https://i.imgur.com/zvq3sgB.png)
