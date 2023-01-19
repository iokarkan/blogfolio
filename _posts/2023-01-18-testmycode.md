---
layout: post
title: "How the pros grade online courses"
tags: helsinki mooc testing
---

<!-- Talking about my favourite courses online, MOOC.fi. The focus is on the very interesting way to evaluate the performance of students on code assignments! -->

<div class="not-prose sm:p-6 mt-6 shadow-lg rounded-lg bg-gray-100 text-gray-700">
  <p class='text-center sm:mx-8 font-semibold text-sm p-4 font-sans'>
    This post is related to MOOC.fi, i.e. the massive open online courses offered by the
    University of Helsinki.
  </p>
  <p class="text-sm px-4">
    These courses are offered to Finnish students during their Bachelor or Master's level courses, cover a plethora
    of
    interesting topics ranging from Software Development to AI Ethics and everyone around the globe can join. The
    university in no way, shape or form sponsors this blog post but I highly recommend them and consider them
    exemplary of
    the
    reputation of Nordic educational excellence.
  </p>

  <div class="w-full p-2">
  <a href="https://www.mooc.fi/en/#courses">
    <button type="button"
      class="block mx-auto px-6 py-2.5 mt-4 bg-blue-600 text-white font-medium text-xs leading-tight uppercase rounded shadow-md hover:bg-blue-700 hover:shadow-lg focus:bg-blue-700 focus:shadow-lg focus:outline-none focus:ring-0 active:bg-blue-800 active:shadow-lg transition duration-150 ease-in-out">
      Check out their free courses
    </button>
    </a>
  </div>
</div>

### Test My Code

