# Github & Asset governance

## Github

Sources:
- [Github docs: Roles in an organization](https://docs.github.com/en/organizations/managing-peoples-access-to-your-organization-with-roles/roles-in-an-organization)
- Testing on new [TEST Juno Org](https://github.com/TEST-Juno-Org) & its Repos

### Repository Roles
Roles are used to grant access and permissions. They are (pre-)defined globally (per Org) but one can be granted to each (invited) member or team for each Repo.
(Custom roles are available on *Enterprise* plan only for 21$/user/month - [see Annex 1](#Annex-1))

**Read**: *Read and clone repositories. Open and comment on issues and pull requests.*
- Council members should be able to read repos that are still private, and comment.

**Triage**: *Read permissions plus manage issues and pull requests.*
- Council members should be able to read repo permissions and create discussions.
- Non-technical Council members shouldn't be able to manage pull requests if there aren't other checks in place, but we can:
    - define Code Owners per repo, who can be required to approve pull requests
    - define Branch protection rules ([see below](#Per-repo-settings))

**Write**: *Triage permissions plus read, clone and push to repositories.*
- Should be reserved to contracted developers only.

**Maintain**: *Write permissions plus manage issues, pull requests and some repository settings.*
- Should be reserved to contracted maintainers only. Note that Maintainers can do everything that Developers can.

**Admin**: *Full access to repositories including sensitive and destructive actions.*
Change visibility, Disable branch protection rules, Archive, Delete, Transfer ownership to another user or Org, plus every other setting.
- Should be reserved to contracted & vested Council developer.

### Members privileges 
:::info
#### Legend:
**Privilege** [default/option - current -> wanted]:
Description
    -default option description
    -other option description
:::

These settings are defined globally (per Org):

- **Base permissions** [Read/roles - Read -> ??]
    The minimum permissions (role) granted to all members that will be added to repos.

- **Private Repo creation** [ON/OFF - ON -> ON]
- **Private Repo forking** [OFF/ON - OFF -> OFF]
- **Repository discussion** [ON/OFF - ON -> OFF]
    - Allow Repo **readers** to create discussions
    - Only Repo triagers can create, readers can comment
- **Projects base permissions** [Write/roles - Write -> Write]
- **Public Pages creation** [ON/OFF - ON -> OFF]
    - all members can publish a website from the Repo's code (even if private)
- **Repository visibility change** [ON/OFF - OFF -> ??]:
    - allow Repo admins to change its visibility
    - only Org admins can change repos' visibility

3. **Repository deletion and transfer** [ON/OFF - OFF -> ??]:
    - 


Issue deletion (OFF/ON -  -> ):
- only Org admins can delete issues
- allow Repo admins to delete issues

Team creation (ON/OFF -  -> ):
- allow **any member of the Org** to create new teams
- only **Org admins** can create new teams


### Moderation
#### Global settings by Org admins (overriding others):
- **Block specific users on all repos**: deny comments, issues, pull requests, forking, watching, editing wiki pages
- **Temporary interaction limits**: apply 24h/3d/1w/1m/6m cool-down for [comments + issues + PRs] to [new Github users, non-prior-committers, and/or non-co  

#### Per repo settings:
**Branch protection rules:**
*Define a protected branch rule to disable force pushing, prevent branches from being deleted, and optionally require status checks before merging.*

These are part of the Rulesets that can be defined Org-wide, but custom ones can be made for each repo. With free plan:
- Rules are only applied to public repos
- Rules on tags (instead of branches of code) are not available

See available options in [Annex 2](#Annex-2).

**Set member user/team role:**
(above the base role) for each


### TODO:

- Organization policy:
    - members & admins transitions
    - private repo review & minimum requirements for publishing
        - default LICENSE (Apache-2.0?)
        - required README with minimum standard (& branding?)
    - commit signoff policy (per repo or to all repos?)
    - repository labels defaults (standard workflow on issues)
    - matrix of (proposed) approved settings per repo
- Security analysis & alerts
    - Review current implementation
    - Test what's possible and provide recommendation


## Other Assets

### TODO:

- Domain name & email
- Social accounts
    - Discord
    - X (Twitter)
    - Spotify
- ??



# Annex 1

Juno is currently on base (free) plan.

See full **Free / Team / Enterprise** comparison at
https://github.com/organizations/TEST-Juno-Org/billing/plans.

The Team plan costs 4$/user/month and is advised on the account creation form with:
1. **Protect your branches**: *Ensure that collaborators on your repository cannot make irrevocable changes to branches.*
2. **Multiple pull requests reviewers**: *Add more control with multiple pull requests reviewers for any changes to your code before it can be merged.*
3. **Code owners**: *who owns the code and is notified of pull requests.*
4. **Draft pull requests**: *After you create a pull request, you can ask a specific team to review the changes you've proposed.*
5. **Required reviewers**: *Ensure that pull requests have a specific number of approving reviews before collaborators can make changes to a protected branch.*
6. **Pages and Wikis**: *Host documentation and simple websites for your project in a wiki format that contributors can easily edit either on the web or command line.*
7. **Environment deployment branches and secrets**: *A job cannot access secrets that are defined in an environment unless it is running on the specified branch.*
8. **3,000 CI/CD minutes/month** (instead of 2000; free for public repos): *Get execution minutes for hosted runners to automate your software development workflows. Write tasks and combine them to build, test, and deploy any code project on GitHub.*
9. **2GB of Packages storage** (instead of 0.5; free for public repos): *Host your own software packages or use them as dependencies in other projects. Both private and public hosting available.*
10. **Web-based support**: *GitHub Support can help you troubleshoot issues you run into while using GitHub.*


# Annex 2
## Branch protection rules
Source: https://github.com/TEST-Juno-Org/TEST-Private-Repo/settings/branch_protection_rules/new

The following are all individual boolean options.

### Protect matching branches:
1. **Require a pull request before merging**
*When enabled, all commits must be made to a non-protected branch and submitted via a pull request before they can be merged into a branch that matches this rule.*
2. **Require status checks to pass before merging**
*Choose which status checks must pass before branches can be merged into a branch that matches this rule. When enabled, commits must first be pushed to another branch, then merged or pushed directly to a branch that matches this rule after status checks have passed.*
3. **Require conversation resolution before merging**
*When enabled, all conversations on code must be resolved before a pull request can be merged into a branch that matches this rule. Learn more about requiring conversation completion before merging.*
4. **Require signed commits**
*Commits pushed to matching branches must have verified signatures.*
5. **Require linear history**
*Prevent merge commits from being pushed to matching branches.*
6. **Require deployments to succeed before merging**
*Choose which environments must be successfully deployed to before branches can be merged into a branch that matches this rule.*
7. **Lock branch**
*Branch is read-only. Users cannot push to the branch.*
8. **Do not allow bypassing the above settings**
*The above settings will apply to administrators and custom roles with the "bypass branch protections" permission.*
9. **Restrict who can push to matching branches**
*Specify people, teams, or apps allowed to push to matching branches. Required status checks will still prevent these people, teams, and apps from merging if the checks fail.*

### Rules applied to everyone including administrators:
10. **Allow force pushes**
*Permit force pushes for all users with push access.*
11. **Allow deletions**
*Allow users with push access to delete matching branches.*
