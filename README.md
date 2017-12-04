[![Build Status](https://travis-ci.org/HumanCellAtlas/ingest-travel-guide.svg?branch=master)](https://travis-ci.org/HumanCellAtlas/ingest-travel-guide)

# HCA DCP Ingest Travel Guide

Base on Patrick Kua's (@patkua) [The Travel Guide to Software Systems](https://www.slideshare.net/thekua/the-travel-guide-to-software-systems).

## History

## Useful facts

## [Culture](pages/culture.md)
* [Coding standards](pages/culture.md#coding-standards)
* Code review/pair programming 
* Conventions in the codebase 
* Common programming patterns 
* Development process

## Maps
* [Design](pages/design.md)
* [Services](pages/services.md)
* [Goals](pages/goals.md)
* [Roadmap](pages/roadmap.md)
* [Flow](pages/flow.md)

## Sites
* [Technology](_pages/technology.md)

## Fun

## Running Locally

### Setting Up Ruby Environment on macOS

By default macOS comes with own version of Ruby installed. To make configuration run easier, it is advised to set up the environment using [Homebrew](https://brew.sh/). Follow the instructions in the official homepage to setup.

#### Installing Ruby

To override the current Ruby installation, use the installation command in Homebrew:

    brew install ruby
    
This should include the Ruby `Gem` package manager. Do note that it may be necessary to restart the terminal when the setup is done.

#### Setting up Jekyll Environment

The official [Web page for Jekyll](https://jekyllrb.com/) provides a quickstart documentation for setting up Jekyll in the environment.

After the required Gems have been installed, serving the pages of this Jekyll blog can be done using the following command:


```
bundle exec jekyll serve
```