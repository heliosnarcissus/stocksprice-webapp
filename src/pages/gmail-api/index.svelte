<script>
 
  let person='';
  let themessage = '';

   async function sendMessage(recipient, msg){
         console.log("sending to : " + recipient);
         console.log("message: " + msg);
         
         const res = await fetch('http://localhost:8081/sendGmail', {
            method: 'POST',
            mode: 'cors',
            headers: {
             'Content-Type': 'application/json'
            },
            body: JSON.stringify({
              recipient: recipient,
              msgSubject: 'sent From RoutifyJS port 5000',
              msgBody: msg
            })
          });
        
          let json =  await res.json()
          console.log(json);
           return json;    
   }
</script>
reyanthonyrenacia@gmail.com
<form onsubmit={sendMessage}>
  <div>
      <label for="recipient" >Send To:</label>
      <input bind:value={person}
          type="text" id="recipient"/>
  </div>
  <div>
      <label for="message" >Message </label>
      <textarea bind:value={themessage}
          id="message" rows="8" cols="50"></textarea>
  </div>
  <div>
      <button on:click|preventDefault={sendMessage( person,themessage)} > Send Mail</button>
  </div>
</form>
