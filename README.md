<b>Construir um aplicativo Multi Tenants com Django, Django Rest Framework e Django Tenant</b>

<img src="https://blog.thinkitive.net/wp-content/uploads/2023/09/meta-image-3-1024x535.jpg" width="50%"></img> 

<b>O que é o aplicativo Multi Locatários</b>

Na arquitetura de software multilocatário (também chamada de multilocação de software), uma única instância de um aplicativo de software (e seu banco de dados e hardware subjacentes) atende a vários locatários (ou contas de usuário). Um locatário pode ser um usuário individual, mas, mais frequentemente, é um grupo de usuários (como uma organização do cliente) que compartilha acesso e privilégios comuns na instância do aplicativo. Os dados de cada locatário são isolados e invisíveis para os outros locatários que compartilham a instância do aplicativo, garantindo a segurança e a privacidade dos dados para todos os locatários. 

<img src="https://blog.thinkitive.net/wp-content/uploads/2023/09/What-is-Multi-Tenants-Application-1024x490.png" width="50%"></img>

<b>Tipos de modelagem multilocatários</b>

<b>Modelagem de replicação de instância:</b> - Nesta modelagem, o sistema gira uma nova instância para cada locatário. Isso é mais fácil de começar, mas difícil de escalar. Torna-se um desafio quando há mais inquilinos. É semelhante à arquitetura de locatário único.

<b>Modelagem de Segregação de Banco de Dados:</b> - Nesta modelagem, separamos bancos de dados para cada Locatário para armazenar seus dados em um banco de dados específico. Novamente, será difícil lidar com bancos de dados quando houver um aumento no número de locatários.

<b>Modelagem de segregação de esquema:</b> - Nesta modelagem, usamos um único banco de dados e uma única instância de um aplicativo. Quando criamos um novo locatário, criamos um novo esquema nesse banco de dados para esse locatário armazenar seus dados separadamente.

<img src="https://blog.thinkitive.net/wp-content/uploads/2023/09/Multi-Tenants-modelling-1024x408.png" width="50%"></img>

<b>Por que usamos aplicativos multilocatários?</b>

Vejamos um exemplo do Domínio Saúde. Neste domínio, cada cliente deseja separar e isolar seus dados uns dos outros. Os dados no domínio Saúde são suscetíveis aos pacientes, por isso os clientes desejam separá-los. No aplicativo multilocatário, separamos o banco de dados ou esquema para que os dados sejam separados. Portanto, devido à conformidade dos clientes relacionada aos dados, estamos usando um aplicativo multilocatário.

<b>O que são esquemas?</b>

Geralmente, um esquema pode ser visto como um diretório em um sistema operacional, cada diretório (esquema) com seu próprio conjunto de arquivos (tabelas e objetos). Isso permite que o mesmo nome de tabela e objetos sejam usados ​​em esquemas diferentes sem conflito.

Um banco de dados contém um ou mais esquemas nomeados, que por sua vez contêm tabelas. Os esquemas também contêm outros objetos nomeados, incluindo tipos de dados, funções e operadores. O mesmo nome de objeto pode ser usado em esquemas diferentes sem conflito; por exemplo, esquema1 e meu esquema podem conter tabelas denominadas minhatabela. Ao contrário dos bancos de dados, os esquemas não são rigidamente separados: um usuário pode acessar objetos em qualquer esquema do banco de dados ao qual esteja conectado, se tiver privilégios para fazê-lo.

<b>Existem vários motivos pelos quais alguém pode querer usar esquemas:</b>

Para permitir que muitos usuários usem um banco de dados sem interferir uns nos outros.
Organize objetos de banco de dados em grupos lógicos para torná-los mais gerenciáveis.
Aplicativos de terceiros podem ser colocados em esquemas separados para que não colidam com os nomes de outros objetos.

Os esquemas são análogos aos diretórios no nível do sistema operacional, exceto que os esquemas não podem ser aninhados. 

<b>Para mais informações:</b> <a src="https://www.postgresql.org/docs/14/ddl-schemas.html">https://www.postgresql.org/docs/14/ddl-schemas.html</a>