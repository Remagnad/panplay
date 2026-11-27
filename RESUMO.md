# Resumo — input do mouse

- Corrigido o `WarpPointer`: agora atualiza o ponteiro pelos listeners do X Server.
- Movimento entre janelas envia `EnterNotify`/`LeaveNotify`; cliques revalidam a janela-alvo.
- Logs de cliques, janelas e botões virtuais ajudam a localizar falhas restantes.
- Workflow testa e gera APK debug **download-only** (componentes Windows são baixados no primeiro uso).
- **Estado:** aguardando CI e reteste no tablet; ainda não confirmado como resolvido.
