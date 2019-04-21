CORE FUNCTIONS
- BEGIN: Defines the start of a function.
- CALL: Used to run an operation within the same module.
- COMMENT BEGIN: Defines the start of a comment.
- COMMENT END: Defines the end of a comment.
- COMPUTE: Calculates a number when an operator is given.
- CREATE: Creates an object.
- DEFINE: Creates a reference to an object with no data.
- END: Defines the end of a function.
- GETDATA: Retrieves information from an input.
- IGNORE: Terminates a running function.
- INCREMENT: Cycles through objects in a space.
- INVERT: Inverts a signal by changing it's BIN value.
- OP: Creates an operations.
- OUT: Outputs an object.
- LOCATION: Reads the location of an object in space.
- MAXNUM(<!REGWITDH>): Defines the maximum number a computer can compute, takes into account the register width.
- MINNUM: Defines the minimum number a computer can compute. Can also be done with INVERT(MAXNUM).
- MOVE: Moves an object to a data stream.
- SET: Assigns a value to an object.
- WHEREIS: Returns the memory address for the object.

FLAGS
- &&: Adds an argument to a comparison.
- ?: Performs a comparison.
- <: Less than.
- >: Greater than.
- **Single line comments**
- <!--Multi-line comments-->

POINTERS
- >>: Express the object (likely of type NUM) as memory address.
- >{OBJECT}: Defines the memory address of the referenced object.
