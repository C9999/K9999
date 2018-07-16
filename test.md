# POC de regressão visual com BackstopJS

Projeto usado para validar alterações de layout dos componentes do Design System de forma automática.

## Instalação

```
    npm install Casperjs –g
```
```
    npm install Backstopjs –g
```

## Configuração

O arquivo backstop.json contém os cenários que serão validados. Dentro da sessão "scenarios" temos os "labels", cada label é responsável por mapear o layout desejado e também possui a URL onde a automação deverá fazer a comparação e validação de equivalência ou diferença.

Exemplo:
```
   "scenarios": [
    {
      "label": "header",
      "url": "http://localhost:3000/#/components/header"
    }
  ],
```

Apenas esses dois parametros são obrigatórios, existem outras configurações que podem ser feitas de forma opcional.

## URL do cenário usada na validação

Essa URL precisar conter o projeto Design System sendo executado. Geralmente dentro do CEIC o projeto fica hospedado no Jarvis.

URL de exemplo: http://jarvisinternet.itau/webview/design-system-dev/#/home/components/loading

Caso queira testar em outros endereços ou locamente é necessário fazer a alteração da url em todos os cenários.

## Principais comandos

Para capturar o layout atual como referência:
```
    backstop reference
```

Validação de layout, usando como comparativo a referência já capturada:
```
    backstop test
```

Caso queria que as novas alterações sejam aprovadas como referência use o comando:  
```
    backstop approve
```

Todos os comando acima podem ter o parâmetro --filter <label>, com isso filtramos aonde queremos fazer as alterações/referência ou podemos testar apenas um label desejado, exemplo:
```
    backstop test --filter button
```

Após o BackstopJS fazer a comparação dos layouts é gerado uma página html com o relatório desse testes, que por padrão após o término do teste o navegador se encarrega de exibir o resultado de forma automática.  

## html_report

Pasta onde o relatório hmtl do último teste executado é guardado. Sempre que um novo teste é executado o relatório anterior é sustituído pelo novo. Nessa pasta também existe a configuração de como esse report é gerado.

## bitmaps_reference

Ao executar o comando "backstop reference" os layouts de referência serão guardados dentro desta pasta. E sempre que a referência é atualiza a imagem antiga é alterada pela nova.

## bitmaps_test

A cada execução do teste através do comando "backstop test", as imagens são capturas e guardadas dentro desta pasta para comparação e usadas no relatório. Ou seja, essa pasta cresce de tamanho muito rapído pois a cada teste novas imagens são salvas nesse local. Devido a isso essa pasta não deve ser commitada e o as suas alterações estão sendo ignoradas pelo Git através do arquivo gitignore.
