Go is a general-purpose language designed with systems programming in mind. It is 
- strongly typed 
- garbage-collected 
- has explicit support for concurrent programming

Programs are constructed from _packages_, whose properties allow efficient management of dependencies.

The grammar is compact and simple to parse, allowing for easy analysis by automatic tools such as integrated development environments.

```mermaid
graph TD

id0(production-cluster-backend)
id6(staging-cluster-backend)

style id1 fill:#f9f
style id2 fill:#f9f
style id5 fill:#f9f

id1(cloud.ym)
id2(beta)
id3(app.ym)

id4(staging.ym)
id5(alpha.ym)

id6 --> id5 & id4
id0 --> id1 & id2 & id3
```
Each of the leaves in the graph contain bot development environments. Each bot development environment has three isolated regions -> sandbox, staging and production. 