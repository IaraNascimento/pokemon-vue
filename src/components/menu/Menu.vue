
<template>
    <nav class="background">
        <img class="logo" src="./../../assets/images/logo.png" />
        <ul class="nav-list">       
            <li v-for="route in routes">
                <router-link class="nav-list-link" :to="route.path">
                    {{ route.title }}
                </router-link>
            </li>
        </ul>
    </nav>
</template>

<script>

export default {
    props: {
        routes: { type: Array, required: true }
    }
}

</script>

<style scoped lang="scss">

    .background {
        position: relative;
        display: flex;
        justify-content: space-between;
        align-items: flex-start;
        width: 100%;
        height: 160px;
        background-image: url("./../../assets/images/background.jpg");
        background-repeat: no-repeat;
        background-size: cover;
        background-position: center 72%;
        overflow: hidden;
    }

    .logo {
        max-height: 100%;
        max-width: 60%;
        padding: 24px;
        box-sizing: border-box;
    }

    .nav-list {
        display: inline-block;
        max-width: 40%;
        vertical-align: top;
        padding: 24px 24px 0 0;
        li {
            background-color: rgba(255, 255, 255, .3);
            border-radius: 4px;
            margin-bottom: 8px;
            padding: 8px 16px;
        }
        &-link {
            text-decoration: none;
        }
    }

    @media (min-width: 800px) {
        .background {
            background-position: center 78%;
        }
    }

</style>
