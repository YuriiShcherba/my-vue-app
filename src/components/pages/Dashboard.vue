<script setup>
    import Grid from '../Grid.vue';
    import { gymHealthFacts } from '../../utils';

    const randomNumber = Math.floor(Math.random() * gymHealthFacts.length);
    const todaysFact = gymHealthFacts[randomNumber];
    const props = defineProps({
        handleSelectWorkout: Function,
        firstIncompleteWorkoutIndex: Number
    });
</script>

<template>
    <section id="dashboard">
        <div class="card tip-container">
            <h2>Welcome</h2>
            <div>
                <p class="tip">
                    <strong>Daily Tip</strong><br/>
                    {{ todaysFact }}
                </p>
            </div>
            <button @click="() => handleSelectWorkout(firstIncompleteWorkoutIndex < 0 ? 0 : firstIncompleteWorkoutIndex)">Start workout &rarr;</button>
        </div>
        <Grid v-bind="props" />
    </section>
</template>

<style scoped>
    #dashboard .card.tip-container {
        margin-bottom: 1rem;
    }
</style>
