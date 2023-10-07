<script>
    import { Label, Textarea, Button } from 'flowbite-svelte';
    import Intro from '$lib/Intro.svelte';

    export let data;
    
    let string
    let fileInput;
    let title="Title";
    let desc="Description";
    let link="Link";

    function handleFileInputChange(event) {
		fileToBase64(event.target.files[0]).then(base64String => {
			string = base64String;
		}).catch(error => {
			console.error(error);
		});
  	}


</script>

<Intro heading={data.meta.title} description={data.meta.description} />

<section class="bg-white dark:bg-gray-900">
	<div class="py-8 px-4 mx-auto max-w-screen-xl lg:px-12">
		<div class="lg:grid lg:grid-cols-2 card items-center mx-auto max-w-screen-xl rounded-lg">
            <div class="col-start-1 p-8 flex flex-col">
                <Label for="textarea" class="mb-2">Title</Label>
                <Textarea id="textarea" rows="2" bind:value={title} class="h-full max-h-96 resize-none"/>
            </div>
            <div class="col-start-1 p-8 flex flex-col">
                <Label for="textarea" class="mb-2">Description</Label>
                <Textarea id="textarea" rows="4" bind:value={desc} class="h-full max-h-96 resize-none"/>
            </div>
            <div class="col-start-2 p-8 flex flex-col bg-gray-100">
            </div>
            <button on:click={()=>fileInput.click()} type="button" class="mt-4 text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 mb-2 dark:bg-blue-600 dark:hover:bg-blue-700 focus:outline-none dark:focus:ring-blue-800">Browse image</button>
			<input type="file" class="hidden" accept="image/*" bind:this={fileInput} on:change={handleFileInputChange}>
            <div class="card-seo-twitter">
                <!-- <div class="card-seo-twitter__image" style="background-image:url(/images/meta-tags.jpg)"></div> -->
                <div class="card-seo-twitter__text">
                    <span class="card-seo-twitter__title">{title}</span>
                    <span class="card-seo-twitter__description">{desc}</span>
                    <span class="card-seo-twitter__link">{link}</span>
                </div>
            </div>
		</div>
	</div>
</section>

<style>
	.card {
		box-shadow: rgba(0, 0, 0, 0.1) 0 0 0 2px;
	}

	:is(.dark .card) {
		box-shadow: rgba(255, 255, 255, 0.5) 0 0 0 2px;
	}
</style>