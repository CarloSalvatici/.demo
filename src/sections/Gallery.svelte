<script>
    export let galleryData

	//Logic for organizing images
	let showAdditionalImages = false
	let images1 = []
	let images2 = []
	console.log(images2)
	if(galleryData.length > 3) {
		images1 = galleryData.slice(0, 3);
		images2 = galleryData.slice(3, galleryData.length)
	} else {
		images1 = galleryData
	}
	
	

	let enlargeBool = false
	let enlargedImage
	const enlargeImage = (imageData) => {
		enlargedImage = {
			URL: imageData.URL,
			name: imageData.name
		}
		enlargeBool = true
	}

	
</script>

<main>
    <div id="gallery" class="gallery">
		<!--Preview for showing the list of images-->
        {#each images1 as imageData}
            <button on:click={() => {enlargeImage(imageData)}} class="gallery-image">
				<span>{imageData.name}</span>
                <img src={imageData.URL} alt={imageData.name}/>
            </button>
        {/each}
		{#if images2.length > 0}
			{#if showAdditionalImages}
				{#each images2 as imageData}
					<button on:click={() => {enlargeImage(imageData)}} class="gallery-image">
						<span>{imageData.name}</span>
						<img src={imageData.URL} alt={imageData.name}/>
					</button>
				{/each}
			{:else}
				<button class="load-images" on:click={() => {showAdditionalImages = true}}>Load Additional Images</button>
			{/if}
		{/if}
		<!--Code for the enlarged image when clicked-->
		{#if enlargeBool}
			<button on:click={() => {enlargeBool = false}} class="enlarged-image">
				<div>{enlargedImage.name}</div>
				<img src={enlargedImage.URL} alt={enlargedImage.name}/>
			</button>
		{/if}
    </div>
</main>

<style>
    .gallery {
		display: block;
		flex-wrap: wrap;
		justify-content: space-around;
		margin-bottom: 20px;
		margin-top: 20px;

	}

	.gallery-image {
		position: relative;
        display: inline;
        align-items: center;
        justify-content: center;
		margin-bottom: 18px !important;
		flex-grow: 1;
		margin: 2%;
		border: none;
		background: none;
	}
	.gallery-image > img {
		object-fit: cover;
        max-width: 300px;
        min-height: 300px;
        min-width: 300px;
        max-height: 300px;
        width: auto;
        height: auto;
		transition: .3s all;
		border: 1px black solid;
		z-index: 1;
	}
	.gallery-image > span {
		position: absolute;
		text-align: center;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		font-weight: bold;
		color: black;
		font-size: 1.5em;
		opacity: 0%;
		transition: .3s all;
	}
	.gallery-image:hover > img {
		transform: scale(1.04);
		opacity: 50%;
		z-index: 0;
	}
	.gallery-image:hover > span {
		opacity: 100%;
		z-index: 2;
	}

	.load-images {
		display: block;
		margin: auto;
	}

	.enlarged-image {
		position: fixed;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		display: block;
		flex-wrap: wrap;
        align-items: center;
        justify-content: center;
		flex-grow: 1;
		height: 100%;
		width: 100%;
		border: none;
		background: rgba(0, 0, 0, 0.726);
		z-index: 4;
	}
	.enlarged-image > img {
		object-fit: cover;
        width: auto;
        height: auto;
		max-width: 90vw;
		max-height: 90vh;
		transition: .3s all;
		border: 1px black solid;
		
	}
	.enlarged-image > div {
		color: white;
		font-size: 1.5em;
	}

	.load-images:hover {
		background: rgba(220, 219, 168, 0.4);
		transition: .3s all;
		cursor: pointer;
	}

	.load-images {
		border: 2px black solid;
		background: none;
		width: fit-content;
		margin: auto;
	}

</style>