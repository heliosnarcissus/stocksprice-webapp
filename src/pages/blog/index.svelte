<script>
  import { url, layout } from "@sveltech/routify";
  import marked from "marked";

  const posts = $layout.parent.children
    .filter((c) => c.meta["frontmatter"])
    .sort((a, b) => b.meta["frontmatter"].published.localeCompare(a.meta["frontmatter"].published));

  const fetchJSON= (async () => {
      const response = await fetch('http://localhost:8081/getJavaMaps')
      return await response.json()
  })();

 /* let mapJSON  = fetch('http://localhost:8081/getJavaMaps')
            .then(response=>response.json())
            .then(json => Object.entries(json)
            .then((obj)=>{fetchJSON = obj}); */

  //console.log(mapJSON);


  //console.log(fetchJSON);
/*
  let looper = fetchJSON.then(e=>{
           return e;
           return Object.entries(e);  
        }); */

  //console.log(fetchJSON);
 // console.log(fetchJSON.length);
 // let entries = Object.entries(fetchJSON);
//  console.log(entries);
   /* let entries ;
  fetchJSON.then(e=>{
       entries = Object.entries(e);
       console.log(entries);
  }); */
 //console.log(entries);
/*
[[PromiseResult]]: Object
One: "Batman"
Three: "Superman"
Two: "Ironman"
*/

/**THE ANSWER
 * 
 * <ul class="posts">
  {#await fetchJSON}
    Loading...
  {:then fetchResults}
  {#each Object.entries(fetchResults) as {result}}
      {result}
  {/each}
  {:catch error}
    <p>Something went wrong: {error.message}</p>
  {/await}
</ul> **/
</script>

<h1>Blog</h1>

<ul class="posts">
  {#await fetchJSON}
    Loading...
  {:then fetchResults}
  {#each Object.entries(fetchResults) as result}
      {result}
  {/each}
  {:catch error}
    <p>Something went wrong: {error.message}</p>
  {/await}
</ul>
