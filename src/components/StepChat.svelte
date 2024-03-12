<script>
    import { Textarea, Label, Spinner } from 'flowbite-svelte'
    import { appStatusInfo } from '../store';
  import { setAppStatusError } from '../store';
    const { id, url, pages } = $appStatusInfo;

    let textareaprops = {
        id: 'question',
        name: 'question-input',
        label: 'Question Input',
        rows: 4,
        placeholder: 'Ask me anything about this document.'
    };

    let answer = ''
    let loading = false;

    const numOfImagesToShow = Math.min(pages, 4)
    const images = Array.from({ length: numOfImagesToShow }, (_, i) => {
        const page = i + 1
        return url
            .replace('/upload/', `/upload/w_200,h_250,c_fill,pg_${page}/`)
            .replace('.pdf', '.jpg')
    })

    

    const handleSubmit = async (event) => {
        event.preventDefault()

        loading = true

        const question = event.target.question.value
        try{
            const res = await fetch("/api/ask", {
                headers: {
                    "Content-Type": "application/json",
                },
                body: JSON.stringify({
                    id,
                    question,
                }),
            })

            if (!res.ok) {
                loading = false
                console.error("Error asking question")
                return
            }

            
            const { answer: apiAnswer } = await res.json()
            answer = apiAnswer
        } catch (e) {
            setAppStatusError()
        } finally {
            loading = false
        }
    }
</script>

<div class="grid grid-cols-4 gap-2">
    {#each images as image}
        <img
          class="rounded w-full h-auto aspect-[200/250]"
          src={image}
          alt="PDF page"
        />
    {/each}
</div>

<form class="mt-8" on:submit={handleSubmit}>
    <Textarea {...textareaprops} />
</form>

{#if loading}
    <div class="flex justify-center items-center flex-col gap-y-2">
        <Spinner />
        <p class="opacity-75" style="color:white">Waiting for response...</p>
    </div>
{/if}

{#if answer}
    <div class="mt-8">
        <p>{answer}</p>
    </div>
{/if}