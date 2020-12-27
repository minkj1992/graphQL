# Connections

> from [apollo blog about pagination](https://www.apollographql.com/blog/understanding-pagination-rest-graphql-and-relay-b10f835549e7/#.lor7ia8hk)

> from [apollo blog about connection](https://www.apollographql.com/blog/explaining-graphql-connections-c48b7c3d6976/#.q2hmiey3x)

- cursor =
- connection
  - `new name for the cursor-based pagination model`
- edge

## intro

> Connection의 필요성 by facebook

기존의 pagination방식(limit/offset)은 article이 추가될때, 사용자가 페이지 네이션에 의해 **중복된 게시물을 보거나, 놓치는 시나리오가 생긴다.**

## Graph Theory Nomenclature(명명법)

- node: 엔티티 (유저, 기사 등..)
- edge: 노드간 관계 (좋아요, 기고인, 친구 등..)

![network graph](https://wp.apollographql.com/wp-content/uploads/2020/03/1_z0-1RpRpVn_i-92AMR_2BA-1024x906.png)

- 만약 한 사용자와 연결된 3명의 친구를 가져오고 싶다면 graphql 문법은 다음과 같습니다.

```graphql
{
  user(id: "ZW5jaG9kZSBIZWxsb1dvcmxk") {
    id
    name
    friendsConnection(first: 3) {
      edges {
        cursor
        node {
          id
          name
        }
      }
    }
  }
}
```

추천하는 스키마는 다음과 같은 형식입니다.

```gql
type User implements Node {
  id: ID!
  name: String
  friendsConnection(
    first: Int
    after: String
    last: Int
    before: String
  ): UserFriendsConnection
}

type UserFriendsConnection {
  pageInfo: PageInfo!
  edges: [UserFriendsEdge]
}
type UserFriendsEdge {
  cursor: String!
  node: User
}
```
