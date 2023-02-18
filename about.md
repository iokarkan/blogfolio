---
layout: page
title: About me
permalink: about
---

<!-- https://stackoverflow.com/questions/40453881/change-of-opacity-using-css-transition-and-vanilla-javascript-works-only-when-fa -->

<div class="md:grid md:grid-cols-2 md:gap-3">

    <!-- Modal Functionality, use: -->
    <!-- https://tailwindui.com/components/application-ui/overlays/modals -->

    <div class="m-auto">
        <p>My name is Ioannis (John) Karkanias, a physicist with a passion for Machine Learning and computational
            statistics.
        <div class="m-auto rounded-2xl bg-slate-700 text-center w-fit">
            <!-- <p class="pt-2 text-center font-bold text-lg text-slate-600 font-mono">Note</p> -->
            <!-- <p class="p-2 text-sm text-white font-mono">
                You can see my CV <a class="text-blue-600 dark:text-slate-100 hover:underline"
                    href="{{site.baseurl}}/assets/pdf/CV_IoannisKarkanias.pdf">here</a>!</p> -->
            <p class="p-2 text-sm text-white font-mono">
                You can see my CV <button type='button' id="modal-open" class="text-blue-600 dark:text-slate-100 underline"
                    href="{{site.baseurl}}/assets/pdf/CV_IoannisKarkanias.pdf">here</button>!</p>

            <div class="relative z-10 hidden" aria-labelledby="modal-title" role="dialog" aria-modal="true"
                id="modal-window">
                <div class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity"></div>
                <div class="fixed inset-0 z-10 overflow-y-auto">
                    <div class="flex min-h-full items-end justify-center p-4 text-center sm:items-center sm:p-0">
                        <div
                            class="relative transform overflow-hidden rounded-lg bg-white text-left shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-lg">
                            <!-- <div class="bg-white px-4 pt-5 pb-4 sm:p-6 sm:pb-4"> -->
                            <!-- <div class="sm:flex sm:items-start"> -->
                            <iframe src="{{site.baseurl}}/assets/pdf/CV_IoannisKarkanias.pdf" width="100%"
                                height="450px">
                            </iframe>
                            <!-- </div> -->
                            <!-- </div> -->
                            <div class="bg-gray-50 px-4 py-3 sm:flex sm:flex-row-reverse sm:px-6">
                                <!-- <button type="button" class="inline-flex w-full justify-center rounded-md border border-transparent bg-red-600 px-4 py-2 text-base font-medium text-white shadow-sm hover:bg-red-700 focus:outline-none focus:ring-2 focus:ring-red-500 focus:ring-offset-2 sm:ml-3 sm:w-auto sm:text-sm">Deactivate</button> -->
                                <button type="button"
                                    class="mt-3 inline-flex w-full justify-center rounded-md border border-gray-300 bg-white px-4 py-2 text-base font-medium text-gray-700 shadow-sm hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 sm:mt-0 sm:ml-3 sm:w-auto sm:text-sm"
                                    id="modal-close">Close</button>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

        </div>

        My current interests
        revolve around Natural Language Processing in python.</p>
    </div>

    <div class="m-auto md:w-2/3 w-1/2">
        <div>
            <img class="" src="{{site.baseurl}}/assets/img/portrait_bus_OCR.jpg">
        </div>
        <div class="text-md">
            <figcaption class="text-center">
                (Object Detection using
                <a href="https://github.com/dmlc/gluon-cv">GluonCV
                </a>)
            </figcaption>
        </div>
    </div>

</div>

<script>

    var modal = document.getElementById('modal-window');
    var modal_close = document.getElementById('modal-close');
    var modal_open = document.getElementById('modal-open');

    // console.log(modal)
    // console.log(modal_close)
    // console.log(modal_open)

    modal_open.addEventListener("click", function clicked() {

        modal.classList.remove("hidden");
        // console.log('clicked')
    })
    modal_close.addEventListener("click", function clicked() {
        
        modal.classList.add("hidden");
        // console.log('clicked')
    })
    

</script>

<!-- TODO: Education and work summary -->

### Blogging

I use a blog to communicate and share my interests, as well as my tinkering, hoping to help or inspire others as I have
been aided and inspired by similar outlets!

> "Nothing in science has any value to society if it is not communicated." \\
> Anne Roe

Feel free to contact me via [📧](ioannis.karkanias@gmail.com) or
[Linked-in](https://www.linkedin.com/in/ioannis-karkanias-71996a1aa/) if you want to talk!