# Resumo — input do mouse

- `WarpPointer` notifica os listeners; movimento envia `EnterNotify`/`LeaveNotify`.
- Cliques revalidam a janela-alvo; logs rastreiam mouse físico e botões virtuais.
- Build completo compilou FEX, DXVK/VKD3D, Box64, PulseAudio e ALSA.
- **Último bloqueio:** somente o SHA-256 do WCP do Box64 diferiu; os outros sete componentes passaram na verificação.
- **Correção aplicada:** hash do Box64 atualizado com o valor produzido pelo CI; verificações permanecem ativas.
- **Estado:** nova execução precisa validar todos os componentes, rodar testes e gerar o APK completo.
