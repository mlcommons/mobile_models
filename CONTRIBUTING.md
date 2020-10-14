# Contributing guidelines

## Pull Request Checklist

Before sending your pull requests, make sure you followed this list.

- Read [contributing guidelines](CONTRIBUTING.md)
- Ensure you have signed the [Contributor License Agreement (CLA)](https://cla.developers.google.com/).
- (Note: additional technical details TBD by community.)

## How to become a contributor and submit your own code

### Contributor License Agreements

We'd love to accept your patches! Before we can take them, we have to jump a couple of legal hurdles.

Please fill out either the individual or corporate Contributor License Agreement (CLA).

  * If you are an individual writing original source code and you're sure you own the intellectual property, then you'll need to sign an [individual CLA](https://code.google.com/legal/individual-cla-v1.0.html).
  * If you work for a company that wants to allow you to contribute your work, then you'll need to sign a [corporate CLA](https://code.google.com/legal/corporate-cla-v1.0.html).

Follow either of the two links above to access the appropriate CLA and instructions for how to sign and return it. Once we receive it, we'll be able to accept your pull requests.

***NOTE***: Only original source code from you and other people that have signed the CLA can be accepted into the main repository. (Note: we need to modify this to allow third party code under Apache2 or MIT license with additional review.)

### Contributing code

If you have improvements to MLPerf, send us your pull requests! For those
just getting started, Github has a [howto](https://help.github.com/articles/using-pull-requests/).

### Contribution guidelines and standards

(Note: Technical details TBD by community.)

#### General guidelines and philosophy for contribution

(Note: Technical details TBD by community.)

#### License

Include a license at the top of new files.

*   [C/C++ license example](https://github.com/mlperf/policies/blob/master/license_example.cpp)
*   [Java license example](https://github.com/mlperf/policies/blob/master/license_example.cpp)

#### Coding styles

The code was originally contributed by Google so it conforms to the
[Google C++ Style Guide](https://google.github.io/styleguide/cppguide.html) and
[Google Java Style Guide](https://google.github.io/styleguide/javaguide.html).

The `format_code.sh` script is the convinent way to format your files. It uses the
[clang-format](https://clang.llvm.org/docs/ClangFormat.html) for checking your C/C++ files,
[buildifier](https://github.com/bazelbuild/buildtools/tree/master/buildifier) for bazel files and
[google-java-format](https://github.com/google/google-java-format) for Javafiles.
To install its dependencies, do:

```bash
sudo apt install clang-format
go get github.com/bazelbuild/buildtools/buildifier
```

Then you can format your files by running:
```bash
bash format_code.sh
```

Optionally, you can add it to pre-commit hook by running:
```bash
sed -i -e '$a\' -e 'bash `git rev-parse --show-toplevel`/format_code.sh && git add *' \
-e "/format_code.sh/d" .git/hooks/pre-commit
```

#### Running sanity check

(Note: Technical details TBD by community.)

#### Running unit tests

(Note: Technical details TBD by community.)
