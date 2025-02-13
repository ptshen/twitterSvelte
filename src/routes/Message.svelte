
<script>

    import trash from '$lib/images/trash.png';

    // import global variable to change if user chooses to delete
    import { globalPosts } from './posts.svelte.js';


    let {post} = $props();
 
    function deletePost(id) {

        //console.log(id);

        // decrement future posts' ids
        // id values are stored in descending order due to prepending nature of posts
        for (let i = id; i >= 0; i--) {
            // console.log(i);
            // console.log(globalPosts.posts[i].id)
            if (globalPosts.posts[i].id > id) {
                globalPosts.posts[i].id--;
            }
        }

        // console.log(typeof id);
        globalPosts.posts.splice(globalPosts.posts.length - id - 1, 1);
    
    }
    


</script>

<!--add delete functionality-->
<!--Messages.svelte should commmunicate delete action to page.svelte-->

<!--completed the above tasks by making posts a global variable which Message component has access to and so does main page-->

<!--add styles to make it prettier-->
<style>

    #deletePost {
        margin-right:10px;
        opacity:0.25;
    }

    #deletePost:hover {
        opacity:1;
    }
    #deletePost img {
        width: 20px;
        height: 20px;
    }

    #username {
        font-weight: bold;
    }


    



</style>


<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css"
rel="stylesheet" crossorigin="anonymous">

<div>

    <div class="container text-center">

        <button id="deletePost" onclick={() => deletePost(post.id)}>
            <img src={trash} alt="trash icon">
        </button>
    
        <span id="username">{post.username}</span>
        <span id="post{post.id}">{post.text}</span>
    </div>

   

</div>
