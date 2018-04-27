# NgConf - Day 3 - 4/20/18

# Day 3 Keynote
## Top 10 "Should I Use X"
## Should I use "Angular"?
  1. Opinionated - puts the developers on "rails"
  2. Trustworthy
    1. Work very hard for developers to not break releases (back-words compatible) 
    2. Public about what they are doing and stick with it
  3. Familiar
  4. Scaled
    1. This is used at Google, so can handle billions of users.
  5. Ecosystem
    1. Very big community
## Should I use the CLI
  1. Pros:
    1. Scaffolding
    2. Adding capabilities
    3. Building / Serving
    4. Keeping up to date
  2. Cons:
    1. Need full control of application
    2. Webpack, SystemJS, Rollup, PostCSS, Bazel (for now)
## Should I use Universal
  1. Should use universal
    1. Content-first apps
    2. Where SEO is a business-critical need
    3. Many users on mobile, especially low-end devices
  2. Consider it:
    1. Complex public facing apps where first impressions matter.
    2. App Shell pattern makes sense for your app.
    3. As a final performance optimization - *not before lazy-loading and service workers!*
  3. Avoid:
    1. Internal/Intranet
    2. Working with legacy backends
    3. Deploying to Cordova, NativeScript, or Electron
    4. You’re starting out with Angular
## Quick Answers
  1. Unit Tests? - Yes
  2. E2E Tests? - Yes - not as many as unit tests
  3. Reactive forms? - Yes
## Should I build a PWA?
  1. If a more reliable and engaging web experience would be helpful, might be worth it.
  2. Ways to deliver on Mobile
    1. Cordova
    2. NativeScript
    3. Native
    4. PWA
  3. PWA - not all items are in the browser yet
    1. Fingerprint, Contacts, etc…
  4. Also have to deliver a web experience
## Should I use Elements?
  1. Adding interactivity to content-heavy apps
  2. Embedding Rich "mini-apps" into other pages
  3. Advanced dev teams pushing the boundaries
  4. Soon:
    1. Building shareable controls for other environments
    2. Content-first
  5. If your primary use base is IE, performance isn’t great.
## Should I use Material?
  1. If you like the design, use it.
  2. If you don’t, use the CDK (component dev kit)
  3. If you don’t, build your own.
  4. **Have a component library focused team**
    1. Make it awesome to opt-in
    2. Extend the CDK
    3. Open your code to create adoption - allows other teams to contribute
## Animations
  1. More work = More benefit
  2. Benefits:
    1. Responsiveness
    2. Hierarchy - Without this requires a tutorial/training.
      1. Visual indicators help users know where to go.
    3. Status
    4. Branding and delight
    5. Happy employees are 12% more productive
## Should I use NgRx?
  1. Do I need a state management library?
  2. No:
    1. New to Angular
    2. small / simple app
    3. comfortable rolling your own patterns
    4. happy without it!
  3. Yes:
    1. Well Supported
    2. Other Options; Redux, MobX, NGXS
## Should I use payed services?
  1. Your team is moving from a different tech stack
  2. You’re building something specialized or complex.
  3. You want to get a jump start on doing things the right way.


# Ready for Readable Code?

Goal: Fast and effective communication
Productivity over time results in a downwards trend of the ability to change things.
**How to make readable code**

- Start with a style guide
- Meaningful Names that you can be.
- VSCode - extract into a function
- Most important stuff should go first
  - Grouped and sorted - doesn’t need to be consistent, but should be clear.
- Smaller functions are more readable.
- Function should be less than 20 lines of code.
- Fix spelling
- Context === clarity
  - Explain in code, not comments
- Comments must be readable and maintained
  1. Explains "What"
  2. Outdated and incorrect - worse 
  3. Should of done something…

**Use Comments When**
Why, Explaining consequences, API Docs (jsdoc)

**Write dirty code, then clean it up**
Iterate over it.

Writing readable code makes your app easier to maintain.  Tips:

- 5 Sec rule, can you read it
- one thing per file
- small functions
- Well Thought Naming
- Use Comments Wisely
- Craft a Style Guide
- Use Prettier

# The magic of template reference variables

Template reference variable - way to crate a simple reference to get the value of the input.
**Inputs**
<input #phone>
<button (click)="callPhone(phone.value)">
**Components**
<app-hello #helloComp><app-hello>
{{helloComp.name}}
**Forms**
<form #form="ngForm">
Form is valid: {{ form.valid }}
In Component
@ViewChild(‘myForm’) ← gives you reference to the reference variable

