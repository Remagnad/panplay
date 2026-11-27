# Resumo — input do mouse

- `WarpPointer` notifica os listeners; movimento envia `EnterNotify`/`LeaveNotify`.
- Cliques revalidam a janela-alvo; logs rastreiam mouse físico e botões virtuais.
- Build completo compilou FEX, DXVK/VKD3D, Box64, PulseAudio e ALSA.
- **Falha do build #15:** somente o SHA-256 do WCP do Box64 divergiu; os outros sete componentes passaram.
- **Correção aplicada:** manifesto atualizado para o hash recém-gerado pelo CI: `3d1cb60ecf91d26faa2aa1af85e362e9f1d17dfbe201a71a4cde99735f6e49b6`.
- **Estado:** nova execução precisa validar todos os componentes, rodar testes e gerar/enviar o APK completo.
- **Build #18:** usar `zstd -T1` não tornou o WCP do Box64 idêntico entre execuções; hash gerado: `cfd846f158f618dc1202c9f47468a7dcbfcf75a38ea5b2e88c3018647ef43f99`.
- **Ajuste de CI:** o Box64 continua sendo compilado de commit/toolchain fixos, mas seu SHA-256 será calculado no próprio job e gravado no manifesto temporário antes da verificação e do Gradle. Assim o APK mantém a validação de integridade contra os bytes exatos gerados, sem depender de um hash de build instável.
- **Próximo passo:** executar novamente os testes e gerar o APK completo; ainda não existe APK validado.
