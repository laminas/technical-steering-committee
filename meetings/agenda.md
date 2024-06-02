# Next Technical Steering Committee Meeting Agenda

- Date: 2024-06-03
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

[Continuation of the May TSC meeting](https://github.com/laminas/technical-steering-committee/blob/main/meetings/minutes/2024-05-06-TSC-Minutes.md)

## Items to Discuss

### Create Media Kit 

- create new logos or improve the current ones , for Laminas and Mezzio
- svg format, various sizes and color
- create few wallpapers
- stickers from stickermule
- banners and badges: "powered by Laminas " , or "powered by Mezzio"
- official banner/seal for  "Official Laminas Commercial Vendor"
- any other ideas related to marketing materials 
  
Responsible: Dotkernel organisation 

Good to have it by: July 2024 TSC meeting 

Where: a Media Kit page on getlaminas.org website 

### getlaminas.org website update 

We need approval for :
- https://github.com/laminas/getlaminas.org/issues/162
- https://github.com/orgs/laminas/projects/23/views/1

Dotkernel organisation want to be involved in this, with Frank Brückner @froschdesign as project lead.

The purpose is to have it ready on a new staging location , by July TSC meeting, for final approval .

### OSS status for packages

  For each package, add a file OSSMETADATA , with possible values 
  - osslifecycle=active
  - osslifecycle=maintenance
  - osslifecycle=archived
and add the badge to readme file
Example:  ![OSS Lifecycle](https://img.shields.io/osslifecycle/dotkernel/api)

#### Note
> Unfortunatelly, for this solution to be in effect,it needs a new release for each package


### Create a status page 
[See this pull request](https://github.com/laminas/technical-steering-committee/pull/175)

For each Github namespaces: laminas-api-tools, laminas, mezzio, and for each package in the namespace:

List all packages and the badge for each ,  with its OSS status : active, maintenance, archived 
