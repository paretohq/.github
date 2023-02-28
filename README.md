# What is Pareto?

Pareto is a project that aims to acheive 80/20 ratio of results/effort (the pareto distribution) in the field of web development.

Pareto is a project where you can describe (in an intuitive DSL) what your project has in terms of data and basic logic descriptions and pareto will generate at least 80% of your projects code for you.

Pareto aims to generate production ready code in **any stack**. An ambitious and certainly non-trivial goal.

With pareto, you sould be able to describe your project once and get the ability to generate production ready code in the stack of your choice. You want Laravel 10 with Nuxt 3? A React frontend with firebase backend? full-stack Next.js on vercel? Pareto has your back.

Pareto's syntax is a superset of prisma's, for example, here's how you would describe a project for a simple blog

```prisma
datasource db {
}

generator pareto {
}

enum {
  ADMIN
  EDITOR
  USER
}

model User {
  id    String @id             @default(increment())
  email String @unique         @rules(email, max:255)
  name  String @rules(max:255)
  
  @@api.ignore(create)
}

model Post {
  id        String      @id             @default(increment())
  title     String      @rules(max:255)
  slug      String      @rules(max:255) @rule.noCreate() // Not required while creating (e.g automatically generated from title)
  author_id Integer     @rules(min:1)
  author    USER        @relation()
}
```
