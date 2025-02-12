^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Changelog for package hri_face_detect
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.0.10 (2024-09-16)
-------------------
* use python3-mediapipe-pip on non-PAL environments
  While here, add missing dep on cv_bridge
* Contributors: Séverin Lemaignan

2.0.9 (2024-09-09)
------------------
* fixed quality of service camera-related subscribers
* Contributors: lorenzoferrini

2.0.8 (2024-08-19)
------------------
* rename diagnostics msg to match documentation (and diagnostic_aggregator) categories
* Contributors: Séverin Lemaignan

2.0.7 (2024-07-04)
------------------
* linting
* Contributors: Séverin Lemaignan

2.0.6 (2024-07-04)
------------------
* launch: use get_pal_configuration from launch_pal
* expose the 'deterministic_ids' in the _with_args launch file
* Contributors: Séverin Lemaignan

2.0.5 (2024-05-24)
------------------
* Removed quotes from topic values
* Contributors: Raquel Ros

2.0.4 (2024-05-23)
------------------
* fix configuration node name
* fix get _pal_configuration
* Contributors: Luka Juricic

2.0.3 (2024-05-08)
------------------
* [launch] impl logic to load overlaid parameters
  This commit:
  - add (and install) default parameters values in config/00-defaults.yml
  - rename (unchanged) launch/face_detect.launch.py to launch/face_detect_with_args.launch.py
  - add a new launch/face_detect.launch.py that implements the PAPS-007 logic
  to fetch possible parameters, remappings and node arguments via ament_index
* Contributors: Séverin Lemaignan

2.0.2 (2024-04-24)
------------------
* add pal module
* Contributors: Luka Juricic

2.0.1 (2024-02-06)
------------------
* fix image calibration K name to lowercase k. This caused the publication of TF
  frames to be broken.
* assign default score detection in case of mesh detection
* add usage example to README
* Contributors: Luka Juricic

2.0.0 (2024-01-18)
------------------

* port to ROS 2 Humble
* change license to apache2
* change folder structure
* Contributors: Luka Juricic

1.5.3 (2023-11-27)
------------------
* rework filtering frame validation
  Now, does not pre-validate the filtering frame: simply try to transform
  to the filtering frame if it is provided, and continue without using
  filtering frame if it is not available.
  Helps in the case hri_face_detect starts before the robot's TF is fully
  published -> the filtering will start in the correct frame as soon as it
  become available.
* Contributors: Séverin Lemaignan

1.5.2 (2023-10-27)
------------------
* port facedetection external cmake to project one
* add tkinter dependency
* Contributors: Luka Juricic

1.5.1 (2023-10-24)
------------------
* fix library external project dependency
* Contributors: Luka Juricic

1.5.0 (2023-10-18)
------------------
* change detector to Yunet
  - large refactor
  - remove record node
  - use timer based logic to process the most recent image only
  - add Yunet detector as standalone C library
  - add Yunet python bindings
  - use Yunet as always on detector
  - use Mediapipe face mesh detector to refine near faces
  - update documentation
* Contributors: Luka Juricic

1.4.9 (2023-07-05)
------------------
* change RoI message type to hri_msgs/NormalizedRegionOfInterest2D
* Contributors: Luka Juricic

1.4.8 (2023-06-22)
------------------
* added filtering_frame parameter
  the user can now decide which frame to use to filter
  the faces position
* Contributors: lorenzoferrini

1.4.7 (2023-05-23)
------------------
* face pose filtering using the one-euro filter
* Contributors: lorenzoferrini

1.4.6 (2023-05-12)
------------------
* add diagnostics
* Migrate to new python3-mediapipe rosdep key
* Contributors: Séverin Lemaignan, lukajuricic, mathiasluedtke

1.4.5 (2023-03-08)
------------------
* ensure mediapipe is not called from 2 threads in parallel
  This was causing mediapipe internal timestamp issues
* Contributors: Séverin Lemaignan

1.4.4 (2022-10-06)
------------------
* fix FacialLandmark object initialisation
  When face_mesh=False, the arguments for the FacialLandmarks
  objects initialisation were not correctly disposed, as the
  first element in a FacialLandmarks message is supposed to be a
  Header.
* Contributors: lorenzoferrini

1.4.3 (2022-08-31)
------------------
* more update to hri_msgs-0.8.0
* Contributors: Séverin Lemaignan

1.4.2 (2022-08-31)
------------------
* update to hri_msgs-0.8.0
* Contributors: Séverin Lemaignan

1.4.1 (2022-08-02)
------------------
* ensure face id are strings starting with a letter
* [cosmetic] code formatting
* pep8 code formatting
* add tool to record faces
* Contributors: Séverin Lemaignan

1.4.0 (2022-04-29)
------------------
* large refactor of the code
  In particular:
  - added a Face class to maintain the state of a detected face
  - reworked how detection results are returned, to simplify code
* publish aligned versions of the face under /humans/faces/<id>/aligned
  (aligned faces are rotated such as the eyes are always horizontal)
* warn about faces height and width having to be equal
* store various face publishers as dict to ease future extension
* Delegated face estimation process to function.
* publish empty list of faces upon closing to clean up state
* update launch file to match hri_fullbody arguments names
* [doc] node suitable for production
* Contributors: Séverin Lemaignan, lorenzoferrini

1.3.1 (2022-03-01)
------------------
* Use tf frame from source image
* Contributors: lorenzoferrini

1.3.0 (2022-03-01)
------------------
* changing the frames name syntax from face<id> to face_<id> and gaze<id> to
  gaze_<id> for compliance with ROS4HRI spec
* [minor] adding default value for camera topics in launch
* Documentation update
* Fixed the default number of detectable faces to 10
* Facial Landmark msg implementation
  Fully implemented facial landmark msg publishing for both basic
  face detection and face mesh detection
* Contributors: lorenzoferrini

1.2.0 (2022-02-14)
------------------
* mediapipe Face-mesh based face detection
  It is now possible to decide between two Mediapipe different
  solutions for face detection: face_detection and face_mesh.
  Since the overall performance (taking into account cpu, memory and
  detection results) appears to be better in the latter case,
  face_mesh detection will be the default option.
* add missing deps
* [minor] launch file modified according to new features available
  It is now possible to specify the solution to use
  (face_detection/face_mesh) and the maximum number of faces
  detectable by the face_mesh model as launch file parameters
* max_num_faces as initialization parameter for FaceDetector class
* [WiP] Correcting face orientation and introducing gaze frame
  Face and gaze frame orientation according to ROS4HRI convention.
* Facial landmarks publishing
  Now publishing the facial landmarks according to the ROS4HRI
  definition, on the topic /humans/faces/<body_id>/landmarks.
  Additionally, the face frame is published now as face\_<body_id>
  and the debug code has been removed.
* first rough implementation of PnP head pose estimation
* Contributors: Séverin Lemaignan, lorenzoferrini

1.1.0 (2022-01-18)
------------------
* publish cropped faces under subtopic /cropped
* add _preallocate_topics parameter (instead of hard-coded constant)
* code formatting
* RegionOfInterestStamped -> regionOfInterest to match changes in hri_msgs 0.2.1
* Contributors: Séverin Lemaignan

1.0.1 (2021-11-09)
------------------
* Added the dependency on python-mediapipe
* Publish an Empty msg on /hri_detect_face/ready when ready to start
  This is eg required for automated testing, to ensure the node is fully
  ready before publishing the first frames.
* added minimal node setup
* Added basic readme
* Simple, rough node using Google Mediapipe to perform fast face detection
* Contributors: Séverin Lemaignan
