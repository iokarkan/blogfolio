---
layout: post-toc
title: "The state of Research Platforms in 2023: A review"
tags: research platform publications journal-hub
icon: "fas fa-newspaper"
---

<h2 id="A brief summary of the modern researcher's needs" class="scroll-mt-[150px]">A brief summary of the modern researcher's needs</h2>

A couple of months ago, the scientific world was mesmerized by the tumultuous pour-down of new papers from the
Artificial Intelligence research community. Studies diving into the capabilities of the hugely successful commercial
ChatGPT, technical reports for aspiring open-source Large Language Model projects from university teams and tech giants,
an undeniable gold-rush situation unfolded within the span of a few weeks. The flow has slowed-down since, but is still
on-going.

Before that, the COVID outbreak produced a huge interest in scientific studies of epidemiology, vaccine production and
efficacy.

All these experiences prompted me to ponder fundamentally about what assists a modern researcher's daily struggle to
follow the trends or communicate with colleagues, what is working about it and what is missing.

Two important factors that I figure make a researcher's life better are:

- **Ease of discovery of research**
- **Ease of networking and collaboration**

To make a long story short, a researcher needs to follow-up on new research, and needs to be able to quickly spin-up a
body of past literature to review. More often than not, they need to also be hit with something outside their bubble, to
broaden their range and spark their inspiration. Second, in the information age they already need to be collaborating
with a large number of associates, up or down the hierarchy.

Naturally, these two are communicating vessels, as fellow collaborators can assist in finding relevant research, and by
contacting authors of new research you can reach a wider audience of scientists to work with.

I cannot refrain from recognizing that the above is connected to the more enveloping issues of **accessibility to
opportunity, funding and equipment**, blocking points that all less-developed research communities and aspiring
researchers struggle with today.

<!-- ### A stalwart ally: Research-hosting databases

I myself was in the fortunate position to be able to actively explore new AI papers and projects on a daily basis, without the pressure of deadlines and work. It appeared that it was quite enough to just hit refresh on the day's pre-print Computer Science paper uploads in what I used to employ as a main source of papers as a physicist researcher, namely [arXiv](https://arxiv.org). arXiv features pre-prints covering a range of (mostly quantitative) disciplines, from the aforementioned Comp. Science to Physics, Mathematics and Computational Biology.

arXiv is backed by Cornell University, and is "a free distribution service and an open-access archive". It hosts pre-prints, meaning that at the time of upload the paper's have not undergone peer-review. It's not the only service to work this way, as there's also the spin-off [medRxiv](https://www.medrxiv.org/), supported by the Cold Spring Harbor Laboratory and associated with Yale University, focusing on Μedicine and most health sciences.

