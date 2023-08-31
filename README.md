# Layout trait example

This repo showcases a simple use case for the layout trait.

## Installing the toolchain
Before we compile and flash the example, we need to install a toolchain. Thankfully, the Rust toolchain gives us Cargo, and excellent way to manage our toolchain and dependencies.
To install the Rust toolchain on your target OS, follow the instructions [here](https://www.rust-lang.org/tools/install). 

On UNIX operating systems, this amounts to running

```curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh```

in a terminal window, and following the on-screen instructions.


To compile for a RISC-V IMAC target, we must also add it to our toolchain. Simply run

``rustup target add riscv32imac-unknown-none-elf``  

in a terminal window.

Next, we use the ``probe-rs`` utility to allow us to easily flash our target, and conveniently provide us with debugging capabilities including printing.

Probe-rs can be installed by following the instructions [here](https://probe.rs/docs/getting-started/installation/). 

For Arch users, there exists a work in progress ``probe-rs`` Arch package [here](https://github.com/hannobraun/probe-rs-arch/tree/main), which is a decent starting point.


## Running the example
With the toolchain set up, all that remains is running

```cargo embed --example pmp_resource --release```

in the root of this directory. The command will compile the pmp_resource example, flash the binary to your ESP32-C3 and open a debug print window.

NOTE: The GPIO pin used to toggle the LED assumes a ESP32-C3-DevKit-RUST-1 . For other development boards, the LED pin might not match up.

To trigger a PMP fault caused by unallowed peripheral access, simply try accessing a non-GPIO peripheral from the ``blinky`` function in the example e.g. by uncommenting the last line.
