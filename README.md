### Dependência opcional no Maven

# 1. Visão Geral
Este breve tutorial descreverá a tag <<optional>> do Maven e como podemos usá-la para reduzir o tamanho e o escopo de um artefato de projeto Maven, como WAR, EAR ou JAR.

Para relembrar o Maven, confira nosso guia completo.

# 2. O que é <opcional>?
Às vezes, criaremos um projeto Maven para ser uma dependência de outros projetos Maven. Ao trabalhar em tal projeto, pode ser necessário incluir uma ou mais dependências que são úteis apenas para um subconjunto dos recursos desse projeto.

Se um usuário final não usar esse subconjunto de recursos, o projeto ainda obterá essas dependências transitivamente. Isso aumenta o tamanho do projeto do usuário desnecessariamente e pode até introduzir versões de dependência conflitantes com outras dependências do projeto.

Idealmente, devemos dividir o subconjunto de recursos do projeto em seu próprio módulo e, portanto, não poluir o resto do projeto. No entanto, isso nem sempre é prático.

Para excluir essas dependências especiais do projeto principal, podemos aplicar a tag <optional> do Maven a elas. Isso força qualquer usuário que deseja usar essas dependências a declará-las explicitamente. No entanto, isso não força essas dependências em um projeto que não precisa delas.

# 3. Como usar <opcional>
Como veremos, podemos incluir o elemento <optional> com um valor true para tornar opcional qualquer dependência do Maven.

Vamos supor que temos o seguinte pom de projeto:

```
<project>
    ...
    <artifactId>project-with-optionals</artifactId>
    ...
    <dependencies>
        <dependency>
            <groupId>com.isaccanedo</groupId>
            <artifactId>optional-project</artifactId>
            <version>0.0.1-SNAPSHOT</version>
            <optional>true</optional>
        </dependency>
    </dependencies>
</project>
```

Neste exemplo, embora o projeto opcional seja rotulado como opcional, ele permanece como uma dependência utilizável do projeto com opcionais, como se a tag <optional> nunca tivesse existido.

Para ver o efeito da tag <optional>, precisamos criar um novo projeto que dependa de projetos com opcionais:

```
<project>
    ...
    <artifactId>main-project</artifactId>
    ...
    <dependencies>
        <dependency>
            <groupId>com.isaccanedo</groupId>
            <artifactId>project-with-optionals</artifactId>
            <version>0.0.1-SNAPSHOT</version>
        </dependency>
    </dependencies>
</project>
```

Agora, se tentarmos referenciar o projeto opcional de dentro do projeto principal, veremos que o projeto opcional não existe. Isso ocorre porque a tag <optional> impede que ele seja incluído transitivamente.

Se acharmos que precisamos de um projeto opcional em nosso projeto principal, simplesmente precisamos declará-lo como uma dependência.

# 4. Conclusão
Neste artigo, vimos a tag <optional> do Maven. Os principais benefícios de usar a tag são que ela pode reduzir o tamanho de um projeto e ajudar a prevenir conflitos de versão. Também vimos que a tag não afeta o projeto que a utiliza.
