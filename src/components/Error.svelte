<script>
    export let error
</script>

{#if typeof error.detail === 'string'}
    <div class="error-message">
        {error.detail}
    </div>
{:else if typeof error.detail === 'object' && error.detail.length > 0 }
    <div class="error-list">
        {#each error.detail as err, i}
        <div class="error-item">
            <strong class="error-field">{err.loc[1]}</strong> : {err.msg}
        </div>
        {/each}
    </div>
{/if}

<style>
    .error-message {
        background-color: #f8d7da;
        color: #721c24;
        padding: 10px;
        border-radius: 5px;
        margin-bottom: 15px;
        font-size: 14px;
        border: 1px solid #f5c6cb;
    }

    .error-list {
        background-color: #f8d7da;
        color: #721c24;
        padding: 15px;
        border-radius: 5px;
        font-size: 14px;
        border: 1px solid #f5c6cb;
    }

    .error-item {
        margin-bottom: 10px;
    }

    .error-field {
        font-weight: bold;
    }
</style>
