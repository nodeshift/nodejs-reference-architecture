# Accessibility

In the context of software development accessibility refers to
the ability of people with disabilities to effectively
use the software being developed. When designing interactions
through the screen, keyboard, mouse and speakers it is
important to ensure that people with disabilities will be
able to effectively participate in those interactions.

For software developed in Node.js the user interface most
often falls into one of the following categories:

1) Browswer based UI delivered though HTML and JavaScript.
1) Desktop type application built on something like
   [electron](https://www.electronjs.org/).
1) Command line scripts/applications.

Both 1) and 2) above leverage JavaScript,
HTML and CSS in a similar manner and we'll use
web based UI to describe both of these.

In web based applications, the HTML, JavaScript and CSS run
in the browser (or equivalent in frameworks like electron)
and is referred to as the front-end. The back-end running
on Node.js then provides the business logic to the front
end through REST APIs, websockets or some other set of APIs.

In this context, for a web based application most of the
focus on accessibility is in the development of the front-end
as opposed to JavaScript running under Node.js

## Recommendation Components

N/A

## Guidance

The teams experience is that it is useful for organizations and teams
building products or components with significant user interfaces to
define specific guidelines that apply to their product or organization.
Excamples of such guidelines which apply to the work of one or more of the team members include:

* [IBM Accessibility requirements](https://www.ibm.com/able/requirements/requirements/)
* [PatternFly accessibility guide](https://pf4.patternfly.org/accessibility-guide/)

It is also best practice to incorporate testing of your application with common
assisitive technologies like screen readers and limiting input to keyboard interaction. 

[List Of Accessibility Documentation Sources And Tools (For GNU/Linux Development And Testing)](https://desktopqe-jenkins.rhev-ci-vms.eng.rdu2.redhat.com:3200/desktopqe/d06-projects/a11y.A11y_devel_doc_sources.html)
provides information on good starting points for those working on Linux.

### Web based applications

For web based applications most of the work is done in the front-end. The 
[Web Content Accessibility Guidelines (WCAG)](https://www.w3.org/TR/WCAG21/) is
the recognized standard for making a web application accessible. The teams
members have found the
[WCAG quick reference](https://www.w3.org/WAI/WCAG21/quickref/) a useful
reference for working with the guidelines.

In the teams experience testing/validation of accessibility requirements will be
against the front-end and not the APIs provided by the Node.js back-end. The result
being that team members building the front-end must be knowleadgeable on
accessibility requirements. Node.js developers will support requirements
that come from the front-end versus driving the accessibility effort.

Server side rendering may blur the line a bit, but most often front-end developers
or those with front-end skills should be involved in the design/development of
the HTML, JavaScript and CSS that will be generated through server side rendering and
the same guidelines apply as when rendered in the browser.

In addition to supporting requirements driven by the front end we recommend that
Node.js developers:

* build APIs so that avoid hard coding resources returned to the front end and
  ensure they can provide all required forms of a resource from the start.
  Resources required by the front-end may need an alternative
  form in order to support accessibility  (for example alternative text for audio, etc.).
* Ensure that error messages are understandable when read aloud. Error messages returned
  to users may be read by screen readers.

As mentioned in later sections, some tools for accessibility testing are written
in Node.js, so Node.js developers may also get involved in helping to automate
accessibility testing.

### Command line scripts/applications.

Command line tools have been historically considered more accessible (see
[Accessibility of Command Line Interfaces](https://dl.acm.org/doi/fullHtml/10.1145/3411764.3445544)
for discussion on this topic).
For this reason most if not all of accessibility standards and guidlines are for
graphical user interfaces. The team is not aware of standards or guidelines that
provide guidance specifically for command line applications. 

If you integrate enhanced visual elements (for example color) into your
command line interfaces, the teams recommendation is that you review the corresponding
sections of the web accessibility guidelines.

[Accessibility of Command Line Interfaces](https://dl.acm.org/doi/fullHtml/10.1145/3411764.3445544))
provides a number of good recommendations which are not specific to Node.js applications. These
include:

* Ensure that a HTML version of all documentation is available.
* Provide a way to translate long outputs into another accessible format.
* Document the output structure for each command.
* Provide a way to translate tables in CLI output into another accessible format.
* Ensure that all commands provide status and progress indication.
* Ensure that all status and progress indicators used are screen reader friendly.
* Ensure that error messages are understandable when read aloud.

### Tooling

Accessibility tooling is generally not Node.js specific, however some tools are
built in Node.js, are delivered through npm and will fit easily in a JavaScript
or Node.js workflow when nessary. For example:
* [eslint-plugin-jsx-a11y](https://www.npmjs.com/package/eslint-plugin-jsx-a11y)
* [axe-core](https://www.npmjs.com/package/axe-core)
* [pa11y](https://www.npmjs.com/package/pa11y))
