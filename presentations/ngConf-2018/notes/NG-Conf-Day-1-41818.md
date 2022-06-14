# NG Conf - Day 1 - 4/18/18

# Keynote - Angular Values

Reviewed reasons for using Angular, and what is coming up in v6. 

## Reasons for using Angular

**Community**

- Users: 1.25M devs monthly | 800 meet-ups
- Design Systems / Design at scale (Clarity Design System)
- 3rd party Libraries

**Developers**

- Angular Core Support Changes:
  - AngularJS 1/30/18 - 1/30/21 (long term support)
  - Angular ~ one year of LTS per major version.  Means we need to upgrade quickly!
  - Angular v6 - May Release: 
    - aligns CLI, Material, and Angular Core major version numbers
# Angular 6 Updates
## CLI

Tree shakable providers - Only download the services you need.
Schematics - allow you to "do things" to your angular project:

- generate, new, update, add
  - *update* - single command to update dependencies, APIs, RxJS, Material
    - Vendors will be able to publish schematics for their own projects.
  - *add* - instant code and library scaffolding
    - Ex: Material, Elements, PWA, bootstrap, clarity, nativescript
      - ng add @angular/pwa
      - also adds ‘generate’ schematics 
  - *generate* - updates to this schematic
    - goal is to make universal libraries easier to build: project scaffolding, test, build system
## Angular Elements
- embedable Angular javascript component - can use in other frameworks (vue, react, etc…)
## Material Design

Focus on component dev kit to make animations better.  Also working on speed as a UX Feature (Server side rendering, and PWAs for speed).

# Ivy Render Engine

This is a new (backwards compatible) rendering engine for Angular, still in WIP (not even in beta yet).  It is faster and the tree-shaking is intelligent (not static).  This results in no-longer needing to worry about AOT or JIT. Features:

## Locality
  - Modules ship using only AOT, in a single file.
  - Strips out a lot of the meta data files, resulting in faster compile times
## TreeShaking

This is the biggest benefit of Ivy, the rendering pipeline removes two steps and using "instructions" to building the DOM, rather than the template data interpreter (i.e. actually reads the code vs. static analysis).  This removes imports that are never used, even if they are referenced in the code.

----------

*Ex: will remove "test2" function from code base*
*function test2() {}*
*function test(x) {*

  *if (x=1) {test2()}*

*}*

----------

**Additional Benefits**

  - Stack trace is much more accurate, and identifies the issue.
  - Break-points in how Angular is going to actually run through the code.
  - The build size is insanely small! Compressed → 36K today, 7.3Kb, 2.7Kb

**Status:** https://github.com/angular/angular/blob/master/packages/core/src/render3/STATUS.md

# SEO & Angular

Gave recommendations on how to make your Angular App more SEO friendly.  In general, treat crawlers like a human users and make your application accessible. App SEO considerations:

## Think about URLs
  1. Every piece of content should have a URL identifier
  2. Links - avoid onclick and imperative navigation
  3. Robots.txt
    1. Blacklist url patterns
    2. exclude test and archive sites from index
    3. use carefully
    4. don’t block javasript, assets, or data API URLs
  4. sitemap.xml
    1. guidance for search crawlers
    2. at minimum add entries for static urls and routes
    3. Deprecate URLs via redirects
    4. Remove once not significant entry-points
## Pick your SEO strategy
  1. effort vs. reward
    1. Hope (bad), client-side SEO (better), server-side SEO (best), Magic (very good)
  2. Factors
    1. audience - how important is it?
    2. resources - how much can you invest?
    3. extras - summary & preview cards (vendor specific)
## Tools
  1. Google Search Console
  2. Fetch as Google - how search engines see the site.
  3. Google Analytics - user patterns
## Client Side
  1. Googlebot - based on Chrome41
  2. polyfills - help the old crawlers
  3. 500s - setup loging & alerts, consider adding "noindex" to the error pages.
  4. 404s - use noindex meta tag.  (see slides)
## Sustaining your success
  1. Monitoring - review to see trends
  2. Logging - capture user agent info
  3. Alerting
    1. Google Alert Search console.  
    2. Google Analytics also has alerts
## SEO-ing your Angular App
  1. ng add @angular/seo
  2. coming with Angular6.
  3. looking for contributors

# Security
- Keeping UpToDate
  - 0 Day Exploit = unknown, Exploit = known
  - Exploit DB to lookup issues
  - #1 security is to keep application up-to-date
  - nsp (npm package)- checks for vulnerabilities
- Searching for bugs
  - Typically caused by very small issues
- Package hacking
  - cross-env vs. crossenv
  - installing from npm = allowing others to run code on the code base
  - people tend to be too trusting of open source
  - solutions: 
    - @scope/package-name = only allows people to load who own the name
    - package-name 
- @jawache

# Change Detection

Putting a function in the UI makes angular call it to see if it changed
Changing a function to a pipe fixes this.  Page uses a cached output.
Pipe: Primitives and Object

- does not do deep change detection
- keep pipes as primitive as possible

# Animations

[@fade]="state" - can be related to a click event.  Take a look at these slides / gitHub

# Docker

Build Docker Image → Run in Docker Container
Docker extensions in VSCode
codewithdan.me/ng-docker-in-5

# Grid

"do for a living what you got in-trouble for as a kid"

# Angular CDK

**New in v6 Material CDK**

