<script>
	import img1 from "$lib/assets/img-1.jpg";
	import img2 from "$lib/assets/img-2.jpg";
	import img3 from "$lib/assets/img-3.jpg";
	import img4 from "$lib/assets/img-4.jpg";

	let uniqueId = () =>
		Date.now().toString(36) + Math.random().toString(36).substring(2);

	$: shopItemsData = [
		{
			id: uniqueId(),
			name: "Casual shirt",
			price: 45,
			desc: "this is the sample text",
			img: img1,
		},
		{
			id: uniqueId(),
			name: "Casual shirt",
			price: 120,
			desc: "Lorem7",
			img: img2,
		},
		{
			id: uniqueId(),
			name: "Casual shirt",
			price: 45,
			desc: "Lorem7",
			img: img3,
		},
		{
			id: uniqueId(),
			name: "Mens suits",
			price: 300,
			desc: "Lorem7",
			img: img4,
		},
	];

	$: basket = [];

	// svelte wayでやるのはどうやんのかな?
	function increment(el) {
		el.quantity = 0;
		console.log(el);
	}

	function decrement(id) {
		basket = basket.filter((el) => el.id !== id);
		console.log(basket);
	}
</script>

<a href="/">home</a>

<!-- navbar -->
<div class="navbar">
	<h2>Clothing Store</h2>
	<div class="cart">
		<div id="cartAmount" class="cartAmount">0</div>
		<i class="bi bi-cart-plus" />
	</div>
</div>
<!-- shopping card js -->
<div class="shop" id="shop" />

{#each shopItemsData as el, i (el.id)}
	<div class="item">
		<img width="220" height="200" src={el.img} alt="" />
		<div class="details">
			<h3>{el.name}</h3>
			<p>{el.desc}</p>
			<div class="price-quantity">
				<h2>$ {el.price}</h2>
				<div class="buttons">
					<button on:click={decrement(el)} class="bi bi-plus-lg">-</button>
					<div id={el.id} class="quantity">0</div>
					<button on:click={increment(el)} class="bi bi-plus-lg">+</button>
				</div>
			</div>
		</div>
	</div>
{/each}
