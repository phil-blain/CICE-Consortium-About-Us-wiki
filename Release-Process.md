**CICE Release Process**

* Determine type of release
  * new branch, new tag
  * merge master to branch, new tag
  * update to branch, new tag
  * Specify test strategy
* Create release project at https://github.com/CICE-Consortium/CICE/projects and create list of release tasks (see template below)
  * code changes
  * Update documentation including doc/source/intro/major_updates.rst
  * Update version via cice.setup --setvers and commit/push (Note that this will automatically change the documentation versioning. No manual changes are necessary.)
  * Push changes to master
  * Test
  * Create release notes at https://github.com/CICE-Consortium/CICE/wiki/CICE-Recent-changes
  * Generate and check html and pdf documentation via readthedocs
* Create release branch in repository if needed.  Naming convention is CICEm.n
  * Clone, branch, and push directly to the consortium repository
* Git Tag the release. Naming convention is CICEm.n.p
  * Tag and push directly to the consortium repository, use annotated tag (ie. git tag -a CICE6.0.0 -m "CICE6.0.0 tag")
* Verify tag/release page generation (should be automatic), https://github.com/CICE-Consortium/CICE/releases
  * Edit the release page to add additional info
* Create release specific tables on wiki, https://github.com/CICE-Consortium/CICE/wiki/CICE-Version-Index
  * Link release page and repo in table
  * Generate static documentation at readthedocs and link to release table (activate the tag under readthedocs "versions", may need to trigger a build of the master docs for the tag to appear), html and pdf.
  * Create DOI on zenodo and link in table
* Move release notes from https://github.com/CICE-Consortium/CICE/wiki/CICE-Recent-changes to https://github.com/CICE-Consortium/CICE/releases
* Move/generate release test results and post on test wiki.
* Post science results as needed
* Send out release email 

-----------------------------------------
**Template for CICE release**    (Icepack will be similar - edit this page to copy)

- [ ] Complete [tasks for release](https://github.com/CICE-Consortium/Icepack/projects/2)
- [ ] Create release notes at https://github.com/CICE-Consortium/CICE/wiki/CICE-Recent-changes
- [ ] Update version/release by running "cice.setup --setvers 6.0.2" and commit/PR modifications
- [ ] Review Copyright
- [ ] Generate and check html and pdf documentation
- [ ] Commit and push final changes to master including, making sure version update is included
- [ ] Create release branch in repository if needed
Naming convention is CICEm.n
- [ ] Generate test results and post to Test-Results wiki, use --bgen with release name if possible
- [ ] Git Tag the release
Naming convention is CICEm.n.p
This generates documentation at readthedocs
- [ ] Move release notes from https://github.com/CICE-Consortium/CICE/wiki/CICE-Recent-changes to https://github.com/CICE-Consortium/CICE/releases, and publish
- [ ] Add to zenodo community
- [ ] Add links in appropriate places on github where to find the release and tar file
[News](https://github.com/CICE-Consortium/About-Us/wiki/Consortium-News-and-Highlights)
[Version index](https://github.com/CICE-Consortium/CICE/wiki/CICE-Version-Index)
- [ ] Post science results as needed
- [ ] Send out release email s

-----------------------------------------
**Template for CICE incremental release** 

- [ ] Update version/release by running "cice.setup --setvers 6.0.2" and commit/PR modifications
- [ ] Review Copyright
- [ ] Create release notes at https://github.com/CICE-Consortium/CICE/wiki/CICE-Recent-changes
- [ ] Test, use --bgen with version name if possible and review tests
- [ ] Verify that html and pdf documentation is generated OK
- [ ] Move to release branch if needed and git tag the release
Naming convention is CICEm.n.p
This generates documentation at readthedocs
- [ ] Move release notes from https://github.com/CICE-Consortium/CICE/wiki/CICE-Recent-changes to https://github.com/CICE-Consortium/CICE/releases, and publish
- [ ] Add to zenodo community
- [ ] Verify readthedocs tags documentation is generated
- [ ] Post to Test-Results wiki
- [ ] Add links in appropriate places on github where to find the release and tar file
[News](https://github.com/CICE-Consortium/About-Us/wiki/Consortium-News-and-Highlights)
[Version index](https://github.com/CICE-Consortium/CICE/wiki/CICE-Version-Index)
- [ ] Merge release to release branch
- [ ] Send out release email s if needed
