<script>
	import header from '../img/twitter-diamond.svg';
	// import palmsprings from '../img/palmsprings.png';
</script>

<div class="bg-container" style="background-image: url('https://images2.alphacoders.com/980/980225.png')">
	<div class="container bg-slate-100/40">
		<div class="grid grid-rows-1 grid-cols-6 pt-4">
			<div class="col-start-2 col-span-4 row-span-1">
				<h1 class="text-6xl">ＣＯＶＦＥＦＥ　•　コブフェフェ</h1>
        <h1><b>C</b>ONDITIONALLY <b>O</b>RTHOGONAL <b>V</b>ERTICES <b>F</b>OR <b>E</b>DGE <b>F</b>ILTERING IN <b>E</b>PIDEMICS</h1>
			</div>
			<div class="col-start-4 col-span-6 row-span-1">
				<h4 class="text-xl">
					<i>【ＢＹ　ＤＡＴＡＭＯＮＫＥＹ】</i><img class="object-scale-down h-10 w-8 inline" src={header} />
				</h4>
			</div>
		</div>

		<div class="items-center bg-slate-100/60">
			<ul class="col-span-6 p-3 mt-5">
				<li class="border-gray-400 mb-2"><a href="overview">ＯＶＥＲＶＩＥＷ　オーバービュー</a></li>
				<li class="border-gray-400 mb-2"><a href="simulated">ＳＩＭＵＬＡＴＩＯＮＳ　シミュ</a><img class="construction" src="https://i0.wp.com/www.bapl.org/wp-content/uploads/2019/02/old-under-construction-gif.gif?fit=266%2C266&ssl=1" /></li>
				<li class="border-gray-400 mb-2"><a href="empirical">ＥＭＰＩＲＩＣＡＬ エンピリカル</a></li>
				<li class="border-gray-400 mb-2"><a href="about">ＡＢＯＵＴ　アバウト</a></li>
			</ul>
		</div>
	</div>
</div>

<style>

  :global(.construction) {
    display: inline;
    vertical-align: middle;
    width: 25px;
    margin-left:5px;
    height: auto;
  }

	.container {
		font-family: '';
		font-size: x-large;
	}

	.bg-container {
		background-image: var(--background-image);
		background-repeat: repeat-x;
		background-size: contain;
		padding: 0px;
		margin: 0px;
		height: 100%;
		width: 100%;
		max-width: 100% !important;
		max-height: 100% !important;
		min-height: 100vh !important;
	}

	.container {
		opacity: 1;
		min-height: 100vh;
		max-width: 100% !important;
		width: 100%;
	}

	.container :global(a) {
		outline: none;
		text-decoration: none;
		padding: 2px 1px 0;
	}

	.container :global(a:link) {
		color: black;
	}

	.container :global(a:visited) {
		color: black;
	}
</style>
