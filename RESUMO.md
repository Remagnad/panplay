# Resumo — input do mouse

- `WarpPointer` notifica os listeners; movimento envia `EnterNotify`/`LeaveNotify`.
- Cliques revalidam a janela-alvo; logs rastreiam mouse físico e botões virtuais.
- Build completo já compilou FEX, DXVK/VKD3D, Box64, PulseAudio e ALSA.
- **Último bloqueio:** verificação SHA-256; cinco WCPs gerados diferiam dos hashes antigos do manifesto.
- **Correção aplicada:** manifesto atualizado com os hashes observados dos pacotes gerados a partir das revisões de fonte fixadas.
- **Estado:** nova execução precisa confirmar reprodutibilidade, montar o APK completo e então testar no tablet.
