# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## Unreleased

### Breaking Changes

- `tree::State::read()` now returns an `Arc` containing the state, rather than a
  read guard. This change has no noticable impact on microbenchmarks, but yields
  more fair writing performance under heavy-read conditions -- something the
  current microbenchmarks don't test but in-development Commerce Benchmark for
  BonsaiDb unvieled.
- `Buffer` has been renamed to `ArcBytes`. This type has been extracted into its
  own crate, allowing it to be used in `bonsaidb::core`. The new crate is
  [available here](https://github.com/khonsulabs/arc-bytes).
- `Root::scan`, `Tree::scan`, `Tree::get_range`, `TransactionTree::scan`, and
  `TransactionTree::get_range` now take types that implement
  `RangeBounds<&[u8]>`. `BorrowByteRange` is a trait that can be used to help
  borrow ranges of owned data.

### Added

- `nebari::tree::U64Range` has been exposed. This type makes it easier to work
  with ranges of u64s.

## v0.1.1

### Added

- `Tree::replace` has been added, which calls through to `TransactionTree::replace`.
- `Tree::modify` and `TransactionTree::modify` have been added, which execute a
  lower-level modification on the underlying tree.

## v0.1.0

Initial release.