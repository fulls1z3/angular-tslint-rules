# angular-tslint-rules [![npm version](https://badge.fury.io/js/angular-tslint-rules.svg)](https://www.npmjs.com/package/angular-tslint-rules) [![npm downloads](https://img.shields.io/npm/dm/angular-tslint-rules.svg)](https://www.npmjs.com/package/angular-tslint-rules)

Shared [TSLint] & [codelyzer] rules to enforce a consistent code style for [Angular] development

[![CircleCI](https://circleci.com/gh/fulls1z3/angular-tslint-rules.svg?style=svg)](https://circleci.com/gh/fulls1z3/angular-tslint-rules)
[![semantic-release](https://img.shields.io/badge/%20%20%F0%9F%93%A6%F0%9F%9A%80-semantic--release-e10079.svg)](https://github.com/semantic-release/semantic-release)
[![Conventional Commits](https://img.shields.io/badge/Conventional%20Commits-1.0.0-yellow.svg)](https://conventionalcommits.org)
[![Angular Style Guide](https://mgechev.github.io/angular2-style-guide/images/badge.svg)](https://angular.io/styleguide)

> Please support this project by simply putting a Github star. Share this library with friends on Twitter and everywhere else you can.

The value of the software produced is directly affected by the **quality of the codebase**, and not every developer might
- be **aware of the potential pitfalls** of certain constructions in [TypeScript],
- be **introduced into certain conventions** when using the [Angular] framework,
- know that not every developer is as capable in **understanding an elegant** (*but abstract*) **solution** as the original
developer.

For that purpose, we need to use **static code analysis tools** such as [TSLint] and [codelyzer] to check readability, maintainability,
and functionality errors.

Although complying with these tools may seem to appear as **undesired overhead** or may **limit creativity**, it becomes
**easier** for any new developers to **read**, **preventing** a lot of **time/frustration spent** figuring out the structure
and characteristics of the code.

Containing a set of [TSLint] and [codelyzer] rules, **`angular-tslint-rules`** has been compiled using many contributions
from colleagues, commercial/open-source projects and some other sources from the Internet, as well as years of development
using the [Angular] framework.

#### NOTE
All [TSLint] rules covered by this project are explained on this article [https://medium.com/burak-tasci/angular-tslint-rules-a-configuration-preset-for-both-tslint-codelyzer-8b5fa1455908](https://medium.com/burak-tasci/angular-tslint-rules-a-configuration-preset-for-both-tslint-codelyzer-8b5fa1455908), in depth. 

If you have questions, comments or suggestions, just create an issue on this repository. I'll try to revise and republish
these rules with new insights, experiences and remarks in alignment with the updates on [TSLint] and [codelyzer].

## <a name="contributing"></a> Contributing
If you want to file a bug, contribute some code, or improve documentation, please read up on the following contribution guidelines:
- [Issue guidelines](CONTRIBUTING.md#submit)
- [Contributing guidelines](CONTRIBUTING.md)
- [Coding rules](CONTRIBUTING.md#rules)
- [ChangeLog](CHANGELOG.md)

#### Thanks to
- [JetBrains], for their support to this open source project with free [WebStorm] licenses.

## <a name="license"></a> License
The MIT License (MIT)

Copyright (c) 2019 [Burak Tasci]

[TSLint]: https://github.com/palantir/tslint
[codelyzer]: https://github.com/mgechev/codelyzer
[Angular]: https://angular.io
[TypeScript]: https://github.com/Microsoft/TypeScript
[JSDoc]: http://usejsdoc.org
[JetBrains]: https://www.jetbrains.com/community/opensource
[WebStorm]:   https://www.jetbrains.com/webstorm
[Burak Tasci]: https://github.com/fulls1z3
