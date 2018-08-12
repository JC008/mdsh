# Examples From README.md

This file verifies that the markdown examples in the README work as advertised.  First we extract the `~~~markdown` blocks and remove their escaping:

    $ printf -v zws $'\xe2\x80\x8b'  # Remove the zero-width-space escapes
    $ sed -ne '/^~~~markdown$/,/^~~~$/ {s/'$zws'//; /^~~~/d; p; }' $TESTDIR/../README.md >demo.md

And then we run the result with mdsh:

    $ "$BASHER_INSTALL_BIN/mdsh" demo.md
    hello world!
    { "hello": "world" }
    
    { "hello": "world" }
    
    { "this is": "great" }
    
    // hey
    
    # line 49, json block:
    def example: {"foo": "bar"}
    ;
    The html is: <html />
    
    hello, world from a python block
    Most tools will highlight this block as shell script

(Notice that the output for each data block includes the line feed that terminated it.)

Also, one of the examples creates a file:

    $ cat file1.txt
    Some text goes here!
