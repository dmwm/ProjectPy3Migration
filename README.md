# ProjectPy3Migration

CMS collaboration is looking for a student to complete ongoing
effort to migrate DMWM (Data Management and Workflow Management) stack from
python2 to python3. The DMWM stack consists of about 200K lines of code along
with about 100 external python packages. A qualified candidate will involve of
setting up VM, build python externals in python3, convert DMWM code and perform
numerious tests among two version of python.

Required skills Python language, Linux, UNIX tools

Tags: python, unix scripts
Supervisor: V. Kuznetsov, E. Vaandering

The goal is py2/py3 transition to produce valid py2/py3 code that moves us towards running on py3

Here is detailed tasks we foresee to accomplish with successfull candidate:

- Read twiki [1] about futurize and this PR [2]
- Setup CERN VM either using cmsweb setup [3] or docker [4]
- Install futurize package (if necessary, should be already in docker setup)
- Clone WMCore code, make new branch and applied futurize --stage2 to it
  here we'll break futurize by features, i.e. apply one feature at a time [5]
  - exclude certain constructs from migration
    iteritems, ... # we need to provide full list
    This can be done manually or via changes to futurize package itself.
  - document each feature changes on twiki, the documentation should come
    with simple example of py2 vs py3 styles, e.g.

```
    # python2
    rdict = {}
    for key, val in rdict.iteritems():

    # python3
    rdict = {}
    for key, val in rdict.items():
```
- Run Unit tests via Jenkins [6], the PR will trigger Jenkins tests.
If Jenkins unit tests fails we may rerun failed tests in a docker container [4]

1. https://twiki.cern.ch/twiki/bin/view/CMS/DMWMTutModernPython
2. https://github.com/dmwm/WMCore/pull/7688
3. CERN VM setup, https://cms-http-group.web.cern.ch/cms-http-group/tutorials/environ/vm-setup.html
4. docker container setup, https://github.com/dmwm/WMCore/wiki/Setup-wmcore-unittest
5. http://python-future.org/futurize.html#stage-2-py3-style-code-with-wrappers-for-py2
6. jenkins: https://github.com/dmwm/WMCore/wiki/Understanding-Jenkins
