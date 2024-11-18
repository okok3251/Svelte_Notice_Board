<script>
    import fastapi from "../lib/api";
    import { link } from 'svelte-spa-router';
    let question_list = []

    function get_question_list() {
        fastapi('get','/question/list',{},(data)=>{
            question_list = data
        })
    }

    get_question_list()
</script>

<div class="main-container">
    <table>
        <thead>
        <tr>
            <th>번호</th>
            <th>제목</th>
            <th>작성자</th>
            <th>작성일시</th>
        </tr>
        </thead>
        <tbody>
        {#each question_list as question, i}
        <tr>
            <td>{i+1}</td>
            <td>
                <a use:link href="/detail/{question.id}" class="question-link">{question.subject}</a>
            </td>
            <td>아무개</td>
            <td>{question.create_date}</td>
        </tr>
        {/each}
        </tbody>
    </table>
    <a use:link href="/question-create" class="create-btn">질문 등록하기</a>
</div>

<style>
    .main-container {
        width: 90vw;
        margin: 20px auto;
        padding: 20px;
        background-color: #f9f9f9;
        border-radius: 8px;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        overflow-x: auto;
    }

    table {
        width: 100%;
        margin-bottom: 20px;
        background-color: #fff;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        border-radius: 5px;
    }

    th, td {
        padding: 12px 15px;
        text-align: center;
        font-size: 14px;
        border-bottom: 1px solid #ddd;
    }

    th {
        background-color: #5C4450;
        color: white;
    }
    td:nth-child(1){
        width:10%;
    }
    td:nth-child(2) {
        width:60%;
    }
    td:nth-child(3){
        width:10%;
    }
    td:nth-child(4){
        width:20%;
    } 

    tr:hover {
        background-color: #f1f1f1;
    }

    .question-link {
        color: #5C4450;
        text-decoration: none;
        font-weight: bold;
    }

    .question-link:hover {
        text-decoration: underline;
        color: #2F3148;
    }

    .create-btn {
        padding: 10px 20px;
        margin-top: 20px;
        background-color: #5C4450;
        color: white;
        text-decoration: none;
        font-size: 16px;
        font-weight: bold;
        border-radius: 5px;
        transition: background-color 0.3s;
    }

    .create-btn:hover {
        background-color: #FF4F00;
    }

</style>
