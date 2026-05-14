================================================================================
                              LIVETRANSLATE
                          Tradução em Tempo Real
================================================================================

LiveTranslate - Tradução de áudio em tempo real para Windows.

Captura áudio do sistema (loopback WASAPI) e microfone opcional, executa ASR
(reconhecimento de fala), traduz via API de IA e exibe os resultados em uma
sobreposição transparente.

Funciona com qualquer áudio do sistema: vídeos, lives, chat de voz.
Não precisa modificar o player.

================================================================================
REQUISITOS
================================================================================

- Sistema: Windows 10 ou 11
- Python: 3.10 ou superior
- GPU (recomendado): NVIDIA com CUDA 12.6 (RTX 50xx requer CUDA 12.8)
- Rede: Acesso a uma API de tradução

================================================================================
FUNCIONALIDADES
================================================================================

- Pipeline em tempo real: Áudio do sistema -> VAD -> ASR -> Tradução -> Sobreposição
- Múltiplos motores ASR: faster-whisper, SenseVoice, FunASR Nano, Anime-Whisper
- Qualquer API compatível com OpenAI: DeepSeek, Grok, Qwen, GPT, Ollama, vLLM
- Exibição de tradução em streaming (caractere por caractere)
- Configurações por modelo (streaming, JSON, histórico de contexto)
- Mixagem de microfone com áudio do sistema
- VAD de baixa latência (32ms + detecção adaptativa de silêncio)
- Sobreposição transparente (sempre no topo, clique-atraves, arrastável)
- 14 temas de cores
- Aceleração CUDA para ASR
- Gerenciamento automático de modelos (ModelScope / HuggingFace)
- Benchmark integrado

================================================================================
CONFIGURAÇÃO DA POSIÇÃO DA JANELA DE LEGENDAS
================================================================================

No arquivo user_settings.json, você define permanentemente a posição da legenda:

{
  "subtitle_mode": {
    "window_x": 900,
    "window_y": 930
  }
}

IMPORTANTE: A posição Y (window_y) NÃO é alterada automaticamente.
Você define uma vez e ela permanece fixa, mesmo quando o texto muda de tamanho.

================================================================================
PROVEDORES LLM SUPORTADOS
================================================================================

LM Studio:
  http://localhost:1234/v1
  http://127.0.0.1:1234/v1

Ollama:
  http://localhost:11434
  http://127.0.0.1:11434

================================================================================
IDIOMAS SUPORTADOS PELO TRADUTOR (44 idiomas)
================================================================================

Código | Idioma
-------|----------------
en     | English (Inglês)
ja     | Japanese (Japonês)
zh     | Chinese (Chinês)
ko     | Korean (Coreano)
pt     | Portuguese (Português)
es     | Spanish (Espanhol)
fr     | French (Francês)
de     | German (Alemão)
it     | Italian (Italiano)
nl     | Dutch (Holandês)
ru     | Russian (Russo)
pl     | Polish (Polonês)
tr     | Turkish (Turco)
ar     | Arabic (Árabe)
th     | Thai (Tailandês)
vi     | Vietnamese (Vietnamita)
id     | Indonesian (Indonésio)
ms     | Malay (Malaio)
hi     | Hindi
uk     | Ukrainian (Ucraniano)
cs     | Czech (Tcheco)
ro     | Romanian (Romeno)
el     | Greek (Grego)
hu     | Hungarian (Húngaro)
sv     | Swedish (Sueco)
da     | Danish (Dinamarquês)
fi     | Finnish (Finlandês)
no     | Norwegian (Norueguês)
he     | Hebrew (Hebraico)

================================================================================
INSTALAÇÃO RÁPIDA
================================================================================

1. Clone o repositório:
   git clone https://github.com/TheDeathDragon/LiveTranslate.git
   cd LiveTranslate

2. Execute install.bat (detecta Python, cria ambiente virtual, instala dependências)

3. Execute start.bat para iniciar

Para atualizar: execute update.bat

================================================================================
PRIMEIRA INICIALIZAÇÃO
================================================================================

1. O assistente de configuração aparece
2. Escolha a fonte de download (ModelScope ou HuggingFace)
3. Os modelos Silero VAD + SenseVoice baixam automaticamente (~1GB)
4. A interface principal aparece quando estiver pronto

================================================================================
CONFIGURAÇÃO DA API DE TRADUÇÃO
================================================================================

Abra Configurações -> Guia Tradução:

- API Base: https://api.deepseek.com/v1 (exemplo)
- API Key: Sua chave
- Model: deepseek-chat (exemplo)
- Proxy: none / system / URL personalizada

================================================================================
MODELOS RECOMENDADOS PARA TRADUÇÃO DE LIVE
================================================================================

1. Qwen2.5-0.5B-Instruct (MELHOR ESCOLHA)
   - Rápido, baixa latência
   - Qualidade de tradução superior
   - Suporta 29+ idiomas

2. Llama-3.2-1B-Instruct
   - Maior (1B), qualidade boa
   - Pode ser mais lento

================================================================================
ARQUITETURA DO PROJETO
================================================================================

main.py                 - Entrada principal e pipeline
audio_capture.py        - Loopback WASAPI + mixagem de microfone
vad_processor.py        - Silero VAD (detecção de voz)
asr_engine.py           - faster-whisper
asr_sensevoice.py       - SenseVoice
asr_funasr_nano.py      - FunASR Nano
asr_anime_whisper.py    - Anime-Whisper (japonês anime/galgame)
translator.py           - Cliente OpenAI (streaming, JSON schema, contexto)
model_manager.py        - Download e cache de modelos
subtitle_overlay.py     - Sobreposição PyQt6
subtitle_window.py      - Janela de legendas para OBS
control_panel.py        - Interface de configurações (7 abas)
dialogs.py              - Assistentes e diálogos
benchmark.py            - Benchmark de tradução
transcript_writer.py    - Salvamento automático de transcrições

================================================================================
AGRADECIMENTOS
================================================================================

- faster-whisper: Inferência Whisper via CTranslate2
- FunASR: SenseVoice / Fun-ASR-Nano
- Anime-Whisper: ASR para japonês (anime/galgame)
- Silero VAD: Detecção de atividade de voz

================================================================================
LICENÇA
================================================================================

MIT License

================================================================================