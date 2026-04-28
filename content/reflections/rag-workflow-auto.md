+++
date = '2026-04-16T23:33:47+02:00'
draft = false
title = 'Automatiseret workflow til Rag-chatbot'
+++

## Intro

Jeg har lavet en Chatbot til min portfolio, der skal hjælpe besøgende
med at forstå mine projekter.

Chatbotten er lavet i Dify og bruger en Rag løsning.

## Nuværende løsning

Jeg har oprettet en knowlegde og der i vedhæftet en pdf
som dokumentation chatbotten kan bruge. 

Jeg bruger en prompt lavet (generet) med chatgpt som instrukser til
hvilke svar chatbotten må give til brugeren hvilke grænser den skal have.

## Deployment

Da jeg skulle have chatbvotten op på min side brugte jeg en api nøgle fra openAi.

Jeg oprettede en Crawler, OpenAiClient og lagde nøglen ind som en miljø variabel og en html fil i frontend.

## Koden

import okhttp3.*;
import org.jsoup.Jsoup;

import java.util.*;
import java.util.regex.*;

public class Crawler {

    private final OkHttpClient client = new OkHttpClient();

    public List<String> getUrls(String sitemapUrl) throws Exception {

        Request request = new Request.Builder().url(sitemapUrl).build();
        Response response = client.newCall(request).execute();

        String xml = response.body().string();

        List<String> urls = new ArrayList<>();
        Matcher matcher = Pattern.compile("<loc>(.*?)</loc>").matcher(xml);

        while (matcher.find()) {
            urls.add(matcher.group(1));
        }

        return urls;
    }

    public String getText(String url) throws Exception {

        Request request = new Request.Builder().url(url).build();
        Response response = client.newCall(request).execute();

        String html = response.body().string();

        String text = Jsoup.parse(html).text();

        text = text.replaceAll("\\s+", " "); // fjerner mega whitespace
        text = text.trim();

        return text;
    }
}


import okhttp3.*;
import org.json.JSONArray;
import org.json.JSONObject;

public class OpenAIClient {

    private final OkHttpClient client = new OkHttpClient();
    private final String apiKey;

    public OpenAIClient(String apiKey) {
        this.apiKey = apiKey;
    }

    public String ask(String content, String question) throws Exception {

        MediaType JSON = MediaType.get("application/json; charset=utf-8");

        content = content.replaceAll("[^\\x20-\\x7E\\n]", "");


        JSONArray messages = new JSONArray();

        messages.put(new JSONObject()
                .put("role", "system")
                .put("content", "Du svarer kun ud fra hjemmesideindholdet. Hvis svaret ikke findes, sig det ikke fremgår."));

        messages.put(new JSONObject()
                .put("role", "user")
                .put("content",
                        "INDHOLD:\n" + content + "\n\nSPØRGSMÅL: " + question));

        JSONObject bodyJson = new JSONObject();
        bodyJson.put("model", "gpt-4o-mini");
        bodyJson.put("messages", messages);

        RequestBody body = RequestBody.create(bodyJson.toString(), JSON);

        Request request = new Request.Builder()
                .url("https://api.openai.com/v1/chat/completions")
                .addHeader("Authorization", "Bearer " + apiKey)
                .addHeader("Content-Type", "application/json")
                .post(body)
                .build();

        try (Response response = client.newCall(request).execute()) {

            if (!response.isSuccessful()) {
                throw new RuntimeException("API error: " + response.code() + " - " + response.body().string());
            }

            String responseBody = response.body().string();

            JSONObject obj = new JSONObject(responseBody);
            return obj.getJSONArray("choices")
                    .getJSONObject(0)
                    .getJSONObject("message")
                    .getString("content");
        }
    }
}

<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>app</groupId>
    <artifactId>Portfolio</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

<dependencies>
    <dependency>
        <groupId>com.squareup.okhttp3</groupId>
        <artifactId>okhttp</artifactId>
        <version>4.12.0</version>
    </dependency>


    <dependency>
        <groupId>org.jsoup</groupId>
        <artifactId>jsoup</artifactId>
        <version>1.17.2</version>
    </dependency>

    <dependency>
        <groupId>org.json</groupId>
        <artifactId>json</artifactId>
        <version>20240303</version>
    </dependency>
</dependencies>

</project>
