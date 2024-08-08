<!DOCTYPE html>
<html>
<head>
    <title>Setup Instructions</title>
</head>
<body>

<h1>Setup Instructions</h1>

<h2>Passo 1:</h2>
<p>Coloque o arquivo <code>amazon-meta.txt</code> dentro da pasta <code>scripts</code>.</p>

<h2>Passo 2:</h2>
<p>Na pasta principal do projeto, inicie os containers com o comando:</p>
<pre><code>docker-compose up -d --build</code></pre>
<p>A sequência de arquivos estará dentro do <code>Dockerfile</code>. Se tudo correr bem, as pastas <code>mongodb</code>, <code>postgre</code> e <code>pokemon</code> serão criadas. (A pasta <code>pokemon</code> pode demorar alguns minutos para ser baixada).</p>

<h2>Passo 3:</h2>
<p>Feche o container com o comando após a finalização:</p>
<pre><code>docker-compose down</code></pre>

<h2>Passo 4:</h2>
<p>Entre na pasta <code>scripts</code> através do terminal e compile o Docker dentro da pasta <code>scripts</code> com o comando:</p>
<pre><code>docker-compose up -d --build</code></pre>

<h2>Passo 5:</h2>
<p>Após a conclusão da instalação, entre no terminal do Docker Spark através do comando:</p>
<pre><code>docker exec -u root -it spark_container /bin/bash</code></pre>
<p>Volte à pasta raiz com o comando:</p>
<pre><code>cd ../../../../../</code></pre>
<p>É importante que você esteja na pasta raiz para os próximos passos.</p>

<h2>Passo 6:</h2>
<p>Configure o caminho com o comando:</p>
<pre><code>export PATH=$PATH:/opt/spark/bin</code></pre>

<h2>Passo 7:</h2>
<p>Compile a sequência de scripts do pipeline na seguinte ordem:</p>
<pre><code>spark-submit --packages org.apache.spark:spark-avro_2.12:3.5.1 /app/AvroScript.py
spark-submit --packages org.apache.spark:spark-avro_2.12:3.5.1 /app/AvroToPaqueta.py
spark-submit --packages org.apache.spark:spark-avro_2.12:3.5.1 /app/staging.py</code></pre>
<p>Os resultados serão salvos dentro da pasta <code>production</code>.</p>

<h2>Descrição de Cada Script:</h2>
<ul>
    <li><strong>Script.py:</strong> Responsável pela inserção e geração dos arquivos JSON para o MongoDB.</li>
    <li><strong>SavePostJson.py:</strong> Responsável por pegar os arquivos Post e transformá-los em JSON.</li>
    <li><strong>PostScript.py:</strong> Responsável pela leitura e inserção dos elementos Amazon no PostgreSQL.</li>
    <li><strong>PokeScript.py:</strong> Responsável por salvar os dados Pokémon em JSON.</li>
    <li><strong>AvroScript.py:</strong> Transforma JSON em Avro.</li>
    <li><strong>AvroToPaqueta.py:</strong> Transforma os arquivos Avro para Parquet.</li>
    <li><strong>staging.py:</strong> Manipula e gera os resultados dos dados na pasta <code>production</code>.</li>
</ul>

</body>
</html>
