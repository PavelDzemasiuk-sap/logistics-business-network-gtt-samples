# Track Sales Order Template App

## What's New in Track Sales Orders app (Micro Delivery 2020.Dec.18)
*	Enhance sales order and sales order item update logic to adapt to core engine asynchronous change. 
*	Fix the issue for sales order delay value calculation when delivery process status turns to Overdue.
*	Implement sendTrackingRequest function in Event-to-Action script.
*	Rename the event code in the ERP extractor, for example SHP_ARRIVAL>>ARRIV_DEST.
* Rename the app from Sales Order Fulfillment to Track Sales Orders.


## Description
Sales Order Fulfillment template app is designed for internal sales representatives to monitor the sales order fulfillment status. The app mainly answers the following questions:
* How many deliveries in my sales order are delayed?
* How many deliveries in my sales order are completed?
* Where are my sales orders?
* What is the ETA of my sales orders?
* ……
![image](https://github.com/SAP-samples/logistics-business-network-gtt-samples/blob/master/lbn-gtt-template-tso/Documents/screenshot.png)

## Requirements
* An SAP Cloud Platform global account with entitlement to the global track and trace option for SAP Logistics Business Network, 1 portal service quota and 2 GB Application Runtime quota
* To integrate with ERP, an SAP ERP or SAP ECC system running on Netweaver 7.31 or higher with SAP NOTE 2937175 being implemented 
* To integrate with visibility provider, log your incident in SAP BCP system with component “SCM-LBN-GTT-COR”

## Download and Installation
* [01_Implementation_Guide-TSO.pdf](https://github.com/SAP-samples/logistics-business-network-gtt-samples/blob/master/lbn-gtt-template-tso/Documents/01_Implementation_Guide-TSO.pdf) 
* [02_Extractor_Creation_Guide-TSO.pdf](https://github.com/SAP-samples/logistics-business-network-gtt-samples/blob/master/lbn-gtt-template-tso/Documents/02_Extractor_Creation_Guide-TSO.pdf) 

## Limitations
* Limitations for Document Flow Implementation: </br>
Recommended number of layers in document flow: ≤6; </br>
For number of layers > 6, please use table view or extend the document flow by click. </br>
Recommended number of nodes in document flow: ≤500; </br>
For number of nodes > 500, please use table view. </br>

* Notes for ERP Extractor Implementation: </br>
The eventMatchKey of the shipment’s planned event = shipmentNo + stopId. "stopId" is set by the stage’s sequence. </br>
The eventMatchKey of the delivery's and delivery item's planned event is null. </br>
To integrate with visibility provider, the following code list sent out from ERP system should be consistent with the code list in Sales Order Fulfillment template model: </br>
transportation mode code, shipping type code, tracked process type code, carrier refrence document type code  

## Known Issue
* If multiple IDOC payloads are generated at the same time or in a very short time in ERP, these payloads will enter the global track and trace system in disorder. This will cause update error in some situations. It is a known issue and is expected to be fixed in the next release.

## FAQs
* Why couldn’t my shipment events be correlated with the delivery and then with the delivery item? </br>
The correlation starts 90 minutes before the planned departure time of the shipment’s first stop and ends when the shipment’s last stop’s POD is reported. </br>
Only during the correlation period can the shipment events be correlated with the delivery and then with the delivery item. </br>
You can set your own correlation period in Event-to-Action by updating “validFrom” and “validTo” logic. </br>

* Why can’t I find any stops and any planned routes in the map? </br>
Check if you have assigned the delivery to any shipments. Or the shipments do not have any stages. </br>
 
* Why are some stops missing in the map? </br>
Check if you have updated the right geocoordinates for those locations in the Manage Locations app. </br>

* Why are some actual events missing in the map? </br>
Only events with valid geocoordinates are shown in the map. </br>

* How is the shipment’s execution status changed? </br>
By default, the shipment’s execution status is “Not Started”. </br>
If the shipment’s planned event is reported, the execution status will be changed to “In Transit”. </br>
If the shipment’s all planned PODs are reported, the execution status will be changed to “Completed”. </br>
Once the execution status is set as “Completed”, it cannot be changed any more. </br>
You can set your own execution status logic in Event-to-Action. </br>

* How is the delivery’s execution status changed? </br>
By default, the delivery item’ execution status is “Not Started”. </br>
If the delivery item’s planned event is reported, the execution status will be changed to “In Transit”. </br>
If the delivery item’s all planned PODs from shipment are reported or the delivery item’s own planned POD is reported, the execution status will be changed to “Completed”. </br>
Once the execution status is set as “Completed”, it cannot be changed any more. </br>
You can set your own execution status logic in Event-to-Action. </br>

## How to Obtain Support
The project is provided "as-is", with no expected support. </br>
If your issue is concerned with global track and trace option, log your incident in SAP BCP system with component “SCM-LBN-GTT-COR”. 
