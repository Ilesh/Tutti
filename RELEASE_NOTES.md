# Release Notes

There are no release notes before v`1.2.0`. For these versions, please check the
git tags. Also note that Tutti doesn't use semver. Breaking changes can occur on
minor version bumps, but not on revision bumps.




## 1.2.2

This version migrates `Tutti` to Swift 4.2 and makes it Xcode 10 ready.



## 1.2.1

In this version, the previously `public` standard deferred classes are now `open`
so that you can inherit and them and override their logic in your own projects.



## 1.2.0

This is a pretty big update with some breaking changes. The most important thing
to be aware of, however, is that the decision making of whether or not a hint or
tutorial should be presented has been moved from the presenters to these classes.

This means that presenters are only responsible for the actual presentation from
now on. They do not have any build-in decision making whatsoever. If you now ask
a presenter to present a hint or tutorial, it will do so every time.

This means that if you migrate to `1.2.0`, you must modify your code to call the
`present` function of your hints and tutorials, NOT your presenters. If you keep
using the presenters, your hints and tutorials will always be presented.


### New features

- I have added a new `DeferredOnboarding` protocol. It lets you specify how many
times `present` must be called before a hint or tutorial is actually presented.

- The `Hint` and `Tutorial` protocols have new `present` functions, which should
be used from now on, if you want automated decision making to take place.

- I have added new `DeferredHint` and `DeferredTutorial` protocols, that inherit
the base protocols and `DeferredOnboarding`. I have also added standard deferred
hint and tutorial classes that inherit the standard non-deferred base classes.

- The `Onboarding` protocol has a new `shouldBePresented` prop that indicates if
an onboarding item should be presented or not. It is implemented by the standard
classes and overridden by the new standard deferred classes as well.


### Breaking changes

- The decision whether or not a hint/tutorial should be presented has been moved
from the presenters to the hint and tutorials. You must use the `present` of the
hints and tutorials instead of the presenters from now on.

- The presenter `present` functions don't have return values anymore, since they
will always present the provided hint/tutorial.


### Deprecated members

- The `LocalizedTutorial` class has been deprecated and will be deleted the next
time Tutti is bumped to a new minor version. Instead, use the localization-based
`StandardTutorial` initializer, which does the same thing.