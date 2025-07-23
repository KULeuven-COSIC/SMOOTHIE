## SMOOTHIE: (Multi-)Scalar Multiplication Optimizations On TFHE

## Setup code
- Clone the tfhe-rs library: `git clone https://github.com/zama-ai/tfhe-rs.git ; cd tfhe-rs`
- Switch to the correct version (V0.11.0): `git checkout 37934e42c11b634d8156ecd2faceab5ee33fceb3`
- Copy patch file and apply patch to the repo: `git apply ../smoothie.patch`

## Source code
Single-Scalar Multiplication Code: tfhe/src/integer/server_key/radix_parallel/scalar_mul.rs <br />
Multi-Scalar Multiplication Code: tfhe/src/integer/server_key/radix_parallel/vector_mul.rs

## Test Correctness

Single-Scalar Mult: Run `make test_scalar_mul` <br />
The block size of input can be set by changing: `pub(crate) const NB_CTXT: usize = 32;` in tfhe/src/integer/server_key/radix_parallel/tests_cases_unsigned.rs <br />
The window size can be changed in tfhe/src/integer/server_key/radix_parallel/scalar_mul.rs - `scalar_mul_assign_parallelized_optimized`

Multi-Scalar Mult: Run `make test_vector_mul` <br />
Block size, vector size and windowsize can be changed in tfhe/src/integer/server_key/radix_parallel/tests_cases_unsigned.rs - `default_vector_mul_test`

## Run Benchmarks

Run `make bench_integer` <br />
Change function to be run in tfhe/benches/integer/bench.rs - `default_scalar_parallelized_ops` <br />
Change bit sizes to be benchmarked in tfhe/benches/utilities.rs - `const BENCH_BIT_SIZES` <br />
Change benchmarked vector size, window size and bucket doubling in tfhe/benches/integer/bench.rs - `bench_server_key_binary_vector_function_clean_inputs_optimized`
