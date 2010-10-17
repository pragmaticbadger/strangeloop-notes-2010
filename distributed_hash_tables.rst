Distributed Hash Tables
=======================

:author: Mike Malone <mike@simplegeo.com> @mjmalone


#. SimpleGeo History

  * Started as a mobile gaming geolocation thing, but tons of data & worth 
    money.
  * Matt Galligan & Joe Stump

#. Based on Cassandra
#. Requirements

  * Performance
  * Spatial
  * Reliability
  * Integrity
  * Scalability
  * Simplicity
  * Availability

#. Conflict

  * Integrity vs. Availability
  * Locality vs. Distributedness
  * Reductionism vs. Emergence

#. Candidates

  * Transactional Relational
  * Structured Stores

#. Integrity vs. Availability

  * ACID definition
  * ACID Helps by handling some hard bits
  * CAP Theorem
    
    * Can only have two out of three.
  
  * ACID sometimes encourages "bad things"
  
    * Locks
  
  * Find Balance

#. Cassandra

  * Distributed Hash Table
  * Fault Tolerance & Decentralization
  * Consistent hashing
  * Replication story
  * Data Model

#. Hash Table Supported Queries

  + Exact Match
  - Range
  - Proximity
  - Anything that's not an exact match

#. Locality vs. Distributedness

  * Order Preserving Partitioner
  
    + Exact Match
    + Range
    - ???
  
#. Dimensionality Reduction With Space-Filling Curves
#. GeoHash

  * Simple to compute
  * Awesome Characteristics

#. Spatial Data is Still Multidimensional

  * Bounding Box
  * Bad around boundaries
  * Hot spots

#. Too much locality

  * Ops nightmare because parts of the hash get overloaded.

#. Hello, Drawing Board

  * Distributed P2P Indexing
  
    * Overlay-dependent
    * Over-DHT
  
  * Another look at PostGIS
  
    * Might work but too tightly coupled.
  
#. Let's Take A Step Back

  * Earth is FLAT AND EMPTY, LIKE A RECT
  * Split in half
  * Earth, Tree, Ring

#. Splitting

  * Just a concurrent tree
  * Split size is tunable
  * Split node & add children, mark then clean up
  * All idempotent
  * Never rebalance the tree (and don't have to)

#. The Root is Hot

  * Maybe a deal breaker
  * Have to start there, traversal hurts due to constantly being read.
  
#. Back To The Books

  * Lots of academic work on the topic
  * Just need something "fast enough"

#. Reductionism vs. Emergence

  * Thinking Holistically
  * Observed that nodes rarely go away
  * State might change but localized impact
  * Just cache the nodes that have been observed

#. LRU Cache of Nodes

  * Anything that's been traversed.
  * Start traversal at the most selective relevant node
  * Return nodes traversed so those get added to the cache

#. Traversal of the Nearest Neighbor
#. Key Characteristic

  * Best case all cached
  * Worst case, nothing cached & O(log n)

#. Does everything in all dimensions
#. B-Tree & KD Tree

  * Possible to support 3D coordinates.