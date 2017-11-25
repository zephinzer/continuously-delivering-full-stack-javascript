---
separator: _____
verticalSeparator: ___
theme: black
revealOptions:
  transition: 'zoom'
  center: false
  controls: true
---

<!-- .slide: class="center" data-background="./front-splash.jpg"  -->
# Continuously Delivering Full-Stack JavaScript

#### IAM: JOSEPH MATTHIAS GOH

___
<!-- .slide: class="center" -->

## about me

<table>
  <tr>
    <td>
      <i class="fa fa-2x fa-info-circle"></i>
    </td>
    <td>
      Software & DevOps Engineer specialising in full-stack web development  
    </td>
  </tr>
  <tr>
    <td>
      <i class="fa fa-2x fa-briefcase"></i>
    </td>
    <td>
      Government Digital Services, GovTech Singapore
    </td>
  </tr>
  <tr>
    <td>
      <i class="fa fa-2x fa-envelope"></i>
    </td>
    <td>
      <i class="fa fa-comment"></i> | <a href="mailto:hello@joeir.net" target="_blank">hello@joeir.net</a>  
      <i class="fa fa-briefcase"></i> | <a href="mailto:joseph_goh@tech.gov.sg" target="_blank">joseph_goh@tech.gov.sg</a>  
      <i class="fa fa-github" style="font-size: 1.18em;"></i> | <a href="https://github.com/zephinzer" target="_blank">zephinzer</a>  
    </td>
  </tr>
</table>


_____
<!-- .slide: class="center" -->

# Overview

___
<!-- .slide: class="center" -->

## what's covered

- deployment-friendly javascript
- reducing time to production
- enabling frequent deployments

___
<!-- .slide: class="center" -->

## content

- background & premise
- codebase management
- development
- build process
- testing
- releasing
- runtime

_____
<!-- .slide: class="center" -->

# Background & premise

___

## Development Lifecycle
___

## Product Architecture
_____

# Codebase Management

___

## One Application; One Repository
___

## Define Infrastructure as Code

___

## Isolate & Ignore Dependencies

___

## Use Yarn

_____

# Development

___

## Limit Environment For Two

___

## Configurations Belong To `process.env.*`

___

## Lazy-Load Development Dependencies

___

## Use Migrations & Seeds

___

## Singleton Pattern for Services

___

## Log to `stdout`

___

## `.listen()` ASAP

___

## Code Splitting

___

## Client-Side Caching

_____

# Build Process

___

## Version Dependencies

___

## Run Builds in Containers

___

## Inject Global Configurations

_____

# Testing

___

## Run Tests After Builds

___

## Use A Linter

___

## Write Stateless Tests

___

## Parallelize Tests

_____

# Releasing

___

## Use `SEMVER` Versioning

___

## Automate Versioning Process

___

## Avoid File-Based Releases

___

## Release Immutably

_____

# Runtime/Scaling

___

## Run Node in Clusters

___

## Prioritise Quantity over Quality

___

