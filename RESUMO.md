# Resumo — input do mouse

- `WarpPointer` notifica os listeners; movimento envia `EnterNotify`/`LeaveNotify`.
- Cliques revalidam a janela-alvo; logs rastreiam mouse físico e botões virtuais.
- CI monta o APK completo: rootfs, Proton, FEX, DXVK/VKD3D, Box64 e áudio.
- **Último build:** FEX compilou; DXVK parou na configuração por ausência de `glslangValidator`.
- **Correção aplicada:** workflow agora instala `glslang-tools`; aguardando nova execução.
- **Estado:** APK completo ainda não gerado; teste no tablet pendente.
