# Groovy-Script-Skills
CopyPast Groovy Script

## ⚠️ IMPORTS

  import com.sap.gateway.ip.core.customdev.util.Message ->  { message.getBody() - message.getHeaders() - message.getProperties() }
    Representa a mensagem que está sendo processada no fluxo de integração. 
    
    def Message processData(Message message) {
    // Pegar o corpo da mensagem como string
    def body = message.getBody(String)
      
    // Adicionar um novo cabeçalho
    message.setHeader("meuHeader", "valor")
    
    // Adicionar uma nova propriedade
     message.setProperty("minhaPropriedade", "valor")
      
    // Alterar o corpo da mensagem
       message.setBody("Novo corpo")
      
      return message
      }
         

  import groovy.json.JsonBuilder ->  { def builder = new JsonBuilder() }
    Útil quando você quer construir um JSON manualmente, a partir de dados manipulados no script.
    
    def builder = new JsonBuilder()
    builder {
    nome "José"
    idade 23
    ativo true
    }

    def jsonString = builder.toPrettyString()

    // Resultado:
    println(jsonString)


  import groovy.json.JsonSlurper
    É usado quando você recebe um JSON (normalmente no corpo da mensagem) e precisa acessar os dados dele para manipular, extrair ou transformar.
    
    def jsonText = '{"nome": "João", "idade": 28}'
    def parser = new JsonSlurper()
    def data = parser.parseText(jsonText)
    
    println data.nome   // João
    println data.idade  // 28

    
  import groovy.json.JsonOutput
    Usado para transformar mapas/listas em JSON string, formatar o JSON com indentação legível (prettyPrint) e usar JSON como saída no corpo da mensagem.

    def Message processData(Message message) {
    def resultado = [
        status: "sucesso",
        codigo: 200
    ]

    def json = JsonOutput.toJson(resultado)
    message.setBody(json)

    return message
    }
    



