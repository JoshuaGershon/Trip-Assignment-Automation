Automated Trip Assignment System
A Python-based workflow that automates trip assignments by matching trip requests to available, compatible drivers using GPT-4o decision-making logic.

Problem Statement
Manual trip assignment leads to inefficiency, scheduling conflicts, and underutilized resources. This system automates the assignment process by matching new trip requests to available, compatible drivers — handling all assignment logic and notifying drivers instantly.

Live Platform Demo
PortalURLManager Portalhttps://isodomic-kayden-decussately.ngrok-free.dev/managerDriver Portalhttps://isodomic-kayden-decussately.ngrok-free.dev/driver
Note: These URLs are active while the Colab notebook is running. To access the platform, run all cells in the notebook first, then open the links above.

Features

Manager Portal — Create new trip requests and view full assignment status dashboard
Automated Assignment — GPT-4o matches each trip to the best available driver based on availability, vehicle type, zone, workload, and priority
Driver Portal — Drivers view their assigned trips and update trip status
Notification System — Instant driver notifications upon assignment
Assignment Logger — Full audit trail of every assignment with GPT reasoning
Conflict Prevention — Time overlap detection prevents duplicate assignments


Tech Stack

Python 3
Google Colab
OpenAI GPT-4o API
Pandas
Flask
ngrok


Project Structure
Joshua_Gershon_UC24_repo/
│
├── trip_assignment_workflow.ipynb   # Main Colab notebook
├── drivers.csv                      # Driver dataset (50 drivers)
├── trips.csv                        # Trip dataset (100 trips)
└── README.md                        # Project documentation

Dataset
drivers.csv
50 drivers with the following fields:
FieldDescriptiondriver_idUnique driver identifiernameDriver full namephoneContact numbervehicle_typeSedan, SUV, Van, Truck, or Minibuslicense_levelStandard, Commercial, CDL-A, CDL-B, Medical Transport CertifiedzoneNorth, South, East, West, CentralshiftShift nameavailability_startShift start timeavailability_endShift end timestatusavailable, busy, or off-shifttrips_completed_todayRunning trip count
trips.csv
100 trips with the following fields:
FieldDescriptiontrip_idUnique trip identifiertrip_typeCorporate shuttle, Medical transport, Delivery run, etc.pickup_timeScheduled pickup timeduration_minsEstimated trip durationoriginPickup locationdestinationDrop-off locationvehicle_requiredRequired vehicle typezoneTrip zonepassengersNumber of passengerspriorityLow, Normal, High, or Urgentspecial_requirementsWheelchair accessible, Temperature controlled, etc.statusunassigned or assignedassigned_driver_idID of assigned driver

How to Run
1. Open in Google Colab
Upload trip_assignment_workflow.ipynb to Google Colab
2. Set up secrets
In the Colab left sidebar click the key icon and add two secrets:

OPENAI_API_KEY — your OpenAI API key from platform.openai.com
NGROK_TOKEN — your ngrok authtoken from ngrok.com

3. Upload datasets
Upload drivers.csv and trips.csv to Google Drive and mount your drive, or upload directly via the Colab file picker.
4. Run cells in order
Run all cells from top to bottom in the following order:

Install dependencies and connect OpenAI API
Generate or load datasets
GPT matching engine
Status updater
Notification system
Assignment logger
Orchestration loop
Manager portal
Driver portal
Flask platform launch

Note: The notebook may contain additional cells used for testing, debugging, and data reloading during development. Run all cells top to bottom for the full workflow.

Design Considerations
RequirementImplementationManager portalCreate trips and view assignment dashboardDriver portalView and update assigned tripsAutomated assignmentGPT-4o matching engine with Pandas pre-filteringInstant notificationsNotification printed immediately after each assignment

Non-Functional Requirements
RequirementImplementationPerformance < 2sPandas pre-filtering reduces GPT input sizeNo duplicate assignmentsTime overlap detection in status updaterNo missed assignmentsThree-layer fallback filter in matching engineRole-based accessSeparate manager and driver portal functionsAuditabilityEvery assignment logged to assignment_log.csv with timestamp and GPT reasoning

Sample Output
==================================================
NOTIFICATION SENT TO: Aisha Brown
Phone: +15552556017
--------------------------------------------------
New trip assignment: TRP009
Type: Emergency supply run
Pickup time: 06:39
From: 963 Poplar Rd
To: Central Station
Passengers: 2
Priority: Normal
Special requirements: None
==================================================

ASSIGNMENT SUMMARY
Total trips processed: 100
Successfully assigned: 64
Could not assign: 36
Assignment rate: 64.0%

Author
Joshua Gershon — HackToHire NYC01
