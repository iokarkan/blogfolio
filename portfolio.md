---
layout: page
title: My work
permalink: portfolio
---


## Project: [Journal Hub](https://www.journal-hub.org)
----
#### Tech Stack
- **Backend:** Flask, PostgreSQL, ChromaDB
- **Frontend:** TailwindCSS, DaisyUI, jQuery, MathJax
- **Deployment:** Docker, Cloudflare, nginx


#### Summary

<div class="flex flex-col gap-1 text-justify">
    <p>Journal Hub is a prototype online literature discussion platform, focused on publicly and privately curated
        collections
        of research publications.</p>
        
        <div class="flex flex-col md:flex-row gap-4">
            <div class="w-xl m-auto rounded-full">
                <a class="cboxElement" href="{{site.baseurl}}/assets/img/journal-hub/home.png"><img class="rounded-lg"
                    src="{{site.baseurl}}/assets/img/journal-hub/home.png" alt="Home page of the Journal Hub alpha.">
                </a>
                <figcaption class="text-center"><b>Home page of the Journal Hub alpha</b></figcaption>
            </div>
            <div class="w-xs m-auto rounded-full">
                <a class="cboxElement" href="{{site.baseurl}}/assets/img/journal-hub/showcase.png">
                    <img class="rounded-lg" src="{{site.baseurl}}/assets/img/journal-hub/showcase.png"
                    alt="An article showcase in Journal Hub alpha.">
                </a>
                <figcaption class="text-center"><b>An article showcase in Journal Hub alpha</b></figcaption>
            </div>
        </div>
        
        <p>As a platform, the vision of Journal Hub is to be an open space for discussing scientific research, and be a tool
            for
            research groups to collaborate on their own scientific scopes.</p>
        </div>
        
### ⚙️ Alpha development
<p class="text-justify">
Journal Hub is in its alpha development stage, however its core features have already been implemented. Along with a few
close-circle volunteers, we are currently rolling out environments for interested groups, and we welcome all your
feedback and ideas!
</p>

<div class="p-2 text-sm text-indigo-800 font-mono m-auto rounded-2xl bg-slate-200 text-center w-fit">
    If you're interested in contributing or using Journal Hub, please send me an email:
    <a href="mailto:journal.hub.team@gmail.com">journal.hub.team@gmail.com</a>
</div>

## AI Development
----
### Large Language Model Applications
#### Models and Libraries
- HuggingFace transformers, pipelines
- gradio
- langchain
- [llama.cpp](https://github.com/ggerganov/llama.cpp) using Stanford's `alpaca` and Nomic AI's `GPT4All`
<div class="m-auto rounded-2xl bg-slate-200 text-center w-fit">
    <p class="p-2 text-sm text-indigo-800 font-mono">Demo of a <a
            href="https://huggingface.co/spaces/ioanniskarkanias/chatbot-with-sources">Chatbot
            with Sources</a></p>
</div>

### Generative text-to-image and image-to-image
#### Models and Libraries
- Stable Diffusion
- [InvokeAI](https://github.com/invoke-ai/InvokeAI)
- [automatic1111/stable-diffusion-webui](https://github.com/AUTOMATIC1111/stable-diffusion-webui)

<div class="flex sm:flex-row sm:gap-5 sm:p-0 mx-6">
    <div class="sm:w-[30%] w-[30%] m-auto rounded-full">
        <img class="rounded-lg"
            src="{{site.baseurl}}/assets/img/vader-stable-diffusion/depositphotos_56832909-stock-photo-muscular-man-holding-ancient-sword.jpg">
    </div>
    <div class="mx-2 my-auto rounded-full">
        <span>⟶</span>
    </div>
    <div class="sm:w-[25%] w-[25%] m-auto rounded-full">
        <img class="rounded-lg" src="{{site.baseurl}}/assets/img/vader-stable-diffusion/pose.png">
    </div>
    <div class="mx-2 my-auto rounded-full">
        <span>⟶</span>
    </div>
    <div class="sm:w-[25%] w-[25%] m-auto rounded-full">
        <img class="rounded-lg" src="{{site.baseurl}}/assets/img/vader-stable-diffusion/vader-resolution-buttons.png">
    </div>
</div>
<div class="m-auto rounded-2xl bg-slate-200 text-center w-fit">
    <p class="p-2 text-sm text-indigo-800 font-mono">Check out this blog post: <a
            href="https://iokarkan.github.io/2023/04/07/stable-diffusion-control.html">Controlling generated images with
            Stable Diffusion</a></p>
</div>

## Research
----
### Applying multivariate methods in Experimental Particle Physics Analysis

#### Libraries
- numpy, pandas, scikit-learn, scipy
- py-$$\mathtt{ROOT}$$
- Keras

#### Summary
<p class="text-justify">
    During my doctorate research, I worked as an author of the ATLAS experiment under an analysis group focusing on a
    special category of particle interactions associated with di-boson (specifically $W^{\pm}Z$) production and
    scattering. The culmination of my thesis was to work with LHC data from the period between 2015 and 2018 to validate
    the
    observation of a purely electroweak signal and set experimental limits for New Physics, based on an extension of
    terms
    of the Standard Model Lagrangian of Particle Physics.
</p>

<div class="">
    <div class="m-auto w-1/2 text-center"><img class="m-auto" src="{{site.baseurl}}/assets/img/PhD-nll.png"
            alt="Likelihood-ratio for the observation of the purely electroweak $W^{\pm}Z$ signal">
        <figcaption style="align: center;"><b>Likelihood-ratio for the observation of the purely electroweak $W^{\pm}Z$
                signal</b></figcaption>
    </div>
</div>

<p class="text-justify">
    The statistical analysis compared single and multi-variate methods (traditionally Boosted Decision Trees) to an
    application of Neural Network trained utilizing a selection of topological features discriminating the various
    exepected
    theoretical signal signatures from the Standard Model background, with the resulting limits on novel interaction
    being
    far more constrained in the latter case. Limits on the New Physics (EFT) model parameters were extracted using the
    profile-likelihood ratio test statistic at a 68% and 95% C.L., being close to $0$ as no significant deviations in
    terms of previously unobserved interactions have been found.
</p>

<div class="mx-5 grid grid-cols-2 gap-10">
    <div class="m-auto text-center"><img src="{{site.baseurl}}/assets/img/PhD-c_scan_M1M0.png"
            alt="Two-dimensional contour plot with limits on EFT model parameters">
        <figcaption style="align: center;"><b>Two-dimensional contour plot with limits on EFT model parameters</b>
        </figcaption>
    </div>
    <div class="m-auto text-center"><img src="{{site.baseurl}}/assets/img/PhD-importance.jpg"
            alt="High-level topological kinematic features used in Neural Network training">
        <figcaption style="align: center;"><b>High-level topological kinematic features used in Neural Network
                training</b></figcaption>
    </div>
</div>

<br />

<div class="m-auto rounded-2xl bg-slate-200 text-center w-fit">
    <p class="p-2 text-sm text-indigo-800 font-mono">You may find a full presentation of my thesis <a
            class="iframe cboxElement" href="{{site.baseurl}}/assets/pdf/Ioannis-Karkanias-PhD-Thesis-Presentation.pdf"
            title="PhD Presentation - 13/5/2022">here</a>!</p>
</div>

<script>
    jQuery('a.iframe').colorbox({ iframe: true, height: "700px", width: "80vw%" });
</script>