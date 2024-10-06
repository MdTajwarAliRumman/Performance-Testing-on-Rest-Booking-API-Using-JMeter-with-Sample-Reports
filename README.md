### **#(Note: Get the entire project by downloading the full code from the collection and environment.)**
## Performance Testing on Rest Booking API using JMeter
This project provides an example of utilizing JMeter for performance testing. The project also offers a report on various thread counts (user counts), with the test commencing at 100 users and concluding with 1800 users and 10 loop counts. 

### **Features**

- Tests for GET, POST, PUT, PATCH, DELETE requests
- Collection of tests covering different API endpoints
- Test Plan setup
- Each Request containing HTTP Header Manager
- View Results Tree

## API Documentation:

### **Technology used:**
- Jmeter

### **Prerequisite:**
- RAM: At least 16Gb RAM, 32GB recommended.

### **Installation**

1. Jmeter: If you haven't already, [download and install Postman.](https://jmeter.apache.org/)

2. Download -> unzip -> bin -> jmeter.bat
*Do not use GUI mode for performance test, debug and setup
Start JMeter

  
## **Testing**

## Test Site:
	
### URL: https://reqres.in/
### URL: https://reqres.in/api/users/2
  	

### **Creating JMeter test:**
- Start JMeter
- Test plan creation
- Thread group
- Sampler (http)
- Listener

### **Listener:**
- view results in tree
- Aggregate report
- Graph results
- Simple data writer

## _**1. Creating HTTP Requests**_
- Select Test Plan
- Add "Thread Group" from Threads
- Add "HTTP Request" from Threads -> Sampler

## _**2. Create Token**_
- Rename "HTTP Request" as "Create Token"

### Protocol: https
### Request URL: restful-booker.herokuapp.com/booking/
### Request Method: POST
### Path: auth

- Add "HTTP Header Manager" -> set (Content-Type: application/json) & (Accept: \*/\*) 
- Add "JSON Extractor"-> set (Names of Variables: extractedToken) & (JSON path extraction: $.token)
 

**Request Body:**
```console 
{
	"username": "admin",
	"password": "password123"
}

  ```

## _**3. Create Booking**_

- Rename "HTTP Request" as "Create Booking"

### Protocol: https
### Request URL: restful-booker.herokuapp.com
### Request Method: POST
### Path: booking

- Add "HTTP Header Manager" -> set (Content-Type: application/json) & (Accept: \*/\*) 
- Add "JSON Extractor"-> set (Names of Variables: ExtractedBookingId) & (JSON path extraction: $.bookingid)
 

**Request Body:**
```console 
{
	"firstname" : "Tajwar",
	"lastname" : "Ali",
	"totalprice" : 111,
	"depositpaid" : true,
	"bookingdates" : {
    	"checkin" : "2018-01-01",
    	"checkout" : "2019-01-01"
	},
	"additionalneeds" : "Breakfast"
}
	
  ```
**Response Body:**
```console 
{"bookingid":4562,"booking":{"firstname":"Tajwar","lastname":"Ali","totalprice":111,"depositpaid":true,"bookingdates":{"checkin":"2018-01-01","checkout":"2019-01-01"},"additionalneeds":"Breakfast"}}
  ```

## _**4. GET Booking**_

- Rename "HTTP Request" as GET Booking

### Protocol: https
### Request URL: restful-booker.herokuapp.com
### Request Method: GET
### Path: booking/${ExtractedBookingId}

- Add "HTTP Header Manager" -> set (Content-Type: application/json) & (Accept: \*/\*) 
 

**Response Body:**
```console 
{"firstname":"Tajwar","lastname":"Ali","totalprice":111,"depositpaid":true,"bookingdates":{"checkin":"2018-01-01","checkout":"2019-01-01"},"additionalneeds":"Breakfast"}
  ```

## _**5. Update Booking**_

- Rename "HTTP Request" as Update Booking with PUT"

### Protocol: https
### Request URL: restful-booker.herokuapp.com
### Request Method: PUT
### Path: booking/${ExtractedBookingId}

- Add "HTTP Header Manager" -> set (Content-Type: application/json), (Accept: \*/\*) & (Cookie: token=${extractedToken})
 
**Request Body:**
```console 
{
	{
	"firstname" : "Jim",
	"lastname" : "Brown",
	"totalprice" : 111,
	"depositpaid" : true,
	"bookingdates" : {
    	"checkin" : "2018-01-01",
    	"checkout" : "2019-01-01"
	},
	"additionalneeds" : "Breakfast"
}

}
	
  ```
**Response Body:**
```console 
{"firstname":"Jim","lastname":"Brown","totalprice":111,"depositpaid":true,"bookingdates":{"checkin":"2018-01-01","checkout":"2019-01-01"},"additionalneeds":"Breakfast"}
  ```

## _**6. Update Booking Using PATCH**_

- Rename "HTTP Request" as Update Booking with PATCH"

### Protocol: https
### Request URL: restful-booker.herokuapp.com
### Request Method: PATCH
### Path: booking/${ExtractedBookingId}

- Add "HTTP Header Manager" -> set (Content-Type: application/json), (Accept: \*/\*) & (Cookie: token=${extractedToken})
 
**Request Body:**
```console 
{
	"firstname" : "Rumman",
	"lastname" : "Ali"
}

	
  ```
**Response Body:**
```console 
{"firstname":"Rumman","lastname":"Ali","totalprice":111,"depositpaid":true,"bookingdates":{"checkin":"2018-01-01","checkout":"2019-01-01"},"additionalneeds":"Breakfast"}
  ```

## _**7. Delete Booking**_

- Rename "HTTP Request" as Update Booking with PATCH"

### Protocol: https
### Request URL: restful-booker.herokuapp.com
### Request Method: DELETE
### Path: booking/${ExtractedBookingId}

- Add "HTTP Header Manager" -> set (Content-Type: application/json) & (Cookie: token=${extractedToken})
 
**Response Body:**
```console 
Created
  ```
## Report Generation Steps:
- Save the jmx file with proper thread count/ramp up/loopcount (keeping in mind -> listener disable, assertion disable)
- Generate the command to run performance test in cmd
- jmeter -n -t Booking_Collection_1800.jmx -l report\Booking_Collection_1800.jtl
- jmeter -g report\Booking_Collection_1800.jtl -o report\Booking_Collection_1800.html

## Newman Report Summary:  
### I’ve completed performance test on frequently used API for test App. Test executed for the below mentioned shows the Booking_collection 800, 1600 & 1800

### For Booking_Collection_800:
![800pass](https://github.com/user-attachments/assets/8b472863-db27-453f-89e1-b2860370d003)
![800](https://github.com/user-attachments/assets/d8d640af-d1b7-4e0e-a778-6fd89c35e09d)

