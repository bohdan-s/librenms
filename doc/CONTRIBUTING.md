Guidelines for contributing to LibreNMS
---------------------------------------

- Test your patches first.  It's easy to set up git to push to a bare
  repository on a local test system, and pull from this into your live
  installation at very frequent intervals.

- Don't break the poller.  User interface blemishes are not critical, but
  losing data from network monitoring systems might be.

- As a general rule, if you're replacing lines of code with new lines of
  code, don't comment them out, just delete them.  Commented out code makes
  the patch and the resultant code harder to read, and there's no good
  reason to it since we can easily get them back from git.

- If you're fixing a bug or making another minor change, don't reformat the
  code at the same time.  This makes it harder to see what's changed.  If
  you need to reformat it after making the change, do so in a separate
  commit.

- Please join us in IRC at irc.freenode.net in channel ##librenms if you're
  able.  Collaborating in real time makes the coordination of contributions
  easier.

- Don't submit code whose license conflicts with the GPLv3.  If you're not
  sure, consult the [Free Software Foundation's license list][1] and see if
  your code's license is on the compatible or incompatible list.  If you
  prefer a non-copyleft license, Apache 2.0 is the recommended choice as per
  the FSF guidelines.

- The current Observium license is incompatible with GPLv3.  Don't submit
  code from current Observium unless you are the copyright holder, and you
  specifically state in the code that you are releasing it under GPLv3 (or a
  compatible license).

  Because contributing to Observium requires that you reassign copyright to
  Adam Armstrong, if you want to release the same code for both Observium
  and LibreNMS, you need to release it for LibreNMS first and mark it with
  your own copyright notice, then release it to Observium and remove your
  copyright, granting Adam ownership.

  Please note that the above is necessary even if you don't care about
  keeping the copyright to your code, because otherwise we could be accused
  of misappropriating Obserivum's code.  As the code bases develop, we
  expect them to diverge, which means this will become less of an issue
  anyway.

- Because the GPL's provisions about linking don't apply to PHP-based
  projects, we interpret the linking provisions of the license to refer to
  the use of PHP library functions called from LibreNMS code.

  We consider inclusion of files such as MIBs in the LibreNMS repository to
  be merely aggregation in a distribution medium as per the last paragraph
  of the GPLv3 section 5 ("Conveying Modified Source Versions"), and because
  they are not combined with LibreNMS to form a larger program, the GPLv3
  does not apply to them.  This is not a legal ruling - it is simply a
  statement of our intent and current interpretation.


Contributor Agreement
---------------------

By contributing code to LibreNMS (whether by a github pull request, or by
any other means), you assert that:

- You have the rights to include the code, either as its original author,
  or due to it being released to you under a compatible license.

- You are not aware of any third party claims on the code, including
  copyright infringement, patent, or any other claim.

- You have not viewed code written under the [Observium License][4] in the
  production of contributed code.  This includes all Observium code after
  Subversion revision 3250 and any patches or other code covered by that
  license from Observium web sites after Tue May 29 13:08:01 2012 +0000 (the
  date of Observium r3250).

To agree with these assertions, please submit a github pull request against
the file doc/AUTHORS.md including your name, email address, and github user
id in the file (so that it can be matched to your commits), and stating in
the commit log that you agree to the conditions of the Contributor Agreement
contained in doc/CONTRIBUTING.md.

Note that contributors to LibreNMS retain copyright to their own code and
are not required to sign over their rights to any other party.  We recommend
that if you add a new file containing original code to the code base that
you include a copyright notice in it as per the Free Software Foundation's
guidelines.


Proposed workflow for submitting pull requests
----------------------------------------------

The basic rule is: don't create merge conflicts in master.  Merges should be
simple fast-forwards from current master.

Following is a proposed workflow designed to minimise the scope of merge
conflicts when submitting pull requests.  It's not mandatory, but seems to
work well enough.

We don't recommend git flow because we don't want to maintain separate
development and master branches, but if it works better for you, feel free
to do that, as long as you follow the golden rule of not creating merge
conflicts in master.

Workflow:

- Ensure you have auto rebase switched on in your gitconfig.
```
[branch]
        autosetuprebase = always
```
- Fork the [LibreNMS repo master branch][2] in your own GitHub account.
- Create an [issue][3] explaining what work you plan to do.
- Create a branch in your copy of the repo called issue-####, where #### is
  the issue number you created.
```
git push origin master:issue-####
```
- Make and test your changes in the issue branch as needed - this might take
  a few days or weeks.
- When you are happy with your issue branch's changes and ready to submit
  your patch, update your copy of the master branch to the current revision;
  this should just result in a fast forward of your copy of master. Do this from your master branch:
```
git pull
```
- Rebase your issue branch from your clone of master.  Fix any conflicts at
  this stage. Do this from your issue-#### branch:
````
git pull
````
- Push your changes to your remote git hub branch so you can submit a pull from your issue-#### branch:
````
git push origin issue-####
````
- Submit a pull request for your patch from your copy of master.

[1]: http://www.gnu.org/licenses/license-list.html
"Free Software Foundation's license list"
[2]: https://github.com/librenms/librenms/tree/master
"LibreNMS master branch"
[3]: https://github.com/librenms/librenms/issues
"LibreNMS issue database"
[4]: http://www.observium.org/wiki/License
"Observium License"

