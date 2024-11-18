<script>
    import fastapi from "../lib/api";
    import Error from "../components/Error.svelte";

    export let params = {}
    let question_id = params.question_id;
    let question = {answers : []}
    let content = "";
    let error = {detail : []}

    function get_question(){
        fastapi('get', '/question/detail/' + question_id, {}, (data)=> {
            question = data
        })
    }

    get_question()

    function post_answer(e){
        e.preventDefault()
        let url = '/answer/create/' + question_id
        let params = {
            content : content
        }
        fastapi('post', url, params, (json)=> {
            content = ''
            error = {detail : []}
            get_question()
        },
        (err_json) => {
            error = err_json
        })
    }
</script>

<div class="detail-container">
    <h2>{question.subject}</h2>
    <div class="question-content">{question.content}</div>
    <div class="question-date">{question.create_date}</div>

    <h5>{question.answers.length}개의 답변이 있습니다.</h5>
    {#each question.answers as answer}
        <div class="answer">
            <div>{answer.content}</div>
            <div class="answer-date">{answer.create_date}</div>
        </div>
    {/each}

    <!-- 답변 등록 폼 -->
    <Error error={error} />
    <form method="post" on:submit|preventDefault="{post_answer}">
        <textarea rows="5" bind:value={content} class="textarea"></textarea>
        <button type="submit" class="submit-btn">답변등록</button>
    </form>
</div>

<style>
    .detail-container {
        max-width: 800px;
        margin: 40px auto;
        padding: 20px;
    }

    h2 {
        font-size: 20px;
        color: #5C4450;
        margin-bottom: 10px;
    }

    .question-content {
        font-size: 16px;
        margin-bottom: 10px;
    }

    .question-date {
        font-size: 14px;
        color: #888;
        margin-bottom: 20px;
    }

    h5 {
        font-size: 16px;
        color: #333;
        margin-bottom: 15px;
    }

    .answer {
        background-color: #f8f8f8;
        padding: 10px;
        margin-bottom: 10px;
        border-radius: 5px;
    }

    .answer-date {
        font-size: 12px;
        color: #aaa;
    }

    .textarea {
        width: 100%;
        padding: 10px;
        margin-bottom: 10px;
        font-size: 14px;
        border: 1px solid #ddd;
        border-radius: 5px;
        resize: vertical;
    }

    .submit-btn {
        width: 100%;
        padding: 12px;
        background-color: #5C4450;
        color: white;
        border: none;
        border-radius: 5px;
        cursor: pointer;
        font-size: 16px;
    }

    .submit-btn:hover {
        background-color: #2F3148;
    }
</style>
