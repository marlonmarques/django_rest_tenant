<b>Construir um aplicativo Multi Tenants com Django, Django Rest Framework e Django Tenant</b>

Baseado no exelente trabalho: <a src="https://www.thinkitive.com/blog/how-to-build-multi-tenants-application-with-django-django-rest-framework-and-django-tenant/">https://www.thinkitive.com/blog/how-to-build-multi-tenants-application-with-django-django-rest-framework-and-django-tenant/</a>

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

<b>Requisitos</b>

1. Python (v3.10) ou superior – <a src="https://www.python.org/">https://www.python.org/</a>
2. PostgreSQL (v14) recomendado – <a src="https://www.postgresql.org/">https://www.postgresql.org/</a>
3. Django (v5.0) ou superio – <a src="https://www.djangoproject.com/">https://www.djangoproject.com/</a>
4. Django Rest Framework (v3.15.0) – <a src="https://www.django-rest-framework.org/">https://www.django-rest-framework.org/</a>
5. Django Tenants (v3.5.0) ou superior – <a src="https://django-tenants.readthedocs.io/en/latest/">https://django-tenants.readthedocs.io/en/latest/</a>

<b>Python</b> – Python é uma linguagem de programação poderosa e fácil de aprender. Possui estruturas de dados eficientes de alto nível e uma abordagem simples, mas eficaz para programação orientada a objetos.

<b>PostgreSQL</b> – PostgreSQL é um poderoso sistema de banco de dados relacional de objeto de código aberto para dados persistentes.

<b>Django</b> – Django é uma estrutura web Python de alto nível que incentiva o desenvolvimento rápido e um design limpo e pragmático. Desenvolvido por desenvolvedores experientes, ele cuida do incômodo do desenvolvimento web, para que você possa se concentrar em escrever seu aplicativo sem reinventar a roda. É gratuito e de código aberto.

<b>Instalação:</b> - pip install Django==5.0

<b>Django Rest Framework</b> – O framework Django REST é um kit de ferramentas poderoso e flexível para construir APIs da Web.
<b>Instalação:</b> - pip install djangorestframework==3.15.0

<b>Django Tenant</b> – Django Tenant é um pacote; usando isso, aplicaremos multilocação em nosso aplicativo.
<b>Instalação:</b> - pip install Django-tenants ==3.5.0

<b>Nota:</b> - Há um problema neste pacote que atualmente suporta multilocação baseada em subdomínio. Além disso, isso pode dificultar novamente a manutenção de muitos subdomínios

Mas modificaremos este pacote para multilocação usando um único domínio. 

<b>Notas: -</b>

* Este aplicativo permite que sites baseados em Django tenham vários locatários por meio de esquemas PostgreSQL. Um recurso vital para todos os sites de software como serviço.
* Atualmente, o Django não fornece uma maneira simples de suportar vários inquilinos usando a mesma instância de projeto, mesmo quando apenas os dados são diferentes. Como não queremos que você execute muitas cópias do seu projeto, você poderá ter o seguinte:
* Vários clientes em execução na mesma instância
– Dados compartilhados e específicos do locatário
– Tenant View-Routing (aceitar o locatário via cabeçalho e depois usar roteamento)

<b>Criar aplicativo de multilocação</b>

<b>1. Crie um aplicativo Django básico</b>

O comando abaixo é usado para criar um projeto Django com o nome django_multi_tenancy
Django-admin start project django_multi_tenancy

<b>2. Crie um aplicativo</b>

O comando abaixo é usado para criar um aplicativo Django com o nome app
– python manage.py start app

<b>3. Crie dois modelos</b>

<b>a. Modelo de Inquilino</b> – Este modelo é responsável por armazenar os nomes dos inquilinos. Você pode adicionar mais campos, se necessário no seu caso.
<b>b. Modelo de Domínio</b> – Este modelo armazena domínios de locatários exclusivos para cada locatário.

From Django.Db import models
from django_tenants.models import DomainMixin, TenantMixin
class Tenant(TenantMixin):
name = models.CharField(max_length=100, unique=True)
#default true, the schema will be automatically created and synced when it is saved
auto_create_schema = True
class Domain(DomainMixin):
Pass

<b>4. Configurações básicas</b>

– Você terá que fazer as seguintes modificações em seu arquivo settings.py.
– Essa configuração é necessária para a multilocação do aplicativo no aplicativo para lidar com a multilocação baseada em esquema.
– Sua configuração DATABASE_ENGINE precisa ser alterada para 
DATABASES = {
"default": {
"ENGINE": "django_tenants.postgresql_backend",
#..
}
}

