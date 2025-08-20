<script setup>
    import { ref } from 'vue';
    import Welcome from './components/pages/Welcome.vue';
    import Workout from './components/pages/Workout.vue';
    import Layout from './components/layouts/Layout.vue';
    import Dashboard from './components/pages/Dashboard.vue';
    import { workoutProgram } from './utils';

    const defaultData = {};
    for (let workoutIdx in workoutProgram) {
        const workoutData = workoutProgram[workoutIdx]
        // a loop to iterate through every workout
        defaultData[workoutIdx] = {}

        //nested loop to loop throgh every exercise within a workout and initialize its input value
        for (let e of workoutData.workout) {
            defaultData[workoutIdx][e.name] = '';
        }
    }
    const selectedDisplay = ref(1);
    const data = ref(defaultData);
    const selectedWorkout = ref(-1)

    const handleChangeDisplay = (idx) => {
        selectedDisplay.value = idx
    }

    const handleSelectWorkout = (idx) => {
        selectedDisplay.value = 3;
        selectedWorkout.value = idx;
        console.log(selectedWorkout.value);
    }

    const handleSaveWorkout = () => {
        localStorage.setItem('workouts', JSON.stringify(data.value));
        selectedDisplay.value = 2;
        selectedWorkout.value = -1;
    }
</script>

<template>
    <Layout>
        <Welcome :handleChangeDisplay="handleChangeDisplay" v-if="selectedDisplay == 1"/>
        <Dashboard :handleSelectWorkout="handleSelectWorkout" v-if="selectedDisplay == 2"/>
        <Workout :data="data" :selectedWorkout="selectedWorkout" v-if="workoutProgram?.[selectedWorkout]"/>
    </Layout>
</template>

<style scoped>

</style>
