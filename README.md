# Programming with Python

[![GitHub release][shields_release]][swc_py_releases]
[![Create a Slack Account with us][create_slack_svg]][slack_heroku_invite]
[![Slack Status][slack_channel_status]][slack_channel_url]

An introduction to Python for non-programmers using inflammation data.

## About the Lesson

This lesson teaches novice programmers to write modular code to perform data analysis
using Python. The emphasis, however, is on teaching language-agnostic principles of
programming such as automation with loops and encapsulation with functions,
see [Best Practices for Scientific Computing][best-practices] and
[Good enough practices in scientific computing][good-practices] to learn more.

The example used in this lesson analyses some model-generated waveheight data. Learners are shown
how it is better to automate analysis using functions instead of repeating analysis
steps manually.

The rendered version of the lesson is available at:
<https://edcarp.github.io/python-novice-esces/>.

This lesson is derived from the [Analaysis of Inflammation Data lesson](inflammation_lesson). [Neil Chue Hong](npch), [Chris Wood](chris_wood), [Lucy Bricheno](lucy_b), and [Daniel Barker](daniel_b) were awarded a [NERC Advanced Short Training Course Grant](nerc_grant) to run Software Carpentry Courses specifically for
NERC domain scientists, to include providing domain-specific examples. The wave-height data was taken from. Bricheno & Wolf (2018) 'Future wave conditions of Europe, in response to high‐end climate change scenarios.' Journal of Geophysical Research: Oceans.


## Episodes

| # |  Episode | Time | Question(s) |
|--:|:---------|:----:|:------------|
| 1 | [Python Fundamentals][episode01] | 30 | What basic data types can I work with in Python?<br>How can I create a new variable in Python?<br>Can I change the value associated with a variable after I create it? |
| 2 | [Analyzing Waveheight Data][episode02] | 60 | How can I process tabular data files in Python? |
| 3 | [Visualizing Tabular Data][episode03] | 50 | How can I visualize tabular data in Python?<br>How can I group several plots together? |
| 4 | [Storing Multiple Values in Lists][episode04] | 30 | How can I store many values together? |
| 5 | [Repeating Actions with Loops][episode05] | 30 | How can I do the same operations on many different values? |
| 6 | [Analyzing Data from Multiple Files][episode06] | 20 | How can I do the same operations on many different files? |
| 7 | [Making Choices][episode07] | 30 | How can my programs do different things based on data values? |
| 8 | [Creating Functions][episode08] | 30 | How can I define new functions?<br>What’s the difference between defining and calling a function?<br>What happens when I call a function? |
| 9 | [Errors and Exceptions][episode09] | 30 | How does Python report errors?<br>How can I handle errors in Python programs? |
|10 | [Defensive Programming][episode10] | 30 | How can I make my programs more reliable? |
|11 | [Debugging][episode11] | 30 | How can I debug my program? |
|12 | [Command-Line Programs][episode12] | 30 | How can I write Python programs that will work like Unix command-line tools? |


## Contributing
[![Travis Build Status][travis_svg]][travis_url]

We welcome all contributions to improve the lesson!
Maintainers will do their best to help you if you have any questions, concerns,
or experience any difficulties along the way.

We'd like to ask you to familiarize yourself with our [Contribution Guide](CONTRIBUTING.md)
and have a look at the [more detailed guidelines][lesson-example] on proper formatting,
ways to render the lesson locally, and even how to write new episodes!

## Maintainer

The lesson maintainer is [Chris Wood][chris_wood].

## License
Instructional material from this lesson is made available under the
[Creative Commons Attribution][cc-by-human] ([CC BY 4.0][cc-by-legal]) license. Except where
otherwise noted, example programs and software included as part of this lesson are made available
under the [MIT license][mit-license]. For more information, see [LICENSE.md](LICENSE.md).

## Citation
To cite this lesson, please consult with [CITATION](CITATION).

