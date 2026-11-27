# Resumo — input do mouse

- `WarpPointer` notifica os listeners; movimento envia `EnterNotify`/`LeaveNotify`.
- Cliques revalidam a janela-alvo; logs rastreiam mouse físico e botões virtuais.
- Build completo compilou FEX, DXVK/VKD3D, Box64, PulseAudio e ALSA.
- **Falha do build #15:** somente o SHA-256 do WCP do Box64 divergiu; os outros sete componentes passaram.
- **Correção aplicada:** manifesto atualizado para o hash recém-gerado pelo CI: `3d1cb60ecf91d26faa2aa1af85e362e9f1d17dfbe201a71a4cde99735f6e49b6`.
- **Estado:** nova execução precisa validar todos os componentes, rodar testes e gerar/enviar o APK completo.

