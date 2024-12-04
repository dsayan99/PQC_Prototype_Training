# Task 1 - Getting Familiar with LIBOQS to evaluate PQC ALgorithms

This task will help in getting familiarised with liboqs starting from building liboqs from source.

For simplicity, the Dockerfile has been made available that will build liboqs in a docker container.

1. `docker build -t liboqs .` This will build liboqs within the container.
2. `docker run -it liboqs`, this will run the docker container and then open a terminal within the container in the `liboqs` directory.
3. In the terminal, navigate to `/build/tests`.

There are also a variety of programs built under the `tests` directory:

	- `test_kem`: Simple test harness for key encapsulation mechanisms
	- `test_sig`: Simple test harness for signature schemes
	- `test_sig_stfl`: Simple test harness for stateful signature schemes
	- `test_kem_mem`: Simple test harness for checking memory consumption of key encapsulation mechanisms
	- `test_sig_mem`: Simple test harness for checking memory consumption of signature schemes
	- `kat_kem`: Program that generates known answer test (KAT) values for key encapsulation mechanisms using the same procedure as the NIST submission requirements, for checking against submitted KAT values using `tests/test_kat.py`
	- `kat_sig`: Program that generates known answer test (KAT) values for signature schemes using the same procedure as the NIST submission requirements, for checking against submitted KAT values using `tests/test_kat.py`
	- `kat_sig_stfl`: Program for checking results against submitted KAT values using `tests/test_kat.py`
	- `speed_kem`: Benchmarking program for key encapsulation mechanisms; see `./speed_kem --help` for usage instructions
	- `speed_sig`: Benchmarking program for signature mechanisms; see `./speed_sig --help` for usage instructions
	- `speed_sig_stfl`: Benchmarking program for stateful signature mechanisms; see `./speed_sig_stfl --help` for usage instructions
	- `example_kem`: Minimal runnable example showing the usage of the KEM API
	- `example_sig`: Minimal runnable example showing the usage of the signature API
	- `example_sig_stfl`: Minimal runnable example showing the usage of the stateful signature API
	- `test_aes`, `test_sha3`: Simple test harnesses for crypto sub-components
	- `test_portability`: Simple test harnesses for checking cross-CPU code portability; requires presence of `qemu`; proper operation validated only on Ubuntu

	The complete test suite can be run using

		ninja run_tests

4. Any of the above tests can be run using `./{file name}`, e.g. `./speed_kem`.

```bash
./speed_kem <options> <alg>
```
### Options

| Option             | Description                                                                   |
|---------------------|-------------------------------------------------------------------------------|
| `--algs`           | Print the list of supported algorithms and terminate.                        |
| `--duration n` / `-d n` | Run each speed test for approximately `n` seconds (default: `3`).             |
| `--help` / `-h`    | Display usage instructions and terminate.                                    |
| `--info` / `-i`    | Print information (e.g., sizes, security levels) about each supported KEM.   |
| `--fullcycle` / `-f` | Perform the full key generation, encapsulation, and decapsulation cycle.      |

### Algorithm (`<alg>`)

Specify one of the supported algorithms listed below to run the test for that specific KEM.

KEM Algorithms

    BIKE-L1
    BIKE-L3
    BIKE-L5
    Classic-McEliece-348864
    Classic-McEliece-348864f
    Classic-McEliece-460896
    Classic-McEliece-460896f
    Classic-McEliece-6688128
    Classic-McEliece-6688128f
    Classic-McEliece-6960119
    Classic-McEliece-6960119f
    Classic-McEliece-8192128
    Classic-McEliece-8192128f
    HQC-128
    HQC-192
    HQC-256
    Kyber512
    Kyber768
    Kyber1024
    ML-KEM-512
    ML-KEM-768
    ML-KEM-1024
    sntrup761
    FrodoKEM-640-AES
    FrodoKEM-640-SHAKE
    FrodoKEM-976-AES
    FrodoKEM-976-SHAKE
    FrodoKEM-1344-AES
    FrodoKEM-1344-SHAKE

Signature Algorithms

    Dilithium2
    Dilithium3
    Dilithium5
    ML-DSA-44
    ML-DSA-65
    ML-DSA-87
    Falcon-512
    Falcon-1024
    Falcon-padded-512
    Falcon-padded-1024
    SPHINCS+-SHA2-128f-simple
    SPHINCS+-SHA2-128s-simple
    SPHINCS+-SHA2-192f-simple
    SPHINCS+-SHA2-192s-simple
    SPHINCS+-SHA2-256f-simple
    SPHINCS+-SHA2-256s-simple
    SPHINCS+-SHAKE-128f-simple
    SPHINCS+-SHAKE-128s-simple
    SPHINCS+-SHAKE-192f-simple
    SPHINCS+-SHAKE-192s-simple
    SPHINCS+-SHAKE-256f-simple
    SPHINCS+-SHAKE-256s-simple
    MAYO-1
    MAYO-2
    MAYO-3
    MAYO-5
    cross-rsdp-128-balanced
    cross-rsdp-128-fast
    cross-rsdp-128-small
    cross-rsdp-192-balanced
    cross-rsdp-192-fast
    cross-rsdp-192-small
    cross-rsdp-256-balanced
    cross-rsdp-256-fast
    cross-rsdp-256-small
    cross-rsdpg-128-balanced
    cross-rsdpg-128-fast
    cross-rsdpg-128-small
    cross-rsdpg-192-balanced
    cross-rsdpg-192-fast
    cross-rsdpg-192-small
    cross-rsdpg-256-balanced
    cross-rsdpg-256-fast
    cross-rsdpg-256-small

To test out the performance of classical algorithms, one can run the tests using openssl.

    openssl speed rsa
    openssl speed ecdsa
    openssl speed ecdh
    openssl speed ffdh
    openssl speed dsa