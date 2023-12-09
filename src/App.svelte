<!-- src/App.svelte -->
<script>
    import { onMount } from 'svelte';
    import similarity from 'string-similarity';
  
    let userInput = '';
    let response = '';
  
    const qaPairs = [
      { question: 'What is your name?', answer: 'My name is TLGpt.' },
      { question: '', answer: '' },
      { question: '', answer: '' },
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
  const inputTokens = tokenizer(userInput);

  // Compare input with each question
  for (const { question, answer } of qaPairs) {
    const questionTokens = tokenizer(question);

    // Check if input is similar to the question
    const similarityScore = similarity.compareTwoStrings(userInput, question);
    if (similarityScore > 0.3) { // Adjust the threshold as needed
      response = answer;
      return;
    }
  }
  
      // No match found
      response = 'Sorry, I don\'t understand.';
    }
  
    onMount(() => {
      // Example: Preload some data or perform any setup here
    });
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
      <h1>Svelte AI App</h1>
      <input bind:value={userInput} placeholder="Type your question" />
      <button on:click={processInput}>Submit</button>
      <p>{response}</p>
    </main>
  