<b>5. Adicione django_tenants.routers.TenantSyncRouter à sua configuração DATABASE_ROUTERS para que os aplicativos corretos possam ser sincronizados, dependendo do que está sendo sincronizado (shared or Tenant)</b>

Este roteador é responsável por lidar com o roteamento para um locatário específico. Quando alteramos o esquema com base no Locatário, isso resolverá essa situação. Usaremos o roteamento para mudar para um esquema de locatário específico.
DATABASE_ROUTERS=(
"django_tenants.routers.TenantSyncRouter",
) 

<b>6. Crie um arquivo middleware.py e adicione este código</b>

Este é um dos arquivos e códigos críticos onde iremos verificar e verificar o Locatário e mudar o esquema com base no Locatário. Quando enviamos o nome do locatário do Tenant-Header, no middleware, encontre esse nome e valide o nome do locatário correto. Se isso estiver correto, alteramos o esquema para esse locatário específico. O código abaixo é responsável por esta lógica. 

```python

from django.conf import settings
from django.core.exceptions import DisallowedHost
from django.db import connection
from django.http import Http404
from django.urls import set_urlconf
from django.utils.deprecation import MiddlewareMixin

"""
@autor: Marlon
@github: https://github.com/marlonmarques/django_rest_tenant
"""

from django_tenants.utils import (
    remove_www,
    get_public_schema_name,
    get_tenant_types,
    has_multi_type_tenants,
    get_tenant_domain_model,
    get_public_schema_urlconf,
)
from .models import Tenant

class TenantMainMiddleware(MiddlewareMixin):
    TENANT_NOT_FOUND_EXCEPTION = Http404
    """
    This middleware should be placed at the very top of the middleware stack.
    Selects the proper database schema using the request host. Can fail in
    various ways which is better than corrupting or revealing data.
    """

    @staticmethod
    def hostname_from_request(request):
        """Extracts hostname from request. Used for custom requests filtering.
        By default removes the request's port and common prefixes.
        """
        return remove_www(request.get_host().split(":")[0])

    def get_tenant(self, domain_model, hostname):
        domain = domain_model.objects.select_related("tenant").get(domain=hostname)
        return domain.tenant

    def process_request(self, request):
        # Connection needs first to be at the public schema, as this is where
        # the tenant metadata is stored.

        connection.set_schema_to_public()
        try:
            hostname = self.hostname_from_request(request)
        except DisallowedHost:
            from django.http import HttpResponseNotFound

            return HttpResponseNotFound()
        #Check the Tenant from headers to change the schema for each request.
        if "Tenant-Header" in request.headers:
            tenant_name = request.headers.get("Tenant-Header")
            domain_model = Tenant
        else:
            domain_model = get_tenant_domain_model()
            
        try:
            if "Tenant-Header" in request.headers:
                tenant = Tenant.objects.get(name__iexact=tenant_name)
            else:
                tenant = self.get_tenant(domain_model, hostname)
        except domain_model.DoesNotExist:
            self.no_tenant_found(request, hostname)
            return

        tenant.domain_url = hostname
        request.tenant = tenant
        connection.set_tenant(request.tenant)
        self.setup_url_routing(request)

    def no_tenant_found(self, request, hostname):
        """What should happen if no tenant is found.
        This makes it easier if you want to override the default behavior"""
        if (
            hasattr(settings, "SHOW_PUBLIC_IF_NO_TENANT_FOUND")
            and settings.SHOW_PUBLIC_IF_NO_TENANT_FOUND
        ):
            self.setup_url_routing(request=request, force_public=True)
        else:
            raise self.TENANT_NOT_FOUND_EXCEPTION(
                'No tenant for hostname "%s"' % hostname
            )

    @staticmethod
    def setup_url_routing(request, force_public=False):
        """
        Sets the correct url conf based on the tenant
        :param request:
        :param force_public
        """
        public_schema_name = get_public_schema_name()
        if has_multi_type_tenants():
            tenant_types = get_tenant_types()
            if not hasattr(request, "tenant") or (
                (force_public or request.tenant.schema_name == get_public_schema_name())
                and "URLCONF" in tenant_types[public_schema_name]
            ):
                request.urlconf = get_public_schema_urlconf()
            else:
                tenant_type = request.tenant.get_tenant_type()
                request.urlconf = tenant_types[tenant_type]["URLCONF"]
            set_urlconf(request.urlconf)

        else:
            # Do we have a public-specific urlconf?
            if hasattr(settings, "PUBLIC_SCHEMA_URLCONF") and (
                force_public or request.tenant.schema_name == get_public_schema_name()
            ):
                request.urlconf = settings.PUBLIC_SCHEMA_URLCONF

```

