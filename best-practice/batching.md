# Server-side Batching & Caching

> https://graphql.org/learn/best-practices/#server-side-batching-caching

> tl;dr
>
> > 다중 db/msa request를 단일 요청으로 batching 할 수 있다. ex) `Facebook DataLoader`

GraphQL is designed in a way that allows you to write clean code on the server, where every field on every type has a focused single-purpose function for resolving that value. However without additional consideration, a naive GraphQL service could be very "chatty" or repeatedly load data from your databases.

This is commonly solved by a batching technique, where multiple requests for data from a backend are collected over a short period of time and then dispatched in a single request to an underlying database or microservice by using a tool like Facebook's DataLoader.

## `Dataloader`

> https://github.com/graphql/dataloader

- 다른 언어로 이식 가능 [python graphene dataloader](https://docs.graphene-python.org/en/latest/execution/dataloader/)
-

- c.f) `Multi Tenant(다중 사용자) Service`
  - 멀티테넌시란 그 용어에서 유추할 수 있듯 여러 테넌트(tenant, 사용자)를 가진 아키텍처라는 의미입니다. 많은 사람이 같은 기능을 사용하는 웹메일 서비스가 대표적인 멀티테넌시 아키텍처 소프트웨어입니다.
