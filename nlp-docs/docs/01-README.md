---
sidebar_position: 1
slug: /
---

# NLP.js

![NLPjs logo](../../screenshots/nlplogo.gif)

[![Build Status](https://travis-ci.com/axa-group/nlp.js.svg?branch=master)](https://travis-ci.com/axa-group/nlp.js)
[![Coverage Status](https://coveralls.io/repos/github/axa-group/nlp.js/badge.svg?branch=master)](https://coveralls.io/github/axa-group/nlp.js?branch=master)
[![NPM version](https://img.shields.io/npm/v/node-nlp.svg?style=flat)](https://www.npmjs.com/package/node-nlp)
[![NPM downloads](https://img.shields.io/npm/dm/node-nlp.svg?style=flat)](https://www.npmjs.com/package/node-nlp)
[![Sonarcloud Status](https://sonarcloud.io/api/project_badges/measure?project=axa-group_nlp.js&metric=alert_status)](https://sonarcloud.io/dashboard?id=axa-group_nlp.js)
[![Maintainability Rating](https://sonarcloud.io/api/project_badges/measure?project=axa-group_nlp.js&metric=sqale_rating)](https://sonarcloud.io/dashboard?id=axa-group_nlp.js)
[![Reliability Rating](https://sonarcloud.io/api/project_badges/measure?project=axa-group_nlp.js&metric=reliability_rating)](https://sonarcloud.io/dashboard?id=axa-group_nlp.js)
[![Security Rating](https://sonarcloud.io/api/project_badges/measure?project=axa-group_nlp.js&metric=security_rating)](https://sonarcloud.io/dashboard?id=axa-group_nlp.js)

"NLP.js" is a general natural language utility for nodejs. Currently supporting:

- Guess the language of a phrase
- Fast _Levenshtein_ distance of two strings
- Search the best substring of a string with less _Levenshtein_ distance to a given pattern.
- Get stemmers and tokenizers for several languages.
- Sentiment Analysis for phrases (with negation support).
- Named Entity Recognition and management, multi-language support, and acceptance of similar strings, so the introduced text does not need to be exact.
- Natural Language Processing Classifier, to classify an utterance into intents.
- NLP Manager: a tool able to manage several languages, the Named Entities for each language, the utterances, and intents for the training of the classifier, and for a given utterance return the entity extraction, the intent classification and the sentiment analysis. Also, it is able to maintain a Natural Language Generation Manager for the answers.
- 40 languages natively supported, 104 languages supported with BERT integration
- Any other language is supported through tokenization, even fantasy languages

![Hybrid bot](../../screenshots/hybridbot.gif)

## New in version 4`!`

Version 4 is very different from previous versions. Before this version, NLP.js was a monolithic library. The big changes:

- Now the library is split into small independent packages.
- So every language has its own package
- It provides a plugin system, so you can provide your own plugins or replace the existing ones.
- It provides a container system for the plugins, settings for the plugins and also pipelines
- A pipeline is code defining how the plugins interact. Usually it is linear: there is an input into the plugin, and this generates the input for the next one. As an example, the preparation of a utterance (the process to convert the utterance to a hashmap of stemmed features) is now a pipeline like this: `normalize -> tokenize -> removeStopwords -> stem -> arrToObj`
- There is a simple compiler for the pipelines, but they can also be built using a modified version of javascript and python (compilers are also included as plugins, so other languages can be added as a plugin).
- NLP.js now includes connectors, a connector is understood to be something that has at least 2 methods: `hear` and `say`. Examples of connectors included: Console Connector, Microsoft Bot Framework Connector and a Direct Line Offline Connector (this one allows you to build a web chatbot using the Microsoft Webchat, but without having to deploy anything in Azure).
- Some plugins can be registered by language, so for different languages different plugins will be used. Also some plugins, like NLU, can be registered not only by language but also by domain (a functional set of intents that can be trained separately)
- As an example of per-language/domain plugins, a Microsoft LUIS NLU plugin is provided. You can configure your chatbot to use the NLU from NLP.js for some languages/domains, and LUIS for other languages/domains.
- Having plugins and pipelines makes it possible to write chatbots by only modifying the configuration and the pipelines file, without modifying the code.