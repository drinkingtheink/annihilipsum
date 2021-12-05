<template>
    <div class="the-passage">
        <p>
            <span v-for="word in passageInWords" :key="word">
                {{ word }}
            </span>
        </p>
    </div>
</template>

<script>
export default {
    name: 'Passage',
    props: {
        passage: String,
        passageInWords: Array
    }
}
</script>

<style>
.the-passage p {
  font-family: 'Smooch', cursive;
  font-size: 2.25rem;
}
</style>
