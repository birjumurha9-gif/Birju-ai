
<!DOCTYPE html>
<html>
<head>
  <title>Birju AI</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body{
      font-family: Arial;
      background:#0f172a;
      color:white;
      text-align:center;
      padding:20px;
    }
    h1{color:#38bdf8;}
    #chatBox{
      max-width:500px;
      margin:auto;
      background:#1e293b;
      padding:15px;
      border-radius:10px;
      height:300px;
      overflow-y:auto;
      text-align:left;
    }
    input{
      width:60%;
      padding:10px;
      border-radius:8px;
      border:none;
    }
    button{
      padding:10px 15px;
      border:none;
      border-radius:8px;
      background:#38bdf8;
      cursor:pointer;
      margin:5px;
    }
  </style>
</head>
<body>

<h1>Birju AI</h1>

<div id="chatBox"></div>
<br>
<input type="text" id="userInput" placeholder="Type your message...">
<button onclick="sendMessage()">Send</button>
<button onclick="startVoice()">🎤</button>

<hr>

<h2>Image Generator</h2>
<input type="text" id="imagePrompt" placeholder="Describe image...">
<button onclick="generateImage()">Generate</button>
<br><br>
<img id="resultImage" width="300"/>

<script>

// CHAT FUNCTION
async function sendMessage(){
  let input = document.getElementById("userInput");
  let chatBox = document.getElementById("chatBox");

  if(input.value.trim()==="") return;

  chatBox.innerHTML += "<p><b>You:</b> "+input.value+"</p>";

  let response = await fetch("https://api.affiliateplus.xyz/api/chatbot?message="+input.value+"&owner=Birju&botname=BirjuAI");
  let data = await response.json();

  chatBox.innerHTML += "<p><b>AI:</b> "+data.message+"</p>";

  input.value="";
  chatBox.scrollTop = chatBox.scrollHeight;
}


// IMAGE GENERATOR (Free Unsplash Random)
function generateImage(){
  let prompt = document.getElementById("imagePrompt").value;
  let img = document.getElementById("resultImage");

  img.src = "https://source.unsplash.com/300x300/?"+prompt;
}


// VOICE INPUT
function startVoice(){
  let recognition = new (window.SpeechRecognition || window.webkitSpeechRecognition)();
  recognition.lang = "en-US";

  recognition.onresult = function(event){
    document.getElementById("userInput").value = event.results[0][0].transcript;
  };

  recognition.start();
}

</script>

</body>
</html>
