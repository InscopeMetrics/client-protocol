Inscope Metrics Build Resources
===============================

0.11.4 - May 15, 2020
------------------------
* Added `request_millis_since_epoch` request field for tracking data freshness starting at the client.

0.11.3 - May 3, 2020
------------------------
* Updated Protoco Buffer dependency to `3.10.0`.

0.11.2 - April 30, 2020
------------------------
* Converted bucket count from int32 to uint64 (backwards compatible).
* Adhered to protocol buffer field naming conventions (wire compatible).

0.11.1 - August 22, 2019
------------------------
* Refactoring of version 3 protocol (**not backwards compatible!**).

0.11.0 - August 12, 2019
------------------------
* Migrated to `io.inscopemetrics` for group id and generate code package path.
* Released protocol version 3 with support for pre-aggregated statisics through augmented-histograms.

0.10.1 - January 14, 2019
------------------------
* Updated dependencies; among them to Protocol Buffers 3.6.1.

0.10.0 - September 6, 2017
------------------------
* Released protocol version 2 with scoped enumerations.

0.9.3 - October 9, 2016
------------------------
* Support `UNIT` unit scale (e.g. 1x).

0.9.2 - September 28, 2016
------------------------
* Separate `millisSinceEpoch` into `endMillisSinceEpoch` and `startMillisSinceEpoch`.

0.9.1 - August 24, 2016
------------------------
* Changed generated package path to `com.inscopemetrics.client.protocol`.

0.9.0 - August 21, 2016
------------------------
* Initial release to `com.inscopemetrics.client.protocol`.
