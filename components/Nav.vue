<template>
    <nav>
        <ul>
            <li>
                <NuxtLink to="/">Nuxt Index</NuxtLink>
            </li>
            <li>
                <NuxtLink to="/about">Nuxt About</NuxtLink>
            </li>
        </ul>
    </nav>

</template>
<style scoped lang="scss">
nav {
    background-color: #346;
    padding-block: 1.5rem;
    padding-inline-end: 1.5rem;

    ul {
        display: flex;
        justify-content: flex-end;
        gap: 3em;
        list-style-type: none;

        a {
            color: #fff;
            text-decoration: none;

            &:visited {
                color: #fff;
            }

            &:hover,
            &.router-link-active {
                color: coral;
                border-bottom: 2px coral solid;
            }
        }
    }
}
</style>