## About Software Carpentry

Software Carpentry is a volunteer project that teaches basic computing skills to researchers since
1998. More information about Software Carpentry can be found [here][swc-about].

## About The Carpentries

The Carpentries is a fiscally sponsored project of [Community Initiatives][community-initiatives],
a registered 501(c)3 non-profit organisation based in California, USA. We are a global community
teaching foundational computational and data science skills to researchers in academia,
industry and government. More information can be found [here][cp-about].

[lesson-example]: https://carpentries.github.io/lesson-example
[chris_wood]: https://github.com/wood-chris
[npch]: https://github.com/npch
[lucy_b]: https://github.com/bricheno
[daniel_b]: https://github.com/phylolvb
[nerc_grant]: http://gotw.nerc.ac.uk/list_full.asp?pcode=NE%2FX009211%2F1
[lauren_ko]: https://github.com/ldko
[maxim_belkin]: https://github.com/maxim-belkin
[mike_trizna]: https://github.com/MikeTrizna
[trevor_bekolay]: http://software-carpentry.org/team/#bekolay_trevor
[valentina_staneva]: http://software-carpentry.org/team/#staneva_valentina
[greg_wilson]: https://github.com/gvwilson
[swc_history]: https://software-carpentry.org/scf/history/
[best-practices]: http://journals.plos.org/plosbiology/article?id=10.1371/journal.pbio.1001745
[good-practices]: http://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1005510
[R]: https://github.com/swcarpentry/r-novice-inflammation
[MATLAB]: https://github.com/swcarpentry/matlab-novice-inflammation
[shields_release]: https://img.shields.io/github/release/swcarpentry/python-novice-inflammation.svg
[swc_py_releases]: https://github.com/swcarpentry/python-novice-inflammation/releases
[create_slack_svg]: https://img.shields.io/badge/Create_Slack_Account-The_Carpentries-071159.svg
[slack_heroku_invite]: https://swc-slack-invite.herokuapp.com
[slack_channel_status]: https://img.shields.io/badge/Slack_Channel-swc--py--inflammation-E01563.svg
[slack_channel_url]: https://swcarpentry.slack.com/messages/C9Y0L6MF0
[travis_svg]: https://travis-ci.org/swcarpentry/python-novice-inflammation.svg?branch=gh-pages
[travis_url]: https://travis-ci.org/swcarpentry/python-novice-inflammation
[episode01]: https://edcarp.github.io/python-novice-esces/01-intro/index.html
[episode02]: https://edcarp.github.io/python-novice-esces/02-numpy/index.html
[episode03]: https://edcarp.github.io/python-novice-esces/03-matplotlib/index.html
[episode04]: https://edcarp.github.io/python-novice-esces/04-lists/index.html
[episode05]: https://edcarp.github.io/python-novice-esces/05-loop/index.html
[episode06]: https://edcarp.github.io/python-novice-esces/06-files/index.html
[episode07]: https://edcarp.github.io/python-novice-esces/07-cond/index.html
[episode08]: https://edcarp.github.io/python-novice-esces/08-func/index.html
[episode09]: https://edcarp.github.io/python-novice-esces/09-errors/index.html
[episode10]: https://edcarp.github.io/python-novice-esces/10-defensive/index.html
[episode11]: https://edcarp.github.io/python-novice-esces/11-debugging/index.html
[episode12]: https://edcarp.github.io/python-novice-esces/12-cmdline/index.html
[community-initiatives]: https://communityin.org
[cp-about]: https://carpentries.org/about
[swc-about]: https://software-carpentry.org/about/
[mit-license]: https://opensource.org/licenses/mit-license.html
[cc-by-human]: https://creativecommons.org/licenses/by/4.0/
[cc-by-legal]: https://creativecommons.org/licenses/by/4.0/legalcode
[inflammation_lesson]: https://github.com/swcarpentry/python-novice-inflammation
