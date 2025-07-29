<script setup>
    import Navbar from './components/1NavbarComponent.vue';
    import LandingComponent from './components/2LandingComponent.vue';
    import ProfileComponent from './components/3ProfileComponent.vue';
    import ProjectsComponent from './components/4ProjectsComponent.vue';
    import ToolsComponent from './components/5ToolsComponent.vue';
    import ContactsComponent from './components/6ContactsComponent.vue';
    import FooterComponent from './components/7FooterComponent.vue';
</script>

<template>
    <Navbar />
    <div>
        <LandingComponent />
        <ProfileComponent />
        <ProjectsComponent />
        <ToolsComponent />
        <ContactsComponent />
    </div>
    <FooterComponent />
</template>

<style scoped>

</style>
