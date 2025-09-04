<template>
    <div class="min-h-screen flex flex-col">
        <Toolbar />
        <div class="p-2 bg-slate-50 flex-grow">
            <slot />
        </div>
        <Footer />
    </div>
</template>