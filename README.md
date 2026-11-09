# ViralPulse AI Studio

Aplicativo web para receber vídeos por upload ou URL, transcrever o áudio com OpenAI,
selecionar momentos com potencial de retenção, classificar os cortes e exportar MP4
vertical 9:16.

## Requisitos

- Docker Desktop instalado e iniciado.
- Chave de API da OpenAI com faturamento/créditos habilitados.
- Conexão com a internet para baixar imagens/modelos e processar links.

## Executar no Windows (sem instalar Python)

1. Instale e abra o Docker Desktop: https://www.docker.com/products/docker-desktop/
2. Extraia o ZIP em uma pasta.
3. Na pasta ViralPulse, copie `.env.example` e renomeie a cópia para `.env`.
4. Abra `.env` no Bloco de Notas e substitua `sk-proj-SUA_CHAVE_AQUI` pela sua chave da OpenAI.
5. Abra o PowerShell nessa pasta e execute:

   ```powershell
   docker compose up --build
   ```

6. Acesse http://localhost:8000 no navegador.
7. Para encerrar, pressione `Ctrl+C` no terminal. Para iniciar novamente:

   ```powershell
   docker compose up -d
   ```

## O que está incluído

- Upload de MP4, MOV, M4V, WEBM, MKV e AVI.
- Entrada por URL via yt-dlp (suporte depende da plataforma, região e restrições do site).
- Transcrição com timestamps pela API de áudio da OpenAI.
- Seleção e classificação de até 10 cortes com GPT.
- Exportação MP4 vertical 1080x1920 e pacote ZIP.
- Título, gancho, descrição, hashtags e justificativa por corte.
- Chave da OpenAI mantida no backend.

## Limitações e observações importantes

- A pontuação é uma estimativa editorial baseada no conteúdo; não prevê nem garante visualizações.
- O enquadramento vertical é centralizado. Não há rastreamento automático de rosto/objeto nesta versão.
- Legendas queimadas no vídeo, edição manual, contas sociais e publicação automática não estão incluídas.
- URLs do YouTube/TikTok e outros sites podem deixar de funcionar devido a alterações, bloqueios, autenticação, DRM ou termos da plataforma. Use apenas conteúdo que você possui ou tem autorização para baixar e processar. O upload é a opção mais confiável.
- O processamento depende dos limites, disponibilidade e cobrança da API OpenAI. A chave não está incluída no ZIP.
- Os trabalhos e resultados ficam no volume local do Docker. A fila é em memória; se o container reiniciar durante um processamento, o trabalho pode precisar ser enviado novamente.
- Para disponibilizar publicamente na internet, configure HTTPS, autenticação, limites de uso, armazenamento privado e política de retenção antes de produção.

## Diagnóstico

- `http://localhost:8000/api/health` mostra se o servidor, a chave OpenAI e o FFmpeg estão configurados.
- Erro 503: verifique `OPENAI_API_KEY` no `.env`.
- Erro de FFmpeg: recrie a imagem com `docker compose up --build`.
- Erro ao obter link: tente o upload do arquivo original.
