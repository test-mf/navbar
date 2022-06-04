<template>
	<ul class="list">
		<li class="list__item">
			{{ userInfo.firstName }} {{ userInfo.middleName }} {{ userInfo.lastName }}
		</li>
		<li class="list__item">Баланс: {{ balance }} руб.</li>
		<li class="list__item">
			<button v-on:click="signOut">Выйти</button>
		</li>
	</ul>
</template>

<script>
import { getUserBalance, getUserInfo, userSignOut } from "@test-mf/api";
import { invokeEvent } from "@test-mf/eventbus";

export default {
	name: "UserItems",
	data() {
		return { userInfo: {}, balance: 0 };
	},
	mounted() {
		getUserInfo().then(userInfo => (this.userInfo = userInfo));
		getUserBalance().then(balance => (this.balance = balance));
	},
	methods: {
		signOut() {
			userSignOut();
			invokeEvent("userSignOut");
		},
	},
};
</script>
