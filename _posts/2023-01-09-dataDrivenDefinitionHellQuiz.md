---
layout: quiz
title: "Data-Driven Definition Hell Quiz"
tags: quiz data analyst engineer scientist
---

## What's that?

An attempt to come up with a term describing the confusion arising from the ease with which terms are thrown around in
today's data-related
job landscape.

A justified reason, of course, is the need for non-technical recruiters to apply filters to perform their job. I believe
this is nothing to poke fun at. What I believe can be poked fun at, however, is the directives that trickle down and
shape job postings, conversations and positions as a result of trend hunting.

To emphasize 'fun' rather than 'poke', I tried to put together a small quiz where everyone can evaluate their knowledge
and opinions on the various data-related business and technical roles, against a sample of the collective experience and
information
found online!

## Test your might!

Select a ☐ to see how well you can anticipate the statements documented in top [Medium](https://www.medium.com) and [Towards
Data Science](https://towardsdatascience.com) member stories
search results regarding the most common descriptions of:

<div class="md:mx-56 text-center rounded-2xl bg-slate-800">
    <p class="p-5 text-sm text-slate-400 font-mono">
        Data Scientists<br />
        Data Engineers<br />
        Data Analysts<br />
        ML Engineers<br />
    </p>
</div>

<!-- <div class="m-auto xs:w-[50%] sm:w-[30%]">
    <img class="m-auto rounded-2xl" src="{{site.baseurl}}/assets/gif/testYourMight.gif">
</div> -->

<div id="quiz-div" class='not-prose pt-5 gap-y-5 grid sm:grid-cols-2 sm:gap-x-5 sm:gap-y-8 p-2 border-double border-2 border-indigo-200'>
    {% for entry in site.data.quiz.questions %}
    <div>
        <p class="font-semibold">🔎 {{ entry.Q }}</p>
        <ul class="m-3" id="{{ entry.correct }}">
            {% for options in entry.A %}
            <li>
                <button id="{{ options[0] }}"
                    class="bg-white text-gray-800 font-semibold m-auto w-4 h-4 border border-gray-400 rounded shadow active:bg-violet-50"></button>
                {{ options[1] }}
            </li>
            {% endfor %}
            <div class="" id="div{{ entry.correct }}">
                <div class="hidden text-xs bg-green-100 rounded-full sm:mx-6 m-auto w-auto mt-4 px-6 py-4"
                    id="correct{{ entry.correct }}">
                    <p class="text-center text-lg font-mono font-bold">Correct!</p>
                    <!-- <p class="">{{ entry.comment }}</p> -->
                </div>
                <div class="hidden text-xs bg-red-100 rounded-full sm:mx-6 m-auto w-auto mt-4 px-6 py-4"
                    id="false{{ entry.correct }}">
                    <p class="text-center text-lg font-mono font-bold">Wrong!</p>
                    <!-- <p class="">{{ entry.comment }}</p> -->
                </div>
            </div>
        </ul>
    </div>
    {% endfor %}
</div>

<div class="md:mx-10 rounded-2xl bg-slate-200">
    <!-- <p class="pt-2 text-center font-bold text-lg text-slate-600 font-mono">Note</p> -->
    <p class="pt-4 pb-4 px-4 text-sm text-slate-600 font-mono">
        If you're interested in the modular custom quiz functionality implemented here with Javascript, Tailwind and Jekyll, have a
        look at the source code for the 
        <a href="https://github.com/iokarkan/iokarkan.github.io/blob/main/_layouts/quiz.html">layout</a>
        and 
        <a href="https://github.com/iokarkan/iokarkan.github.io/blob/main/_posts/2023-01-09-dataDrivenDefinitionHellQuiz.md">post</a>
        for this post on Github!
    </p>
</div>

<div class="md:mx-10 rounded-2xl bg-slate-200">
    <p class="pt-2 text-center font-bold text-lg text-slate-600 font-mono">References</p>
    <p class="pt-1 px-4 text-sm text-slate-600 font-mono">
        See below for the full quotes:
    </p>
    <ul class="px-4 pb-2 text-sm">
        <li><a href="https://towardsdatascience.com/data-analyst-vs-data-scientist-a83af97ad472">Data Analyst vs. Data
                Scientist</a><br /></li>
        <li><a href="https://towardsdatascience.com/ml-engineer-vs-data-scientist-53c047666739">ML Engineer vs Data
                Scientist: Whom Should You Hire?</a><br /></li>
        <li><a href="https://towardsdatascience.com/mlevsds-3c89425baabb">Machine Learning Engineer vs Data Scientist
                (Is Data Science Over?)</a><br /></li>
        <li><a
                href="https://medium.com/@writuparnabanerjee/the-difference-in-the-career-options-in-data-science-data-scientist-vs-data-engineer-vs-data-33209d0ac880">The
                difference in the career options in Data Science: Data Scientist vs Data Engineer vs Data Analyst vs ML
                Engineer</a><br /></li>
        <li><a href="https://towardsdatascience.com/data-engineer-vs-data-scientist-bc8dab5ac124">Data Engineer VS Data
                Scientist</a><br /></li>
    </ul>
</div>


### Any take-aways?

I believe this quiz may illustrate how context-specific these definitions are. It is arguable that, if one knows
beforehand, for example, the title of the story containing a quote (i.e. how the author chooses to refer to each of the
roles compared) it would be far easier to choose correctly between the available options. 

But the fact remains, that different roles are discussed using definitions with near-perfect similarity. And while this confusion will resolve itself
significantly as time goes by, nebulous role details can only result in an overall feeling of job insecurity for new or existing employees.

<!-- ### Check also:
[https://datascience.stackexchange.com/questions/2403/data-science-without-knowledge-of-a-specific-topic-is-it-worth-pursuing-as-a-ca/2406#2406](https://datascience.stackexchange.com/questions/2403/data-science-without-knowledge-of-a-specific-topic-is-it-worth-pursuing-as-a-ca/2406#2406)

[https://www.springboard.com/blog/data-science/data-engineer-vs-data-analyst/#:~:text=Data%20analysts%20try%20to%20find,right%20career%20choice%20for%20you](https://www.springboard.com/blog/data-science/data-engineer-vs-data-analyst/#:~:text=Data%20analysts%20try%20to%20find,right%20career%20choice%20for%20you)

[https://www.quora.com/Whats-the-difference-between-a-data-scientist-and-an-AI-researcher](https://www.quora.com/Whats-the-difference-between-a-data-scientist-and-an-AI-researcher) -->