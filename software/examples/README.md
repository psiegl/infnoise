# Usage examples for Infinite Noise

## Integrate the binary to python

See the python examples `serial-numbers.py` and `randomserver.py` to see how you could integrate it with python.

#### serial-numbers.py
An extended version of this script was used to generate the serial numbers of all Infinite Noise's made by 13-37.org. The numbers generated by this simpler one are not guaranteed to be unique, thats why I use the UNIQUE constraint of a database when storing them.

This simple version just prints the serials to stdout. Call like this:

    $ ./serial-numbers.py -c 3 -l 8
    0A8BBA15
    0341F762
    813DC0BD

#### randomserver.py

A simple webserver based on the web.py framework to serve random data via a REST interface. 
An improved version is hosted on [rng.13-37.org](https://rng.13-37.org).

## libinfnoise

Under libinfnoise/examples you'll find two examples on how to integrate libinfnoise, which consist of the following functions:

    // returns a struct of infnoise_devlist_node listing all connected FTDI FT240 devices by their USB descriptors
    devlist_node listUSBDevices(char **message);

    // initialize the Infinite Noise TRNG - must be called once before readData() works
    bool initInfnoise(struct infnoise_context *context, char *serial, bool keccak, bool debug);

    // Reads some bytes from the TRNG and stores them in the "result" byte array.
    // The array has to be of sufficient size. Please refer to the example programs. 
    // (64 byte for normal operation or 128byte for multiplier mode)
    uint32_t readData(struct infnoise_context *context, uint8_t *result, bool raw, uint32_t outputMultiplier);

The infnoise_context struct is also part of the interface. See [libinfnoise.h](../libinfnoise.h) for it's definition and the interface documentation.
