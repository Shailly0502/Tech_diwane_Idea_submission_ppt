### _A solution is provided for the Problem Statement titled as Automated Cheque Processing,in Bank of Baroda Hackathon 2022 hosted on TechGig._

## Provided Problem Statement(Automated Cheque Processing)

Bank handles large volumes of cheques in the clearing process. The process involves many technical verifications including signature verification. Some of these steps are manual and require human intervention to complete the process. The current process requires the high human capital deployment and longer processing time.

## Expected Solution

Using rule-based and AI/ML/ICR/ OCR (Optical Character Recognition) capabilities for automation and doing technical and signature verification of the cheques.
* Automation of the clearing process using AI/ML/ICR/OCR techniques
* Automatic Data Entry & Technical verification
* Signature Verification
* Support Multilingual
* Reduce Human Efforts
* Reduce Processing time
* Detecting Potential Frauds

## Proposed Solution

### Workflow

* A cheque image is taken as an input & scanned. Then this scanned image is transformed into many different small part where every part contain seperate useful information like signature,amount,account number,payee name,bank name,etc. 
* These parts that extracted by drawing boxes on those parts of the scanned cheque image that contain these information with help of __OpenCV__ and __Geometry.__
* With the help of __Azure APIs__ these small different parts of the scanned images are sent to __OCR(Optical Character Recognition)__ for  processing information written in these small images.
* OCR model returns a list of detections and then among that list, there are both useful information and additional informations. Among complete list, detections of only required information are considered(this is  known as __text cleaning or extracting of useful information__).

_Please make a note that Useful information here mean that only that information that is relevant or required for cheque verification and processing._

* After cleaning or extracting useful detection from OCR list, the information of the payee is used to verify with the payee's existing record information in database __so as to verify if payee is genuine or not__. 

* For verifying the identity of the payee, Verification of different extracted information takes with the help of ML modules._This process is known as __Verification Process__ and is the most crucial part of the whole process._

  * __Signature Verification__ is done with the help of __signver module__ that contains __sub-modules__ such that:
 
    * _Cleaner module_ returns a list of cleaned signature images (removal of background lines and text), given a list of signature images.
    * _Extactor module_ returns a list of vector representations, given a list of image tensors/np arrays.
    * _Matcher module_ returns a distance measure given a pair of signatures (where one signature image is the image of payee's signature extracted from input cheque image and other image is the image present in payee's existing records in the database). _If both images match, then signature is verified otherwise signature on input cheque is a forgery or fake signature of payee._

    _Diagrametic Representation of signver module_

  ![signature verification](https://raw.githubusercontent.com/fastforwardlabs/signver/main/docs/images/signature_pipeline.png)
  
   * Extracted __Account Number__ is verified by checking if any user information with this account number exists.
  
   * Extracted __Payee Name__ is verified by matching payee name present in the database of the extacted account number and extracted payee name.
   * __Amount Verification__ is done to check if account contains sufficient amount such that transaction of mentioned amount could take place in future after successful verification of cheque details because _If sufficient amount is present in account then only transaction will take place._

 _Only after the successful verification, any processes or transactions(as instructed on cheque like transferring of money to the intended user bank account) takes place._

* __After successful cheque processing, the details of the sender gets further updated in the database as per the transaction took place successfully.__

![cheque verification](https://raw.githubusercontent.com/fastforwardlabs/signver/main/docs/images/signature_pipeline.png)



### Features

* Supports Multilingual _(Hindi,English)_
* Reduce Human Efforts _(By automating process of verification and data updation after processing)
* Reduce Processing time _(Machine take less time than humans so it fastens the cheque processing time )
* Detecting Potential Frauds _(Through verification processing)_
