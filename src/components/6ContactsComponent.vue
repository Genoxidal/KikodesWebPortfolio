<template>
    <section id="contact" class="py-5 bg-light text-dark">
        <div class="container my-3">
            <h2 class="display-4 fw-bold mb-5 text-center">Let's <span class="bg-dark text-light">build</span>
                something together.</h2>

            <div class="row justify-content-center align-items-center g-3">

                <div class="col-12 col-md-6 col-lg-5">
                    <div class="map-container rounded shadow border border-2 border-dark">
                        <iframe
                            src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3861.329424771057!2d121.0608408!3d14.5802953!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x3397c81492f33951%3A0x40b177c0069702f1!2sUniversity%20of%20Asia%20and%20the%20Pacific%20(UA%26P)!5e0!3m2!1sen!2sph!4v1750168001988!5m2!1sen!2sph"
                            width="100%" height="450" allowfullscreen="" loading="lazy"
                            referrerpolicy="no-referrer-when-downgrade"></iframe>
                    </div>
                </div>

                <div class="col-12 col-md-6 col-lg-5">
                    <form @submit.prevent="submitForm" class="p-4 rounded shadow-sm bg-dark text-white" action="#"
                        target="_blank">
                        <div class="mb-3">
                            <label for="fullName" class="form-label visually-hidden">Your Name</label>
                            <input v-model="name" type="text" class="form-control" id="fullName" placeholder="Your Name"
                                required>
                        </div>
                        <div class="mb-3">
                            <label for="email" class="form-label visually-hidden">Email</label>
                            <input v-model="email" type="email" class="form-control" id="email" placeholder="Email"
                                required>
                        </div>
                        <div class="mb-3">
                            <label for="message" class="form-label visually-hidden">Message</label>
                            <textarea v-model="message" class="form-control" id="message" rows="5" placeholder="Message"
                                required></textarea>
                        </div>

                        <div class="d-flex justify-content-between align-items-center mt-4">
                            <div class="d-flex">
                                <a href="https://www.facebook.com/ryanoxales/" target="_blank" class="social-btn me-2">
                                    <img :src="facebook" alt="Facebook" width="24" height="24">
                                </a>
                                <a href="https://www.linkedin.com/in/ryan-oxales-3060932a6/" target="_blank"
                                    class="social-btn me-2">
                                    <img :src="linkedin" alt="LinkedIn" width="24" height="24">
                                </a>
                                <a href="https://github.com/Genoxidal" target="_blank" class="social-btn">
                                    <img :src="github" alt="GitHub" width="24" height="24">
                                </a>
                            </div>

                            <button type="submit" class="contact-submit-btn" :disabled="isLoading">{{ isLoading ?
                                "Sending..." : "Submit" }}</button>
                        </div>
                    </form>
                    <div class=" d-flex justify-content-center mt-2">
                        <div class="rounded border border-1 border-dark" ref="recaptchaContainer"></div>
                    </div>
                </div>

            </div>
        </div>
    </section>
</template>

<script setup>

import facebook from '@/assets/images/facebook.svg';
import linkedin from '@/assets/images/linkedin.svg';
import github from '@/assets/images/github.svg';

import { ref, onMounted, onBeforeUnmount } from 'vue';
import { Notyf } from 'notyf';
import 'notyf/notyf.min.css';

const notyf = new Notyf();
const WEB3FORMS_ACCESS_KEY = 'c8794c4f-1f10-4677-bcea-264b822d7645';

const subject = "New message from portfolio contact form";

const name = ref("");
const email = ref("");
const message = ref("");

const isLoading = ref(false);

// The submitForm() handler function sends the form data to web3forms and displays success or failure notifications toast.
const submitForm = async () => {

    if (!recaptchaToken.value) {
        notyf.error('Please verify that you are not a robot.');
        return;
    }

    // Set the loading state to true.
    isLoading.value = true;
    try {
        // Send the form data to web3forms using fetch() API.
        // The fetch() API is used to send HTTP requests to a server.
        // Sends a POST request to the https://api.web3forms.com/submit endpoint.
        // The request body contains the form data and the web3forms access key.
        const response = await fetch("https://api.web3forms.com/submit", {
            method: "POST",
            headers: {
                "Content-Type": "application/json",
                Accept: "application/json",
            },
            body: JSON.stringify({
                access_key: WEB3FORMS_ACCESS_KEY,
                subject: subject,
                name: name.value,
                email: email.value,
                message: message.value,
                // reply_to:email.value
            }),
        });
        const result = await response.json();

        // Check if the form submission was successful.
        // If successful, display success notification toast.
        if (result.success) {
            console.log(result);
            // Set the loading state to false.
            isLoading.value = false;
            notyf.success("Message Sent!");
        }
    } catch (error) {

        // If not successful, display failure notification toast.
        console.log(error);
        // Set the loading state to false.
        isLoading.value = false;
        notyf.error("Failed to send message.");
    } finally {
        resetRecaptcha();
    }
}

/** 
 * 
 * reCaptcha Integration 
 * 
 */

const SITE_KEY = '6Ldv2JIrAAAAAJMaQbUQKzjV5ir4bZrCebAeX3S7';  // Replace with your site key

const recaptchaContainer = ref(null);
const recaptchaWidgetId = ref(null);
const recaptchaToken = ref('');

// Callback called by reCAPTCHA when successful
function onRecaptchaSuccess(token) {
    recaptchaToken.value = token;
}

// Callback when expired
function onRecaptchaExpired() {
    recaptchaToken.value = '';
}

// Function to render the reCAPTCHA widget
function renderRecaptcha() {
    if (!window.grecaptcha) {
        console.error('reCAPTCHA not loaded');
        return;
    }

    recaptchaWidgetId.value = window.grecaptcha.render(recaptchaContainer.value, {
        sitekey: SITE_KEY,
        size: 'normal', // or 'compact'
        callback: onRecaptchaSuccess,
        'expired-callback': onRecaptchaExpired,
    });
}

// Function to reset reCAPTCHA 
function resetRecaptcha() {
    if (recaptchaWidgetId.value !== null) {
        window.grecaptcha.reset(recaptchaWidgetId.value);
        recaptchaToken.value = '';
    }
}



onMounted(() => {
    // This code waits for the Google reCAPTCHA library to load, then renders the reCAPTCHA widget using onMounted hook. 
    // The widget is rendered with grecaptcha.render(), which requires a sitekey. 
    // Callback functions handle success and expiration events. 
    // reCAPTCHA is reset upon form submission to clear the token.
    const interval = setInterval(() => {
        if (window.grecaptcha && window.grecaptcha.render) {
            renderRecaptcha();
            clearInterval(interval);
        }
    }, 100);

    onBeforeUnmount(() => {
        clearInterval(interval);
    });
});


</script>