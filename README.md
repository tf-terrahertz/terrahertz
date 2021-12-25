# Terrahertz
> Hertz: the SI unit of frequency

Terrahertz is a tool to enable a pull-request based workflow for infrastructure as code.
It aims to speed up the rate of how fast these infrastructure changes can be deployed from a centralized place.

## Goals

_Note: this is a wishlist for now_

- Small core
- Externalized state
- Extension plugins for integration with VCS systems, runners and approval
- Fast execution by caching plugins and providers
- Correctness of dependencies by still fetching/validating them in parallel

## Why

### Why not BitHubLabCircleJenkins CI?
Often, people use CI tools to deploy their infrastructure as code. IMHO this is a risky endeavor.

Even for code, this makes it hard to have an ever-green mainline branch, see the rationale why a tool like [`bors-ng`](https://github.com/bors-ng/bors-ng#but-dont-githubs-protected-branches-already-do-this) is usefull.

Besides these issues, Terraform deals with stateful systems. Compared to code, state is way more annoying to repair.
On a broken mainline branch, one can either create a new PR to fix the breakage, or revert to the previous version of code.
If you throw away, or corrupt a stateful system, this has immeadiate customer impact, and is much more labuourous to repair.

Thankfully, Terraform allows us to generate a plan, and using that, explore the impact of our code changes on the resources
that Terraform manages. Approving these plans can be implemented in some CI systems.

## Why not Atlantis?

[Atlantis](https://www.runatlantis.io/) is an awesome tool!
It is well suited if you have many small infra repo's.

It does not work as nice as that for infra monorepos.

## Why implemented in Golang?

Many Infrastructure as Code tools are implemented in Go. Therefore there exists a rich ecosystem in libraries that we can leverage.
