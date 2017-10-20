Cirs RFCs
---

Many changes, including bug fixes and documentation improvements can be
implemented and reviewed via the normal GitHub pull request workflow.

Some changes though are "substantial", and we ask that these be put through a
bit of a design process and produce a consensus among the Cirs community.

The "RFC" (request for comments) process is intended to provide a consistent
and controlled path for new features to enter the language and standard
libraries, so that all stakeholders can be confident about the direction the
language is evolving in.


# Table of Contents

  - [Opening](#cirs-rfcs)
  - [Table of Contents](#table-of-contents)
  - [When you need to follow this process](#when-you-need-to-follow-this-process)
  - [License](#license)
      - [Contribution](#contribution)


# When you need to follow this process

You need to follow this process if you intend to make "substantial" changes to
Cirs or the RFC process itself. What constitutes a "substantial" change is may
include the following.

  - Any semantic change to the C language implementation that is not a bugfix.
  - Removing language features, including those that are feature-gated.
  - Changes to the interface between the compiler and libraries, including lang
    items and intrinsics.

Some changes do not require a RFC:

  - Rephrasing, reorganizing, refactoring, or otherwise "changing shape does
    not change meaning".
  - Additions that strictly improve objective, numerical quality criteria
    (warning removal, speedup, better platform coverage, more parallelism, trap
    more errors, etc.)
  - Additions only likely to be _noticed by_ other developers-of-cirs,
    invisible to users-of-cirs.

If you submit a pull request to implement a new feature without going through


# What the process is

In short, to get a major feature added to Cirs, one must first get the RFC
merged into the RFC repository as a markdown file. At that point the RFC is
"active" and may be implemented with the goal of eventual inclusion into Cirs.

  - Fork the RFC repo [RFC repository]
  - Copy `0-template.md` to `text/0-my-feature.md` (where "my-feature" is
    descriptive. don't assign an RFC number yet).
  - Submit a pull request. As a pull request the RFC will receive design
    feedback from the larger community, and the author should be prepared to
    revise it in response.
  - The RFC pull request is discussed, as much as possible in the
    comment thread of the pull request itself.
  - RFCs rarely go through this process unchanged, especially as alternatives
    and drawbacks are shown. You can make edits, big and small, to the RFC to
    clarify or change the design, but make changes as new commits to the pull
    request, and leave a comment on the pull request explaining your changes.
  - Specifically, do not squash or rebase commits after they are visible on the
    pull request.

# License

Cirs RFCs are licensed under either of

* Apache License, Version 2.0, ([LICENSE-APACHE](LICENSE-APACHE) or http://www.apache.org/licenses/LICENSE-2.0)
* MIT license ([LICENSE-MIT](LICENSE-MIT) or http://opensource.org/licenses/MIT)

at your option. Some parts of the repository are already licensed according to those terms. For more see [RFC 2044](https://github.com/rust-lang/rfcs/pull/2044) and its [tracking issue](https://github.com/rust-lang/rust/issues/43461).

## Contributions

Unless you explicitly state otherwise, any contribution intentionally submitted for inclusion in the work by you, as defined in the Apache-2.0 license, shall be dual licensed as above, without any additional terms or conditions.
