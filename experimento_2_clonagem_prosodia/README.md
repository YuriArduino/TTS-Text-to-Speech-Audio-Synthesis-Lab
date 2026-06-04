# Experimento 2: Clonagem de Voz Zero-Shot e Análise de Prosódia

## Objetivo
Investigar os limites da clonagem de voz instantânea (Zero-Shot) utilizando o modelo multimodal XTTS v2, focando na transferência de timbre e na retenção da prosódia natural em português brasileiro.

## Processo Desenvolvido
- **Ambiente:** Configuração e resolução de dependências do ecossistema `coqui-tts` no ambiente Python 3.12 (Google Colab).
- **Inferência Condicionada:** Extração de *Speaker Embeddings* (vetores de identidade sonora) a partir de áudios curtos de referência (5-10 segundos) para guiar o decodificador do TTS sem re-treinamento de pesos (congelamento de VRAM).

## Descobertas e Insights Técnicos
- **O Limite do Zero-Shot:** Áudios de referência muito curtos limitam a capacidade do modelo de mapear a prosódia complexa. O modelo replica a textura das cordas vocais (timbre), mas falha na dinâmica pulmonar (cadência de inspirar/expirar).
- **Percepção de Voz Truncada:** A sensibilidade auditiva humana a vozes familiares (testado com a voz da esposa) torna micro-desvios de entonação e falhas de suavização imediatamente evidentes, revelando um aspecto "truncado" ou engasgado na síntese linear.
- **Importância da Entrada:** Ruídos milimétricos no áudio de referência são interpretados pelo modelo como características do locutor, degradando a fluidez da fala gerada.

## Próximos Passos para Pesquisa (Roadmap)
1. **Amostragem Expandida:** Testar referências mais longas (~1 minuto) utilizando textos balanceados foneticamente com palavras complexas e coarticulações nativas do português.
2. **Pipeline de Pré-Processamento Acústico:** Integrar ferramentas de isolamento e diarização (`pyanote.audio`) combinadas com normalização estatística de ganho e *silence clipping* (`pydub`) no áudio de referência antes da extração do embedding.
3. **Desacoplamento de Arquitetura:** Conectar este módulo de fala ("boca" *stateless*) a um motor de *Reasoning* assíncrono em NLP para fluxos de conversação em tempo real.
