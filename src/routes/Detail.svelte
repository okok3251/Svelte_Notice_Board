<script>
    import fastapi from "../lib/api";
    import Error from "../components/Error.svelte";

    export let params ={}
    let question_id = params.question_id;
    let question = {answers : []}
    let content = "";
    let error = {detail : []}

    function get_question(){
        fastapi('get','/question/detail/' + question_id, {}, (data)=> {
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
        fastapi('post',url,params,(json)=>{
            content = ''
            error = {detail : []}
            get_question()
        },
        (err_json) => {
            error = err_json
        }
        )
    }
</script>

<h1>{question.subject}</h1>
<div>
    {question.content}
</div>
<ul>
    {#each question.answers as answer}
        <li>{answer.content}</li>
    {/each}
</ul>
<Error error={error}/>
<form method="post">
    <textarea rows="15" bind:value={content}></textarea>
    <input type="submit" value="답변 등록" on:click={post_answer}>
</form>


<style>
    textarea{
        width:100%;
    }
    input[type=submit] {
        margin-top: 10px;
    }
</style>