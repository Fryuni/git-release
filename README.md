# git-release
[![Release](https://img.shields.io/github/v/release/anton-yurchenko/git-release)](https://github.com/anton-yurchenko/git-release/releases/latest)
[![codecov](https://codecov.io/gh/anton-yurchenko/git-release/branch/master/graph/badge.svg)](https://codecov.io/gh/anton-yurchenko/git-release)
[![Go Report Card](https://goreportcard.com/badge/github.com/anton-yurchenko/git-release)](https://goreportcard.com/report/github.com/anton-yurchenko/git-release)
[![Tests](https://github.com/anton-yurchenko/git-release/workflows/unit%20tests/badge.svg)](https://github.com/anton-yurchenko/git-release/actions)
[![Docker Build](https://img.shields.io/docker/cloud/build/antonyurchenko/git-release)](https://hub.docker.com/r/antonyurchenko/git-release)
[![Docker Pulls](https://img.shields.io/docker/pulls/antonyurchenko/git-release)](https://hub.docker.com/r/antonyurchenko/git-release)
[![License](https://img.shields.io/github/license/anton-yurchenko/git-release)](LICENSE.md)

A **GitHub Action** for creating a **GitHub Release** with **Assets** and **Changelog** whenever a new **Tag** is pushed to the repository.  

![PIC](docs/images/release.png)

## Features:
- Parse Tag to match Semantic Versioning.  
- Upload build artifacts (assets) to the release.  
- Add a changelog to the release.  

## Manual:
1. Add your changes to `CHANGELOG.md` in the following format (according to [keepachangelog.com](https://keepachangelog.com/en/1.0.0/ "Keep a ChangeLog")):
```
## [3.0.0-rc.1] - 2019-12-21 
### Added
- Feature A
- Feature B
- GitHub Actions as a CI system
- GitHub Release as an Artifactory system

### Changed
- User API

### Removed
- Previous CI build
- Previous Artifactory
```
2. Tag a commit with Version (according to [semver.org](https://semver.org/ "Semantic Versioning")).
    - Prefix support is available (for example `v3.0.1`), see configuration section in order to enable it.
3. Push and watch **Git-Release** publishing a Release on GitHub ;-)  
![PIC](docs/images/log.png)

## Configuration:
1. Change the workflow to be triggered on Tag Push:
    - For example `'*'` or a more specific like `'v*'`:
```
on:
  push:
    tags:
    - 'v*'
```
2. Add Release stage to your workflow:  
    - Customize configuration with **env.vars**:
        - Provide a list of assets as `args` (divided by one of: `new line`, `space`, `comma`, `pipe`)
        - `DRAFT_RELEASE: [true, false]` - Save release as draft instead of publishing it (default `false`).
        - `PRE_RELEASE: [true, false]` - GitHub will point out that this release is identified as non-production ready (default: `false`). 
        - `CHANGELOG_FILE: string` - Changelog filename (default: `CHANGELOG.md`).
        - `ALLOW_EMPTY_CHANGELOG: [true, false]` - Allow publishing a release without changelog (default `false`).
        - `ALLOW_TAG_PREFIX: [true, false]` - Allow prefix on version Tag, for example `v3.0.1` or `release-3.0.1` (default: `false`).
```
    - name: Release
      uses: docker://antonyurchenko/git-release:latest
      env:
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        DRAFT_RELEASE: "false"
        PRE_RELEASE: "false"
        CHANGELOG_FILE: "CHANGELOG.md"
        ALLOW_EMPTY_CHANGELOG: "true"
        ALLOW_TAG_PREFIX: "true"
      with:
        args: |
            build/darwin-amd64.zip
            build/linux-amd64.zip
            build/windows-amd64.zip
```

## Remarks:
- **Git Tag** should be identical to **Changelog Version** in order for changes to be parsed properly. This does not include **Tag Prefix** like `release-*`.
- This action is automatically built at **Docker Hub**, and tagged with `latest / v3 / v3.0 / v3.0.1`. You may lock to a certain version instead of using **latest**.  
(*Recommended to lock against a major version, for example* `v3`)
- Instead of using pre-built image, you may build it during the execution of your flow by changing `docker://antonyurchenko/git-release:latest` to `anton-yurchenko/git-release@master`

## License
[MIT](LICENSE.md) © 2019-present Anton Yurchenko