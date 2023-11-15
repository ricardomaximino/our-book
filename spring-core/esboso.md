Spring-core

Bom para começar eu acho importante ter uma idéia do que o spring faz, para explicar de uma maneira bem simplificada imagina que o spring inteiro é uma class com varias propriedades e varios metodos, bem agora imagine que o spring core esta compuesta por uma das propriedades e dois metodos.
A propriedade core é um objeto do tipo Map<String,Object> e o metodo core faz o siguente:

*	ele tem uma lista de class para instanciar e guardar na propriedade map(propriedade core)

*	o outro metodo é bem simples retorna a referencia da instancia de uma classe pelo nome. Exp: public Object getBean(String beanName){
           return map.get(beanName);
  }
isso é o spring core o responsavel de criar a lista de classes que devem ser instanciadas, instanciar as classes e retornar a instancia da classe necessaria sempre que for solicitado.
	Beleza agora vamos intenter:
    
*	como o nosso spring vai saber quais classes devem ser instanciadas.

*	e como se solicita a referencia da instancia de uma classe para o nosso spring

Configurações

	1 - Para que nosso spring sabe quais classes ele debe instanciar a gente deve configurar o nosso spring antes de iniciar a applicação.
	Para configuarar o spring existem varias maneiras:

*	XML
*	@ANNOTATION
*	JAVA CONFIGURURATION

a gente vai focar nas @ANNOTATION e JAVA CONFIGURATION.
	Então a primeira coisa que vamos ver são as maneiras de avisar o spring que uma classe deve ser instanciada.

	A maneira mais simples de todas na minha opinião é @Component

Se criamos uma classe e colocamos a anotação @Component o spring já sabe que tem que instanciar essa classe.

	A anotação @Component tem vários filhos, derivantes:

	=> @Controller
	=> @RestController
	=> @Service
	=> @Repository
	=> @Named => casos especiais
	=> @ManagedBean => casos especiais

ou usando uma classe de configuração que nada mais é que uma classe normal anotada com a anotação @Configuration com metodos publicos que criam e retornam objetos, esses metodos devem serem anotados com @Bean

@Configuration
public class Config 

@Bean
public ClassA classA(){
return new ClassA();
}
}

Pronto já sabemos todas as maneiras de avisar o spring quais classes devem ser instanciadas. Mais adiante vamos ver tudo isso de uma maneira muito mais profunda, mas que momento isso é suficiente.

	2-  Agora vamos ver como solicitar a referencia de instancia de uma classe.
	Existem duas maneiras de solicitar  ao spring uma instancia 
*	@ANNOTATION
*	PROGRAMATICALLY

	A maneira que todos nós já estamos familiarizado é a PROGRAMATICALLY
	
	ClassA classA = (ClassA) spring.get(''classA'');
	por constructor anotado com @Autowired ou constructor único  sem anotação de uma classe anotada com @Component o uma de suas variantes.
	Por propriedades anotadas com @Autowired de classes anotadas com @Component ou uma de suas variantes.
	Ou em metodos  invocado diretamente pelo spring como é o caso dos Controller.

Pronto já sabemos como solicitar a referencia da instacia de uma classe para o spring. Mais adiante vamos ver tudo isso de uma maneira muito mais profunda, mas que momento isso é suficiente.

As configurações em nível de classes são:

*	Nome (id)
*	scope (singleton, prototype importante conhecer(
*	primary
*	qualifiers
*	lifecicle
*	init e destroy method's name
*	Lazy or Eager


As configurações em nível de metodos e propriedades são:

*	qualifiers
*	required (default)
	
Problemas especiais de injeção de dependencias:

*	dependencias circulares
*	ambiguidades

AOP e Spring SpEL também fazem parte do core mas eu prefiro voltar mais adiante para falar só disso.
