---
title: Ruby
subsection: ruby
section: tech-languages
order: 1
version: 2.2.2
description: A dynamic programming language with a focus on readability, simplicity and productivity.
---

# Ruby installation

## CRuby

To install CRuby, simply type:

```
$ sudo dnf install ruby
```

Above command will install latest stable CRuby packages including RDoc, Psych, JSON, BigDecimal and IO/Console, and interactive Ruby shell `irb`. Other bundled libraries such as TclTk bindings, Rake and Test::Unit found in upstream Ruby distribution needs to be installed separately:

```
$ sudo dnf install ruby-tcltk rubygem-rake rubygem-test-unit
```

Please note that we have already unbundled these libraries from Ruby itself, so they come in their own packages and need a specific dependency requirement in .gemspec or Gemfile as well as a specific `require()` call in your Ruby code.

## JRuby

Alternatively Fedora comes with JRuby packages that can be installed via:

```
$ sudo dnf install jruby
```

Please note that JRuby packages in Fedora are not yet in the best shape and things might be broken. If you are not willing to experiment, please use the CRuby packages for now or use a Ruby version manager of your choice.

## Choosing Ruby with RubyPick

All Rubies come installed with RubyPick, the Fedora Ruby manager. Therefore CRuby has its executable at `/usr/bin/ruby-mri`, JRuby has its at `/usr/bin/jruby` and `/usr/bin/ruby` is a RubyPick executable that chooses the right version of Ruby to run.

You don't need to do anything to set up RubyPick to use CRuby as CRuby is the default. RubyPick was actually introduced to enable Fedora users run other Ruby implementations that might make their way into official Fedora repositories such as JRuby.

To use different Ruby via RubyPick run:

```
ruby _mri_ [params]
ruby _jruby_ [params]
```

Or set the expected environment variables as follows:

```
RUBYPICK=_mri_
RUBYPICK=_jruby_
```

[Read more about RubyPick](https://github.com/fedora-ruby/rubypick).
