# promises.all

const posts =[{title:'post1'}];

function printPosts(){
    posts.forEach((post)=>{
        console.log(post.title);
    })
}

function createPost2(){
    return new Promise((resolve, reject)=>{
        setTimeout(()=>{
            posts.push({title:'post2'});
            resolve();
        },2000)
    })
}

function createPost3(){
    return new Promise((resolve, reject)=>{
        setTimeout(()=>{
            posts.push({title:'post3'});
            resolve();
        },1000)
    })
}

function deletePost(){
    return new Promise((resolve, reject)=>{
        setTimeout(()=>{
            posts.pop();
            resolve();
        },1000)
    })
}


function updateLastUserActivityTime(){
            return new Promise((resolve, reject)=>{
                console.log("last updated on "+ new Date());
                resolve();
            },1000)
}

// createPost2().then(()=>{
//     createPost3().then(()=>{
//             printPosts();
//                 Promise.all([createPost2(), createPost3()]).then(()=>{
//                     updateLastUserActivityTime();
//                 })
//             })
// })

createPost2().then(()=>{
    createPost3().then(()=>{
        deletePost().then(()=>{
            printPosts();
            Promise.all([createPost2(), createPost3(), deletePost()]).then(()=>{
                updateLastUserActivityTime();
            })
        })
          
    })
})
