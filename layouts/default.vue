<template>
    <div>
        <AppHeader />
            <main>
                <slot>
                    Some content goes here
                </slot>
            </main>
        <AppFooter />
    </div>
</template>

<style>
    main {
        padding: 1rem;
    }
</style>