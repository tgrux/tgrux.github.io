# NG Conf - Day 2 - 4/19/18

# Reactive Testing Strategies with NgRx

*Grand Ballroom A/D*

## Testing Tools

**JEST**
Test Runner.  Benefits: 

- Easy to setup and configure
- VERY fast
- Snapshot testing - lets you automate creating assertions.
  - expect(state).toMatchShapshot().
  - writes out a good snapshot to GIT
  - Cons:
    - Trust, but verify snapshots.
    - No way to log that the snapshots were verified 
- VSCode plugin snapshottools

Setup:

- npm install jest-preset-angular
  - package.json using configuration
- VERY nice output :)

**Jasmine Marbles**

- Visual testing for observables
- Express time and sequencing elegantly
- Assert behaviors of streams

“-” equals 10sec of time, “a” = emit, “|” complete, “#” is an error.
ex: 
-------- = observable.never
---(ab)--| = 30ms, emit a&b, 20ms, complete.
.flush() = runs the sequence.  → always flush at the end of the test.
Schedulers perform tasks on a schedule. ex: interval(17).subscrive(i=> console.log(i));
Setup:

- jasmine-marbles

**Angular Testing Library**

- Create component fixtures quickly
- Magically mock out dependencies
- Snapshot test Angular components

TestBed.configureTestingModule({

  imports: [
    NoopAnimationsModule ← disables animations
  ],
  …

})
createComponentFixture ← similar to the test bed.

## Examples

Ngrx Sample Book App

## TESTING Presentational & Smart Components

Functional Purity: Only depends on input and has an output.  Does not depend on anything else.  

## Reducers

Need to be pure function.
Good reducer always outputs the same thing, never depends on anything else.


## Side Effects

verify: for a given input, it is going to initialize an effect.
provideMagialMock(GoogleBooksService) ← looks at the service and provides mocks for it automatically.

Simple doesn’t need marbles.  More complex does.

## Selectors

Need to be pure function.
There are two types, “getters” and “derivers”

**Getters** are easy to test
const result = fromBooks.getAllBooks(initalState);
expect(result.length).toBe(2);

using the projector function
const result = fromBooks.getAllBooks.projector(

  state…,
  state…

);

**Derivers** are harder to test

## Components

Leverage snapshot tests, crazy easy!!!

1. create component fixture
2. beforeEach: async() + await fixture.compile({book});
3. Should Compile: expect(fixture).toMatchSnapshot();
## Container Tests

The same as testing a component.

----------
# NgRx Schematics

@angular-devkit/schematics - @angular-devkit/schematics/cli
@ngrx/schematics → Nrwl team
Ex:
ng g feature heroes/Heroes —reducers=../reducers/index.ts

## Extend Schematics

@angular-devkit/schemtics-cli
schematics schematic —name=featch-actions
@ngrx/schematics
Rule Factory → function that returns how to change the filesystem.
fetch-actions, files, __path__ → ?

----------
# Complex Forms Build Character

this.fb.group({
test: [{value: “test”, disabled: true}]
});
formGroupName has to be an index.

She built a custom class that generates formControls.
**Publish / Subscribe pattern (pubSub)**


- Create a custom class for nested form groups
- Publish-Subscribe Pattern - eliminates that need for event emitters.  I’m kind of doing that, but not in such an organized way.

Code → https://github.com/nscarlyon/dnd
natasha.carlyon@greatersum.com

----------
# Ngrx Complex Form

**Container Presentation**

- Container - how things work.  Loading and Dispatching
- Presentation - presenting the data, how things work, but doesn’t deal with observables.

Container → Input/Output ← Presentation

**NgRx Entity**
How to normalize data. (see slide)
Don’t do nested data, it forces a re-render.   Use the entity library to fix this.

Container gets data → Presentation patches values onto formGroup → Value Changes → Emit Event back to → Back to Container → Container decides when to add to store.


