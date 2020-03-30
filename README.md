<h1 align="center">
  <image src="https://github.com/lucasiori/gobarber-backend/blob/master/.github/gobarber-backend.png" alt="GoBarber" width="500" />
</h1>

<h3 align="center">GoBarber</h3>

<blockquote align="center">Aplicação base desenvolvida durante o Bootcamp GoStack</blockquote>

<p align="center">
  <a href="#sobre-aplicacao">Sobre a aplicação</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#comecando">Começando</a>
</p>

<br />

<h2 id="sobre-aplicacao">ℹ Sobre a aplicação</h2>
<p>A aplicação trata-se de um sistema de gerenciamento de horários para barbearias, onde o provedor de serviços faz o seu cadastro 
na plataforma web e pode consultar a sua agenda para qualquer dia. Nessa consulta são mostrados todos os horários que estão disponíveis
para novos agendamentos ou horários que já estão ocupados.</p>
<p>No aplicativo mobile, o usuário realiza o seu cadastro e pode agendar um horário com o provedor de serviços de sua escolha, além de consultar e cancelar seus agendamentos existentes.</p>

<br /> 

<h2 id="comecando">▶ Começando</h2>

<p>Antes de iniciar o serviço, é necessário configurar as variáveis ambientes no arquivo ".env".</p>
<p>Todas as variáveis que precisam de configuração estão listadas no arquivo ".env.example"</p>
<p>Acesse a pasta do projeto e execute o seguinte comando para instalar as dependências necessárias para o projeto:</p>
<p><code>npm install</code></p>
<p>Agora, com todas as dependências instaladas, para iniciar o serviço execute o comando:</p>
<p><code>npm start</code></p>
<p>Para iniciar o servidor de tarefas em background:</p>
<p><code>npm queue</code></p>

<br /> 

<h2 id="entidades-rotas">✅ Entidades e Rotas</h2>

<h3>Entidades</h3>

<ul>
  <li>
    <h4>Usuário</h4>
    <table>
      <thead>
        <th>Propriedade</th>
        <th>Descrição</th>
      </thead>
      <tbody>
        <tr>
          <td>name</td>
          <td>Nome do usuário (String)</td>
        </tr>
        <tr>
          <td>email</td>
          <td>Email do usuário (String)</td>
        </tr>
        <tr>
          <td>password</td>
          <td>Senha do usuário (String)</td>
        </tr>
        <tr>
          <td>provider</td>
          <td>Identificação de usuário provedor de serviços (Boolean)</td>
        </tr>
        <tr>
          <td>avatar_id</td>
          <td>ID do avatar no banco de dados (Number)</td>
        </tr>
      </tbody>
    </table>
  </li>
  
  <li>
    <h4>Agendamento</h4>
    <table>
      <thead>
        <th>Propriedade</th>
        <th>Descrição</th>
      </thead>
      <tbody>
        <tr>
          <td>user_id</td>
          <td>ID do usuário que esta fazendo o agendamento (Number)</td>
        </tr>
        <tr>
          <td>provider_id</td>
          <td>ID do provedor de serviços (Number)</td>
        </tr>
        <tr>
          <td>date</td>
          <td>Data e hora do agendamento (Date)</td>
        </tr>
        <tr>
          <td>canceled_at</td>
          <td>Data e hora do cancelamento do agendamento (Date)</td>
        </tr>
      </tbody>
    </table>
  </li>
  
  <li>
    <h4>Notificação</h4>
    <table>
      <thead>
        <th>Propriedade</th>
        <th>Descrição</th>
      </thead>
      <tbody>
        <tr>
          <td>user</td>
          <td>ID do provedor que receberá a notificação (Number)</td>
        </tr>
        <tr>
          <td>content</td>
          <td>Conteúdo da notificação (String)</td>
        </tr>
        <tr>
          <td>read</td>
          <td>Identificação de leitura da notificação (Boolean)</td>
        </tr>
      </tbody>
    </table>
  </li>
</ul>

<h3>Rotas</h3>

<h4>GET</h4>