- New schematics, allowing devs to use pre-made templates easily.
  - ng add @angular/material → adds theme file, icon-fonts, Animation Module
  - ng generate @angular/material:materialNav —name=main-nav → injects the code into your new component.
  - ng generate @angular/material:material-table —name=main-table → injects a ton of code (class and template)
- New Tree component - **Full talk on Friday**
  - *might be good for folders in Advanced Reporting*
  - can do badges - this also might be awesome for *Advanced Reporting*
  - data table - expandable rows, but is difficult…
- Flexible overlays: handles scrolling effects for long content
- Badges
- Bottom Sheets


# SwitchMap

Rather then using two "maps" for multiple observables, which would result in multiple subscriptions, switchMap will replace an existing observable with a new one.
hotFrameworkTweets.pipe(

  map(frameworkTweet => getAgency(frameworkTweet) ),
  switchMap(agency => agency.getRecruitsObservable() ) 

).subscribe(res => console.log(res));

# Google Cloud

Data Loss Prevention API (DLP)

- Nice way to automatically remove sensitive information in your system.

Auto ML Vision API - image learning

- Upload images, train, deploy, and generate predictions

BigQuery

- Use SQL to search HUGE amounts of data
- RDBMS - managed.   Queried all of GitHub for package.json and inside what is the top npm dependency in about 

Serverless - worth a look.

# Angular Modules
- No dynamic components encapsulation
- No modules hierarchy
- Eager is the same as lazy

Angular only creates factors for compiled modules (not imported ones).  All of these are put into one factory with one injector.  This is the reason it can’t be dynamic, it needs to know during compile time.
**DOM manipulation talk tomorrow**

# Angular Elements
## **Web Components**

Set of web platform APIs for reusable custom elements.  Custom elements are something like <hello></hello>.  
Allows you to add the component in real time (document.createElement(‘hello-world’);
**Injectors:**
Platform Injector, Module Injector, Component Injector, Element Injector.

  - These injectors need to be done ahead of time because there is no other opportunity since a custom element is dynamically added to the DOM.

**Content Projection:**  Works as expected, but it needs to be done when the page renders for the first time.  This is for <ng-content>.

**Shadow DOM:** Slots = native version of ViewEncapsulation.  <slot name="main">some content</slot>

**Use Cases:** 

1. Elements in apps.  dynamic components, angular.io - CMS, SSR / Hybrid Rendering
  1. Allows devs to just drop the element on the page, it will boot itself up.
  2. next.angular.io - custom elements library for angular.io
2. Element Containers
  1. mini-apps, micro-front-ends, ngUpgrade, sharepoint
3. Re-useable Widgets
  1. Cross Framework Compatibility
  2. Material / CDK Components in any environment
  3. Design Systems - build once, use anywhere.

**Elements + Ivy**: 
Could allow a simple declaration when creating the component.
Polyfill back to IE9.
**6.0 Release** - this will be part of the next release.  createCustomElement.

# MultiPlatform Angular Apps

Platform Super Powers:  AMP, Service Workers, Native
**xplat** 

- build on top of Nrwl → Nx Workspace
- Micro-target apps
- Platform-agnostic libs
- Platform-specific xplat

SketchPoints.io → Angular codebase on all platforms
xplat directory allows you to put in specific components for the platform
into a new Nx Workspace → npm i @nstudio/schematics —save-dev 
ng g xplat —prefix=foo
ng g app.nativescript name —prefix=foo
ng g mode web / ng g mode nativescript → allows you to focus on a specific platform.
example → github.com/nstudio/xplat-sample

# Testing Best Practices for Angular Apps

Why do we write tests?  Makes the developer’s life easier.
Unit Tests:

- Testing isolated small pieces of code
- Most should be unit tests
- Async tests - Promise (microtask), Timer, XHR (HttpClient)
- Promise:
  - Tests can complete too early.  Use "done();"
  - done(); can’t handle errors
  - use async await
    - it("", async() => {});  await fixture.whenStable();
- Timer
  - Debounce: fakeAsync
  - Everything is synchronous in fakeAsync zone. 
    - if("fke", fakeAsync() =>
- XHR
  - Jasmine spyOn
  - Better: HttpTestingController
- async/await → need to move here.
  - // disable the deprecated async method?
## Future

AOT Test - use aot mode in unit test, much faster.
Component harness - page object framework for components.  Shared between unit tests and e2e tests.

# Notes
## Slides

link unavailable, `confsnap` is no longer in operation
https://github.com/DanWahlin/Angular-Docker-Microservices
http://g.co/ng/seo-talk
https://oasisdigital.com/
http://hiRes.io????

## Items to followup on
- HTML5 web speech recognition API → SpeechRecognition();
- https://www.producthunt.com/
- blog.angularindepth.com
- Clarity - free
- Google API Explorer - https://developers.google.com/apis-explorer
- Nrwl - capital one is working with them…
  - Spoke with them, might be well worth looking into.
- VSCode Code Snippets
- Adventures in Angular Podcast
- ngrx-data: no longer have to write actions/reducers/selectors again….
  - https://github.com/johnpapa/angular-ngrx-data
- StackBlitz
  - Instant edit and run apps, Faster than NPM
  - bookmarklet: ng-now
- CSS "games"
  - Grid Critters - gridcritters.com
  - Flexbox Zombies
- Ivy
  - https://github.com/angular/angular/blob/master/packages/core/src/render3/STATUS.md

