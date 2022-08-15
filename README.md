# Sauce Helper (SHelper)

[![crates.io](https://img.shields.io/crates/v/shelper.svg)](https://crates.io/crates/shelper)
[![Documentation](https://docs.rs/shelper/badge.svg)](https://docs.rs/shelper)

CLI wrapper and library for the Sauce Labs public API.  Obtain Job details for specific jobs, builds.  At the time of this writing a Job is: Virtual Desktop, iOS Simulator, or Android Emulator session. Real Device jobs coming in 2020.

## Installation
`cargo install shelper`

This is the easiest installation method but you will need `cargo` installed. 

#### Installing Cargo
[Cargo](https://doc.rust-lang.org/cargo/getting-started/installation.html) installs the binary from [crates.io](https://crates.io/crates/shelper).  To install cargo, [copy-paste](https://orly-appstore.herokuapp.com/generate?title=Blindly%20copy-pasting%20shell%20scripts&top_text=what%20could%20go%20wrong%3F&author=sudo%20!!&image_code=16&theme=2&guide_text=The%20Whoops%20Edition&guide_text_placement=bottom_right):

```curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh```

Accept the prompts and choose the Defaults.

Read more here: https://www.rust-lang.org/tools/install

#### Install w/ Cargo

```cargo install shelper```

#### Compile from Source
To install and compile from source (or to develop):
1. Git clone
2. `cargo build --release`
3. Find the .exe in `./target/release/shelper`

## Usage
`shelper -h` or `shelper --help`

#### Examples
`shelper --job <session-id> --job <session-id>` 

`shelper -j <session-id> <session-id> <session-id>`

`shelper -j https://app.saucelabs.com/tests/<session-id>`

If you want info about a tunnel you would run
`shelper -t <tunnel-id> -o <owner-of-the-tunnel>`

If you owned the tunnel and have your Sauce credentials saved as environment variables you could omit the -o and -k
flags.

```
    -k, --key <key>                       Sauce Access Key
    -j, --jobinfo <one or more job>...    Get job details.  Takes a URL link to a session or a Job ID string
    -o, --owner <sauce_username>          Sauce account that owns a sauce resource (tunnel, job, asset)
    -r, --region <region>                 Region/datacenter to search. [possible values: EU, US]
    -t, --tunnelinfo <tunnel_id>...       Get information about a tunnel. REQUIRES:
                                          - the sauce username that created the tunnel, either in the Owner
                                          flag(-o/--owner) OR as an env. variable
                                          - the access key used to authenticate (env variable or as a flag)
                                          - the tunnel id, provided at tunnel runtime
```

## Development
`cargo doc --open`: compile and run the documentation

`cargo install`: install all the dependencies

`cargo test`: run all tests

`cargo test -- --nocapture some_test_name`: run a specific test & print all the stuff to stdout/stderr

## Testing
Unit tests are not all 100% local. Real credentials are pulled from the env. variables in some cases.  Real HTTP calls are made against the real API.  Do not run tests endlessly as you could get rate limited with a 429.