<b>7. Adicione o middleware apps.tenant.middleware.TenantMainMiddleware ao topo do MIDDLEWARE para que cada solicitação possa ser configurada para usar o esquema correto.</b>

Este código é responsável por adicionar a classe de middleware acima ao aplicativo Django, portanto, quando uma solicitação chegar, primeiro esse middleware será chamado e, de acordo com o esquema do locatário, será alterado.

MIDDLEWARE=(
"apps.tenant.middleware.TenantMainMiddleware",
#…
) 

<b>8. Adicione a opção do processador de contexto django.template.context_processors.request context_processors de TEMPLATES; caso contrário, o Locatário não estará disponível mediante solicitação.</b>

O código abaixo é responsável por adicionar um locatário ao objeto da solicitação para que em nossa solicitação possamos encontrar o Locatário e definir o Locatário na solicitação. 

TEMPLATES = [
{
#…
'OPTIONS': {
'context_processors': [
'django.template.context_processors.request',
#…
],
},
},
] 

<b>9. Suporte administrativo (para Django Super Admin)</b>

TenantAdminMixin está disponível para registrar o modelo de locatário. O mixin desabilita os botões salvar e excluir quando não estiver no Tenant atual ou público (evitando exceções). 

from django.contrib import admin
from django_tenants.admin import TenantAdminMixin
from app.models import Domain, Tenant
# Register domain model
admin.site.register(Domain)
# Register tenant model
@admin.register(Tenant)
class TenantAdmin(TenantAdminMixin, admin.ModelAdmin):
list_display = ('name', )

Tive dificuldade de acessar a api pelo localhost mais encontrei a solução adcionado no settings

SHOW_PUBLIC_IF_NO_TENANT_FOUND = True #fix localhost em tenant

<b>10. Crie um de nossos modelos de caso de uso</b>

Criaremos um modelo de amostra que será específico do locatário e, em seguida, verificaremos se nossa implementação de multilocação é ou não aplicada em nosso aplicativo. Usarei este modelo como TENANT APPS. 

From django.db import models
class Hotel(models.Model):
name = models.CharField(max_length=255)
location = models.CharField(max_length=255)
description = models.CharField(max_length=255)
picture = models.ImageField()

<b>11. Configurar aplicativos de locatário e compartilhados</b>

Para usar aplicativos compartilhados e específicos de locatário, há duas configurações chamadas SHARED_APPS e TENANT_APPS. SHARED_APPS é uma lista de strings como INSTALLED_APPS e deve conter todos os aplicativos que você deseja sincronizar ao público. No entanto, se SHARED_APPS estiver definido, esses serão os únicos aplicativos sincronizados com seu esquema público! O mesmo se aplica a TENANT_APPS, que espera uma tupla de strings onde cada string é um aplicativo. Se definido, apenas esses aplicativos serão sincronizados com todos os seus locatários. Aqui está um conjunto de amostras. THIRD_PARTY_APPS e o aplicativo Django padrão serão adicionados como SHARED_APPS, e nosso modelo de caso de uso (como o modelo de hotel) é TENANT_APPS

THIRD_PART_APPS = [
# Third party apps
]SHARED_APPS = [
‘django_tenants’,
‘django.contrib.contenttypes’,
‘django.contrib.auth’,
‘django.contrib.sessions’,
‘django.contrib.sites’,
‘django.contrib.messages’,
‘django.contrib.admin’,
] + THIRD_PART_APPS
TENANT_APPS = [
# your tenant-specific apps
‘app.Hotel’,
]
INSTALLED_APPS = SHARED_APPS + [app for app in TENANT_APPS if app not in SHARED_APPS] 

<b>12. Você também deve definir onde seus modelos de locatário e domínio estão localizados.</b>

As linhas abaixo são necessárias para especificar nosso inquilino e modelo de domínio para que o Django Tenant encontre esses modelos no aplicativo.

TENANT_MODEL = 'tenant.Tenant'
TENANT_DOMAIN_MODEL = "tenant.Domain"
TENANT_SUBFOLDER_PREFIX = "tenant"
TENANT_TIMEZONE_DISPLAY_GMT_OFFSET = False

