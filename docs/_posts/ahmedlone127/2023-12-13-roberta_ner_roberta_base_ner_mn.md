---
layout: model
title: Mongolian RobertaForTokenClassification Base Cased model (from bayartsogt)
author: John Snow Labs
name: roberta_ner_roberta_base_ner
date: 2023-12-13
tags: [bert, ner, open_source, mn, onnx]
task: Named Entity Recognition
language: mn
edition: Spark NLP 5.2.1
spark_version: 3.0
supported: true
engine: onnx
annotator: RoBertaForTokenClassification
article_header:
  type: cover
use_language_switcher: "Python-Scala-Java"
---

## Description

Pretrained RobertaForTokenClassification model, adapted from Hugging Face and curated to provide scalability and production-readiness using Spark NLP. `roberta-base-ner` is a Mongolian model originally trained by `bayartsogt`.

## Predicted Entities

`LOC`, `PER`, `MISC`, `ORG`

{:.btn-box}
<button class="button button-orange" disabled>Live Demo</button>
<button class="button button-orange" disabled>Open in Colab</button>
[Download](https://s3.amazonaws.com/auxdata.johnsnowlabs.com/public/models/roberta_ner_roberta_base_ner_mn_5.2.1_3.0_1702506271760.zip){:.button.button-orange.button-orange-trans.arr.button-icon}
[Copy S3 URI](s3://auxdata.johnsnowlabs.com/public/models/roberta_ner_roberta_base_ner_mn_5.2.1_3.0_1702506271760.zip){:.button.button-orange.button-orange-trans.button-icon.button-copy-s3}

## How to use



<div class="tabs-box" markdown="1">
{% include programmingLanguageSelectScalaPythonNLU.html %}
```python
documentAssembler = DocumentAssembler() \
        .setInputCol("text") \
        .setOutputCol("document")

sentenceDetector = SentenceDetectorDLModel.pretrained("sentence_detector_dl", "xx")\
       .setInputCols(["document"])\
       .setOutputCol("sentence")

tokenizer = Tokenizer() \
    .setInputCols("sentence") \
    .setOutputCol("token")

tokenClassifier = BertForTokenClassification.pretrained("roberta_ner_roberta_base_ner","mn") \
    .setInputCols(["sentence", "token"]) \
    .setOutputCol("ner")

pipeline = Pipeline(stages=[documentAssembler, sentenceDetector, tokenizer, tokenClassifier])

data = spark.createDataFrame([["Би SPARK NLP-т дуртай"]]).toDF("text")

result = pipeline.fit(data).transform(data)
```
```scala
val documentAssembler = new DocumentAssembler() 
          .setInputCol("text") 
          .setOutputCol("document")

val sentenceDetector = SentenceDetectorDLModel.pretrained("sentence_detector_dl", "xx")
       .setInputCols(Array("document"))
       .setOutputCol("sentence")

val tokenizer = new Tokenizer() 
    .setInputCols(Array("sentence"))
    .setOutputCol("token")

val tokenClassifier = BertForTokenClassification.pretrained("roberta_ner_roberta_base_ner","mn") 
    .setInputCols(Array("sentence", "token")) 
    .setOutputCol("ner")

val pipeline = new Pipeline().setStages(Array(documentAssembler,sentenceDetector, tokenizer, tokenClassifier))

val data = Seq("Би SPARK NLP-т дуртай").toDF("text")

val result = pipeline.fit(data).transform(data)
```
</div>

{:.model-param}
## Model Information

{:.table-model}
|---|---|
|Model Name:|roberta_ner_roberta_base_ner|
|Compatibility:|Spark NLP 5.2.1+|
|License:|Open Source|
|Edition:|Official|
|Input Labels:|[document, token]|
|Output Labels:|[ner]|
|Language:|mn|
|Size:|465.7 MB|
|Case sensitive:|true|
|Max sentence length:|128|

## References

References

- https://huggingface.co/bayartsogt/roberta-base-ner