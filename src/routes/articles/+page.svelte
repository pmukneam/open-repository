<script lang="ts">
	import { marked } from 'marked';
	import markedKatex from 'marked-katex-extension';

	const options = {
		throwOnError: false
	};
	let textHTML: string = `We know that $P_m(\\mathbb{R})$ has dimension of $m + 1$. To prove that a list of $m + 1$ vectors, $1, x-5, \\ldots, (x - 5)^m$ are basis for $P_m(\\mathbb{R})$, we only need to verify that these are linearly independent and the final result follows from Theorem of a linearly independent vectors of right length.

Consider,
        $$ a_0(1) + a_1(x - 5) + \\cdots + a_m(x-5)^m = 0 $$

It is easy to see that $a_0 = 0$. To obtain $a_1, \\ldots, a_m$, we take derivative of both side one by one and replacing all previous $a_{i - 1}$. After $m+1$ differentiation, we can infer that $a_m = 0$.Now $a_i = 0$, and we are done.`;

	// config marked
	marked.use(markedKatex(options));
</script>

<svelte:head>
	<link
		rel="stylesheet"
		href="https://cdn.jsdelivr.net/npm/katex@0.16.8/dist/katex.min.css"
		integrity="sha384-GvrOXuhMATgEsSwCs4smul74iXGOixntILdUW9XmUC6+HX0sLNAK3q71HotJqlAn"
		crossorigin="anonymous"
	/>
</svelte:head>
<div class="grid">
	<!-- Article area -->
	<div class="editor-grid">
		<div class="area-title">Article</div>
		{@html marked.parse(textHTML)}
	</div>

	<!-- Prview area -->
	<div class="preview">
		<div class="area-title">Notes</div>
	</div>
</div>

<style>
	.area-title {
		text-align: center;
		align-items: center;
		font-size: 30px;
		font-weight: bold;
	}
	div {
		padding: 0;
		margin: 0;
	}
	.grid {
		display: grid;
		grid-template-columns: 1fr 1fr;
		height: 100vh;
	}

	.editor {
		width: 100%;
		height: 100%;
		background-color: transparent;
		border: none;
		font-size: 20px;
	}

	.editor-grid {
		padding: 20px;
		overflow-y: auto;
		border-right-color: black;
		border-right-style: solid;
		border-right-width: 3px;
	}
	.preview {
		padding: 20px;
		overflow-y: auto;
	}

	.preview {
		background-color: #f8f8f8;
	}
</style>
