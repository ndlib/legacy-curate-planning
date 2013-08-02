# Site Structure

## Home (/)
- Login
- Search
- About
- Contact
- Report a Problem

## Login (/login)
User session management will be managed with [devise](https://github.com/plataformatec/devise).

[OmniAuth](https://github.com/intridea/omniauth) provides an API for multi-provider authentication and can be [used with devise](https://github.com/plataformatec/devise/wiki/OmniAuth:-Overview).
There are many [OmniAuth strategies](https://github.com/intridea/omniauth/wiki/List-of-Strategies) including several of interest to Hydra partners:

- [CAS](https://github.com/dlindahl/omniauth-cas)
- [Shibboleth](https://github.com/toyokazu/omniauth-shibboleth)
- [Kerberos](https://github.com/naffis/omniauth-krb5)
- [LDAP](https://github.com/intridea/omniauth-ldap)

CurateND only has need for CAS integration during the first phase of development.

### Feature Evolution
- Allow the user to choose login strategy and persist strategy choice via cookie OR prompt for *login* only and determine authentication system from provided identifier
- Request an account
- Account recovery

## After Login
- Accept terms of service (if required)
- Prompt to update profile (if required)

## Profile
- Add authentication mechanisms
- Add personal identifiers e.g. ORCID, google plus
	- Validate identities via OAuth with the external services
- Authorize external storage systems e.g. [Box](https://www.box.com), [Dropbox](https://www.dropbox.com/), [Transporter](http://www.filetransporter.com/)
- Enrich Person metadata
- Manage avatar (delegate to [gravatar](http://en.gravatar.com/) for now)
- Notification settings
- Manage account delegation

## Dashboard
- Submit a Work
- Search
- About
- Contact
- Report a Problem
- Profile
- What's going on / What's happening
	- My Activity
	- My Notifications

## Activity & Notifications
### My Activity (What's happening?)
- What have I done?
	- Search actions
	- Display actions as tabular data
	- Graph actions
- What are others doing with things I observe?
	- The things I observe include but are not limited to works I have submitted
	- Implied `observers` table with pid, class, user_id/user_pid, owner_pid
	- Search usage
	- Display usage as tabular data
	- Graph usage

### My Notifications (What to do?)
- link to notification settings
- list of tasks that are waiting on me: title, state, snooze
- list of things I care about that are "in process"
	- Search list of in process items
	- Allow a user to "follow" up on an item waiting for approval
- list of things I care about that have been recently marked "done"
	- Search list of recently "done" items

## Mediation
- Notify both sending and receiving parties on state change
- Allow for changes in authorization based on item state
	- (Can a non-owner alter an item? Probably not.)
- Render form for state & concern
	- ActionView lookup
- Support "locked" state (only privileged users can alter it)

## Authority Management

## Syndication

## PURL Service

## File Dissemination

## Metadata Dissemination

## API Design