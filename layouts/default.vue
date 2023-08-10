<template>
    <div>
       <Title>Nuxt 3</Title>
        <nav>
            <ul>
                <li><NuxtLink to ="/" href="">Home</NuxtLink></li>
                <li><NuxtLink to ="/about" href="">About</NuxtLink></li>
                <li><NuxtLink to ="/contact" href="">Contact</NuxtLink></li>
            </ul>
             <slot />
         </nav>
    </div>
</template>
