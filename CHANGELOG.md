## [3.0.0] - 2020-01-03
This is a major release because default behavior was changed.  
Semantic versioning now enforced by default and in order to allow custom prefixes like `v*` or `release-*`, **ALLOW_TAG_PREFIX** env.var should be enabled.  

Pay attention that prefix is related only to Tags, Changelog versions are still expected to be a valid **semver**.

### Changed
- Replace CircleCI with GitHub Actions as a Continuous Integration system
- Better 'GITHUB_REPOSITORY' regex validation
- Improved 'Changelog' package parsing capabilities

### Fixed
- Semantic Versioning compliance
- Keep a Changelog compliance

### Added
- 'ALLOW_TAG_PREFIX' to control version prefix like `v` or `release`

## [2.0.2] - 2019-12-29
### Added
- CircleCI integrated as a Continuous Integration system
- GolangCI integrated as a Continuous Code Quality system
- CodeCov integrated as a Continuous Code Quality system

### Changed
- DockerHub setup as a Continuous Delivery system

## [2.0.1] - 2019-12-28
### Changed
- Disable unit testing on Docker Hub auto builds

## [2.0.0] - 2019-12-28
This is a major release as most of the code was refactored and some behavior was changed, for example "Tag version is set as a release title".

### Fixed
- Artifact files not found caused panic - all files now being validated before release creation
- Custom changelog file now being validated before release creation
- Arguments parsing fixed

### Added
- Unit testing
- Docker image now built from scratch, resulting in decreased size 139.73MB -> 2.43MB, improving action overall speed.
- **app** package
- `ALLOW_EMPTY_CHANGELOG` env.var to allow publishing a release without changelog (default **false**)
- Artifacts (provided as arguments) can now be separated by one of: `new line '\n', pipe '|', space ' ', comma ','`

### Changed
- **local** package renamed to **repository**
- **remote** package splitted into 2 packages: **asset**, **release**
- Tag version is set as a release title

## [1.1.0] - 2019-12-21
### Added
- [PR #3](https://github.com/anton-yurchenko/git-release/pull/3) Allow any prefix to semver tag. (*Thanks to [Taylor Becker](https://github.com/tajobe) for the PR*)

### Fixed
- PreRelease overwriting Draft configuration. (*Thanks to [Taylor Becker](https://github.com/tajobe) for reporting an issue*)

## [1.0.0] - 2019-10-01
- First stable release.

## [0.2.1] - 2019-10-01
### Fixed
- Wrong PRE_RELEASE message when set.
- Correct 'creating release' log message.

## [0.2.0] - 2019-10-01
### Added
- Changelog reader.
- MIT License.

### Changed
- Remove 'v' from release name.

### Fixed
- Create release without assets.

## [0.1.1] - 2019-09-29
### Added
- Tag regex to match v1.0.0 and 1.0.0.
- Log when procedure finished.

### Removed
- 'DRAFT_RELEASE=false' warning logging.
- 'PRE_RELEASE=false' warning logging.

## [0.1.0] - 2019-09-29
### Added
- Create GitHub Release.
- Upload Assets.
- Control Release Draft through env.var 'DRAFT_RELEASE'.
- Control Release Pre Release through env.var 'PRE_RELEASE'.