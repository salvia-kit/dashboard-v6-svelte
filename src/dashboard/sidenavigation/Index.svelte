<script>
	import { open } from '../provider/store';
	import SidenavItems from './Items.svelte';
	import SidenavHeader from './Header.svelte';
	import { clickOutside } from '../provider/click-outside';

	const style = {
		mobilePosition: {
			left: 'left-0',
			right: 'right-0'
		},
		close: `hidden`,
		container: `pb-32 lg:pb-12`,
		open: `absolute w-8/12 z-40 sm:w-5/12`,
		default: `bg-[#25074d] h-screen overflow-y-auto top-0 lg:flex lg:relative lg:w-64 lg:z-auto`
	};

	const closeSidenav = () => {
		//close sidenav on click outside when viewport is less than 1024px
		if (window.innerWidth < 1024) {
			$open = false;
		}
	};
	export let mobilePosition = 'right';
</script>

<aside
	use:clickOutside
	on:click_outside={closeSidenav}
	class={`${style.default} ${style.mobilePosition[mobilePosition]}
       ${$open ? style.open : style.close} scrollbar`}
>
	<div class={style.container}>
		<SidenavHeader />
		<SidenavItems />
	</div>
</aside>

<style>
	.scrollbar::-webkit-scrollbar {
		width: 0;
		background: transparent; /* hide sidenav scrollbar on Chrome, Opera and other webkit Browsers*/
	}
	.scrollbar {
		-ms-overflow-style: none;
	}
</style>
