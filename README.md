# Processo de atualizações das branches Develop e Main/Master

1. Ao receber uma tarefa é necessário clonar o repositório e criar uma branch para efetuar o desenvolvimento:

    ```bash
    git clone url_do_git_obtida_no_repositorio
    cd pasta_do_projeto
    git checkout -b feat123/titulo-da-tarefa
    ```

2. Se por acaso o projeto já havia sido clonado em outra tarefa, ainda assim é necessário criar uma branch com base na versão mais atual da Main/Master:

    ```bash
    git checkout main
    git pull origin main
    git checkout -b feat123/titulo-da-tarefa
    ```

3. Durante todo o desenvolvimento, deve-se concentrar todos os commits e pushes na branch que foi criada:

    ```bash
    git add .
    git commit -m "feat: descricao do commit"
    git push origin feat123/titulo-da-tarefa
    ```

4. Após terminar a tarefa, ou pelo menos tiver alguma versão pronta para testes, e todo o código já está no GitHub, deve-se abrir uma Pull Request (PR) da sua branch para a branch de develop. Você mesmo pode realizar o merge dessa PR, sem precisar de avaliação.

5. Se possível, após efetuar o merge, testar no ambiente de develop. Se tudo estiver de acordo, e a atualização estiver aprovada, é necessário abrir uma PR para a branch Main/Master. Nessa PR, é necessário adicionar o Murilo, e se possível outro dev como Reviewers para que possam analisar coisas como funcionalidades, nomes de variáveis e funções, possíveis pontos de refatoração. Esse merge só pode ser realizado pelo Murilo, e só após todos os Reviewers aprovarem.

6. Caso tenha alguma solicitação de mudança na PR aberta para a Main/Master, não é necessário fechar a PR nem criar outra branch. Basta efetuar a atualização na mesma branch conforme solicitado, e subir na mesma branch (a PR vai ser atualizada automaticamente). Lembre-se que ainda se faz necessário efetuar um merge para a Develop com as novas solicitações (conforme ponto 3).

## Minha PR para Develop deu conflito... e agora?

1. Se a PR para Develop tiver conflito, é necessário utilizar alguns comandos para que possa solucionar os conflitos e efetuar o merge:

    ```bash
    git checkout develop
    git pull
    git merge feat123/titulo-da-tarefa
    ```

    Nota: Os 3 comandos precisam ser executados, mesmo se acreditar que o seu ambiente está atualizado.

2. Após efetuar o merge da sua branch em Develop, serão exibidos todos os arquivos que tenham conflitos. É necessário abrir esses arquivos e fazer as devidas correções de cada conflito.

3. Depois que todos os conflitos forem resolvidos, pode efetuar o push para Develop e o merge já estará feito:

    ```bash
    git commit -m "Merge branch 'feat123/titulo-da-tarefa' into develop"
    git push origin develop
    ```

    Nota 2: Apenas efetue push em develop em situações de resolução de conflitos. Nunca desenvolva features e correções diretamente na develop.

    Nota 3: Nunca confunda o processo de resolução de conflitos da Develop com o processo realizado na Main.

## Minha PR pra Main deu conflito... e agora?

1. Se a PR pra Main deu conflito, deve-se executar alguns comandos para fazer um merge na branch da sua tarefa a partir da Main, e resolver os conflitos que surgirem:
   
    ```bash
    git checkout main
    git pull
    git checkout feat123/titulo-da-tarefa
    git merge main
    ```

    Nota: Os 3 comandos precisam ser executados, mesmo se acreditar que o seu ambiente está atualizado.

2. Após efetuar o merge da main na sua branch, serão exibidos todos os arquivos que tenham conflitos. É necessário abrir esses arquivos e fazer as devidas correções de cada conflito.

3. Depois que todos os conflitos forem resolvidos, pode efetuar o push para Develop e o merge já estará feito:

    ```bash
    git commit -m "Merge branch main into 'feat123/titulo-da-tarefa'"
    git push origin feat123/titulo-da-tarefa
    ```

4. Uma vez que o push tenha sido feito para sua branch, a PR será atualizada e o botão de merge estará habilitado (desde que os Reviewers tenham aprovado as alterações).

    Nota 2: Nunca confunda o processo de resolução de conflitos da Main com o processo realizado na Develop.

## Fiz merge da Develop na minha branch e dei push... e agora?

1. Se por acaso você confundir os processos de resolução de conflitos, pode acabar se deparando com essa situação. Se você efetuar o push após um merge da develop para a main, a primeira coisa a fazer é fechar a PR para a main (ou não abrir PR para a Main).

2. Será necessário criar uma nova branch, com base no último commit que você havia realizado para a sua branch (antes do merge da Develop na Main).

    ```
    git checkout hash_do_ultimo_commit
    git checkout -b feature123/minha-tarefa
    git push origin feature123/minha-tarefa
    ```

    Nota: Cuidado para não confundir com algum commit do merge. Deve-se pegar o último commit de funcionalidade da sua tarefa.

    Nota 2: Usar um nome diferente da primeira branch que havia criado. Uma dica é usar feat123 e feature123, por exemplo.

3. Após isso, basta efetuar os mesmos processos de PR para Develop e para Main.
