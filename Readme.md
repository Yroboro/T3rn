## 1: Создаем приложение React
Вводим следующие команды:
```
npx create-react-app timegraph-app
cd timegraph-app
```
## 2: Устанавливаем необходимые пакеты
```
npm install @polkadot/extension-dapp @analog-labs/timegraph-js dotenv
```
## 3: Создаем a .env файл
заменяем в командной строке `your-session-key-here` на свой сессионный ключ. Его ранее копирывали в ваш профиле на сайте ANALOG Watch:
```
REACT_APP_SESSION_KEY=your-session-key-here
```
## 4: Настраиваем приложение React 
В папке src меняем код в файле App.js `src/App.js` на код указанный ниже
```javascript
import React, { useEffect, useState } from "react";
import { TimegraphClient } from "@analog-labs/timegraph-js";
import { web3Enable } from "@polkadot/extension-dapp";

const sessionKey = process.env.REACT_APP_SESSION_KEY;
const timegraphGraphqlUrl = "https://timegraph.testnet.analog.one/graphql";

async function watchSDKTesting(setData, setAliasResponse, name, hashId) {
  await web3Enable("abcd");

  const client = new TimegraphClient({
    url: timegraphGraphqlUrl,
    sessionKey: sessionKey, 
  });

  let aliasResponse = await client.alias.add({
    name: name,
    hashId: hashId,
    identifier: name,
  });

  console.log(aliasResponse);
  setAliasResponse(aliasResponse); 

  const data = await client.view.data({
    _name: name, 
    hashId: hashId, 
    fields: ["_index"],
    limit: 10,
  });

  setData(data);
}

function App() {
  const [data, setData] = useState(null);
  const [aliasResponse, setAliasResponse] = useState(null); 
  const [name, setName] = useState("");
  const [hashId, setHashId] = useState("");

  const handleSubmit = (e) => {
    e.preventDefault(); 
    watchSDKTesting(setData, setAliasResponse, name, hashId);
  };

  return (
    <div>
      <h1>Timegraph Data</h1>
      
      <form onSubmit={handleSubmit}>
        <div>
          <label>
            Name:
            <input
              type="text"
              value={name}
              onChange={(e) => setName(e.target.value)}
              required
            />
          </label>
        </div>
        <div>
          <label>
            Hash ID:
            <input
              type="text"
              value={hashId}
              onChange={(e) => setHashId(e.target.value)}
              required
            />
          </label>
        </div>
        <button type="submit">Submit</button>
      </form>

      
      {aliasResponse && (
        <div>
          <h2>Alias Response</h2>
          <pre>{JSON.stringify(aliasResponse, null, 2)}</pre>
        </div>
      )}

      {data ? (
        <div>
          <h2>Timegraph Data</h2>
          <pre>{JSON.stringify(data, null, 2)}</pre>
        </div>
      ) : (
        <p>Loading data...</p>
      )}
    </div>
  );
}

export default App;
```
## 5: Запускаем приложение
```
npm start
```
## 6: Доступ к приложению для запуска кода
Если все выполнено верно, вы перейдете в веб версию приложения где будете указывать name view и hash которые возьмете в дискорде в разделе POST YOUR VIEW HERE.
Проверка завершена. Получаем 15 Поинтов.
