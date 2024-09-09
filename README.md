<b>Construir um aplicativo Multi Tenants com Django, Django Rest Framework e Django Tenant</b>

<img src="https://blog.thinkitive.net/wp-content/uploads/2023/09/meta-image-3-1024x535.jpg" width="35%"></img> 

<b>O que é o aplicativo Multi Locatários</b>

Na arquitetura de software multilocatário (também chamada de multilocação de software), uma única instância de um aplicativo de software (e seu banco de dados e hardware subjacentes) atende a vários locatários (ou contas de usuário). Um locatário pode ser um usuário individual, mas, mais frequentemente, é um grupo de usuários (como uma organização do cliente) que compartilha acesso e privilégios comuns na instância do aplicativo. Os dados de cada locatário são isolados e invisíveis para os outros locatários que compartilham a instância do aplicativo, garantindo a segurança e a privacidade dos dados para todos os locatários. 

<img src="https://blog.thinkitive.net/wp-content/uploads/2023/09/What-is-Multi-Tenants-Application-1024x490.png" width="40%"></img>

<b>Tipos de modelagem multilocatários</b>

    <b>Modelagem de replicação de instância:</b> - Nesta modelagem, o sistema gira uma nova instância para cada locatário. Isso é mais fácil de começar, mas difícil de escalar. Torna-se um desafio quando há mais inquilinos. É semelhante à arquitetura de locatário único.

    <b>Modelagem de Segregação de Banco de Dados:</b> - Nesta modelagem, separamos bancos de dados para cada Locatário para armazenar seus dados em um banco de dados específico. Novamente, será difícil lidar com bancos de dados quando houver um aumento no número de locatários.

    <b>Modelagem de segregação de esquema:</b> - Nesta modelagem, usamos um único banco de dados e uma única instância de um aplicativo. Quando criamos um novo locatário, criamos um novo esquema nesse banco de dados para esse locatário armazenar seus dados separadamente.
