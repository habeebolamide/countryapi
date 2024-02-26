<template>
    <div class="header">
        <span class="logo"> <b>Where in the world</b></span>
        <label class="switcher">
            <input type="checkbox" v-model="isDarkTheme">
            <span class="slider round"></span>
        </label>
        <div class="logo ml-auto">
            <span v-if="isDarkTheme">Light Mode</span>
            <span v-else>Dark Mode</span>
        </div>
    </div>
</template>

<script>
export default {
    name: 'HeaderComponent',
    components: {
    },
    data: () => {
        return {
            isDarkTheme: localStorage.getItem('theme') === 'dark'
        }
    },
    watch: {
        isDarkTheme: {
            handler(val) {
                const theme = val ? 'dark' : 'light';
                document.documentElement.setAttribute('data-theme', theme);
                localStorage.setItem('theme', theme);
            },
            immediate: true
        }
    }
}
</script>

<style lang="sass">
@import "@/assets/sass/_variables.sass"

h1,h2,h3,h4,h5,h6,p
    color: var(--color-text-primary)
.form-control
    background: var(--color-background-secondary)
.form-control::focus
    background: var(--color-background-primary)
.card
    background: var(--color-background-primary)
.card-body
    background: var(--color-background-primary)
.header
	height: $header-height
	background: var(--color-background-secondary)
	display: flex
	align-items: center
	padding: 35px 15px

	.logo
		font-size: 20px
		font-weight: 600
		color: var(--color-text-primary)
		margin-right: 15px

    
	.switcher
		position: relative
		display: inline-block
		width: 44px
		height: 22px
		input
			opacity: 0
			width: 0
			height: 0
		.slider
			position: absolute
			cursor: pointer
			top: 0
			left: 0
			right: 0
			bottom: 0
			background-color: #d7d7d7
			transition: .3s
			&.round
				border-radius: 34px
				&:before
					position: absolute
					content: ""
					height: 16px
					width: 16px
					left: 4px
					bottom: 3px
					background-color: white
					transition: .3s
					border-radius: 50%
		input:checked + .slider
			background-color: var(--color-accent)
		input:checked + .slider:before
			transform: translateX(20px)
</style>

<style>
.header {
    box-shadow: var(--color-boxshadow-primary) 0px 7px 29px 0px;
}

.form-control {
    border: none;
    color: var(--color-text-primary);
    box-shadow: var(--color-boxshadow-primary) 0px 7px 29px 0px;
}

.form-control:focus {
    background: var(--color-background-secondary);
    border: none;
    color: var(--color-text-primary);
    box-shadow: var(--color-boxshadow-primary) 0px 7px 29px 0px;
}

.card {
    border: none;
    box-shadow: var(--color-boxshadow-primary) 0px 7px 29px 0px;
}
</style>