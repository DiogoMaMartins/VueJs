import Vue from 'vue';
import Router from 'vue-router';
import Home from './views/Home.vue';

Vue.use(Router)

export default new Route({
	routes: [
		{
			path: '/',
			name: '/home',
			component: Home
		},
		{
			path: '/about',
			name: 'about',
			component: () => import(/*webpackChunckName:"about" */ './views/About.vue')
		}
	]
})