However, my experience is that if you ask a medical researcher, they'll tell you that they're using [PubMed](https://pubmed.ncbi.nlm.nih.gov/) as their literature database. Here comes the elephant in the room, however, as PubMed hosts not-only open-access full-text works, but also research published in major publishing houses' journals, such as Springer's *Nature*, AAAS' *Science* as well as smaller ones. Similar in this aspect, but in the field of engineering, is the [IEEE](https://www.ieee.org/) institute and its corresponding journals, and [ERIC](https://eric.ed.gov/) in the field of education. Naturally, there are plenty more, but you get the gist. There is also [Google Scholar](https://scholar.google.com/), a fully-fledged search engine allowing you to find what you're looking after in some of those open-source databases, as well as major publication houses. -->

The issue going hand-in-hand with ease of discovery is that of accessibility. As it currently stands, most peer-reviewed
publications are indeed behind a "pay-wall", requiring either one-time purchase fees, monthly or yearly personal
subscriptions, or membership in a subscribing public or private research institution.

<h3 id="Networking and collaboration platforms... for research?" class="scroll-mt-[150px]">Networking and collaboration platforms... for research?</h3>

Online social media applications have penetrated every aspect of society, and it is no wonder that they are also a place
where discussion about research happens. Social media offer ways of interacting publicly, and also of creating private
groups, thus allowing for any kind of conversation scope. The profile of social media applications ranges from relaxed
(think Reddit) to more sometime more preppy (think LinkedIn), and research is indeed discussed under a wide spectrum of
seriousness. Some allow their users to remain anonymous (or pseudonymous), and some encourage using your actual given
name.

But as has been observed time and time again, an emergent property of social media is that they will be associated with
a certain type of behaviour or content, and it seems hard to me to isolate this *branding* of existing platforms, and to
re-purpose them, for example, as the place of a rather serious research discussion venture.

In practice, however, most researchers will publicly network within those platforms, mostly refraining from engaging in
substantial public discourse, and perhaps create closed communities. Those communities, I imagine, are rather used more
for generic coordination than for fine-grained exchange of ideas and brainstorming under specific research contexts.
I've come to realize that such exchanges are mostly done in private using instant messaging apps, with various links to
publication resources thrown around and a continuous unstructured stream of comments flowing through, until someone
interrupts the flow to use the app for something more urgent that actually needs to instantly catch the group's
attention.

Regarding research hosting databases (such as PubMed or arXiv), most of them offer some sort of programmatic access
(API), a means for developers in the wild to build code that connects to their archives and retrieves metadata, or even
the actual research article text. But for pay-walled articles, the text not retrievable unless the application developed
is in some way explicitly affiliated or subscribed to the journal source.

There's another, perhaps not-so obvious reason why this is an important aspect of the research landscape, and relates
also the ease of networking mentioned earlier. The reproduction of text from a pay-walled article is usually legally not
allowed, therefore somewhat prohibiting detailed public discourse post-publication. This is why pre-prints are a thing,
and this is why it's hard to build an all-inclusive platform where all researchers can be un-restricted in elaborating
their comments and critique.

The point is today's researchers of all disciplines could benefit from tools that provide ease of discovery and ease of
networking in research. Each of these tools has its own degree of focus to research content. One of my goals in this
article is to **make a list of the pros and cons of the most popular options I'm aware of, based on my understanding, as
a starting point for a discussion.** In the end, I'll go through my own attempt at creating such a tool.

*(Please feel free to contact me regarding factual errors in my review below. This does not claim to be an exhaustive
list of features, pros & cons.)*

<h2 id="Review of modern research discovery & collaboration options" class="scroll-mt-[150px]">Review of modern research discovery & collaboration options</h2>


{% assign entry = site.data.lit-review.social %}
<div class="not-prose shadow-lg bg-gray-100 py-4 w-auto mx-[15%] md:[35%] text-center rounded-xl text-xl font-semibold">
    <h3 id="{{entry.title}}" class="scroll-mt-[150px]">{{entry.title}}</h3>
</div>
<div class="flex flex-row mx-auto justify-center gap-2 py-4 cursor-default">
    {% for badge in entry.badges %}
    <badge class="bg-indigo-600 text-white px-2 py-1 text-center font-bold text-xs rounded-lg">{{badge}}</badge>
    {% endfor %}
</div>
<div class="text-center">
    ({% for name in entry.names %}
    <span class="font-semibold">{{name}}</span>
    {% endfor %})
</div>
**Ups:**
<div class="flex flex-col gap-2">
    {% for pro in entry.ups %}
    <span><i class="md:ml-6 md:mr-4 mr-2 my-auto fas fa-check p-1" style="color: #3b930b;"></i>{{pro}}</span>
    {% endfor %}
</div>
**Downs:**
<div class="flex flex-col gap-2">
    {% for con in entry.downs %}
    <span><i class="md:ml-6 md:mr-4 mr-2 my-auto fas fa-times p-1" style="color: #f26440;"></i>{{con}}</span>
    {% endfor %}
</div>

<br />

{% assign entry = site.data.lit-review.messaging %}

<div class="not-prose shadow-lg bg-gray-100 py-4 w-auto mx-[15%] md:[35%] text-center rounded-xl text-xl font-semibold">
    <h3 id="{{entry.title}}" class="scroll-mt-[150px]">{{entry.title}}</h3>
</div>
<div class="flex flex-row mx-auto justify-center gap-2 py-4 cursor-default">
    {% for badge in entry.badges %}
    <badge class="bg-indigo-600 text-white px-2 py-1 text-center font-bold text-xs rounded-lg">{{badge}}</badge>
    {% endfor %}
</div>
<div class="text-center">
    ({% for name in entry.names %}
    <span class="font-semibold">{{name}}</span>
    {% endfor %})
</div>
**Ups:**
<div class="flex flex-col gap-2">
    {% for pro in entry.ups %}
    <span><i class="md:ml-6 md:mr-4 mr-2 my-auto fas fa-check p-1" style="color: #3b930b;"></i>{{pro}}</span>
    {% endfor %}
</div>
**Downs:**
<div class="flex flex-col gap-2">
    {% for con in entry.downs %}
    <span><i class="md:ml-6 md:mr-4 mr-2 my-auto fas fa-times p-1" style="color: #f26440;"></i>{{con}}</span>
    {% endfor %}
</div>

<br />

{% assign entry = site.data.lit-review.search %}

<div class="not-prose shadow-lg bg-gray-100 py-4 w-auto mx-[15%] md:[35%] text-center rounded-xl text-xl font-semibold">
    <h3 id="{{entry.title}}" class="scroll-mt-[150px]">{{entry.title}}</h3>
</div>
<div class="flex flex-row mx-auto justify-center gap-2 py-4 cursor-default">
    {% for badge in entry.badges %}
    <badge class="bg-indigo-600 text-white px-2 py-1 text-center font-bold text-xs rounded-lg">{{badge}}</badge>
    {% endfor %}
</div>
<div class="text-center">
    ({% for name in entry.names %}
    <span class="font-semibold">{{name}}</span>
    {% endfor %})
</div>
**Ups:**
<div class="flex flex-col gap-2">
    {% for pro in entry.ups %}
    <span><i class="md:ml-6 md:mr-4 mr-2 my-auto fas fa-check p-1" style="color: #3b930b;"></i>{{pro}}</span>
    {% endfor %}
</div>
**Downs:**
<div class="flex flex-col gap-2">
    {% for con in entry.downs %}
    <span><i class="md:ml-6 md:mr-4 mr-2 my-auto fas fa-times p-1" style="color: #f26440;"></i>{{con}}</span>
    {% endfor %}
</div>

<br/>

{% for entry in site.data.lit-review.standalone %}
<!-- <TEMPLATE> -->
<div class="not-prose shadow-lg bg-gray-100 py-4 w-auto mx-[15%] md:[35%] text-center rounded-xl text-xl font-semibold">
    <a class="no-underline" href="{{entry.url}}">
        <h3 id="{{entry.name}}" class="scroll-mt-[150px]">{{entry.name}}</h3>
    </a>
</div>
<div class="flex flex-row mx-auto justify-center gap-2 py-4 cursor-default">
    {% for badge in entry.badges %}
    <badge class="bg-indigo-600 text-white px-2 py-1 text-center font-bold text-xs rounded-lg">{{badge}}</badge>
    {% endfor %}
</div>
**Ups:**
<div class="flex flex-col gap-2">
    {% for pro in entry.ups %}
    <span><i class="md:ml-6 md:mr-4 mr-2 my-auto fas fa-check p-1" style="color: #3b930b;"></i>{{pro}}</span>
    {% endfor %}
</div>
**Downs:**
<div class="flex flex-col gap-2">
    {% for con in entry.downs %}
    <span><i class="md:ml-6 md:mr-4 mr-2 my-auto fas fa-times p-1" style="color: #f26440;"></i>{{con}}</span>
    {% endfor %}
</div>
<br />
<!-- </TEMPLATE> -->
{% endfor %}

<h2 id="Problem solved? - The space for new platforms" class="scroll-mt-[150px]">Problem solved? - The space for new platforms</h2>

After compiling this list, I have seen that there are many platforms out there to empower researchers (and I sure must
have missed a lot of them). However, it is often the case that not all these tools are utilized to their maximum
potential. I believe that mainstream attraction depends on:

- Aesthetic appeal
- Ability to break the inertia of habit
- Providing ease of use
- Simplicity of implementation
- All-in-one integrations

Out of all the options presented to the researcher, I believe there are many satisfactory approaches to **searching**
for publications. The options regarding **discovery** and recommendation of papers are still competing against one
another, and frequently appear as paid services, and have also taken in the AI boom and seemingly integrated Machine
Learning recommendation algorithms.

However, I feel that the **networking** and discussion aspect remains anchored in the general-purpose social media and
messaging platforms. I have found discussion elements in some platforms. I can't exactly verify the extent to which
these are used in the global research community, but, for example, PubPeer has been around for around a decade,
HuggingFace's popularity has sky-rocketed and ResearchRabbit claims to be used by researchers in over 100 countries.

I personally had the idea of an alternative to social media for public and group discussions on user-curated paper
collections before having explored the above app landscape, and it inspired me to create the [Journal
Hub](https://www.journal-hub.org) platform. It shares many common elements with the options listed above, and
encapsulates my vision of what such a platform should facilitate at minimum:

- public discussion of any paper
- public and private group collections under a specific scope
- papers are curated by users
- integration of all available open-access databases, with all scientific fields in scope
- an in-app comment system, supporting LaTeX
- ability to authenticate via oauth providers

Outside this set many other attractions are found in the wild, such as visualization and personalized recommendation
features. I haven't used such tools during my research activity and I am wary of their effectiveness, but they may be
helpful to others.

An all-in-one platform for research discovery and networking may be a goose chase, or it may be a matter of time.