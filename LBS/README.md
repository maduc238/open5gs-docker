# Tài liệu cần quan tâm:

- Location Base Service https://www.queryhome.com/tech/42618/location-based-services-lcs-architecture-for-lte-eps
- Source code JDiameter: https://jar-download.com/artifacts/org.mobicents.diameter/jdiameter-api/1.7.0.75/source-code
**Mục đích: Tạo GMLC**

## GMLC

The Gateway Mobile Location Center (GMLC) is the first node an external LCS client accesses in a Mobile Network. The GMLC may request routing information from the HSS. It supports routing of positioning requests and responses. The GMLC also performs authorization and checks the subscriber’s privacy profile.
- The “Requesting GMLC” is the GMLC, which receives the request from the LCS client.
- The “Visited GMLC” is the GMLC, which is associated with the serving node of the target mobile.
- The “Home GMLC” is the GMLC residing in the target mobile’s home PLMN, which is responsible for the control of privacy checking of the target mobile.
