CICE Release Process
* Determine type of release
  * new branch, new tag
  * merge master to branch, new tag
  * update to branch, new tag
  * Specify test strategy
* Create release project at https://github.com/CICE-Consortium/CICE/projects and create list of release tasks
  * code changes
  * Update doc/source/intro/major_updates.rst
  * Update README.md
  * Update version in doc/source/conf.py version/release and version.txt
  * Push changes to branch/master
  * Create release notes at https://github.com/CICE-Consortium/CICE/wiki/CICE-Recent-changes
  * Generate and check html and pdf documentation via readthedocs
  * Generate test results and post to wiki. Use --bgen with the full release name

* Create release branch in repository if needed.  Naming convention is CICEm.n
* Create release specific tables on wiki
* Git Tag the release. Naming convention is CICEm.n.p
* Generate documentation at readthedocs
  * activate the tag under "versions", may need to trigger a build of the master docs for the tag to appear
* Move release notes from https://github.com/CICE-Consortium/CICE/wiki/CICE-Recent-changes to https://github.com/CICE-Consortium/CICE/releases
* Add links in appropriate places on github where to find the release and tar file
* Post science results as needed
* Send out release email 