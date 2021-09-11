# Component-based architecture

The deconstruction of the design into discrete functional or logical components that represent well-defined communication interfaces comprising methods, events, and characteristics is the focus of component-based architecture. It gives the problem a higher degree of abstraction and divides it into sub-problems, each with its own set of component divisions.

The major goal of component-based architecture is to ensure that components can be reused. A component is a reusable and self-deployable binary unit that encapsulates the functionality and behaviors of a software element. Component frameworks such as COM/DCOM, JavaBean, EJB, CORBA,.NET, web services, and grid services are all common. Graphic JavaBean components, MS ActiveX components, and COM components, all of which can be reused by simply dragging and dropping, are commonly utilized in local desktop GUI program design.

The advantages of component-oriented software architecture over standard object-oriented approaches include :

+ Reduced time in market and the development cost by reusing existing components.
+ Increased reliability with the reuse of the existing components.

## What is a Component?

A component is a well-defined set of modular, portable, replaceable, and reusable functionality that encapsulates and exports its implementation as a higher-level interface.

A component is a software object that encapsulates specific functionality or a group of functionalities and is designed to interact with other components. It has a clearly defined interface and follows a specified behavior that other components in an architecture should follow.

Only a software component with a contractually stated interface and explicit context dependencies can be defined as a unit of composition. In other words, a software component can be deployed independently and is subject to third-party composition.

### A Component's Views

An object-oriented view, a conventional view, and a process-related view are all possible views for a component.

#### Object-oriented view

A component can be thought of as a collection of one or more collaborating classes. Each issue domain (analysis) and infrastructure (design) class is described in detail to identify all features and procedures that pertain to its implementation. It also entails the creation of interfaces that allow classes to interact and collaborate.

#### Conventional view

It is considered as a program's functional element or module that combines processing logic, internal data structures required to accomplish the processing logic, and an interface that allows the component to be invoked and data provided to it.

#### Process-related view

Instead of generating each component from scratch, the system in this approach builds from a library of existing components. Components are chosen from the library and utilized to populate the program architecture as it is developed.

+ Grids, buttons referred to as controls, and utility components are examples of user interface (UI) components that offer a subset of functionalities required by other components.

+ Components that are resource intensive, not regularly accessible, and must be triggered utilizing the just-in-time (JIT) technique are also common.

+ Many components, such as Enterprise JavaBean (EJB),.NET components, and CORBA components, that are distributed in enterprise business systems and internet web applications are invisible.

### Characteristics of Components

+ Reusability − Components are usually designed to be reused in different situations in different applications. However, some components may be designed for a specific task.

+ Replaceable − Components may be freely substituted with other similar components.

+ Not context specific − Components are designed to operate in different environments and contexts.

+ Extensible − A component can be extended from existing components to provide new behavior.

+ Encapsulated − A A component depicts the interfaces, which allow the caller to use its functionality, and do not expose details of the internal processes or any internal variables or state.

+ Independent − Components are designed to have minimal dependencies on other components.

#### Principles of Component−Based Design

A component-level design can be represented by using some intermediary representation (e.g. graphical, tabular, or text-based) that can be translated into source code. The design of data structures, interfaces, and algorithms should conform to well-established guidelines to help us avoid the introduction of errors.

+ The software system is decomposed into reusable, cohesive, and encapsulated component units.

+ Each component has its own interface that specifies required ports and provided ports; each component hides its detailed implementation.

+ A component should be extended without the need to make internal code or design modifications to the existing parts of the component.

+ Depend on abstractions component do not depend on other concrete components, which increase difficulty in expendability.

+ Connectors connected components, specifying and ruling the interaction among components. The interaction type is specified by the interfaces of the components.

+ Components interaction can take the form of method invocations, asynchronous invocations, broadcasting, message driven interactions, data stream communications, and other protocol specific interactions.

+ For a server class, specialized interfaces should be created to serve major categories of clients. Only those operations that are relevant to a particular category of clients should be specified in the interface.

+ A component can extend to other components and still offer its own extension points. It is the concept of plug-in based architecture. This allows a plugin to offer another plugin API.

