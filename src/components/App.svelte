<script>
    import { Alert } from 'flowbite-svelte'
    import { APP_STATUS, appStatus } from '../store'
    import StepUpload from './StepUpload.svelte'
    import StepLoading from './StepLoading.svelte'
    import StepChat from './StepChat.svelte'
</script>


{#if $appStatus == APP_STATUS.INIT}
    <StepUpload />
{:else if $appStatus == APP_STATUS.LOADING}
    <StepLoading />
{:else if $appStatus == APP_STATUS.CHAT_MODE}
    <StepChat />
{:else if $appStatus == APP_STATUS.ERROR}
    <Alert>
        <span class="font-medium">Something wrong happened!</span>
        There is something wrong in the app
    </Alert>
{:else}
    <Alert>
        <span class="font-medium">Unkown action</span>
        This app status is unkown
    </Alert>
{/if}
