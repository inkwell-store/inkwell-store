# Seeding database with Open Library's data

## Context

An e-commerce application needs products to work with. In this case, I need to find a way to generate data for books that user can browse and order. This catalog can generated in a number of ways. In truth any amount of books is enough to perform certain tasks, such as place or cancel an order, emit a receipt etc.

## Options considered

1. Create manually (or with the use of tool) a few entries for books.
2. Use a real database, like Open library or Project Gutemberg's.

## Decision

This project has already many constraints placed upon it, and making a realistic dataset is something I really want to do it. I belive it will make the application closer to a real one and provide a better user experience.

In addition to that, a big database like open library's contains many relevant information about books, editions and authors. At the same time it is a good opportunity to work with a big bulk of data, by processing and normalizing it to a my own database schema.  

## Consequences

* The application will have a somewhat realistic dataset.
* Because it will be normalized into my own database schema importing another dataset or updating the records is going to be straightforward.
* Open library's dataset is massive. I need to be careful as not to produce a database so large where docker hub might block it.