<b>13. Agora execute os comandos</b>

Esses comandos geram os arquivos de migração para modelos criados e aplicam essas migrações em cada esquema de banco de dados. 

<b>– python manage.py makemigrations</b>
<b>– python manage.py migrate</b>

<b>14. Crie inquilinos e teste a multilocação</b>

Passo 1 – Crie um superusuário 
python manage.py createsuperuser

Passo 2- Faça login no painel de administração
http://127.0.0.1:8000/admin/ 

Etapa 3 – Crie um locatário no painel de administração

Passo 4 – Crie um domínio no painel de administração para esse locatário

Criei dois inquilinos, <b>demo1 e demo2 </b>

<img src="https://blog.thinkitive.net/wp-content/uploads/2023/09/tenants-and-test-multi-tenancy-1024x453.png" width="75%"></img>
<img src="https://blog.thinkitive.net/wp-content/uploads/2023/09/tenant-demo-2-1024x449.png" width="75%"></img>

<b>15. Crie API CRUD para o modelo Hotel</b>

#arquivo serializers.py

Este arquivo é usado para criar um serializador Django Rest Framework para API.

Os serializadores permitem que dados complexos, como conjuntos de consultas e instâncias de modelo, sejam convertidos em tipos de dados nativos do Python e rapidamente renderizados em JSON, XML ou outros tipos de conteúdo. Os serializadores também fornecem desserialização, permitindo que os dados analisados ​​sejam convertidos em tipos complexos após a validação dos dados recebidos. 

from rest_framework import serializers
from app.models import Hotel
class HotelSerializer(serializers.ModelSerializer):
class Meta:
model = Hotel
fields = "all"

#arquivo visualizações.py

Este arquivo é usado para criar conjuntos de visualizações para a API Django Rest Framework.

A estrutura REST do Django não apenas permite combinar a lógica para um conjunto de visualizações relacionadas em uma única classe chamada conjunto de visualizações. Mas você também pode encontrar implementações conceitualmente semelhantes, como 'Recursos' ou 'Controladores' em outras estruturas. 

from rest_framework.viewsets import ModelViewSet
from app.serializer import HotelSerializer
from app.models import Hotel
class HotelViewSet(ModelViewSet):
queryset = Hotel.objects.all()
serializer_class = HotelSerializer

#arquivo urls.py

Este arquivo é usado para criar URLs para APIs de aplicativos.

A estrutura REST suporta roteamento automático de URLs para Django e também fornece uma maneira simples, rápida e consistente de conectar sua lógica de visualização a um conjunto de URLs usando um roteador. 

from django.conf import settings
from rest_framework.routers import DefaultRouter, SimpleRouter
from app.views import HotelViewSet
if settings.DEBUG:
router = DefaultRouter()
else:
router = SimpleRouter()
router.register("", HotelViewSet, basename="hotel-apis")
urlpatterns += router.urls

<b>Nota: - Agora sua API está pronta para o teste com multilocação</b>

<b>16. Chame a API com seu locatário (prova de conceito)</b>

<img src="https://blog.thinkitive.net/wp-content/uploads/2023/09/Call-API-with-your-Tenant-1-1024x278.png" width="75%"></img>

<img src="https://blog.thinkitive.net/wp-content/uploads/2023/09/Call-API-with-your-Tenant-2.png" width="75%"></img>


<b>1. Obter API</b>

Primeiro, chame a API GET para ambos os locatários. Ambos os inquilinos atualmente não há dados disponíveis em nenhum dos inquilinos

<b>2. API POST</b>

<img src="https://blog.thinkitive.net/wp-content/uploads/2023/09/postAPI.png" width="75%"></img>

Não vou colocar mais imagens pois seque como funciona a api.

Nota: – Aqui, a chave Tenant-Header é responsável pelo nome do seu inquilino. Certifique-se de passar o nome correto do locatário no cabeçalho do locatário. Você deverá passar aqui o nome do Inquilino. Se passada como pública, esta API usará o esquema padrão para manipular dados no banco de dados. 

mais adiante farei outro tutorial mostrando como funciona com frontend em react ou nextjs

<img src="https://github.com/marlonmarques/django_rest_tenant/blob/main/imgs/Captura%20de%20tela%20de%202024-09-09%2022-07-48.png?raw=true" width="75%"></img>