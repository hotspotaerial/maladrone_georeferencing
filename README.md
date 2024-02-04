<img src="https://user-images.githubusercontent.com/870796/190517543-96f85ea2-55d0-4f3f-a1d6-18c926f8c8f5.png" data-canonical-src="https://user-images.githubusercontent.com/870796/190517543-96f85ea2-55d0-4f3f-a1d6-18c926f8c8f5.png" width="640" />

# Detect and Map Mosquito breeding sites from Drone Videos

This project extracts the location of objects of interest from a drone video and plots them on a map. By combining the video with data from its flight log and a computer vision model trained on [Maladrone](https://wwww.hotspotaerial.com), it demonstrates georeferencing a machine learning model's predictions to GPS coordinates and using them to visualize the location of detected breeding sites on a map using [Mapbox](https://mapbox.com).

https://user-images.githubusercontent.com/870796/189461690-122f4e64-a66e-40f0-ac4b-68258a8abe7e.mov
https://user-images.githubusercontent.com/870796/189461690-122f4e64-a66e-40f0-ac4b-68258a8abe7e.mov

## Try It in Your Browser

The project is [deployed to Github Pages here](https://hotspotaerial.github.io/maladrone-georeferencing/) and you can test it out with [this sample video and flight log](https://drive.google.com/drive/folders/1m0lmYyLEQJiaykf821rYtyRvlO5Q_SAf).

If you have your own Drone video you'd like to use, [follow the instructions in the blog post to pull your detailed flight log from Airdata](https://blog.roboflow.com/georeferencing-drone-videos/).

## Resources

* Accompanying Blog Post: [Georeferencing Breeding sites in Drone Videos](https://hotspotaerial.com)

## Run It Locally

* Clone this repo
* Run `npm install` in the main directory
* Run `npm run build:dev` to start a webpack build with livereload
* Open a new terminal window and run `npx serve dist`
* Open `http://localhost:3000` in your browser

## Customize It

This repo can easily be changed to run any custom model trained with [Roboflow](https://app.roboflow.com) including the thousands of [pre-trained models shared on Roboflow Universe](https://universe.roboflow.com/search?q=aerial%20imagery%20top%20down%20view%20trained%20model). Simply swap out your `publishable_key` and the `model` ID and `version` in the `ROBOFLOW_SETTINGS` at the top of [`main.js`](src/main.js).

Other ideas for how to use this repo:
* [Search & Rescue](https://universe.roboflow.com/lifesparrow/images-25-8/browse?queryText=&pageSize=50&startingIndex=0&browseQuery=true)
* [Monitoring swimmer safety](https://universe.roboflow.com/yolo-training/man-over-board/browse?queryText=&pageSize=50&startingIndex=0&browseQuery=true) in triathlons
* Helping governments [identify zoning violations](https://universe.roboflow.com/hruthik-sivakumar/swimming-pool-b6pz4/browse?queryText=&pageSize=50&startingIndex=0&browseQuery=true)
* Monitoring core infrastructure like pipelines for [potential hazards like excavators and construction equipment](https://universe.roboflow.com/project-ip0vc/final-75vvh/browse?queryText=&pageSize=50&startingIndex=0&browseQuery=true) nearby
* [Finding people with bonfires](https://universe.roboflow.com/srichandana055-gmail-com/fire-and-smoke-videoo/browse?queryText=&pageSize=50&startingIndex=0&browseQuery=true) in high risk fire areas
* [Tracking wildlife](https://universe.roboflow.com/elephantdetection-90mt9/newprojectelephant/browse?queryText=&pageSize=50&startingIndex=0&browseQuery=true)
* Mapping [oil wells](https://universe.roboflow.com/haritha-r/oilwells/browse?queryText=&pageSize=50&startingIndex=0&browseQuery=true)
* Monitoring [land use and tree cover](https://universe.roboflow.com/treedataset-clsqo/tree-top-view/browse?queryText=&pageSize=50&startingIndex=0&browseQuery=true)
* [Finding boats](https://universe.roboflow.com/jacob-solawetz/aerial-maritime) fishing in restricted areas
* Counting [cars in parking lots](https://universe.roboflow.com/swee-xiao-qi/parking-lot-availability/browse?queryText=&pageSize=50&startingIndex=0&browseQuery=true)
* [Tracking human rights violations](https://blog.roboflow.com/computer-vision-for-human-rights/)
* [Other Aerial Datasets & Models](https://universe.roboflow.com/browse/aerial) to get your gears turning

### Getting Your Flight Log

You can get the detailed flight log from a DJI drone using [Airdata](https://airdata.com). The [sample video and flight log](https://drive.google.com/drive/folders/1m0lmYyLEQJiaykf821rYtyRvlO5Q_SAf) were taken from a DJI Mavic Air 2. Full details are [in the blog post](https://blog.roboflow.com/georeferencing-drone-videos/).

<img width="659" alt="flighlog" src="https://user-images.githubusercontent.com/870796/190518745-278df36e-1866-4e15-9359-667848598557.png">

### Training a Custom Model

If you can't find a pre-trained model that accurately detects your particular object of interest on [Roboflow Universe](https://universe.roboflow.com) you can create a dataset and train your own custom model using [Roboflow](https://roboflow.com).

Once you've trained a custom model, update your publishable API Key, model ID, and version in the configuration at the top of [`main.js`](src/main.js).

## Contributing

Pull requests are welcome to improve this repo. Ideas for improvements that could be made:

* Taking into account changes in the ground elevation & their impact on the `distance` calculations
* Intelligently choosing the correct part of the flight log based on the duration of `isVideo` compared to the duration of the loaded video
* Exporting a JSON file of the detected objects
* Adding a CLI for processing outside of a web browser
* Rendering the flight video and predictions into a single image (patching video frames together)
* Video controls (play/pause, scrubbing)
* Option to show the video in a static position vs flying over the flight path
* Add smoothing to the video positioning to account for the flight-log only having a 100ms resolution
* Allowing dynamically swapping the model endpoint & version in the UI to easily try other models in the UI without having to change the code
* Improve the breeding sites detection model to make better predictions
