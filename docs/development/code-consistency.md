---
sidebar_position: 2
---

# Code Consistency

It is important to the efficiency of teams working
on JavaScript (and other languages) to have consistency
in formatting within the projects managed by their team.

Not having a consistent coding style documented or enforcing
consistency manually as part of code reviews or
other manual techniques is error prone, potentially
harmful to relationships between team members,
is a barrier to attracting external contributions and can
result in bugs because the is harder to understand and spot
repeating patterns.

Consistency should be enforced through automated tooling
which is well integrated into the process of landing
Pull Requests (or equivalent).

There are benefits to consistency across an organization but
it is also important that teams are empowered to do what is
right for their projects. We recommend starting with an
organizational standard and then adjusting based on the
needs of the team.

## Recommended Components

- ESLint - https://eslint.org/

ESLint is broadly used with the `teams` organizations and has broad usage
across the JavaScript ecosystem with > 11 million weekly downloads.
It can be configured to reflect the coding style followed by most
if not all teams.

# Guidance

- Use one of the pre-existing ESLint shareable configurations. There are a number
  of pre-existing configurations and re-using one of these has a number
  of benefits:

  - minimizing what can be potentially divisive discussions to agree
    on the style to be followed.
  - leveraging the experience of what has worked for other teams.
  - increasing the likelihood of familiarity for new team members.

  Examples include:

  - eslint-config-airbnb-standard - https://www.npmjs.com/package/eslint-config-airbnb-standard
  - eslint-config-semistandard - https://www.npmjs.com/package/eslint-config-semistandard
  - eslint-config-standard - https://www.npmjs.com/package/eslint-config-standard
  - eslint-config-prettier - https://github.com/prettier/prettier-eslint

  with a complete list available through this query: https://www.npmjs.com/search?q=eslint-config-&ranking=popularity

- Integrate eslint into your package.json so that it runs before scripts. For example:

  ```json
    "scripts": {
        "pretest": "eslint --ignore-path .gitignore ."
    }
  ```

- set your project to extend your chosen eslint-config-X by populating an eslintrc.json file:

  ```
    echo '{"extends": "X"}' > .eslintrc.json
  ```

  substituting X with your chosen config. You can also get started by running `npx eslint --init` which
  will ask you a number of interactive questions and then create your `.eslintrc.json` file and add
  the required dependencies into your package.json.

- Ensure you have a gitignore file so derived files do not get linted. A minimal one can be
  created with:

  ```shell
  echo node_modules/ >> .gitignore
  ```

  Some additional useful suggestions are available in this
  [article](https://medium.com/the-node-js-collection/why-and-how-to-use-eslint-in-your-project-742d0bc61ed7).

- When adopting a pre-existing shareable config it is important to understand that these
  configs can change over time. Include time in your regular workflow to review these changes
  and update your code base appropriately.

- Configure hooks to run eslint before committing code, but ensure that this pre-commit check does not take too long to execute which may cause complaints from developers.

  - Use [husky](https://github.com/typicode/husky) to configure scripts to run before git commits and git pushes.
    - These checks can be skipped by a developer when needed via `git commit --no-verify`
  - Use [lint-staged](https://github.com/okonet/lint-staged) to reduce amount of code to be linted. This speeds up linting step before commit/push.
    These can be integrated into package.json as follows:

  ```json
  "lint-staged": {
    "**/*.js": "eslint"
  },
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged"
    }
  }
  ```

- Always ensure CI/CD is running linting regardless of hooks.

## Further Reading

[Introduction to the Node.js reference architecture: Code Consistency](https://developers.redhat.com/articles/2021/05/17/introduction-nodejs-reference-architecture-part-3-code-consistency)
