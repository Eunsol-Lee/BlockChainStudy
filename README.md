# Blockchain Study

# Coursera cryptocurrency lecture
## Week1
### Cryptographic hash functions
- Hash function
  - takes any string as input
  - fixed-size output
    - bitcoin: 256 bits
  - efficiently computable
- Security properties
  - Collision-free
    - nobody can find x != y and H(x) = H(y)
    - collisions exist, but nearly impossible to find
    - Application: Hash as message digest
      - H(x) = H(y) --> x = y
      - file --> hash --> remember
  - Hiding
    - Given H(x) --> infeasible to find x
    - r <-- chosen from a probability distribution that has high min-entropy
    - H(r | x) --> infieasible to find x
    - Application: Commitment
      - commit to a value, reveal it later
      - Commitment API
        - (com, key) := commit(msg)
        - match := verify(com, key, msg)
        - To seal msg in envelope:
          - (com, key) := commit(msg)
          - then publish com
        - To open envelope:
          - publish key, msg
          - anyone can use verify() to check validity
        - Two security properties
          - Hiding: given com, infeasible to find msg
          - Binding: Infeasible to find msg != msg' such that verify(commit(msg), msg') == true
        - commit(msg) := (H(key|msg), key)
          - key is a random 256-bit value
        - verify(com, key, msg) := ( H(key|msg) == com )
        - Security properties
          - Hiding: Given H(key|msg), infieasbile to find msg != msg' such that H(key|msg) == H(key|msg')
  - Puzzle-friendly
    - infeasible to find x such that H(k|x)=y
      - k is chosen from a distribution with high min-entropy
    - Applicatoin: Search puzzle
      - given id(puzzle ID, from high min-entropy distrib.), target set Y
      - try to find H(id|x) in Y
      - property: no solving strategy better than tyring random values of x
  - SHA-256 hash function
    - 512 bits block: (message+padding)/512
    - IV(256 bits) + block1 --> c + block2 --> ... --> c --> Hash
          
