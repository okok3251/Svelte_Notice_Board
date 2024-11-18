<script>
    import { push } from 'svelte-spa-router'
    import fastapi from "../lib/api"
    import Error from "../components/Error.svelte"

    let error = {detail:[]}
    let subject = ''
    let content = ''

    function post_question(event) {
        event.preventDefault()
        let url = "/question/create"
        let params = {
            subject: subject,
            content: content,
        }
        fastapi('post', url, params, 
            (json) => {
                push("/")
            },
            (json_error) => {
                error = json_error
            }
        )
    }
</script>

<div class="form-container">
    <h5 class="form-title">질문 등록</h5>
    <Error error={error} />
    <form method="post" on:submit|preventDefault="{post_question}">
        <div class="form-group">
            <label for="subject">제목</label>
            <input type="text" id="subject" class="form-input" bind:value="{subject}">
        </div>
        <div class="form-group">
            <label for="content">내용</label>
            <textarea id="content" rows="10" class="form-textarea" bind:value="{content}"></textarea>
        </div>
        <button type="submit" class="submit-btn">저장하기</button>
    </form>
</div>

<style>
    .form-container {
        width: 80vw;
        max-width: 600px;
        margin: 40px auto;
        padding: 20px;
        background-color: #f9f9f9;
        border-radius: 8px;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    }

    .form-title {
        font-size: 24px;
        margin-bottom: 20px;
        font-weight: bold;
        color: #5C4450;
    }

    .form-group {
        margin-bottom: 20px;
    }

    label {
        display: block;
        margin-bottom: 8px;
        font-size: 14px;
        color: #333;
    }

    .form-input, .form-textarea {
        width: 100%;
        padding: 10px;
        font-size: 16px;
        border: 1px solid #ddd;
        border-radius: 5px;
        background-color: #fff;
    }

    .form-textarea {
        resize: vertical;
    }

    .form-input:focus, .form-textarea:focus {
        border-color: #5C4450;
        outline: none;
    }

    .submit-btn {
        padding: 12px 20px;
        width: 100%;
        background-color: #5C4450;
        color: white;
        font-size: 16px;
        font-weight: bold;
        border: none;
        border-radius: 5px;
        cursor: pointer;
        transition: background-color 0.3s;
    }

    .submit-btn:hover {
        background-color: #2F3148;
    }

    .submit-btn:focus {
        outline: none;
    }
</style>
