# Getting Started

> **Helper repository, contains a road-map to develop a quality application.**

## Everything Mandatory

* [TDD (Test Driven Development)](https://en.wikipedia.org/wiki/Test-driven_development)

* [Decent Architecture](https://github.com/FlareCodeflit/Git#flares-app-architecture-proposal)

* [State Management Solution](https://github.com/felangel/bloc)

* [Loose Coupling](https://en.wikipedia.org/wiki/Loose_coupling)


> **A code has to compile, pass unit, integration, performance tests and, pass code review by the programmer himself/herself or other prior developers.**

## Versioning

**{Major}.{Minor}.{Patch}** is **1.0.0**


____



# Flare’s App Architecture Proposal

**Start by dividing every “feature/attribute” of App into layers so that nothing will clutter and only a desired part of the layer will communicate with another layer.**

* **Every feature will be divided into three layers: -**

> 1. **Foundation**
> 2. **Data**
> 3. **Presentation**


## Foundation: -

Foundation layer is the inner layer which shouldn’t be affected by any changes occurs in other two layers. It will contain only the core business logic- Use Cases, business objects– Entities and interface- Repositories. It should be totally independent of every other layer.

* **Foundation layer will be further divided into three sub-categories: -**

> 1. **Entities**
> 2. **Repositories**
> 3. **Use Cases**

**Entities** – Data layer don’t return Entities rather Models. The reason behind this is that transforming raw data into Dart objects requires some conversion code. We don’t want this conversion code inside the foundation layer. Therefore, we create Model to communicate between both layers. These models pass data to Entities which will be further used.

**Repositories** – It contains the interface of the Use Case Implementations (contracts).

**Use Cases** – It encapsulates business logics for all the possibilities for the particular feature (sub-features).

## Data: -

Data layer consists of the Data Sources, Models, and Implementations. It holds all the outer world complications of getting and setting data and returns the clean Data Objects to the foundation layer.

* **Data layer will be further divided into three sub-categories: -**

> 1. **Data Sources**
> 2. **Models**
> 3. **Implementations**

**Data Sources** – Data Sources deals with all the sources of data transactions (API, Database or Local).

**Models** – It holds the logic to manipulate raw data which is coming from the data sources and returns Dart Objects (Entities) to foundation layer.

**Implementations** – All the contracts created inside the repositories must be implemented to complete the cycle between Foundation and Data layer, which should be executed here.

## Presentation: -

Presentation layer doesn’t do much by itself, it handles basic code conversions, inputs and validations. Mostly, it contains the UI.
It consists of presentation logic holders- Bloc, Pages, Widgets.

* **Presentation layer will be further divided into three sub-categories: -**

> 1. **Bloc**
> 2. **Pages**
> 3. **Widgets**

**Bloc** – It contains Streams to manage the app state.

**Pages** – Different pages of App related to feature.

**Widgets** – Reusable code snippets for UI formation.

### Extra*: -
_Features and other Global Objects which may be used throughout the App will be placed inside the core folder inside lib._

_Bloc can either be used for app's state management, or complete implementation of the app._

_Repository in the foundation layer and Implementation in the Data layer both are same also, can be named same. Because repository holds only the contracts for the implementation but we use them in separate layers, because the app should be independent from unpredictable outside world._

_Call Flow in this architecture will starts from the Presentation layer and flow towards the Data layer through our inner core layer (Foundation layer)._

_Data Flow is vice-versa of Call Flow._

_Bloc has a different flow, bloc dispatch events from UI and then return states which will be further used to manage the state in UI. Bloc can be replaced with any other equivalent for app's state management i.e. Inherited Widget, Change Notifier, Redux etc.._

_Interface is a simple abstract class which holds contract for the implementation._

_Entity holds the kind of data/fields which the Model will return._

_Most of the Business Logic gets executed in Use Cases._

_These monstrous separations of layers also help in testing the codes in parts rather than writing the huge test codes, which is also beneficial while applying TDD (Test Driven Development)._

_Functional Programming concepts and equality comparisons help in testing faster and easier._

_Mocking needed for testing without writing concrete implementations of classes._

_Test files always mapped as production files by appending “\_test” as a suffix._