---
layout: post
title: Useful tips for writing a thesis in LaTeX
category: articles
comments: true
tags: honours
---

These recent weeks I have been working on the [literature review](https://github.com/atyndall/honours/tree/master/litreview) section of my thesis, and while doing that I've been trying to use LaTeX packages to make that experience as easy as possible. I'll outline some of the things I've done here.

## Use `subfiles` for a modular thesis
The first thing I realised was that my thesis is going to very quickly get unwieldy if it is all contained in one document. I did some research, and I found that the [`subfiles`](http://www.ctan.org/tex-archive/macros/latex/contrib/subfiles) package was well suited to my situation.

`subfiles` allows you to have separate LaTeX files for different chapters, while allowing you to still compile both the chapters separately, and the whole document. This is great, as while I'm working on the literature review section, for instance, I don't want to waste my time compiling my whole thesis document when all I care about is one section.

This is the directory structure of my thesis;

	honours/
	├── cshonours.cls
	├── discussion
	│   └── discussion.tex
	├── introduction
	│   └── introduction.tex
	├── litreview
	│   └── litreview.tex
	├── methods
	│   └── methods.tex
	├── proposal
	│   └── proposal.tex
	├── references
	│   └── primary.bib
	├── results
	│   └── results.tex
	└── thesis
	    └── thesis.tex

Using subfiles is pretty easy; what it does is copies the header of your "main document" to your subdocuments. I have my main document, `thesis/thesis.tex`, which looks similar to this;

{% highlight latex %}
\documentclass{../cshonours}
\usepackage{subfiles}
\usepackage{etoolbox}

% Configure bibliography
\bibliographystyle{acm}
\defaultbibliography{../references/primary}
\defaultbibliographystyle{acm}

\begin{document}
\newcommand{\mainfile}{} % we use the existence of this command to see if we're compiling the whole thesis or just a chapter

\subfile{../introduction/introduction}
\subfile{../litreview/litreview}
\subfile{../methods/methods}
\subfile{../results/results}
\subfile{../discussion/discussion}

\bibliography{../references/primary}

\end{document}
{% endhighlight %}

and a bunch of subfiles like my literature review chapter, `litreview/litreview.tex`, which look like this;

{% highlight latex %}
\documentclass[../thesis/thesis.tex]{subfiles}
\begin{document}
 \chapter{Literature Review}
 \label{chap:litreview}
 
 % Content goes here
 
 \ifcsdef{mainfile}{}{\bibliography{../references/primary}}
\end{document}
{% endhighlight %}

Both documents can be successfully compiled without problems.

### Conditional actions with `subfiles`

One improvement I've made over the default subfiles configuration is the use of `\newcommand{\mainfile}{}`. This defines a pointless command called `\mainfile` if you are compiling `thesis.tex` directly. However, because it is in the body of `thesis.tex`, not the header, this command will not be defined if you are compiling an individual chapter.

This means we can use the `\ifcsdef` function (provided by `etoolbox`) to check if `\mainfile` is defined, and make things print or not print depending on if the document is being compiled as the whole, or just a part.

{% highlight latex %}
\ifcsdef{mainfile}{}{\bibliography{../references/primary}}
{% endhighlight %}

The above line prints a copy of the bibliography after the chapter, provided we're just compiling the chapter on its own. This is useful, as if I'm working on an individual chapter, I still want to see the bibliography for that specific chapter, but if I'm compiling the whole document, I don't want to see the bibliography after each chapter.

### Using the same style file for each subfile

One problem that you run into with `subfiles` is that if you have a custom document class file like I do (`cshonours.cls`), you can't write `\documentclass{cshonours}` in your main document, or other subfiles will look for the `cshonours.cls` file in their own directories, not in the main document's directory. If LaTeX cannot find the style file there, the compile will fail.

One way to solve this problem is to have a copy of your `.cls` file in each subfiles' directory, but another trickier way to solve it is to also put your main document (in my case `thesis/thesis.tex`) in its own subdirectory, and use a relative path that is correct for all subfiles AND the main file; `\documentclass{..\cshonours}`. You'll get a warning message from LaTeX, but it will compile just fine.

## Acronyms and abbreviations

If you're like me and doing a thesis in an area with a lot of tech, chances are you're going to be using a lot of acronyms and abbreviations to describe things. I've found both the [`acronyms`](http://www.ctan.org/tex-archive/macros/latex/contrib/acronym) and [`abbrevs`](http://www.ctan.org/tex-archive/macros/latex/contrib/frankenstein) packages useful for this.

Here is part of my `thesis/thesis.tex` header;

{% highlight latex %}
\usepackage{abbrevs}
\usepackage{acronym}

% Acronyms for common stuff
\acrodef{lowpan}[6LoWPAN]{IPv6 over Low power Wireless Personal Area Networks}
\acrodef{coap}[CoAP]{Constrained Application Protocol}
\acrodef{iot}[IoT]{Internet of Things}

% Abbreviation commands for common stuff
\newabbrev\lphy{802.15.4-2006}
\newabbrev\lowpan{\ac{lowpan}}
\newabbrev\coap{\ac{coap}}
\newabbrev\iot{\ac{iot}}
{% endhighlight %}

What the `\acrodef` does is defines an acronym, which you can then reference with `\ac{acroname}`. If you use that, the first time you use it, it will define the whole acronym, and subsequent times, it will just use the acronym. For example;

{% highlight latex %}
We can see that \ac{lowpan} is a good system by which to etc, etc.
\ac{lowpan} is also good for x, y, z.
{% endhighlight %}

will produce

>We can see that IPv6 over Low power Wireless Personal Area Networks (6LoWPAN) is a good system by which to etc, etc.  
>6LoWPAN is also good for x, y, z.

The abbreviations package is similar, in that it lets you define more simple abbreviations to map to LaTeX commands, or just text. This is different to using `\newcommand`, as it handles spacing a lot better. I use it to define some IEEE standards that I mention a lot, as well as even shorter versions of the acronym commands. This allows me to use this, instead of the above;

{% highlight latex %}
We can see that \lowpan is a good system by which to etc, etc.
\lowpan is also good for x, y, z.
{% endhighlight %}

which I find very convenient.

## `fancyref` support for subsections

I also use the [`fancyref`](http://www.ctan.org/tex-archive/macros/latex/contrib/fancyref) package for cross-referencing. `fancyref` provides a much smarter cross-referencing system that automatically describes the type of thing you're referencing, and the page it is on.

One thing that `fancyref` doesn't seem to have support for is referencing subsections. If you add these commands to your document header, it should be able to reference them;

{% highlight latex %}
% Source; https://github.com/openlilylib/tutorials/blob/master/aGervasoni/orchestralScores/example-materials/OLLbase.sty
\newcommand*{\fancyrefsubseclabelprefix}{subsec}

\fancyrefaddcaptions{english}{\providecommand*{\frefsubsecname}{subsection}\providecommand*{\Frefsubsecname}{Subsection}}

\frefformat{plain}{\fancyrefsubseclabelprefix}{\frefsubsecname\fancyrefdefaultspacing#1}
\Frefformat{plain}{\fancyrefsubseclabelprefix}{\Frefsubsecname\fancyrefdefaultspacing#1}

\frefformat{vario}{\fancyrefsubseclabelprefix}{\frefsubsecname\fancyrefdefaultspacing#1#3}

\Frefformat{vario}{\fancyrefsubseclabelprefix}{\Frefsubsecname\fancyrefdefaultspacing#1#3}
{% endhighlight %}


These are just some of the things I've done to improve my thesis' LaTeX experience. You can see all of my changes on its [repository page](http://github.com/atyndall/honours).