Introducing itself as a programming assignment evaluator, [Test My Code](http://testmycode.github.io/) (TMC for short),
is open-source software developed to facilitate efficient automation in supporting coding exercises for courses that
allow for remote participation. Developed as a software engineering project in a lab of the university, TMC is used by
the student to **set-up a local course environment, evaluate their attempts against test cases and provide their
solutions to exercises**. Data gathered by the tool is utilized by research teams aiming to streamline MOOC
participation, but also as a means to provide hints to students regarding why their attempts at solving are
unsuccessful.

### How does it work?

<div class="sm:mx-10">
  <figure>
    <img class="rounded-xl" src="https://testmycode.github.io/images/tmc-systems-diagram.png" />
    <figcaption class="text-xs italic text-center">The TMC plug-in communicates with sandboxes on the server-side to
      execute user-submitted code, but also allows for local testing, as shown in this UML diagram (courtesy of
      <a href="http://testmycode.github.io/">tmc.github.io</a>).
    </figcaption>
  </figure>
</div>


My (crude) understanding of the way a user-side plug-in is integrated in TMC is the following:

- a language-specific tester framework (e.g. [python](https://github.com/testmycode/tmc-python-tester)) is downloaded by the user-side plug-in and run
- at the user's command, user-created code is bundled and shipped by the plug-in to a server-side sandbox
- tests are run by the sandbox and results are produced in a standardized output (e.g. JSON), containing information about the student, the evaluation results and the course
- and the output file with the results is parsed, loaded and the scores are registered on the server using language-specific modules from the unifying [Java framework](https://github.com/testmycode/tmc-langs/blob/master/tmc-langs-python3/src/main/java/fi/helsinki/cs/tmc/langs/python3/Python3TestResultParser.java#L26)

The team behind TMC has developed a Java framework to allow for any programming language to be plugged into TMC (called [tmc-langs](https://github.com/testmycode/tmc-langs)). For Java, for example, there is a NetBeans plug-in. Having such a plug-in allows the student to submit code to the server but also enables harmless self-evaluation via local trial and error. Apparently, the plug-in downloads the language-specific tester framework at the user-side plug-in that is used to locally run exercise tests.


<!--TODO: Expand on this stub -->

### TMC tests for Data Analysis with Python 2023 (or 2022)

For python, conveniently, there exists a plug-in for VSCode (see [here](https://github.com/rage/tmc-vscode)).
Once the plug-in on the user-side is installed, it allows the student to identify the course and download all
course-related exercises.
Within the folder structure downloaded, there exists for each exercise module:

- a source code template for the student to use
- a pre-defined test suite, integrated to the source code, that performs tests on the user's code

There are a number of course-specific package dependencies to be satisfied, but once loaded, it looks something like
this (apparently using the metadata from its previous iteration):

<div class="sm:mx-10">
  <img class="object-scale-down rounded-xl" src="{{site.baseurl}}/assets/img/tmc-vscode.png" />
</div>

The entirety of available exercises can be downloaded with a single-click, and a folder structure is prepared. The
student can easily identify the green-lit exercises already completed, to match the full progress counter shown in the
course's TMC home page.ß

<div class="sm:mx-10">
  <img class="object-scale-down rounded-xl" src="{{site.baseurl}}/assets/img/tmc-vscode-folders.png" />
</div>

Local source and test files are separated:

```none
├── <part>-<exercise>_<name>/
      └── src/          # user-defined source code
        └── <template>.py
      └── test/       # the test suite
        └── __init__.py
        └── test_<template>.py
      └── tmc/          # the local language-specific TMC source code
        └── __init__.py
        └── __main__.py
        └── points.py
        └── result.py
        └── runner.py
        └── utils.py
```

The Hello World exercise is accompanied by some interesting test code at the user side:

```python
#!/usr/bin/env python3

import unittest
from tmc import points
from tmc.utils import load, get_stdout

module_name="src.hello_world"
main = load(module_name, "main")

@points('p01-01.1')
class HelloWorld(unittest.TestCase):
def test_first(self):
main()
self.assertEqual(get_stdout(), "Hello, world!")

if __name__ == '__main__':
unittest.main()
```

Test cases are orchestrated using the `unittest` module from the python STL, and the imports are rounded up with
`points`, `load` and `get_stdout` from the `tmc` core library.

- `load` and `get_stdout` are TMC [utilities](https://github.com/testmycode/tmc-python-tester/blob/master/tmc/utils.py). The first one is used for relative imports of the student's files (from `src`) and the second catches the output when `src` files are run
- `points` is called as a decorator, and points (forgive me) to the exercise's name. The [implementation](https://github.com/testmycode/tmc-python-tester/blob/master/tmc/points.py#L16) of the `points` function is to save points for either a whole exercise or for a specific part of it. Accumulatively, this allows checking all kinds of grades for the student.

What is a python test without an `assert` call? Did you know assert can add a helper message? Did you know this can be a great way to massage hints to assist the student into the code tests? Well, the folks that developed TMC know!

```python
def call_helper(self, countlist):
        with patch(module_name+'.triple', side_effect=triple) as tr:
            with patch(module_name+'.square', side_effect=square) as sq:
                main()
                self.assertIn(len(tr.mock_calls), countlist,
                              msg="Are you sure you called 'triple' the right number of times?")
                self.assertIn(len(sq.mock_calls), countlist,
                              msg="Are you sure you called 'square' the right number of times?")
```

User-code is compressed, wired over to the server, and the plug-in finally provides a model solution to the student upon successful submission of the exercise, prepared by the course staff. I assume TMC also has a part to play on online student examinations and not just offline course material, but I have yet to come across such a case (previous courses I've taken consisted of online quizzes)

## Few words on other evaluation methods

Personally, its the first time I encounter such an elegant solution to MOOC course evaluation. In other courses even from MOOC.fi, I have encountered multiple-choice quizzes along with peer-reviewed essays from the student. This source titled ["Teaching in a Digital Age"](https://tell.colvee.org/mod/book/view.php?id=646&chapterid=1075) mentions that computer-marked multiple-choice assignments dates back to 1970, but feedback wasn't as immediate back then. It is also mentioned that some essay evaluations have also been automated, but primarily regarding their technical aspects, grammatical or syntactic.

Peer-review is applied by having other participants of the course having a look on the answer you have given on a question, usually 3, and grading it. If none are available at the time, as they're at different parts in the course, then they can be substituted by course staff. The Big Data Platforms course I have attended wholly embraced this evaluation method and I found it quite stimulating to review submissions from people that clearly had much more experience than me on the topic.

## Wrap-up

There's a ton of infrastructure behind this, as in every decent software engineering project, that I couldn't go into even if I wanted to, but that's not the point of this post. I just want to praise the level of this dedicated effort to allow the student to code in their own environment, even bringing them closer to the testing aspect of their code.