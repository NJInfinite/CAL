<!--
BITMATH takes into account the register width of the system. It is then able
to perform caculations (dependant on the operator) up to MAXNUM.

Firstly, we must consider the fact that not all computers are made equal. In
particular, whilst most consumer-grade computers are 64-bit, there are some
that have a greater or lesser register width. Therefore, we must define what
the maximum number is that a computer can work with.

We then set INPUTS to a number, this represents the amount of numbers that are
going to be used in the caculation.

Two comparisons are made before moving on, firstly, we check that the sum of
the operated numbers is less than MAXNUM. We also check that there is a bus
available for that particular number, we do this by expressing the operated
number as a memory address.

If it's true, we set RESULT to the operated inputs, we assign bus object
X the memory address of RESULT, we set DATA_LOCATION to X, finally, we move
RESULT to the DATA_LOCATION (note, we use the >> pointer to express RESULT
as a memory address.) and then we output the number.

If it's false, we create and output an error message, reset the objects, and
terminate the operation.
-->

CREATE OPERATOR AS OB (REP(<!OPERATOR>))
CREATE X AS OB (REP(<!BUS>))
CREATE RESULT AS OB (<NUM>)
CREATE REG_WIDTH AS OB (REP(<!REGWIDTH>))

DEFINE DATA_LOCATION
DEFINE BIGNUM
DEFINE INPUTS
DEFINE ERROR_MESSAGE

OP "BITMATH" [OPERATOR, REGWIDTH, RESULT]
  BEGIN
    SET BIGNUM TO MAXNUM(REG_WIDTH)
    SET INPUTS TO <NUM>

    **Checks if sum is less than BIGNUM, and checks if there is a memory address at sum.**
    ? OPERATOR(GETDATA(INCREMEMENT(INPUTS))) < BIGNUM && ? LOCATION((WHEREIS(OPERATOR(RESULT)))) IS BIN_1
      TRUE
        SET RESULT TO OPERATOR(GETDATA(INCREMENT(INPUTS)))

        SET X TO WHEREIS(RESULT)
        SET DATA_LOCATION TO X
        **Send RESULT to the memory address at DATA_LOCATION.**
        MOVE >> RESULT TO DATA_LOCATION

        OUT(RESULT)
      FALSE
        SET ERROR_MESSAGE TO "THE REGISTER FOR THAT NUMBER DOES NOT EXIST. RESULT MAY HAVE EXCEEDED MAXNUM."
        OUT(ERROR_MESSAGE)

        SET INPUTS TO <!NULL>
        SET DATA_LOCATION TO <!NULL>
        SET RESULT TO BIN_0

        IGNORE
  END
