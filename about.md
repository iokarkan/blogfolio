---
layout: page
title: About me
permalink: about
---

<!-- https://stackoverflow.com/questions/40453881/change-of-opacity-using-css-transition-and-vanilla-javascript-works-only-when-fa -->

<div class="md:grid md:grid-cols-2 md:gap-3">

    <!-- Modal Functionality, use: -->
    <!-- https://tailwindui.com/components/application-ui/overlays/modals -->

    <div class="m-auto text-justify">

        <p>My name is Ioannis (John) Karkanias, a physicist with a passion for Machine Learning, Computational
            Statistics and Web Development. </p>

        <div class="m-auto rounded-2xl bg-slate-200  text-center w-fit">
            <!-- <p class="pt-2 text-center font-bold text-lg text-slate-600 font-mono">Note</p> -->
            <!-- <p class="p-2 text-sm text-white font-mono">
                    You can see my CV <a class="text-blue-600 dark:text-slate-100 hover:underline"
                        href="{{site.baseurl}}/assets/pdf/CV__Ioannis_Karkanias.pdf">here</a>!</p> -->
            <p class="p-2 text-sm text-indigo-800 font-mono">
                You can see my CV <a class="iframe cboxElement"
                href="{{site.baseurl}}/assets/pdf/CV_Ioannis_Karkanias.pdf"
                title="CV - Ioannis Karkanias (2023)">here</a>!
            </p>
        </div>

        <p>
            I am the creator and developer for the <a href="{% link portfolio.md %}">Journal Hub</a> project, an open literature discussion platform.
        </p>


        <p>
            My current ML interests
            revolve around open-source Generative Transformer-based Deep Learning models.
        </p>
    </div>

    <div class="m-auto md:w-2/3 w-1/2">
        <div>
            <img class="" src="{{site.baseurl}}/assets/img/portrait_bus_OCR.jpg">
        </div>
        <div class="text-md">
            <figcaption class="text-center">
                (Object Detection using
                <a href="https://github.com/dmlc/gluon-cv">GluonCV</a>)
            </figcaption>
        </div>
    </div>

</div>

<script>
    jQuery('a.iframe').colorbox({ iframe: true, height: "700px", width: "80vw%" });

</script>


<!-- TODO: Education and work summary -->

### Blogging

I use a blog to communicate and share my interests, as well as my tinkering, hoping to help or inspire others as I have
been aided and inspired by similar outlets!

> "Nothing in science has any value to society if it is not communicated." \\
> Anne Roe

Feel free to contact me via [📧](ioannis.karkanias@gmail.com) or
[Linked-in](https://www.linkedin.com/in/ioannis-karkanias-71996a1aa/) if you want to talk!