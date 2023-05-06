# FAST: Finding Specification Blind Spots via Fuzz Testing
A formally verified program can only be as correct as its specifications (<span class="smallcaps">SPEC</span>). But how to assure that <span class="smallcaps">SPEC</span> is complete and free of loopholes?
FAST(<ins>F</ins>uzzing-<ins>A</ins>ssisted <ins>S</ins>pecification <ins>T</ins>esting) is an architecture which examines <span class="smallcaps">SPEC</span> incompleteness issues in an automated way. It first locates <span class="smallcaps">SPEC</span> gaps via mutation testing, i.e., by checking whether a <span class="smallcaps">CODE</span> variant conforms to the original <span class="smallcaps">SPEC</span>. If so, FAST further leverages the test suites to infer whether the gap is introduced by intention or by mistake. Depending on the size of the codebase, FAST is applied to two open-source codebases. FAST aims to highlight the prevalence of <span class="smallcaps">SPEC</span> incompleteness in real-world applications.


## Mutation Rules



## Enumerative <span class="smallcaps">CODE</span> mutant generation

<img src="/fig/mutation_rule.png"  width=35% height=35%>


## AWS S2N-TLS



## Installation using Docker

Under ./docker
~~~~{.sh}
# build docker
$ make build

# go into the docker once and dicsard the container afterwards
$ make once

# run docker with script
$ make script
~~~~

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

