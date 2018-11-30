CICE Release Process
* Determine type of release
  * new branch, new tag
  * merge master to branch, new tag
  * update to branch, new tag
  * Specify test strategy
* Create release project at https://github.com/CICE-Consortium/CICE/projects and create list of release tasks
  * code changes
  * Update documentation including doc/source/intro/major_updates.rst
  * Update version via cice.setup --setvers and commit/push (Note that this will automatically change the documentation versioning. No manual changes are necessary.)
  * Push changes to master
  * Test
  * Create release notes at https://github.com/CICE-Consortium/CICE/wiki/CICE-Recent-changes
  * Generate and check html and pdf documentation via readthedocs
* Create release branch in repository if needed.  Naming convention is CICEm.n
* Git Tag the release. Naming convention is CICEm.n.p
* Verify tag/release page generation (should be automatic), https://github.com/CICE-Consortium/CICE/releases
* Create release specific tables on wiki, https://github.com/CICE-Consortium/CICE/wiki/CICE-Version-Index
  * Link release page and repo in table
  * Generate static documentation at readthedocs and link to release table (activate the tag under readthedocs "versions", may need to trigger a build of the master docs for the tag to appear), html and pdf.
  * Create DOI on zenodo
* Move release notes from https://github.com/CICE-Consortium/CICE/wiki/CICE-Recent-changes to https://github.com/CICE-Consortium/CICE/releases
* Move/generate release test results and post on test wiki.
* Post science results as needed
* Send out release email 