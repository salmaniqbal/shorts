# Run LLM locally

## Run on Mac

minikube start --driver=qemu2 --memory=6144 --cpus=2

Install
`brew install ollama`

Start the Ollama service (or just run it directly):
`ollama serve`

Pull and run a model (start small-ish first):
`ollama run llama3.1:8b`

Container 
`docker run -d -v ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama`


`k port-forward service/ollama 8081:80`


Pull the image
`kubectl -n llm exec -it deployment/ollama -- ollama pull llama3.1:8b`



1. Do the deployment 
2. Exec into pod:
    `kubectl exec -it ollama-89fb74d5-hlpm4 -- sh`
     `ollama pull tinyllama`
3. Exit pod
4. `curl http://localhost:11434/api/tags`
5. Request:
curl http://localhost:11434/api/chat -d '{
  "model": "tinyllama:latest",
  "messages": [{
    "role": "user",
    "content": "Why is the sky blue?"
  }],
  "stream": false
}'