<template>
    <section id="landing" class="text-white">
        <div class="py-5 container-fluid bg-dark min-vh-100">
            <div class="row my-5 py-5 justify-content-center align-items-center">

                <div class="col-12 col-lg-4 text-center text-md-start mb-4 mb-md-0 order-md-1">
                    <h1 id="title" class="wrapped-heading">
                        Let's code your <span id="landing-website">website</span> to life!
                    </h1>
                    <a href="#contact" id="base" class="mt-4 d-inline-block text-decoration-none">LET'S TALK</a>
                </div>

                <div class="col-12 col-lg-3 text-center order-md-2">
                    <DotLottieVue class="lottie-animation w-100" autoplay loop
                        src="/Animation - 1750150534672.lottie" />
                </div>
            </div>
        </div>
    </section>
</template>

<script setup>
import { DotLottieVue } from '@lottiefiles/dotlottie-vue'
</script>