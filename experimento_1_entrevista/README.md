# Experimento 1: Pipeline de Diarização para Entrevistas Acadêmicas

## Objetivo
Desenvolver um pipeline automatizado capaz de extrair e sintetizar diálogos de arquivos PDF (especificamente periódicos psicanalíticos), superando desafios de layout, rodapés e cabeçalhos.

## Processo Desenvolvido
- **Extração:** Uso de `pypdf` para leitura de camadas de texto.
- **Limpeza (NLP):** Aplicação de expressões regulares (Regex) para higienização de ruídos editoriais e padronização de falantes (JORNAL vs FABIO).
- **Processamento Acústico:**
  - `edge-tts` para síntese neural.
  - `pydub` para normalização estatística de ganho e remoção de silêncios dinâmicos.
- **Estruturação:** Pipeline em lote com feedback visual via `tqdm`.

## Lições Aprendidas
- A importância de estruturar a limpeza de texto por "bloco de fala" antes do envio ao TTS para evitar erros de requisição.
- O ajuste de ganho estatístico foi crucial para uniformizar o volume entre as vozes de diferentes motores.
