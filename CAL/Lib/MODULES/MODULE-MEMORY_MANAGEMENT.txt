<!--
Contains operations to write, read, and clear memory.

In MEMWRITE, we set the location of the data to the stream input. This is so
we know where to write the data from. If it is activated (BIN_1), then we may
proceed, otherwise we ignore, terminating the function.
We then set the location of the data to the location of the input stream, because
it is activated, we set the value of BIT to BIN_1. We then set the Block at the
location of the data to BIT.

In MEMREAD, we check if the location of the data block is written to, we also
check if the output stream is activated (the output stream is read, not the
data block). If it's true, then we output the output stream. Otherwise, we
output an error message.

In MEMCLEAR, we increment through the data location within the constraints of
activated data blocks within the block. When the location of an activated data block
is found, we set the value of the BIT in that block to 0. We also reset the
location of the data.
-->

CREATE X AS <NUM>
CREATE Y AS <NUM>
CREATE DATA_BLOCK AS OB (<BLOCK(X,Y)>)
CREATE STREAM_IN AS OB (REP(<!BUS>))
CREATE STREAM_OUT AS OB (REP(<!BUS>))

DEFINE BIT
DEFINE DATA_LOCATION
DEFINE ERROR_MESSAGE

OP "MEMWRITE" [STREAM_IN, DATA_LOCATION, DATA_BLOCK, BIT, ERROR_MESSAGE]
  BEGIN
    CREATE DATA_LOCATION ? STREAM_IN IS BIN_1
      TRUE
        SET DATA_LOCATION TO LOCATION(STREAM_IN)
        CREATE BIT AS BIN_1
        SET DATA_BLOCK(<BLOCK(DATA_LOCATION)>) TO BIT
      FALSE
        SET ERROR_MESSAGE TO "CANNOT WRITE DATA TO NULL LOCATION."
        OUT(EROR_MESSAGE)
        IGNORE
  END

OP "MEMREAD" [DATA_BLOCK, DATA_LOCATION, STREAM_OUT, ERROR_MESSAGE]
  BEGIN
    ? DATA_BLOCK(<BLOCK(DATA_LOCATION)>) IS BIN_1 && ? LOCATION(STREAM_OUT) IS BIN_1
      TRUE
        OUT(STREAM_OUT)
      FALSE
        SET ERROR_MESSAGE TO "NO DATA COULD BE READ AT LOCATION."
        OUT(ERROR_MESSAGE)
        IGNORE
  END

OP "MEMCLEAR" [DATA_LOCATION, DATA_BLOCK, ERR0R_MESSAGE]
  BEGIN
    INCREMENT DATA_LOCATION ? BIT >{DATA_BLOCK(<BLOCK(DATA_LOCATION)>)} IS BIN_1
      TRUE
        SET >{DATA_BLOCK(<BLOCK(DATA_LOCATION)>)} TO <!NULL>
        SET DATA_LOCATION TO <!NULL>
      FALSE
        SET ERROR_MESSAGE TO "NO DATA COULD BE FOUND."
        OUT(ERROR_MESSAGE)
        IGNORE
  END
