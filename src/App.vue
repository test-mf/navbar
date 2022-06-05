<template>
	<nav class="navbar">
		<div class="navbar__wrapper">
			<a href="#/" class="logo">
				<img src="./assets/logo.png" />
				@test-mg/navbar
			</a>
			<UserItems v-if="isSignIn" />
			<GuestItems v-if="!isSignIn" />
		</div>
	</nav>
</template>

<script>
import UserItems from "@/components/UserItems";
import GuestItems from "@/components/GuestItems";
import { isUserLogin } from "@test-mf/api";
import { handleEvent } from "@test-mf/eventbus";

export default {
	name: "NavBar",
	components: {
		GuestItems,
		UserItems,
	},
	data() {
		return { isSignIn: isUserLogin() };
	},
	mounted() {
		handleEvent("userSignIn", () => (this.isSignIn = true));
		handleEvent("userSignOut", () => (this.isSignIn = false));
	},
};
</script>

<style>
a {
	color: #555;
}

.navbar {
	font-family: sans-serif;
	position: fixed;
	top: 0;
	width: 100%;
	background-color: #fff;
	box-shadow: 1px 1px 1px 1px #ccc;
	height: 80px;
	display: flex;
	align-items: center;
	justify-content: center;
}

.navbar__wrapper {
	max-width: 1200px;
	width: 100%;
	display: flex;
	align-items: center;
	justify-content: space-between;
}

.logo {
	font-size: 1.5em;
	font-weight: bold;
	display: flex;
	align-items: center;
	gap: 10px;
}

.logo img {
	width: 40px;
}

.list {
	list-style: none;
	display: flex;
	align-items: center;
	gap: 15px;
}

.list__item {
}
</style>
