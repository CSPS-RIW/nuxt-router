<script setup>
import { ref, onMounted, watch, computed } from 'vue'

const messages = ref([])
const name = ref()
const inputContent = ref()

const messagesAscending = computed(() => messages.value.sort((a, b) => {
    return b.createdAt - a.createdAt
}))

const addMesage = () => {
    if (inputContent.value?.trim() === '' || inputContent.value === undefined) {
        return
    }
    messages.value.push({
        content: inputContent.value,
        timeOfCreation: new Date().getTime()
    })

    inputContent.value = ''

}

watch(messages, newMessage => {
    localStorage.setItem('riwThings', JSON.stringify(newMessage))
}, { deep: true })

watch(name, (newName) => {
    localStorage.setItem('myName', newName)
})

onMounted(() => {
    name.value = localStorage.getItem('myName')
    messages.value = JSON.parse(localStorage.getItem('riwThings')) || []
})

definePageMeta({
    title: 'Home'
})

</script>
<template>
    <div class="home">
        <h2>Hello {{ name }}</h2>
        <input type="text" name="message" id="message" class="mt-sm custom-input"
            placeholder="Write your name here" v-model="name" autocomplete="off">
        <form action="POST" @submit.prevent="addMesage" class="riw-form">
            <p class="instructions mt-sm">Write something about RIW</p>
            <input type="text" placeholder="Write somenting here"
                class="mt-xsm custom-input" v-model="inputContent">
            <button class="btn btn-secondary">Save your Nuxt message</button>
        </form>
        <div class="about-show" aria-live="polite">
            <section>
                <h2>
                    Your RIW Messages
                </h2>
                <div v-for="message in messagesAscending" :key="message.content">
                    <p class="fun-text">{{ message.content }}</p>
                </div>
            </section>
        </div>


    </div>
</template>

<style scoped lang="scss">
.home {
    width: 80vw;
    display: flex;
    flex-flow: column wrap;
    justify-content: center;
    align-items: center;
}

h1 {
    color: green;
}

.fixed {
    width: 30rem;
}

.btn {
    margin: 1rem;
    padding: 0.5rem 1rem;
    height: 3rem;
    // margin: auto;
    font-size: 1.5rem;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    filter: grayscale(0);
    transition: filter 250ms ease-in;

    &:hover {
        filter: grayscale(70%);
    }

    &-primary {
        color: #fff;
        background-color: #369;
    }

    &-secondary {
        color: #fff;
        background-color: #3a0763;
    }
}

.custom-input {
    border: 1px solid #333;
    border-radius: 5px;
    width: 20rem;
    height: 3rem;
    font-size: 1.25rem;
    padding-left: 0.75rem;
}

.riw-form {
    display: flex;
    flex-flow: column wrap;
    justify-items: flex-start;
    align-content: center;

    .btn {
        margin-right: auto;
    }
}

.mb-sm {
    margin-bottom: 1rem;
}

.mt-sm {
    margin-top: 1rem;
}

.mt-xsm {
    margin-top: 0.5rem;
}
</style>
