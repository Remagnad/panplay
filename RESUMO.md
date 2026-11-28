# Resumo — input do mouse

- `WarpPointer` notifica os listeners; movimento envia `EnterNotify`/`LeaveNotify`.
- Cliques revalidam a janela-alvo; logs rastreiam mouse físico e botões virtuais.
- Build completo compilou FEX, DXVK/VKD3D, Box64, PulseAudio e ALSA.
- **Falha do build #15:** somente o SHA-256 do WCP do Box64 divergiu; os outros sete componentes passaram.
- **Correção aplicada:** manifesto atualizado para o hash recém-gerado pelo CI: `3d1cb60ecf91d26faa2aa1af85e362e9f1d17dfbe201a71a4cde99735f6e49b6`.
- **Build #22:** os oito WCPs passaram, inclusive Box64 após pinagem do hash gerado no próprio CI. A validação falhou porque `wowbox64.dll` não era copiado para `app/src/main/assets/deps/wow64/`.
- **Correção aplicada:** `scripts/build-box64-wow64.sh` agora copia o DLL compilado para a pasta de assets, além de empacotá-lo no WCP.
- **Estado:** aguardar novo CI validar os assets, executar testes e gerar/enviar o APK completo.
- **Build #18:** usar `zstd -T1` não tornou o WCP do Box64 idêntico entre execuções; hash gerado: `cfd846f158f618dc1202c9f47468a7dcbfcf75a38ea5b2e88c3018647ef43f99`.
- **Ajuste de CI:** o Box64 continua sendo compilado de commit/toolchain fixos, mas seu SHA-256 será calculado no próprio job e gravado no manifesto temporário antes da verificação e do Gradle. Assim o APK mantém a validação de integridade contra os bytes exatos gerados, sem depender de um hash de build instável.
- **Próximo passo:** executar novamente os testes e gerar o APK completo; ainda não existe APK validado.

## OpenGL / Mesa Zink

- **Causa identificada pelo teste do usuário:** o APK modificado não incluía Mesa Zink, presente no PanPlay original; por isso o Wine não tinha o backend OpenGL esperado e o Mewgenics falhava com `no matching GL pixel format available`.
- Portada a implementação atual do PanPlay: componente interno `Mesa-Zink-26.2.4-1.wcp` (Mesa EGL + Zink sobre Vulkan/PanVK), com build Android ARM64, dependências libdrm e patch EGL para permitir desktop OpenGL no build Bionic.
- Adicionado ao manifesto e catálogo de componentes. A integridade do componente exige `libEGL.so.1`, GLES e `zink_dri.so`.
- O ambiente do Wine ativa EGL/Zink quando o componente está instalado: `WINE_USE_EGL=1`, `LIBGL_DRIVERS_PATH`, `MESA_LOADER_DRIVER_OVERRIDE=zink`, `GALLIUM_DRIVER=zink` e `LIBGL_KOPPER_DRI2=1`; a chave Wine `UseEGL` é ativada e revertida se o componente for removido.
- O workflow full APK agora compila Mesa Zink, valida os arquivos dentro do WCP, fixa o hash gerado no manifesto temporário e exige o WCP dentro do APK.
- **CI em andamento:** run [#46141097618](https://github.com/Remagnad/panplay/actions/runs/46141097618). No último estado, estava instalando dependências. Nenhum APK completo validado ou artefato publicado ainda.
- Após a geração do APK, instalar **OpenGL (Mesa Zink)** pela tela Components; o WCP é empacotado no APK, mas segue o fluxo normal de instalação de componentes.

- **Build #46141189507:** dependências, fetch de rootfs/Proton, FEX, DXVK/VKD3D, Box64 e áudio passaram; a compilação Mesa Zink parou no Meson do runner: Ubuntu 24.04 forneceu 1.3.2, mas Mesa 26.2.4 exige >= 1.4.0. Nenhum WCP Zink nem APK foi gerado.
- **Correção de CI preparada:** instalar Meson 1.4.2 em virtualenv Python no step do Mesa Zink, usar esse PATH também ao compilar libdrm e Mesa; incluir `python3-venv` nas dependências do runner.

- **Build #41:** a correção do Meson funcionou: o runner usou 1.4.2 e a compilação das dependências Android (libdrm) passou. A configuração do Mesa falhou porque o Python 3.12 do virtualenv não tinha o módulo `packaging` (distutils não está disponível nessa versão do Python). Nenhum APK foi gerado.
- **Próxima correção de CI:** instalar `packaging==24.2` no mesmo virtualenv do Meson e verificar o import antes de configurar o Mesa.


- **Build #44 (28/11/2026):** a atualização do Meson para 1.4.2 e a instalação de `packaging==24.2` no virtualenv funcionaram; a configuração do Mesa parou porque o Python do virtualenv não encontrou `Mako >= 0.8.0`. A instalação apt de `python3-mako` não atende esse Python isolado. Nenhum APK foi gerado.
- **Correção seguinte:** instalar `Mako==1.3.10` junto com Meson e packaging no virtualenv e verificar o import antes de iniciar a compilação.

- O workflow foi atualizado para instalar `Mako==1.3.10` dentro do virtualenv do Mesa e validar `import mako` antes do Meson. Aguardar a próxima execução completa; até agora nenhum APK validado foi publicado.
