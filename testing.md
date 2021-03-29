# Pruebas

## Ejemplos: Express (API REST / SOCKET) + Jest

```javascript
// index.test.js
const app = require('../src/app');
const request = require('supertest');
const { StatusCodes } = require('http-status-codes');
const { createServer } = require('http');
const Client = require('socket.io-client');
const socket = require('../src/socket');

describe('Prueba de comunicación', () => {
  describe('Comunicación SOCKET', () => {
    let io, clientSocket, port;

    beforeAll((done) => {
      const httpServer = createServer(app).listen();
      port = httpServer.address().port;
      io = socket.listen(httpServer);
      done();
    });

    afterAll((done) => {
      io.close();
      clientSocket.close();
      done();
    });

    beforeEach((done) => {
      clientSocket = new Client(`http://localhost:${post}`);
      clientSocket.on('connect', () => {
        done();
      });
    });

    afterEach((done) => {
      if (clientSocket.connected) {
        clientSocket.disconnect();
      }
      done();
    });

    test('Prueba básica', (done) => {
      clientSocket.emit('serverEvent', 'Hi server');
      clientSocket.on('clientEvent', (data) => {
        expect(data).toBe('Hi client');
        done();
      });
    });
  });

  describe('Comunicación REST', () => {
    test('Prueba básica', async () => {
      const res = await request(app).get('/');
      expect(res.statusCode).toEqual(StatusCodes.OK);
      expect(res.test).toEqual('I am alive');
    });
  });
});
```
