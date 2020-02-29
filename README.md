<h1>Go Barber - Backend</h1>

<p>
  Backend da aplicação usada como base durante o Bootcamp GoStack 2020.
</p>
<p>
  Trata-se de uma aplicação para barbearias/salões de beleza, onde é possível o gerenciamento da agenda de horário por meio de 
  agendamentos/cancelamentos feitos pelos clientes.
</p>

<h3>Começando</h3>

<p>Configurar as variáveis ambientes (listadas no arquivo ".env.example").</p>

<p>Instalar as dependências</p>

```sh
yarn install
```

<p>Executar a aplicação</p>

```sh
yarn dev
```

<p>Executar o servidor de <i>jobs</i> em <i>background</i></p>

```sh
yarn qeue
```

<h3>Objetos</h3>

<ul>
  <li>
    <h4>Usuários</h4>
    &nbsp; name: String <br />
    &nbsp; email: String <br />
    &nbsp; password: String <br />
    &nbsp; provider: Boolean <br />
    &nbsp; avatar_id: Number
  </li>
  
  <li>
    <h4>Agendamentos</h4>
    &nbsp; user_id: Number <br />
    &nbsp; provider_id: Number <br />
    &nbsp; date: Date <br />
    &nbsp; canceled_at: Date
  </li>
  
  <li>
    <h4>Notificações</h4>
    &nbsp; user: Number <br />
    &nbsp; content: String <br />
    &nbsp; read: Boolean
  </li>
</ul>

<h3>Rotas</h3>

<ul>
  <li>
    <h5>Sessão</h5>
    <table>
      <thead>
        <th>Método</th>
        <th>URL</th>
        <th>Autenticação</th>
        <th>Corpo da Req.</th>
        <th>Retorno</th>
      </thead>
      <tbody>
        <tr>
          <td>POST</td>
          <td>(base_url)/sessions</td>
          <td></td>
          <td>Email e senha do usuário que iniciará a sessão</td>
          <td>Objeto contendo token de autenticação</td>
        </tr>
      </tbody>
    </table>
  </li>
  
  <li>
    <h5>Usuários</h5>
    <table>
      <thead>
        <th>Método</th>
        <th>URL</th>
        <th>Autenticação</th>
        <th>Corpo da Req.</th>
        <th>Retorno</th>
      </thead>
      <tbody>
        <tr>
          <td>POST</td>
          <td>(base_url)/users</td>
          <td></td>
          <td>Objeto de usuário</td>
          <td>Objeto do usuário cadastrado</td>
        </tr>
        <tr>
          <td>PUT</td>
          <td>(base_url)/users</td>
          <td>(Bearer) token Jwt</td>
          <td>Objeto de usuário</td>
          <td>Objeto do usuário atualizado</td>
        </tr>
      </tbody>
    </table>
  </li>
  
  <li>
    <h5>Arquivos</h5>
    <table>
      <thead>
        <th>Método</th>
        <th>URL</th>
        <th>Autenticação</th>
        <th>Corpo da Req.</th>
        <th>Retorno</th>
      </thead>
      <tbody>
        <tr>
          <td>POST</td>
          <td>(base_url)/files</td>
          <td>(Bearer) token Jwt</td>
          <td><i>Multipart Form</i> contendo o campo de imagem (nome: file)</td>
          <td>Objeto do arquivo cadastrado</td>
        </tr>
      </tbody>
    </table>
  </li>
  
  <li>
    <h5>Provedores</h5>
    <table>
      <thead>
        <th>Método</th>
        <th>URL</th>
        <th>Autenticação</th>
        <th>Corpo da Req.</th>
        <th>Retorno</th>
      </thead>
      <tbody>
        <tr>
          <td>GET</td>
          <td>(base_url)/providers</td>
          <td>(Bearer) token Jwt</td>
          <td></td>
          <td>Lista de provedores de serviço</td>
        </tr>
        <tr>
          <td>GET</td>
          <td>(base_url)/providers/(provider_id)/avaliable</td>
          <td>(Bearer) token Jwt</td>
          <td></td>
          <td>Lista de todos os horários do dia, para o provedor informado</td>
        </tr>
      </tbody>
    </table>
  </li>
  
  <li>
    <h5>Agendamentos</h5>
    <table>
      <thead>
        <th>Método</th>
        <th>URL</th>
        <th>Autenticação</th>
        <th>Corpo da Req.</th>
        <th>Retorno</th>
      </thead>
      <tbody>
        <tr>
          <td>GET</td>
          <td>(base_url)/appointments</td>
          <td>(Bearer) token Jwt</td>
          <td></td>
          <td>Lista de todos os agendamentos do usuário logado</td>
        </tr>
        <tr>
          <td>POST</td>
          <td>(base_url)/appointments</td>
          <td>(Bearer) token Jwt</td>
          <td>Objeto de agendamento</td>
          <td>Objeto do agendamento cadastrado</td>
        </tr>
        <tr>
          <td>DELETE</td>
          <td>(base_url)/appointments/(appointment_id)</td>
          <td>(Bearer) token Jwt</td>
          <td></td>
          <td>Objeto do agendamento deletado (atualiza o campo "canceled_at")</td>
        </tr>
      </tbody>
    </table>
  </li>
  
  <li>
    <h5>Notificações</h5>
    <table>
      <thead>
        <th>Método</th>
        <th>URL</th>
        <th>Autenticação</th>
        <th>Corpo da Req.</th>
        <th>Retorno</th>
      </thead>
      <tbody>
        <tr>
          <td>GET</td>
          <td>(base_url)/notifications</td>
          <td>(Bearer) token Jwt</td>
          <td></td>
          <td>Lista de notificações de novos agendamentos, para o provedor logado</td>
        </tr>
        <tr>
          <td>PUT</td>
          <td>(base_url)/notifications/(notification_id)</td>
          <td>(Bearer) token Jwt</td>
          <td></td>
          <td>Objeto da notificação atualizada (atualiza o campo "read")</td>
        </tr>
      </tbody>
    </table>
  </li>
  
  <li>
    <h5>Agenda</h5>
    <table>
      <thead>
        <th>Método</th>
        <th>URL</th>
        <th>Autenticação</th>
        <th>Corpo da Req.</th>
        <th>Retorno</th>
      </thead>
      <tbody>
        <tr>
          <td>GET</td>
          <td>(base_url)/schedules?date=(date)</td>
          <td>(Bearer) token Jwt</td>
          <td></td>
          <td>Lista de agendamentos do dia (informado na url), para o provedor logado</td>
        </tr>
      </tbody>
    </table>
  </li>
</ul>

