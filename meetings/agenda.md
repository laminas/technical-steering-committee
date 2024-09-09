# Next Technical Steering Committee Meeting Agenda

- Date: 2024-09-09
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to Discuss

### Laminas Ecosystem
   We should discuss in more details this [RFC](https://github.com/laminas/getlaminas.org/issues/199).
   
   The purpose is to create a curated section in getlaminas.org website, where we collect and display various 3rd party libraries, ready to be used in or with Laminas, Laminas MVC, Mezzio.
   
   [@gsteel](https://github.com/gsteel) proposed to host a JSON file , and authors can publish their packages by PR.
   
   From that JSON file, we can display the content in getlaminas.org website in various ways(filter, search, sections). 
   
   Potential categories (tags): middleware, wrappers(hooks?),  MVC.

   Acceptance criteria:
   - _must_ be installable via `composer`
   - _must_ use a `ConfigProvider` and/or a `Module`
   - _must_ provide a license
   - _must_ not be archived or outdated
   

### Proposal for new Maintainers

[@arhimede](https://github.com/arhimede) is proposing as maintainers the below:
 - [Claudiu Pintiuta](https://github.com/cPintiuta), more details in this [issue](https://github.com/laminas/technical-steering-committee/issues/190)
 - [Alexis Karajos](https://github.com/alexmerlin) for other packages where help is needed.
     Below are his merged PR's for mezzio-session:
    - https://github.com/mezzio/mezzio-session/pull/61
    - https://github.com/mezzio/mezzio-session/pull/63
    - https://github.com/mezzio/mezzio-session/pull/71
   
     One PR which is not merged yet, but worth to be mentioned since it was a lot of discussions around it : https://github.com/laminas/laminas-config-aggregator/pull/47

### Clarify maintainer's duties 
  Continue the discussion around this [draft PR](https://github.com/laminas/technical-steering-committee/pull/193)

### Presentations (slideshow) 
 The purpose is to allow us to create **official** presentations , to be used on various conferences, user groups, ad-hoc presentation , related to Laminas project. 
 And most important, to be able to collect feedback before a presentation is published. The so-called **PR dance**.
 
 First presentation we may want to create is "What is Laminas Project", and to be presented at 2 separate events: WEUC 2024, and Unkonf 2024 Mannheim.
 
 At Dotkernel we created a proof of concept, and *we want to copy the same setup in a repository under Laminas Org on github*. 
 - a repository: https://github.com/dotkernel/presentation , containing mostly RevealJS library
 - If you want to create a new presentation for a certain event, then create a new folder:  * /presentations/new-subject/event-year/*
 - If you to customize an existing presentation for a *different* event, then create a new folder:  * /presentations/new-subject/another-event-year/*
 - a subdomain need to be used as Github pages , like in example below
 - github action to build the pages

The end result will be like below:

[Index page, with all presentations listed](https://show.dotkernel.org/)

[Mannheim 2024 What is Laminas Project](https://show.dotkernel.org/presentations/what-is-laminas-project/mannheim-2024/)
   
   
 
 

   
   
