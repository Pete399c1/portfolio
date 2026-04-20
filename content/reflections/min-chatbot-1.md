+++
date = '2026-04-16T23:33:47+02:00'
draft = false
title = 'Min Doctor Chatbot'
+++

## Overvejelser om design og dokumentvalg i min RAG chatbot

I udviklingen af min RAG chatbot har jeg arbejdet med, hvordan dokumenter og 
svarstruktur påvirker brugeroplevelsen.

## Valg af fokusområde

Jeg valgte at arbejde med nyresygdomme, da dette er et relevant medicinsk 
område med tydelige symptomer og behandlingstyper, som egner sig godt til en 
knowledge base.

## Designvalg i chatbotten

Jeg har bevidst valgt, at chatbotten skal give direkte svar i stedet for at gengive lange tekstuddrag fra dokumentet.

Dette blev gjort for at:

- gøre svarene mere læsevenlige
- forbedre brugeroplevelsen
- sikre korte og præcise svar
- undgå at brugeren selv skal finde information i lange kilder

## Refleksion

Selvom jeg ikke viser hele kildematerialet direkte i chatbotten, bygger alle svar 
stadig på den uploadede knowledge base. Dette sikrer, at informationen er faktuel 
og dokumentbaseret.