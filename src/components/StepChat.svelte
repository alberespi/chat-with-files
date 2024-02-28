<script>
    import { Textarea, Label, Spinner } from 'flowbite-svelte'
    import { appStatusInfo } from '../store';
    const { id, url, pages } = $appStatusInfo;

    let textareaprops = {
        id: 'question-input',
        name: 'question-input',
        label: 'Question Input',
        rows: 4,
        placeholder: 'Lore ipsum...'
    };

    let loading = false;

    const numOfImagesToShow = Math.min(pages, 4)
    const images = Array.from({ length: numOfImagesToShow }, (_, i) => {

    })

    w_200,h_250,c_fill,pg_2

    const handleSubmit = () => {

    }
</script>

<form on:submit={handleSubmit}>
    <Textarea {...textareaprops} />
</form>