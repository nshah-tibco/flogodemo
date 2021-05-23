# Co-Win Vaccine Appointment Availability Demo


This demo sample sends emails and SMS alerts about the Co-Win Vaccine Appointment Availability Slots to the user based on the input parameters for a district_id, date, min_age, dose.

## Prerequisites:

1. TIBCO Flogo® Enterprise - Since Co-Win public API's are allowed only to be accessed from IP address range only from India, so you will need TIBCO Flogo® Enterprise to generate the binary/docker image for this application and deploy it locally or on any PaaS platform like AWS, Azure, GCP in India region.
2. SendMail Activity needs to be configured with Server, Port, Username, Password for sending email to the user about the available slots.
3. TIBCO Flogo® Connector for Twilio - This app sends SMS to the user about the available PIN codes for vaccine appointment. So you will need to install this FLOGO Connector.

## Notes:

1. If you just want to play around with this app and try it in flow tester, then you can delete these SendMail and SendTwilioMessage activites from the app and run the flow in flow tester. You will still be able to run the app end to end.
2. If you want to run this app in TIBCO Cloud™ Integration (TCI), then you can replace ReceiveHTTPMessage and Timer trigger with AWSAPIGatewayLambdaTrigger and deploy this app as Amazon API Gateway in AWS  in the Asia Pacific (Mumbai) ap-south-1 region and invoke the public API endpoints with appropriate Query Parameters. 


## Import a sample

1. Download the sample's .json file.

2. Create a new empty app.

3. On the app details page, select Import app.

4. Browse on your machine or drag and drop the .json file for the app that you want to import.

5. Click Upload. The Import app dialog displays some generic errors and warnings as well as any specific errors or warnings pertaining to the app you are importing. It validates whether all the activities and triggers used in the app are available in the Extensions tab.

6. You have the option to import all flows from the source app or selectively import flows.

7. Click Next. If you had not selected a trigger in the previous dialog, the flows associated with that trigger are displayed. You have the option to select one or more of these flows such that the flows get imported as blank flows that are not attached to any trigger. By default, all flows are selected. Clear the check box for the flows that you do not want to import. If your flow(s) have subflows, and you select only the main flow but do not select the subflow, the main flow gets imported without the subflow. Click Next.

## Testing the app

1. To test the flows in flow tester, Import the corresponding Launch Configuration in Flow Tester for the flow and update the Query Parameters according to your need.
2. To get the district_id, first run the "Metadata API-States" flow in Flow Tester and get the state_id. 
3. Run the "Metadata API - Districts" flow in flow tester with the state_id as the Query Parameter and get the district_id for your District.
4. Run the "Appointment Availability by PIN" flow and give date and pincode as Query Parameter and get all the available slots for your pincode. date should be of the format dd-mm-yyyy for eg: 23-05-2021 
5. Run the "Appointment Availability by District" flow and give date and district_id as Query Parameter and get all the available slots in your district. date should be of the format dd-mm-yyyy for eg: 23-05-2021 and district_id as 363 for Pune District
6. Run the "Appointment Availability by District by Age Dose Vaccine" flow to get the available slots for a given date, min_age_limit, district_id, dose. date format is dd-mm-yyyy for eg: 23-05-2021. min_age_limit can be 18 or 45. dose value can be 1 or 2. district_id value needs to be fetched from #2 and #3.

## Running the app

The steps are similar to the ones mentioned in "Testing the app" section.
You will need to export the variables as below based on your needs -

export district_id=363
export min_age=18
export dose=18
export email=[email on which alert emails need to be sent]
export username=[username for SendEmail activity]
export password=[password for SendEmail activity]
export FromNumber=[Twilio From Number]
export ToNumber=[The number on which SMS alerts need to be sent]

Run the app using below command from the terminal -

FLOGO_APP_PROPS_ENV=auto ./[app binary name]

If you are running the app locally then few examples for the endpoints to be hit from postman or any other REST client :

1. http://localhost:9999/location/states - To get list of states
2. http://localhost:9999/location/districts/21 - To get list of districts in the State of Maharashtra
3. http://localhost:9999/appointment/sessions/calendarByPin?date=23-05-2021&pincode=411001 - Get available slots for 1 week from 23-05-2021 for the pincode - 411001
4. http://localhost:9999/appointment/sessions/calendarByDistrict?date=23-05-2021&district_id=363 - Get available slots for 1 week from 23-05-2021 for Pune district (district_id = 363)
5. http://localhost:9999/appointment/sessions/calendarByDistrict/ByAgeDoseVaccine?date=23-05-2021&district_id=363&dose=1&min_age_limit=18 - Get available slots for Pune district (district_id = 363) for 1 week from 23-05-2021 for 18+ Dose 1


## Help

Please visit our [TIBCO Cloud<sup>&trade;</sup> Integration documentation](https://integration.cloud.tibco.com/docs/) and TIBCO Flogo® Enterprise documentation on [docs.tibco.com](https://docs.tibco.com/) for additional information.
