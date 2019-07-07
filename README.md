## HIBPBloomFilter

This is a [Bloom filter](https://en.wikipedia.org/wiki/Bloom_filter) for the [HIBP Offline Check](https://github.com/mihaifm/HIBPOfflineCheck) KeePass plugin.

This repository contains only the filter in binary format, the source code for generating it can be found in the [HIBPOfflineCheck](https://github.com/mihaifm/HIBPOfflineCheck) repository.
You can generate the filter from the plugin options in under one hour. On a modern system with a SSD this time can be reduced to under 15 minutes.

For convenience however, you can download the filter directly from this repository's releases.

### Bloom Filter characteristics

**Size**: 952 MB    
**False positive rate**: approx. 0.1%    
**Capacity**: 551509767 items (hashed passwords)    
**Hashing algorithm**: [MurMurHash3](http://blog.teamleadnet.com/2012/08/murmurhash3-ultra-fast-hash-algorithm.html)

### Binary file format

|Offset (bytes)|Length (bytes)|Name|Type|Description|
|---|---|---|---|---|
|0|8|Capacity|long|The number of items in the filter|
|8|4|ErrorRate|float|Theoretical false positive rate|
|12|8|BitCount|ulong|Number of bits in the filter|
|20|4|NumHashFuncs|int|Number of hash functions. Actually the same hash function is used multiple times with different seeds|
|24|4|Algorithm|int|Not used at the moment. Reserved for future use, in case the hashing algorithm changes|
|28||Bloom filter||Bloom filter data divided into arrays of 64 * 1024 * 1024 bytes|