- holding the data in the *container* prevents unsaved data from going to the store.
- Container has action and selector
- Presentation:  builds form and Output (Event Emitter) back to container

**Take aways**

- Create models to combine entities
- Really understand the Container/Presentation Patter (smart / dumb component)
- Understand NgRx Forms Basics
- NgRx makes complex forms easy
- Doesn’t really need NgRx, you can do this with a *container* connecting directly to the service.
- State to store: allows you to recreate a situation based on the sate.  It should be deterministic.
  - Entity State → 
  - App State → login info
  - UI State → current page

http://confsnap.com/#/event/ng-conf-18/131

----------
# Reducing the Boilerplate with NgRx

Actions and reducers are not boilerplate (they are explicitness).

- *actions* describe uniqe events
- *reducers* are where business logic happens

Boilerplate:

- connecting reducers to the store
- registering effects
- handling common state shapes
## What state belongs in the store: SHARI

**S**hared - shared state is accessed by many components and services
**H**ydrated - state that is persisted and hydrated from storage
**A**vailable - state that needs to be available when re-entering routes
**R**etrieved - State that needs to be retrieved with a side effect
**I**mpacted - state that is impacted by actions from other sources

## What doesn’t belong in the store
- Forms: full of stateful information.
  - Keep unserialized state out of the Store.  
- Data that can’t be serialized.
- State that is solely owned by a component doesn’t belong in the store.
## Schematics

NgRx Schematics works with the CLI.
Blueprints that make it very easy to use.

## State Management Blueprints
- Store
- Actions
- Reducers
- Effects
## Feature Management Blueprints
- Entity - generate a collection for common shapes
- Feature - generates action, reducer, effect
- Container - hooks up a component to the store.  Should be used with a presentation component.
## Boilerplate
- Registering Feature States
- Wire up Effects
- Integration with ngModules

@ngrx-store-devTools

## Entity
- Helpers to manage collections
- Provides set of the functions for CRUD operations
- Extendable

**Collections**

- How many T are in the collection
- Give me one T at a time
- Give me all T
- Reducer<Collection<T>>

EntityState<Entity> {

  ids: string[];
  entitles: { [id: string]: Entity };

}
look up can be done just by the ID.
const adapter = createEntityAdapter({

  selectId: (entity: Entity) => entity._id,
  sortComparer: () => a.name.localeCompare(b.name)

});
const initalState: State = … adapter?

!!! → adapter.createSeletors();


## Future of NgRx
- TypeScript 2.8
- Add/Update using the Angular CLI
- NgRx Data is becoming an official NgRx package


## Entity State

Zero Ngrx Boilerplate
NgRx Data Module ← Awesome!  

----------
# Advancing Unit Tests
## TDD
- Requirements → specific test cases → Software dev to pass those tests.
  - You should be writing one test, write code to pass, then repeat.

WTF…


## Building awesome components with the power of the Angular Component Dev Kit
----------
# CDK Example

https://github.com/EladBezalel/ngconf-cdk-workshop

----------
# NgRx Mobile with Ionic

NgRx Mobile: 

- Simplify our application
- Container/Presentation
- Easier to handle data as it shows up

Create Ionic app as usual

- Integrate angular-cli
- NgRx Schematics
- Use path aliases
- “ionic start myApp”
- Copy an existing .angular-cli.json file
  - rename the project
  - install angular-cli
  - install ngrx
  - install store freeze
    - npm i @ngrx/store-devtools ngrx-store-freeze --save-dev
    - this helps with debugging
- Configure Schematics
  - ng set defaults.schematics.collection=@nrgx/schematics
- Path Aliases
  - tsconfig.json → paths
  - webpack.config.js
    - useDefaultConfig[env].resolve
- Install JEST for unit test supports
  - npm i jest-presets-angular --save-dev ← everything you need for JEST
  - jest.config.js
    - module.exports = {…} (see slides)
  - setup-jest.ts
    - see slides
