# FAST: Finding Specification Blind Spots via Fuzz Testing
A formally verified program can only be as correct as its specifications (<span class="smallcaps">SPEC</span>). But how to assure that <span class="smallcaps">SPEC</span> is complete and free of loopholes?

FAST(<ins>F</ins>uzzing-<ins>A</ins>ssisted <ins>S</ins>pecification <ins>T</ins>esting) is an architecture which examines <span class="smallcaps">SPEC</span> incompleteness issues in an automated way. It first locates <span class="smallcaps">SPEC</span> gaps via mutation testing, i.e., by checking whether a <span class="smallcaps">CODE</span> variant conforms to the original <span class="smallcaps">SPEC</span>. If so, FAST further leverages the test suites to infer whether the gap is introduced by intention or by mistake. Depending on the size of the codebase, FAST is applied to two open-source codebases. FAST aims to highlight the prevalence of <span class="smallcaps">SPEC</span> incompleteness in real-world applications.


## Mutation Rules

<img src="/fig/mutation_rule.png"  width=35% height=35%>

## Enumerative <span class="smallcaps">CODE</span> mutant generation

Move compiler with mutation feature integrated lives in [Move](https://github.com/watssec/move/tree/mutation_testing)

DPN smart contracts code lives in [Diem](https://github.com/diem/diem)

The smart contracts file can be found under `diem/language/diem-framework/modules`


### Usage

Basic knowledge about Rust is assumed. (Rust has been properly installed on the testing environment)

First download the mutation integrated move-cli:

```
# build Move CLI
# Under move/language/tools/move-cli
$ cargo build
# Install move binary in the Cargo binary directory
$ cargo install --path .
```

Perform mutation testing in DPN
```
# Under diem/language/diem-framework/modules
$ move package mutation
```


## AWS S2N-TLS



### Installation using Docker

Under ./docker
~~~~{.sh}
# build docker
$ make build

# go into the docker once and dicsard the container afterwards
$ make once

# run docker with script
$ make script
~~~~

The above commands start a fuzzing process.

Survived mutants can be found under `work/survival`

Seed information can be found under `work/seed`

### Enviornment Setup

Go into deps dir, make build all the dependencies. (SAW verification is quite fragile in terms of version requirement. The deps listed in this dir are most stable)

In order to match the script with in FAST on parsing the error messages returned from SAW verification, replace executable file saw in saw-nightly built from `make saw-nightly` with the one from:

[Workable saw nightly build, not available on their page anymore](https://github.com/meng-xu-cs/s2n-tls/blob/mutation-testing-add/tests/saw/deps/Linux-bins.zip)
### Replay

To replay a mutant, in the docker:

~~~~{.sh}
# Apply the mutation rules on source code
# This will mutate and link the all_llvm.bc file into tests/saw/bitcode/all_llvm.bc
$ python3 main.py replay addr_to_trace
# After the mutation, test on the mutated code
$ saw verify_xxxx.saw
~~~~

There has been some trials on the efficiencies of mutants of different categorizes. To be specific:

1) One mutation trial on a single CODE location;
2) Multiple mutation trials on a single CODE location (retrial mutants);
3) Mutations on multiple CODE locations (higher-order mutants).

For information on this part of code, please refer to [this link](https://github.com/meng-xu-cs/s2n-tls/blob/mutation-testing-add/tests/saw/MANUAL.md).


## Authors

Ru Ji <r2ji@uwaterloo.ca>

Meng Xu <m285xu@uwaterloo.ca>

## Publication

```
@inproceedings{fast,
  title = {{Finding Specification Blind Spots via Fuzz Testing}},
  author = {Ru Ji and Meng Xu},
  booktitle = {Proceedings of the 2023 IEEE Symposium on Security and Privacy (Oakland)},
  year = 2023,
  month = 5,
  address = {San Francisco, CA},
}
```

## Confirmed Cases

DPN: PR [1](https://github.com/diem/diem/pull/10152) [2](https://github.com/diem/diem/pull/10176) [3](https://github.com/diem/diem/pull/10178)

s2n-tls: [Report](https://mesquite-train-690.notion.site/Missing-specs-in-s2n-tls-90e3e6221e8b42ce84c788491cdc2a3f)

