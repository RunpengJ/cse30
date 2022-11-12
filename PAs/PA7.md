pitfalls
- not doing null pointer checks for parameters -> segfault
- not initialzing all members of a struct after allocting it-> segfault
- not setting pointer to null after dereferencing a variable-> segfault
- where to add new node to linked list in insertticket() ->

![PA6](images/PA6-1.png)
```
struct vehicle {
    char *state;            /* state on license plate */
    char *plate;            /* id on license plate the plate number */
    unsigned int tot_fine;  /* summary field; all tickets */
    unsigned int cnt_ticket;/* number of tickets unpaid */
    struct vehicle *next;   /* pointer to next vehicle on hash chain add vehicles at front */
    struct ticket *head;    /* pointer to the vehicles first ticket; add tickets to end */
};

struct ticket {
    unsigned long long summons;   /* summons or ticket id */
    time_t date;                  /* date summons was issued */
    unsigned int code;            /* fine code 1-99 */
    struct ticket *next;          /* pointer to next ticket */
};
```

```
insertticket(string summons, string plate, string state, string date, int summons code number)
```
- call vehiclelookup to find if the vehicle already exist
- if not found, a struct vehicle is malloc (can't use calloc). 
  - use strdup() to allocate space for state and plate; 
  - insert the vehicle in front of the hash chain
- the new struct ticket is inserted at the end of the linked list for tickets
- when traversing the ticket list, check if there is a duplicate ticket
- each time add a summons, update tot-fine using finetab, (fineTab[code])
- update cnt_ticket


```
delticket(string plate, string state, string summons)
```
- use vehiclelookup(plate, state) (faster than sumlookup, which is a full table scan)
- if not found return -1
- convert summons using strtosumid
- search down the ticket lists by comparing the member number, return -1 if not found
- if found, delete the ticket/summons by freeing the heap memory used by the struct ticket node
- update tot_fine and cnt_ticket in the struct vehicle node
  - if tot_fine and cnt_ticket goes to zero, free vehicle
