# Accessibility

In the context of software development accessibility refers to
the use of assistive technologies to aid users in effectively
using the software being developed. When designing interactions
through the screen, keyboard, mouse, and speakers it is
important to ensure that the widest possible group of users will be
able to effectively participate in those interactions.

For software developed with JavaScript the user interface (UI) typically
falls into one of the following:

1) Browswer based UI delivered though JavaScript, HTML and CSS.
1) Desktop type application built on something like
   [electron](https://www.electronjs.org/).
1) Command line scripts/applications.

Both 1) and 2) above leverage JavaScript,
HTML and CSS in a similar manner and we'll use
web based applications to describe both of these.

In web based applications, the HTML, JavaScript and CSS run
in the browser (or equivalent in frameworks like electron)
and is referred to as the front-end. The back-end running
on Node.js provides the business logic to the front
end through REST APIs, websockets or some other set of APIs.

In this context, the focus on accessibility is in the
development of the front-end as opposed to
JavaScript running under Node.js in the back-end.

## Recommendation Components

N/A

## Guidance

The teams experience is that it is useful for organizations and teams
building products or components with significant user interfaces to
define guidelines and or design systems that apply to their product or organization
and help ensure accssibility is planned in from the start.
Examples of such guidelines which apply to the work of the team members include:

* [IBM Accessibility requirements](https://www.ibm.com/able/requirements/requirements/)
* [PatternFly accessibility guide](https://pf4.patternfly.org/accessibility-guide/)

It is also best practice to incorporate testing of your application with common
assisitive technologies like screen readers and limiting input to keyboard interaction. See [tooling](#tooling) below.

For those working on Linux
[List Of Accessibility Documentation Sources And Tools (For GNU/Linux Development And Testing)](https://desktopqe-jenkins.rhev-ci-vms.eng.rdu2.redhat.com:3200/desktopqe/d06-projects/a11y.A11y_devel_doc_sources.html)
provides information on good starting points.

### Web based applications

In web based applications most of the accessibility work is done in the front-end. The 
[Web Content Accessibility Guidelines (WCAG)](https://www.w3.org/TR/WCAG21/) is
the recognized standard for making a web application accessible. The teams
members have found the
[WCAG quick reference](https://www.w3.org/WAI/WCAG21/quickref/) a useful
reference for working with the guidelines. The [WAI-ARIA Authoring Practices Examples](https://www.w3.org/TR/wai-aria-practices/examples/) provide a comprehensive list of exemplary widgets complete with code snippets and live demos.

In the teams experience testing/validation of accessibility requirements will be
against the front-end and not the APIs provided by the Node.js back-end. The result
being that team members building the front-end must be knowleadgeable on
accessibility requirements. Back-end Node.js developers, on the other hand, will support
requirements that come from the front-end versus driving the accessibility effort.

Server side rendering may blur the line a bit, but most often front-end developers
or those with front-end skills should be involved in the development of
the HTML that will be rendered on the server and the same guidelines apply as
when rendered in the browser.

In addition to supporting requirements driven by the front end, we recommend that
Node.js developers:

* build APIs in a way that avoids hard coding resources returned to the front end and
  ensuring they can provide all required forms of a resource. Resources required by
  the front-end may need an alternative form in order to support accessibility
  (For example alternative text for audio, etc.).
* Ensure that error messages are understandable when read aloud. Error messages returned
  to users may be read by screen readers.

As mentioned in later sections, some tools for accessibility testing are written
in Node.js. As a result, Node.js developers may also be involved in helping to automate
accessibility testing.

### Command line scripts/applications.

Command line tools have been historically considered more accessible (see
[Accessibility of Command Line Interfaces](https://dl.acm.org/doi/fullHtml/10.1145/3411764.3445544)
for discussion on this topic).
For this reason, most if not all of accessibility standards and guidlines are for
graphical user interfaces. The team is not aware of standards or guidelines that
provide guidance specifically for command line applications. 

If you integrate enhanced visual elements (for example color) into your
command line interfaces, the team recommends that you review the corresponding
sections of the web accessibility guidelines.

[Accessibility of Command Line Interfaces](https://dl.acm.org/doi/fullHtml/10.1145/3411764.3445544)
provides a number of good recommendations which are not specific to Node.js. These
include:

* Ensure that an HTML version of all documentation is available.
* Provide a way to translate long outputs into another accessible format.
* Document the output structure for each command.
* Provide a way to translate tables in CLI output into another accessible format.
* Ensure that all commands provide status and progress indication.
* Ensure that all status and progress indicators used are screen reader friendly.
* Ensure that error messages are understandable when read aloud.

### Tooling

Accessibility tooling is generally not Node.js specific. However some tools are
built in Node.js and are delivered through npm. They will, therefore, fit easily in a JavaScript
or Node.js workflow when nessary. For example:
* [eslint-plugin-jsx-a11y](https://www.npmjs.com/package/eslint-plugin-jsx-a11y)
* [axe-core](https://www.npmjs.com/package/axe-core)
* [pa11y](https://www.npmjs.com/package/pa11y)
* [web test runner](https://modern-web.dev/docs/test-runner/overview/) and [open-wc testing helpers](https://open-wc.org/docs/testing/chai-a11y-axe/) provide framework-agnostic a11y unit testing tools. See [PatternFly Elements' `<pfe-accordion>`](https://github.com/patternfly/patternfly-elements/blob/6363f03d2d95db5146eee6453330b919655fb034/elements/pfe-accordion/test/pfe-accordion.spec.ts#L449-L452) for an example of how to write keyboard accessibility tests for interactive widgets
