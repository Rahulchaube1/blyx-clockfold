<img src="assets/logo.png" width="112" height="112" alt="Blyx penguin opening a folded clock to reveal two possible instants.">

# ClockFold

Classify a local time around one supplied offset transition. This Blyx library is part of the calendar, scheduling and local time collection.

One wall time can occur twice during a fall-back transition and disappear entirely during a forward jump. Expose the number of valid UTC candidates. [PEP 495, local time disambiguation](https://peps.python.org/pep-0495/)

## Install and run

Install [Blyx 0.2.1](https://www.blyx-lang.space/download) with a Rust toolchain and host linker for native builds.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-clockfold.git
cd blyx-clockfold
blyxc native-run example.blyx
blyxc native-run tests.blyx
```

[Run the editable browser example](https://www.blyx-lang.space/play?example=package-clockfold) · [Package page](https://www.blyx-lang.space/packages/clockfold) · [Handbook](https://doc.blyx-lang.space/guide/blackbird)

## Import the module

Run this in the directory containing your application's entry file.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-clockfold.git vendor/clockfold
```

```blyx
use vendor::clockfold::clockfold;

fn main() {
    let local = 11000.0;
    let transition = 10000.0;
    let before = 3600.0;
    let after = 0.0;
    let result = clockfold_classify(local, transition, before, after);
    if len(result) == 0 { println!("invalid"); return; }
    let mut i = 0;
    while i < len(result) {
        println!(at(result, i));
        i += 1;
    }
}
```

Expected output

```text
2
7400
11000
```

## API

`clockfold_classify(local, transition, before, after)`

Returns [number of valid UTC candidates, earliest candidate, latest candidate]. A forward gap yields [0,0,0]; a backward fold yields two candidates. Invalid arguments and nonfinite results return an empty vector. Integers carried in numeric vectors use the exact range from −(2^53−1) to 2^53−1.

| Argument | Domain |
| --- | --- |
| local | A exact signed integer |
| transition | A exact signed integer |
| before | A exact signed integer |
| after | A exact signed integer |

## In use

[Blackbird](https://github.com/Rahulchaube1/blyx-blackbird) uses this module to resolve a wall-clock timestamp at a known gap or fold without guessing its offset.

## Verification and contributions

The regression suite in [tests.blyx](tests.blyx) checks the example, boundary cases and invalid inputs. Include a short reproducer and your compiler version in [an issue](https://github.com/Rahulchaube1/blyx-clockfold/issues). The source is dual-licensed under [MIT](LICENSE-MIT) or [Apache-2.0](LICENSE-APACHE). Read the [artwork notice](assets/NOTICE.txt) for credits.

## Connect with Rahul Chaube

[Portfolio](https://www.rahulchaube1.com/) · [GitHub](https://github.com/Rahulchaube1) · [LinkedIn](https://www.linkedin.com/in/rahulchaube1) · [Hugging Face](https://huggingface.co/oncody) · [X](https://x.com/RahulChaube_) · [EverestQ](https://www.everestqai.com/) · [Contact](https://www.rahulchaube1.com/contact)

[Blyx website](https://www.blyx-lang.space/) · [BlyxTorch](https://www.blyx-lang.space/packages/blyxtorch) · [Handbook](https://doc.blyx-lang.space/) · [Community](https://www.blyx-lang.space/community)

Support Rahul’s open-source work through [GitHub Sponsors](https://github.com/sponsors/Rahulchaube1) or [Buy Me a Coffee](https://buymeacoffee.com/rahulchaube).
