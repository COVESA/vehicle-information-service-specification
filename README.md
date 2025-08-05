![Status - Active](https://img.shields.io/static/v1?label=Status&message=Active&color=3FFF3A&style=for-the-badge)

# vehicle-information-service-specification

[![License](https://img.shields.io/badge/License-MPL%202.0-blue.svg)](https://opensource.org/licenses/MPL-2.0)

### Maintainers

Ulf Björkengren - Ford Motor Company

Ted Guild - Geotab Inc.

Peter Winzell - Volvo Cars

Wonsuk Lee - 한국전자통신연구원(ETRI)
 
### Lead editors

Ulf Björkengren - Ford Motor Company
 
### Working group meetings
The VISS working group meets every other Monday at 16.00 CET.
The schedule and link to meeting can be found [here](https://wiki.covesa.global/display/WIK4/COVESA+Common+Meeting+Schedule).<br>
Minutes of meetings is found [here](https://wiki.covesa.global/display/WIK4/VISS+Meeting+Topics+and+Meeting+Notes).

## Overview

>Vehicle Information Service Specification (VISS) is an API for accessing the COVESA Vehicle Signal Specification (VSS) data. The work started at [The World Wide Web Consortium (W3C)](https://www.w3.org) in collaboration with GENIVI and its successor COVESA. The W3C Automotive Working Group closed in February of 2024 and the work is continuing at COVESA.

To see the most recent HTML rendered version of the specifications from this repository can be found at the following:

- [COVESA VISS version 3.1 - Core](https://raw.githack.com/COVESA/vehicle-information-service-specification/v3.1/spec/VISSv3.1_Core.html)
- [COVESA VISS version 3.1-Payload Encoding](https://raw.githack.com/COVESA/vehicle-information-service-specification/v3.1/spec/VISSv3.1_PayloadEncoding.html)
- [COVESA VISS version 3.1-Transport](https://raw.githack.com/COVESA/vehicle-information-service-specification/v3.1/spec/VISSv3.1_Transport.html)

The [VISS explainer](./VISS-explainer.md) gives some background and rationale to this interface.

## Latest version
[VISS version 3.0](https://github.com/COVESA/vehicle-information-service-specification/releases/tag/v3.0)

## Previous versions
[VISS version 2.0](https://github.com/COVESA/vehicle-information-service-specification/releases/tag/v2.0)
[VISS version 1](https://www.w3.org/TR/vehicle-information-service/)

## Reference Implementation
[http://github.com/COVESA/vissr](http://github.com/COVESA/vissr)

## Specification references
The Adaptive AUTOSAR R24-11 official publication.

[AUTOSAR](https://www.autosar.org/) released the [Adaptive AUTOSAR R24-11](https://www.autosar.org/search?tx_solr%5Bfilter%5D%5B1%5D=platform%3AAP&tx_solr%5Bfilter%5D%5B2%5D=category%3AR24-11&tx_solr%5Bq%5D=) including Automotive API Gateway specification at the end of December 2024. Automotive API Gateway specification is developed based on the [COVESA VISS v2-Core](https://github.com/COVESA/vehicle-information-service-specification/releases/tag/v2.0) and [COVESA VISS v2-Transport](https://github.com/COVESA/vehicle-information-service-specification/releases/tag/v2.0) specifications. The related standards and technical documents are as follows:
- [Explanation of Automotive API](https://www.autosar.org/fileadmin/standards/R24-11/AP/AUTOSAR_AP_EXP_AutomotiveAPI.pdf)
- [Requirements on Automotive API Gateway](https://www.autosar.org/fileadmin/standards/R24-11/AP/AUTOSAR_AP_RS_AutomotiveAPIGateway.pdf)
- [Specification of Automotive API Gateway](https://www.autosar.org/fileadmin/standards/R24-11/AP/AUTOSAR_AP_SWS_AutomotiveAPIGateway.pdf)
- [Technical Report on VSS Representation](https://www.autosar.org/fileadmin/standards/R24-11/AP/AUTOSAR_AP_TR_VSSRepresentation.pdf)
- [Adaptive Platform Release Overview](https://www.autosar.org/fileadmin/standards/R24-11/AP/AUTOSAR_AP_TR_ReleaseOverview.pdf)

## Tools

- [ReSpec](https://www.w3.org/respec/) has been used to style the specifications allowing the editors to focus on functionality and ensure consistency and referential integrity
- The [API Design Cookbook](http://www.w3.org/TR/api-design/) has been used as a guide for the use of WebIDL

## Style Guidelines

### JavaScript Style Guidelines
JavaScript should be written using the [JSCS](http://jscs.info/) rule set defined by [Echidna](https://github.com/w3c/echidna/blob/master/.jscs.json).

## Contributors
VISS is an open standard and we invite anybody to contribute. Currently VISS contains - among others - significant  contributions from

 - [Volvo Cars](https://www.volvocars.com/)
 - [Geotab Inc](https://www.geotab.com/about/)
 - [Ford Motor Company](https://www.ford.com/)
 - [한국전자통신연구원(ETRI)](https://etri.re.kr/eng/main/main.etri)
 - [Mitsubishi Electric](https://www.mitsubishielectric.com/en/)
 - [Jaguar Land Rover](https://www.jaguarlandrover.com/)
