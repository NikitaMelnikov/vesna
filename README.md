```scala
transaction { implicit tx =>
  from(User) { u => 
    join(Client) { c =>
      select(u.name, u.email)
      .where(u.name like "%name%")
      .forUpdate
    }
  } 
} : IO[Select[User :: Client :: HNil], Effect.Read :: Effect.Transaction :: Effect.Lock :: HNil]
```
