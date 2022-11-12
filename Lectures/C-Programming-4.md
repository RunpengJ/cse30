## Hashing

Hash table: an array of pointers to the head of different linked lists (called hash chains)

Each data item must have a unique key that identifies it (e.g., license plate)
- h(k): the hash value of key k to encode the key k into an integer

Use the hash value to map to one entry in the ahsh table T[] of size TABLESZ
- index = h(k) % TABLESZ

After hashing a key, you then traverse the selected linked list to find the entry