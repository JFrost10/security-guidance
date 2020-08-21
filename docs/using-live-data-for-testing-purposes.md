# Using Live Data for Testing purposes

## Summary

This document describes the use of live data during testing of Ministry of Justice \(MOJ\) systems. In general, using live data for testing purposes is considered bad practice. By default, the MOJ does not permit testing using live data. It is highly likely that using live data for testing purposes would not be compliant with GDPR.

## Who is this for?

This guide is aimed at two audiences:

1.  The in-house MOJ Digital and Technology staff who are responsible for testing systems as part of technical design, development, system integration and operation.
2.  Any other MOJ business group, agency, contractor, IT supplier and partner who in any way designs, develops or supplies services \(including processing, transmitting and storing data\) for, or on behalf of the MOJ.

## Do you really need to use live data?

Data used for testing purposes must have characteristics that are as close as possible to operational data. But that is not the same thing as needing to use live data.

Check whether you really need to use live data, by considering the following questions:

1.  Speed: What are your time requirements for test data provisioning?
2.  Cost: What is an acceptable cost to create, manage and archive test data?
3.  Quality: What are the important factors to consider related to test data quality?
4.  Security: What are the privacy implications of these two sources of test data?
5.  Simplicity: Is it easy for testers to get the data they need for their tests?
6.  Versatility: Can the test data be used by any testing tool or technology?

The best test data simulates live operations data.

**Note:** It is important that test data is protected to the same standard as the live data. This is to ensure that details of the system design and operation are not compromised.

To protect test data; the following principles should be followed:

-   The test manager must authorise the use of test data.
-   Test data should be erased from a testing environment immediately after the testing is complete or when no longer required.
-   The copying and use of test data should be logged to provide an audit trail.

By default:

-   Data used for testing must not contain any live data.
-   Using live data containing personal information is prohibited.

In exceptional circumstances, the use of live system data may be permitted. Permission to use live data is by exception only. A valid business case must be approved by the MOJ CISO, system assurer and the Information Asset Owner \(IAO\).

A thorough risk assessment should be carried out to ensure where interdependent applications, systems, apis, BACS, XML, process etc., may be required, these are appropriately reviewed and security controls put in place.

## Anonymising data

-   Is it possible to do this?
-   What processes can you follow to generate acceptable data?
-   Is randomisation sufficient?
-   What about obfuscation?
-   When is production-like data acceptable \(or not\) for testing purposes?
-   How do you ensure that production-like data is sufficient for testing purposes?
-   What are the expectations regarding suppliers - for code, and for services?

Examples of data that must be anonymised:

-   personal data revealing racial or ethnic origin
-   personal data revealing political opinions
-   personal data revealing religious or philosophical beliefs
-   personal data revealing trade union membership
-   genetic data
-   biometric data \(where it can be used for identification purposes\)
-   data concerning health
-   data concerning a person's sex life
-   data concerning a person's sexual orientatio
-   data concerning criminal offences
-   email addresses
-   bank details
-   telephone numbers
-   postal or residential addresses

This list is not exhaustive.

Recommendations for anonymising data:

-   Replace with synthetic data.
-   Suppress \(remove\) or obfuscate.
-   A useful link for anonymising telephone numbers is [here](https://www.ofcom.org.uk/phones-telecoms-and-internet/information-for-industry/numbering/numbers-for-drama).

## Data Privacy considerations

There are sometimes valid reasons when you do need to use live data for test purposes but they are normally the exception rather than the norm and typically looked at on a case by case basis where appropriate risk management calls can be taken.

Looking at datasets being pulled out of databases are a prime example of where you may need to use live data to make sure that a software application is functioning correctly. For some things it is not always possible to use synthetic data.

Where a project is considering the use of live data for test purposes, it is essential to understand the data first, to be clear about what GDPR related factors apply.

You might need to look at fair processing notices and take these into account around the context of the tests being performed.

**Note:** It may actually be illegal to perform planned tests if fair processing notices do not allow using the data for test purposes.

Where the data involves personal information, help must be obtained from the MOJ Data Privacy team.

If there is no option to use live data some of the things that should be considered will include the following:

-   How will the data be extracted or obtained, and who will perform or oversee the extraction? What clearance do they have?
-   What controls are in place to extract the data?
-   Where is the data going to be extracted to? In other words, what media or mechanism will be used? For example, is the data extracted using electronic means such as SFTP, or is the data extracted to removable media, or does it remain 'in situ'?
-   How is this data going to be protected at rest and during transit?
-   What systems will the data be copied to, and in what environments?
-   What systems will the data be processed by?
-   How will access to this information be controlled both at rest and during transit for all systems that are involved in processing it?
-   What access controls are in place end to end?
-   Once testing is complete how will the data be removed/destroyed? What assurances do you have over this?

If live data is being used for test purposes within the Production environment, then backups are key and the testing to make sure that backups can be quickly restored is a must. There needs to be a good rollback plan in place. There also has to be an appetite for risk acceptance.

### GDPR

There are 6 lawful grounds for processing personal data:

1.  the data subject has given consent to the processing of his or her personal data for one or more specific purposes
2.  processing is necessary for the performance of a contract to which the data subject is party or in order to take steps at the request of the data subject prior to entering into a contract
3.  processing is necessary for compliance with a legal obligation to which the controller is subject
4.  processing is necessary in order to protect the vital interests of the data subject or of another natural person
5.  processing is necessary for the performance of a task carried out in the public interest or in the exercise of official authority vested in the controller
6.  processing is necessary for the purposes of the legitimate interests pursued by the controller or by a third party, except where such interests are overridden by the interests or fundamental rights and freedoms of the data subject which require protection of personal data, in particular where the data subject is a child

### Ensuring test data is GDPR compliant

-   Well-defined documentation of personal data information in all test environments
-   Effective data discovery to understand and unearth sensitive data information
-   Implementing the test data management process for the entire data life cycle that includes profiling, sub setting, masking, provisioning and archiving data in test environments
-   Ensuring an irreversible “on-the-fly” data masking process on production data to a centralized repository
-   Permission and alerts in place for data exports and access outside the region, as this is restricted
-   Prevent access to personal data from unauthorized access points

## If testing is to go ahead

### Developer access

In a normal working environment, developers working on an application, platform or service would be segregated away from access to live/production data. They would never be able to see or manipulate this data. The use of live data for test purposes would potentially negate these controls.

Also, developer roles are often specified as not requiring SC clearance of above. This applies also to external \(3rd party\) software suppliers generating bespoke applications or services. The assumption is that the developers do not ever have access to live data.

The use of live data for testing may mean that the clearance levels for developers on a given project would need review.

### Preparing for tests

Any code or tests involving live data should ensure the following:

-   Code performs input validation.
-   Output is correctly encoded.
-   Full authentication and authorisation is in place.
-   Session management is in place to ensure that code and data is not continually available outside the testing activities.
-   Strong cryptography is used to protect data 'at rest', 'in transit' and 'in use'.
-   All errors and warnings generated by applications, services, or recorded in logs are monitored, captured and actioned.
-   A Data Protection Impact Assessment has been performed.
-   Any backup processes will correctly filter out or otherwise protect the live data within the test environment.
