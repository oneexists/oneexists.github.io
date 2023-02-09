---
layout: post
title: "Creating a Readme"
author: skylar_lynner
categories: [ documentation, readme ]
---

When creating a new application, it is all too tempting to jump into development.
The planning stage is often an afterthought as it is easy to get started building
parts of the project that appear to be simple enough to get started on right away.
It is also difficult to feel that progress is being made if there is a significant
overhead in the planning stage before any code is actually written.

Thankfully, with some practice, it can become easier to build the planning stage
into a regular routine to create a balanced and more Agile approach. This can
allow for a Readme document to naturally grow with the project and continue to
be updated as changes are made. Taking the time to plan the project through the
creation of a Readme document helps guide the planning stage while also creating a
central location for project knowledge.

The documentation can be divided into three areas to be written alongside the
development process. This will provide enough information to allow the Readme
document to become a source for others to learn about the project while also
providing an organized way to document any problem solving and resources used.
The motivations behind these three areas of documentation can be summarized as:
providing an introduction to the project, guides for setup and use, and creating
a software specification document.

## Writing an Introduction

The introduction to the project can become the homepage of the project. It can
be quickly created at the root folder of the project, which will allow it to be
easily identified and if the project is shared to GitHub, it will be displayed on
the project's main page.

The first part of this document can describe the business case and project
vision. This will be the area where it justifies its existence by answering
what problems it can solve, defining a vision statement and providing a brief
overview with any relevant background information. The purpose of this section is to
sell the project and define its impact. Taking the time to start this early
on as one of the first tasks in building the project will help identify the
use cases, break down problem sets and identify the core functionality to be
built.

This section of the document can be outlined with some links to the rest of
the documentation and links to technologies being used as they are identified.
As the use cases are developed, sections can be flushed out or added to showcase
the application in action. This will help to review and identify some of the
core functionality or areas that could be highlighted to show the project in
action. This addition will give a visual overview of the project through either
screenshots or links to video demonstrations.

## Guides

Providing instructions for setting up the project may not serve much of a
purpose early on, but providing this section of the documentation allows for
others to be able to become more familiar with the project as it is built.
This will help with identifying any areas where the process can be simplified,
provide a central location for introducing how technologies are used and
creating a list of links to learning resources.

After the setup instructions, it may be useful to provide an overview of how
the application may be used, such as any API endpoints to be aware of.
Reviewing the use cases being identified through the creation of the project
can be helpful in guiding this section to allow it to demonstrate the
implementation of solutions the project provides.

## Software Specification

This section of the documentation can be home to the technical aspects of the
implementation of the application. As the use cases and requirements are
identified, they can be documented in a few different sections. Providing
functional and non-functional requirements will provide a technical overview
of the problems being solved as development progresses. The non-functional
requirements can identify the user interface and user experience considerations
being made to add value to the project.

Another area of concern that can be addressed in this section of the documentation
can be the process analysis and target process of the project. Creating these
sections and maintaining them will aide in documenting the process of building
the project, communicate any concerns or problems addressed, along with creating
an easy to digest section for the goals of the project in future development.

As the project grows, diagrams may be written to document design decisions being
made or problem solving that has taken place. This is another area that can be
addressed within the specification. Creating a central place to find all the
diagrams being built gives those who are interested in the design choices being
made an easy point of reference while also enhancing the ability of others to
understand the layout of the project. These documents could include any class
diagrams, sequence diagrams, or even state machine diagrams. Keeping them together
with the specification allows for a visual representation of the problems being
solved to appear alongside the descriptions of the process to identify and
solve them.

## Creating the Documentation Process

Following an iterative design approach, such as that proposed by Agile development,
will create a framework to start tackling the documentation process as a tool for
designing the project being built. The intentional creation of habits within
development will help keep the documentation up to date and reduce the overhead of
the planning process, especially in the early stages of development.

Some proposed triggers to build this habit is to identify areas where learning
resources are documented and adding those resources to their respective sections
of the documentation as they are used in development. Building a routine of
adding to the process analysis will help build a location for others to learn
about the decisions being made when making design decisions and solving problems.
Using the target process as a living list will create a section of the documentation
that will give the satisfaction of crossing items off of a to-do list and moving
them into the requirements section of the documentation while also encouraging
additions to any future goals in development.

A general guide to keeping the documentation in mind while developing is to make
it a goal to identify an area of the documentation that can be improved, updated
or expanded with each contribution to the project. Taking the time to reflect on
what problems are solved with each piece of code added to the project can answer
questions about what to contribute and taking the time to regularly review the
documentation at every contribution will help with identifying other areas that
may have fallen out of date or could be expanded upon. Creating a list of items
to regularly review as a reflection point can help guide the process, such as
identifying areas of development and how they relate to the different sections of
the documentation.

## Proposed Structure of the Readme Document

- Introduction
  - Business Case and Project Vision Statement
  - Links to Documentation Pages or Sections
  - Technologies
  - Screenshots or Videos of Core/Featured Functionality
- Guides
  - Setup Instructions
  - Technology Guides, Links to Relevant Documentation
  - API Endpoint Documentation
  - Use Case Implementation Guides
- Software Specification
  - Functional Requirements
  - Non-Functional Requirements
    - User Interface Requirements
    - User Experience Requirements
  - Process Analysis
  - Target Process
  - Diagram Documentation
