# NAB-Challenge 

[Live version](https://nab-challenge.lehongnam.com/).

## Architecture
From the architectural point-of-view the online store can be seen as a composition of 2 
independent services: the products service and the gateway service. The first one is responsible 
for storage and management of the products while the second simply receives user´s requests and 
conveys them to the products service.

To ensure that our system is resilient to failures we will run the products and 
the gateway services in dedicated nodes (node-1 and node-2). If you recall, running 
services at dedicated nodes means that the transporter module is required for inter 
services communication. Most of the transporters supported by Moleculer rely on a 
message broker for inter services communication, so we’re going to need one 
up and running. Overall, the internal architecture of our store is represented in the figure below.

**Flow of user’s request**
![user flow](https://2.pik.vn/2020cd679e01-f369-43df-aa4d-62f269a738d4.jpg)

## Folder structure
![Folder structure](https://2.pik.vn/20201f9c91d8-802d-4c4b-a663-830d3f2a403c.png)

## Clustering
This project supports several software architectures.

### Monolith architecture
In this version, all services are running on the same node like a monolith. There is no network 
latency and no transporter module. The local calls are the fastest. 
Deploy example at `docker-compose-monolith.yml`.

![Monolith](https://2.pik.vn/20201131a4d3-1687-43c4-8ce3-1122a1742a21.jpg)

### Microservices architecture
This is the well-known microservices architecture when all services are running on individual 
nodes and communicate via transporter. In this case, the network latency is not negligible. 
However, your services can be scaled to be resilient and fault-tolerant. 
Deploy example at `docker-compose-microservices.yml`.

![Microservices](https://2.pik.vn/2020be82dda6-51c9-4343-81f2-ef3643e7b535.jpg)

### Mixed architecture
In this case, we are running coherent services in a group on the same node. It combines 
the advantages of monolith and microservices architectures. For example, if the products 
service calls the analytics service multiple times, put them to the same node, so that the 
network latency between these services is cut down. If the node is overloaded, just scale it up.
Deploy example at `docker-compose-mixed.yml`.

![Mixed](https://2.pik.vn/20201ea5778b-56c5-463e-b94e-5e46ebf4016e.jpg)

## Some notable features
- Promise-based solution (async/await compatible)
- request-reply concept
- support event driven architecture with balancing
- load balanced requests & events (round-robin, random, cpu-usage, latency, sharding)
- many fault tolerance features (Circuit Breaker, Bulkhead, Retry, Timeout, Fallback)
- plugin/middleware system
- support versioned services
- service mixins
- caching solution (Memory, Redis)
- pluggable loggers (Console, File, Pino, Bunyan, Winston, Debug, Datadog, Log4js)
- pluggable transporters (TCP, NATS, MQTT, Redis, NATS Streaming, Kafka, AMQP 0.9, AMQP 1.0)
- pluggable serializers (JSON, Avro, MsgPack, Protocol Buffer, Thrift)
- pluggable parameter validator
- multiple services on a node/server
- master-less architecture, all nodes are equal
- unit test
- CI/CD with github and docker

## Usage
Start the project with `npm run dev` command. 
After starting, open the http://localhost:3000/ URL in your browser. 
On the welcome page you can test the generated services via API Gateway and check the nodes & services.

In the terminal, try the following commands:
- `nodes` - List all connected nodes.
- `actions` - List all registered service actions.
- `call greeter.hello` - Call the `greeter.hello` action.
- `call greeter.welcome --name John` - Call the `greeter.welcome` action with the `name` parameter.
- `call products.list` - List the products (call the `products.list` action).


## Services
- **api**: API Gateway services
- **greeter**: Sample service with `hello` and `welcome` actions.
- **products**: Sample DB service to hold products information.
- **analytics**: Sample DB service to track user behavior for sale and future purpose.

## Mixins
- **db.mixin**: Database access mixin for services. 

## Useful links

* Moleculer website: https://moleculer.services/
* Moleculer Documentation: https://moleculer.services/docs/0.14/

## NPM scripts

- `npm run dev`: Start development mode (load all services locally with hot-reload & REPL)
- `npm run start`: Start production mode (set `SERVICES` env variable to load certain services)
- `npm run cli`: Start a CLI and connect to production. Don't forget to set production namespace with `--ns` argument in script
- `npm run lint`: Run ESLint
- `npm run ci`: Run continuous test mode with watching
- `npm test`: Run tests & generate coverage report
- `npm run dc:up`: Start the stack with Docker Compose
- `npm run dc:down`: Stop the stack with Docker Compose


## Disclaimer and Conclusion
I also don't create Entity relationship diagram because simplicity of project and in favor of NoSQL/MongoDB.

CURL no longer needed because I already implemented (not-so-much) playful web client.
![web](https://2.pik.vn/20200bf09edc-4f52-4d4f-9752-29d92ae7c5a2.jpg)

In this project I don't have chance to show-off my coding skill or rather my coding convention much, 
so you can take a look at some solutions I created long time ago on CheckIO. It isn't much, but it can show how "functional" I am.
[https://js.checkio.org/user/namle1412/solutions/share/daa21baf2c65729833dcf8fcfe81c47e/](https://js.checkio.org/user/namle1412/solutions/share/daa21baf2c65729833dcf8fcfe81c47e/)
