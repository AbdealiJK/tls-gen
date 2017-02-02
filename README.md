## TLS/SSL Certificate Generator

These certificates are self-signed and supposed to be used for development.

The project is extracted from a number of RabbitMQ test suites.


## What It Does

`tls-gen` generates a self-signed Certificate Authority (CA) certificate
and 2 pairs of keys: client and server, with a single command.
It can also generate a chain of CA certificates.

Use these certificates in development and QA environments. They are self-signed and not intended to be used
in production.

## Usage

Certificate authorities (CAs) and certificates can form chains. tls-gen provides
different "profiles", for example:

 * A root CA with leaf certificate/key pairs signed by it
 * A root CA with multiple shared intermediary certificates and leaf pairs signed by the intermediaries

Each profile has a sub-directory in repository root. All profiles use
the same `make` targets and directory layouts that are as close as possible.

### Basic Profile

To generate a CA, client and server private key/certificate pairs, run
`make` from the [basic](./basic) profile directory with `PASSWORD` environment variable
providing the passphrase:

    cd [path to tls-gen repository]/basic
    # pass a password using the PASSWORD env variable
    PASSWORD=bunnies make
    # results will be under the ./result directory
    ls -lha ./result

Generated CA certificate as well as client and server certificate and private keys will be
under the `result` directory.

### Verification

You can verify the generated client and server certificates against the generated CA one with

    make verify

### Overriding CN (Common Name)

By default, certificate's CN ([Common Name](http://tldp.org/HOWTO/Apache-WebDAV-LDAP-HOWTO/glossary.html)) is calculated using `hostname`.

It is possible to override CN with an environment variable:

    CN=secure.mydomain.local PASSWORD=bunnies make

### Chained Certificates Profile 1

To generate a root CA, 2 intermediate CAs, client and server key/certificate pairs, run `make` from
the [two_shared_intermediates](./two_shared_intermediates) directory the same way:

    PASSWORD=bunnies make
    # results will be under the ./result directory
    ls -lha ./result


## License

Mozilla Public License, see `LICENSE`.