- generate entity, component, or pages
  - component is a subset of a page
## Detecting Changes on a Form

this.customerForm.valueChanges.pipe(takeWhile(() => this.alive), skip(1), debounceTime(500)).subscribe

## Plugins
- You can use NgRx for plugins as well.  
  - Example, camera get picture success / fail
    - Effect will watch for anytime a picture is requested and handle it correctly
  - Example, geolocation success / fail
    - Store contains the location
    - Effect will 
----------
# “Containerizing” Angular with Docker
## Containers
- Docker provides an easy way for building, shipping, running apps
- Docker CE - alpine linux
- Image = read only template
- Container = Read / Write
- DockerFile → docker build → Docker Image → push somewhere
## Steps to start
- Install Docker CE
- Create a custom Dockerfile (if needed) or pull image.
- Run Docker client commands to build images and run containers
- “docker pull nginx:alpine”
- “docker run -d -p 8080:80 nginx:alpine”
  - -d = detached mode
  - -p = open port 8080 → forward to 80 (external port → internal port)
- “docker ps -a”
  - Shows all containers that are running
- “docker stop {id}” 
  - Stops the container
  - The ID echoed back is a good thing.
## Steps to Run Angular in a Container
- Dockerfile → build → Docker Image → run
- docker run -d -p 8080:80 -v $(pwd)/dist:/usr/share/nginx/html nginx:alpine
  - $(pwd) = working directory
  - ng build -dop false
    - this allows us to keep the dist folder, as opposed to removing the folder.
    - dop = delete output path
## Building a Custom Image

docker build -t DanWahlin/ngapp:1.0.0 .

  repository, image, location

docker run -d -p 8080:80 danwhalin
Containers can be used to build automate Angular builds locally or on a CI/CD.

## Multi-Stage Dockerfiles

Allows you to have multiple containers build that depend on each other.
Dockerfile → Build Angular → Node.js image → copy dis → Docker Image

## Docker Compose

Orchestrates spinning up many images.
docker-compose.yml is used to do this.
docker-compose build | docker-compose up
Sea Advisor = easy way to monitor containers

**Pushing a docker image**
docker push → repository (local or URL)

Azure for containers.  


----------
# Customizing your Angular build with Bazel

https://bazel.build
Google’s build tool

## Benefits of Bazel
- Fast at Scale
- Full-Stack
- Customizable
  - Inputs files, structure of application, not “how”
  - Configure local to sources

**To customize**

- Structure of the app
- Paths for output
- Plugins for the languages and tools
- Configuration 

CLI support for multiple build tools

## Bazel rules
- Rulses perform build steps/actions
- Chained together
- Abstract complexities
- Input file → action → output file
## Incremental Builds
- Depends on the size of the change, not the size of the app

**Roadmap:**
Now via AngularLabs
This Year: Ergonomics, Performance, Code-splitting
Later → converge with Angular CLI

http://g.co/ng/abc
http://g.co/ng/abc
http://github.com/alexeagle/angular-bazel-example
http://github.com/alexeagle/angular-bazel-example/wiki


----------
# Follow-up

Container Presentation
https://github.com/ngrx/platform
https://medium.com/ngrx/introducing-ngrx-entity-598176456e15
http://blog.codewithdan.com
http://codewithdan.me/ng-containers
https://store.docker.com/editions/community/docker-ce-desktop-mac
.pipe() 
.alive()
@ngrx/entity
ngrx dev tools - Schematics
this.store.pipe(select(…));
http://confsnap.com/#/event/ng-conf-18/131
https://github.com/ngrx/platform/blob/master/example-app/app/books/reducers/books.spec.ts


----------


- 5:30 - 5:50: 
  - Customizing your Angular build with Bazel
  - Grand Ballroom C
- 6 - 8 
  - ng-Hackathon
  - Grand Ballroom A/D
- 7pm Meetup on 3rd floor in Belvedere Room



