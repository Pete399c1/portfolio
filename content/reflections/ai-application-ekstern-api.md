+++
date = '2026-04-16T23:33:47+02:00'
draft = false
title = 'AI-dreven applikation, som kalder et eksternt API med en LLM.'
+++

## AI-dreven applikation med LLM integration

I dette projekt har jeg udviklet en simpel AI-dreven applikation, som kan analysere opgaver og generere en vurdering automatisk ved hjælp af en Large Language Model (LLM).

Applikationen består af et backend API med et endpoint (`POST /api/assessments`), som modtager en request med en fil og et ønsket output. Når endpointet kaldes, læser systemet filens indhold og sender det videre til et eksternt API hos OpenAI.

Her bliver teksten behandlet af en LLM, som genererer en vurdering baseret på en prompt. Resultatet bliver derefter gemt som en ny fil og returneret til brugeren.

Jeg har også arbejdet med at teste løsningen ved hjælp af `curl`, samt sikre korrekt håndtering af API-nøgler via miljøvariabler.

Projektet har givet mig en grundlæggende forståelse for, hvordan man integrerer AI i en applikation og arbejder med eksterne API’er i praksis.

Jeg har også lavet en prompt selv ved hjælp af chatgpt så jeg kunne generer nogle filer og mapper ud fra det.

## Prompt


Byg en minimal Java Spring Boot backend og React frontend oven på min eksisterende filstruktur.

Min nuværende struktur er:

data/
- student1.md
- student2.md
- student3.md
- krav-til-rapport.md
- dare-share-care.md
- laeringsmaal.md

prompts/
- systemprompt-praktikvurdering.md
- userprompt-student1-vurdering.md
- userprompt-student2-vurdering.md
- userprompt-student3-vurdering.md

output/
- student1-vurderingen.md
- student2-vurderingen.md
- student3-vurderingen.md

Derudover har jeg:
- .env
- .env.example
- .gitignore

Lav backend i /backend med Java 21 + Spring Boot.

Backend skal have:

1. GET /api/assignments
- Returnér alle .md filer fra /data
- Returnér fx:
["student1.md", "student2.md", "student3.md"]

2. POST /api/assessments
Body:
{
  "assignmentFile": "student1.md",
  "resultFileName": "student1-vurderingen.md"
}

Backend skal:
a - læse valgt rapport fra /data
b - læse systemprompt fra /prompts/systemprompt-praktikvurdering.md
c - vælge korrekt userprompt ud fra rapportfil:
   student1.md -> prompts/userprompt-student1-vurdering.md
   student2.md -> prompts/userprompt-student2-vurdering.md
   student3.md -> prompts/userprompt-student3-vurdering.md
d - kalde OpenAI API med OPENAI_API_KEY fra .env/environment variable
e - gemme svaret i /output/{resultFileName}
f - returnere JSON:
{
  "assessment": "...",
  "savedPath": "output/student1-vurderingen.md"
}

Lav disse backend-filer:
- PraktikEvaluatorApplication.java
- AssessmentController.java
- AssessmentService.java
- LlmApiClient.java
- FileStorageService.java
- EnvConfigService.java
- AssessmentRequest.java
- AssessmentResult.java
- AssignmentListResponse.java
- ApiExceptionHandler.java

Lav frontend i /frontend med React + Vite:
- Hent rapportlisten fra GET /api/assignments
- Vis dropdown med rapporter
- Knap: "Vurder rapport"
- Send POST til /api/assessments
- Foreslå automatisk outputfilnavn ud fra valgt rapport:
  student1.md -> student1-vurderingen.md
- Vis loading state
- Vis fejlbesked
- Vis vurderingsresultat på siden

Sikkerhed:
- API key må aldrig ligge i frontend
- .env skal ikke committes
- .env.example skal kun indeholde:
OPENAI_API_KEY=your_api_key_here
- Sørg for at .gitignore ignorerer .env

README:
- Forklar kort hvad projektet gør
- Forklar dataflow
- Forklar endpoints
- Forklar hvordan backend startes
- Forklar hvordan frontend startes
- Forklar at OpenAI API key læses fra .env/environment variable
