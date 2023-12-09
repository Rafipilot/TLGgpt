<!-- src/App.svelte -->
<script>
    import { onMount } from 'svelte';
    import similarity from 'string-similarity';
  
    let userInput = '';
    let response = '';
  
    const qaPairs = [
      { question: 'What is your name?', answer: 'My name is TLGpt.' },
      { question: 'Hello', answer: 'Hi' },
      { question: 'Hi', answer: 'How can i help you' },
      { question: '', answer: '' },
      { question: '', answer: '' },
      { question: '', answer: '' },
      { question: '', answer: '' },
      { question: '', answer: '' },
      { question: '', answer: '' },
      { question: '', answer: '' },
      // Add more question-answer pairs as needed
    ];
  

    
    const tokenizer = input => input.toLowerCase().split(/\s+/);
    

function processInput() {
  console.log(userInput)
  userInput = userInput.toLowerCase()
  const inputTokens = tokenizer(userInput);

  // Compare input with each question
  for (const { question, answer } of qaPairs) {
    const questionTokens = tokenizer(question);

    // Check if input is similar to the question
    const similarityScore = similarity.compareTwoStrings(userInput, question);
    if (similarityScore > 0.1) { // Adjust the threshold as needed
      response = answer;
      return;
    }
  }
  
      // No match found
      response = 'Sorry, I don\'t understand.';
    }
  
 
    </script>
  
    <style>
      main {
        text-align: center;
        margin: 20px;
      }
  
      h1 {
        color: #333;
      }
  
      input, button {
        margin-top: 10px;
      }
    </style>
  
    <main>
      <h1>TLGpt</h1>
      <input bind:value={userInput} placeholder="Ask a question" />
      <button on:click={processInput}>Send</button>
      <p>TLGpt: {response}</p>
    </main>
  