# Angular Material’s Trees

http://material-tree-nested.stackblitz.io
Lazy loading of children!
DataSource → Tree Control → Template
This is a part of v6. :(

# Let’s Build A Form Around It

Forms are only "forms" when they don’t work.
**What makes a bad form:**

- Don’t how errors before they happen.
- Doesn’t let me submit if they are doing something wrong.
- Focus only on what the user is currently doing, not other fields.
  - Validate only one field at a time.
- Keep forms very short.
- Only "submit" once.  Tell the user what the error are beforehand.

**Better forms in Angular:**

- Observe - know what is happening with a field
- Empathy - give inputs flexibility, adjust formatting after.
- Compose - reusable
- Extend - allows you to extend your forms.

**Building blocks**

- FormControl
  - Used to bind to individual inputs in template
- FormGroup
  - Works mainly with the HTML "Form" Element
  - Used to aggregate controls
- FormArray
  - Like a FormGroup, but in an array format
  - Can intake any abstract control

**Demo**
http://sign-up-form.stackblitz.io
http://asycnc-validation.stackblitz.io 
http://stackblitz.com/@saniyusuf
http://angular.io/guide/reactive-forms

**Async Validator**
*Used for server call validation*
zipapotimis API for zipcode

# Angular at Large Organizations

Confidence - consistency, safety, maintainability
Why Angular is good for large companies

- No Fragmentation
- Predictable release cycle
- Angular works great with Typescript
## SCM & Dep Mangement

Apps → App-Specific Libraries → Reusable Libraries → 3rd party
Developers should be able to:

- Create app specific libraries
- *See Slides*
## Best Practice vs. Bad Practice
- only run tests against code that has been changed "--untracked"
- npm *yarn dept-graph* allows you to visualize dependencies
## Promote Best Practices Using Tooling

**Typically**

- An out-of-sync wiki page no one reads
- Code reviews that don’t check much

**To Fix**

- schematics
  - data-access-lib
  - yarn workspace-schematic …
  - allows users to have a basic boiler plate
- yarn [dep-graph](https://yarnpkg.com/en/package/dep-graph)
- Create custom schematics
- Create custom lint checks
- Automate everything that can be automated (use Prettier)
- Checklist: https://drive.google.com/drive/folders/13OnVqbFvz-w-dDc2FQ9_Yv2eXmrhBl5X
# Introducing RxJS6!

No-longer use Obeservable.of, import it directly of()
pipe-able operators need to be used.
now in RC, publishing in a few days

## Breaking:
- New unhandled error behavior
  - if error with no handler, it will throw it as an async
  - do not depend on sync errors (try/catch)
    - .subscribe(fn, error, complete)
  - *this is going to break unit tests that have observables throw errors*
- simplified imports
- deprecation
- new operator (not exciting)
- ***Error is on Stack blitz, look at slides***
- config to handle error outputs.  
## Importing
- Importing is MUCH easier, there are only two Ng Devs need to worry about:
  - rxjs
  - rxjs/operators
- Only can import "of" directly, it is no loner available on Observable.of

Deprecating

- result selectors for mergeMap
  - this is replaced by using a .pipe(map(…))
- operator versions of concat, merge, zip
  - use them as static functions

Operator

- throwIfEmpty - if completes without throwing values, it will error out.

Migrate and Update

1. Update to 5.5.10
2. Update to 6.0.0
  1. ng update rxjs
  2. Install rxjs-compat
  3. Update to remove rxjs-compat

*yarn add rxjs-tslint*

- run tslint -fix will fix everything to be 6.0 compliant!  Wooo!
- should be able to remove rxjs-compat at this point

Google is running RxJs6 in prod now.

v7 work is public, much smaller 


# Notes - Take Away
- Learning - http://rxmarbles.com/
- Google: "Do scaleable things"
- Ivy in next 6 months
- Article "Do I need Redux
- Ultimate Angular - course used at Google
- Upgrading AngularJS
- angular.io/resources
- gitter.im/angular/angular
- https://github.com/angular/material2/blob/master/CONTRIBUTING.md - ready the contributing docs.
- Angular Style Guide
- VS Code
  - Angular Essentials Plugin
  - Winter is Coming Theme
- http://blog.angulartraining.com
- https://ui.school/
- Look at Nrwl slides for recommendations
  - https://drive.google.com/drive/folders/13OnVqbFvz-w-dDc2FQ9_Yv2eXmrhBl5X
- https://google.github.io/styleguide/jsguide.html