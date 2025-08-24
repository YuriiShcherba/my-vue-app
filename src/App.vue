<script setup>
    import { ref, computed, onMounted } from 'vue';
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

    const isWorkoutComplete = computed(() => {
        const currWorkout = data.value?.[selectedWorkout.value];
        if (!currWorkout) {
            return false;
        }

        const isCompleteCheck = Object.values(currWorkout).every(ex => !!ex);
        return isCompleteCheck;
    });

    const firstIncompleteWorkoutIndex = computed(() => {
        const allWorkouts = data.value;
        if (!allWorkouts) { return -1; }

        //loop every key value+pair and check wether workout is done or no
        for (const [index, workout] of Object.entries(allWorkouts)) {
            const isComplete = Object.values(workout).every(ex => !!ex);
            if (!isComplete) {
                return parseInt(index);
            }
        }

        return -1;
    });

    const handleChangeDisplay = (idx) => {
        selectedDisplay.value = idx
    }

    const handleSelectWorkout = (idx) => {
        selectedDisplay.value = 3;
        selectedWorkout.value = idx;
    }

    const handleSaveWorkout = () => {
        localStorage.setItem('workouts', JSON.stringify(data.value));
        selectedDisplay.value = 2;
        selectedWorkout.value = -1;
    }

    const handleResetPlan = () => {
        selectedDisplay.value = 2;
        selectedWorkout.value = -1;
        data.value = defaultData;
        localStorage.removeItem('workouts');
    }

    onMounted(() => {
        console.log('Mounted App.vue');
        if (!localStorage) { return; } //safety check
        const savedData = localStorage.getItem('workouts');
        if (savedData) {
            data.value = JSON.parse(savedData);
            selectedDisplay.value = 2; //go to dashboard if there's saved data
        }
    });
</script>

<template>
    <Layout>
        <Welcome :handleChangeDisplay="handleChangeDisplay" v-if="selectedDisplay == 1"/>
        <Dashboard :handleResetPlan="handleResetPlan" :firstIncompleteWorkoutIndex="firstIncompleteWorkoutIndex" :handleSelectWorkout="handleSelectWorkout" v-if="selectedDisplay == 2"/>
        <Workout :handleSaveWorkout="handleSaveWorkout" :isWorkoutComplete="isWorkoutComplete" :data="data" :selectedWorkout="selectedWorkout" v-if="workoutProgram?.[selectedWorkout]"/>
    </Layout>
</template>

<style scoped>

</style>
