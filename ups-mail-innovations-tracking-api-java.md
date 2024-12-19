UPS Mail Innovations Tracking API - Java
================================
Use Java to track UPS Mail Innovations shipments with UPS Mail Innovations Tracking API.

Features
--------
- Real-time UPS Mail Innovations tracking.
- Batch UPS Mail Innovations tracking.
- Other features to manage your UPS Mail Innovations tracking.

Installation
------------

**Maven**

    $ <dependency>
    $ <groupId>io.github.trackingmores</groupId>
    $ <artifactId>trackingmore-sdk-java</artifactId>
    $ <version>1.0.3</version>
    $ </dependency>

**Gradle**

    $ implementation "io.github.trackingmores:trackingmore-sdk-java:1.0.3"

Quick Start
----------
Get the API key:

To use this API, you need to generate your API key.

- <a href="https://admin.trackingmore.com/developer/apikey" target="_blank" rel="noreferrer">
  Click here</a> to access TrackingMore admin.

- Go to the "Developer" section.

- Click "Generate API Key".

- Give a name to your API key, and click "Save" .


Then, start to track your UPS Mail Innovations shipments.

Usage
----------

Create a tracking (Real-time tracking):

    package com.trackingmore.example.upsmi;
    
    import com.trackingmore.TrackingMore;
    import com.trackingmore.exception.TrackingMoreException;
    import com.trackingmore.model.TrackingMoreResponse;
    
    import java.io.IOException;
    import java.util.List;
    
    public class CreateUPSMailInnovationsTrackingExample {
    
        public static void main(String[] args) {
            try {
                String apiKey = "your api key";
                TrackingMore trackingMore = new TrackingMore(apiKey);
                
                CreateTrackingParams createTrackingParams = new CreateTrackingParams();
                createTrackingParams.setTrackingNumber("92612903104062543400000915");
                createTrackingParams.setCourierCode("ups-mi");
                TrackingMoreResponse<Tracking> result = trackingMore.trackings.CreateTracking(createTrackingParams);
                System.out.println(result.getMeta().getCode());
                if(result.getData() != null){
                   Tracking trackings = result.getData();
                   System.out.println(trackings);
                   System.out.println(trackings.getTrackingNumber());
                }
            } catch (TrackingMoreException e) {
                System.err.println("error：" + e.getMessage());
            } catch (IOException e) {
                System.err.println("error：" + e.getMessage());
            }
        }
    
    }


Create trackings (Max. 40 tracking numbers create in one call):

    package com.trackingmore.example.upsmi;
    
    import com.trackingmore.TrackingMore;
    import com.trackingmore.exception.TrackingMoreException;
    import com.trackingmore.model.TrackingMoreResponse;
    
    import java.io.IOException;
    import java.util.List;
    
    public class CreateUPSMailInnovationsTrackingsExample {
    
        public static void main(String[] args) {
            try {
                String apiKey = "your api key";
                TrackingMore trackingMore = new TrackingMore(apiKey);
                
                List<CreateTrackingParams> paramsList = new ArrayList<>();
                
                CreateTrackingParams createTrackingParams1 = new CreateTrackingParams();
                createTrackingParams1.setTrackingNumber("92419999920412543483090901");
                createTrackingParams1.setCourierCode("ups-mi");
                
                CreateTrackingParams createTrackingParams2 = new CreateTrackingParams();
                createTrackingParams2.setTrackingNumber("92419999920594513018295593");
                createTrackingParams2.setCourierCode("ups-mi");
                
                paramsList.add(createTrackingParams1);
                paramsList.add(createTrackingParams2);
                
                TrackingMoreResponse<BatchResults> result = trackingMore.trackings.BatchCreateTrackings(paramsList);
                System.out.println(result.getMeta().getCode());
                BatchResults batchResults = result.getData();
                if(result.getData() != null){
                    System.out.println(batchResults);
                    for (BatchItem batchItem : batchResults.getSuccess()) {
                        String trackingNumber = batchItem.getTrackingNumber();
                        String courierCode = batchItem.getCourierCode();
                        System.out.println("Tracking Number: " + trackingNumber);
                        System.out.println("Courier Code: " + courierCode);
                    }
                    for (BatchItem batchItem : batchResults.getError()) {
                        String trackingNumber = batchItem.getTrackingNumber();
                        String courierCode = batchItem.getCourierCode();
                        System.out.println("Tracking Number: " + trackingNumber);
                        System.out.println("Courier Code: " + courierCode);
                    }
                }
            } catch (TrackingMoreException e) {
                System.err.println("error：" + e.getMessage());
            } catch (IOException e) {
                System.err.println("error：" + e.getMessage());
            }
        }
    }


Get status of the shipment:

    package com.trackingmore.example.upsmi;
    
    import com.trackingmore.TrackingMore;
    import com.trackingmore.exception.TrackingMoreException;
    import com.trackingmore.model.TrackingMoreResponse;
    
    import java.io.IOException;
    import java.util.List;
    
    public class GetUPSMailInnovationsTrackingExample {
    
        public static void main(String[] args) {
            try {
                String apiKey = "your api key";
                TrackingMore trackingMore = new TrackingMore(apiKey);
                
                GetTrackingResultsParams trackingParams = new GetTrackingResultsParams();
                # Perform queries based on various conditions
                # trackingParams.setTrackingNumbers("92419999920412543483090901,92419999920594513018295593");
                trackingParams.setCourierCode("ups-mi");
                trackingParams.setCreatedDateMin("2023-08-23T06:00:00+00:00");
                trackingParams.setCreatedDateMax("2023-09-05T07:20:42+00:00");
                TrackingMoreResponse<List<Tracking>> result = trackingMore.trackings.GetTrackingResults(trackingParams);
                System.out.println(result.getMeta().getCode());
                List<Tracking> trackings = result.getData();
                for (Tracking tracking : trackings) {
                    String trackingNumber = tracking.getTrackingNumber();
                    String courierCode = tracking.getCourierCode();
                    
                    System.out.println("Tracking Number: " + trackingNumber);
                    System.out.println("Courier Code: " + courierCode);
                }
            } catch (TrackingMoreException e) {
                System.err.println("error：" + e.getMessage());
            } catch (IOException e) {
                System.err.println("error：" + e.getMessage());
            }
        }
    }


Update a tracking by ID:

    package com.trackingmore.example.upsmi;
    
    import com.trackingmore.TrackingMore;
    import com.trackingmore.exception.TrackingMoreException;
    import com.trackingmore.model.TrackingMoreResponse;
    
    import java.io.IOException;
    import java.util.List;
    
    public class UpdateUPSMailInnovationsTrackingExample {
    
        public static void main(String[] args) {
            try {
                String apiKey = "your api key";
                TrackingMore trackingMore = new TrackingMore(apiKey);
                
                String idString = "9dc04fc69689eaa1eadd65882ca66857";
                UpdateTrackingParams updateTrackingParams = new UpdateTrackingParams();
                updateTrackingParams.setCustomerName("New name");
                updateTrackingParams.setNote("New tests order note");
                TrackingMoreResponse<UpdateTracking> result = trackingMore.trackings.UpdateTrackingByID(idString, updateTrackingParams);
                System.out.println(result.getMeta().getCode());
                System.out.println(result.getData());
                if(result.getData() != null){
                    UpdateTracking  updateTracking= result.getData();
                    System.out.println(updateTracking);
                    System.out.println(updateTracking.getTrackingNumber());
                }
            } catch (TrackingMoreException e) {
                System.err.println("error：" + e.getMessage());
            } catch (IOException e) {
                System.err.println("error：" + e.getMessage());
            }
        }
    }
