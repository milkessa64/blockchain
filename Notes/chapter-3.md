
Chapter 3

Arrays

   - arrays are our first refernce type.
   - arrays are quite differently in storage us memory/calldata.
   - arrays aren't used as frequently as mappings
          .useful for ordered data or when you need iteration.
          .unlimited size plus iteration can be DOS vector.


  Reference Types

    -Reference Types: string, bytes, arrays, mappings, and structs.
    - as an argument you must declare the memory location: calldata, memory or storage.
    - potentially passed by reference, as opposed to value types.


Structs
   
  -group Variables under a single name.
  -can be stored in the different data collection.
  -can go within other structs/arrays/mappings.

example:

     struct User {
          
           bool isActive;
           uint balance;
      }

      User user = User(true,0);


mappings

    -key/value hash lookup.
    -storage only.
    -can not be passed as an argument.