<ul>
  <li>
    <span><strong>(base_url)/providers</strong> - Retorna uma lista de provedores de serviços</span> <br />
     &nbsp;&nbsp; <strong>Autenticação:</strong> Bearer token Jwt <br /><br />
  </li>
  
  <li>
    <span>
      <strong>(base_url)/providers/(provider_id)/available</strong> - Retorna uma lista de horários disponíveis para o 
      provedor de serviços
    </span> <br />
      &nbsp;&nbsp; <strong>Route Param:</strong> <br />
     &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <strong>provider_id:</strong> ID do provedor que deseja buscar os horários disponíveis <br />
     &nbsp;&nbsp; <strong>Query Param:</strong> <br />
     &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <strong>date:</strong> Data do dia que deseja buscar os horários disponíveis (Timemillis) 
    <br />
     &nbsp;&nbsp; <strong>Autenticação:</strong> Bearer token Jwt <br /><br />
  </li>
  
  <li>
    <span><strong>(base_url)/appointments</strong> - Retorna uma lista de agendamentos do usuário logado</span> <br />
     &nbsp;&nbsp; <strong>Autenticação:</strong> Bearer token Jwt <br /><br />
  </li>
  
  <li>
    <span><strong>(base_url)/notifications</strong> - Retorna uma lista de notificações para o provedor de serviços logado</span> <br />
     &nbsp;&nbsp; <strong>Autenticação:</strong> Bearer token Jwt <br /><br />
  </li>
  
  <li>
    <span><strong>(base_url)/schedules</strong> - Retorna uma lista de agendamentos para o provedor de serviços logado</span> <br />
     &nbsp;&nbsp; <strong>Query Param:</strong> <br />
     &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <strong>date:</strong> Data do dia que deseja buscar os agendamentos <br />
     &nbsp;&nbsp; <strong>Autenticação:</strong> Bearer token Jwt <br /><br />
  </li>
</ul>

<h4>POST</h4>

<ul>
  <li>
    <span><strong>(base_url)/sessions</strong> - Iniciar uma nova sessão de login</span> <br />
     &nbsp;&nbsp; <strong>Body:</strong> Email e senha do usuário (JSON) <br />
     &nbsp;&nbsp; <strong>Retorno:</strong> Token de autenticação (JSON) <br /><br />
  </li>
  
  <li>
    <span><strong>(base_url)/users</strong> - Cadastrar um novo usuário</span> <br />
     &nbsp;&nbsp; <strong>Body:</strong> Dados do usuário (JSON) <br />
     &nbsp;&nbsp; <strong>Retorno:</strong> Dados do usuário cadastrado (JSON) <br /><br />
  </li>
  
  <li>
    <span><strong>(base_url)/files</strong> - Realizar upload de uma nova imagem</span> <br />
     &nbsp;&nbsp; <strong>Autenticação:</strong> Bearer token Jwt <br />
     &nbsp;&nbsp; <strong>Body:</strong> Input com a imagem (Multipart Form) <br />
     &nbsp;&nbsp; <strong>Retorno:</strong> Dados da imagem cadastrada (JSON) <br /><br />
  </li>
  
  <li>
    <span><strong>(base_url)/appointments</strong> - Cadastrar um novo agendamento</span> <br />
     &nbsp;&nbsp; <strong>Autenticação:</strong> Bearer token Jwt <br />
     &nbsp;&nbsp; <strong>Body:</strong> Dados do agendamento (JSON) <br />
     &nbsp;&nbsp; <strong>Retorno:</strong> Dados do agendamento cadastrado (JSON) <br /><br />
  </li>
</ul>

<h4>PUT</h4>

<ul>
  <li>
    <span><strong>(base_url)/users</strong> - Atualizar um registro de usuário</span> <br />
     &nbsp;&nbsp; <strong>Autenticação:</strong> Bearer token Jwt <br />
     &nbsp;&nbsp; <strong>Body:</strong> Dados do usuário (JSON) <br />
     &nbsp;&nbsp; <strong>Retorno:</strong> Dados do usuário atualizado (JSON) <br /><br />
  </li>
  
  <li>
    <span><strong>(base_url)/notifications/(notification_id)</strong> - Atualizar um registro de notificação (apenas o campo "read")</span> <br />
     &nbsp;&nbsp; <strong>Route Param:</strong> <br />
     &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <strong>notification_id:</strong> ID do registro que será atualizado <br />
     &nbsp;&nbsp; <strong>Autenticação:</strong> Bearer token Jwt <br />
     &nbsp;&nbsp; <strong>Retorno:</strong> Dados da notificação atualizada (JSON) <br /><br />
  </li>
</ul>

<h4>DELETE</h4>

<ul>
  <li>
    <span><strong>(base_url)/appointments/(appointment_id)</strong> - Deletar um registro de agendamento (Cancelamento)</span> <br />
     &nbsp;&nbsp; <strong>Route Param:</strong> <br />
     &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <strong>appointment_id:</strong> ID do registro que será deletado (cancelado) <br />
     &nbsp;&nbsp; <strong>Autenticação:</strong> Bearer token Jwt <br />
     &nbsp;&nbsp; <strong>Retorno:</strong> Objeto do agendamento cancelado (JSON) <br /><br />
  </li>
</ul>
