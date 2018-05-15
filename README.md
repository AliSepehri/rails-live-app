# My experiences in a live Rails application

1. Idempotency for `seed files`, `rake tasks` and `background jobs`.

1. Do not ignore `schema.rb` file in Git. Use `rake db:schema:load` instead of `rake db:migrate` to initialize database (for example when you clone a new project).

1. Use just a single way to define environment variables in your app.

1. Don’t ignore `Gemfile.lock` file.

1. You need both of application layer validations and database layer constraints. For example if you’re using multi process/thread app-servers(like `unicorn`, `puma`, …) in addtion to model uniqueness validation, also define database uniqueness constraint to protect againist race condition. Read [this](https://robots.thoughtbot.com/validation-database-constraint-or-both) great article.

1. As far as possible don’t use `Rails.env.production?`, `Rails.env.development?` or any same conditions in your code. Sometimes you need them in config files.

1. Put your data changes in migration files. For example if you want to add a column and store concatenation of two another columns into it, in this case after creation of new column iterate all rows and update it in your new migration file (and then delete old columns). Also before goieng live, test your data migration functions with your existing live database in your development environment (if it is possible).

1. Don’t bypass model validations to save specific data by `update_attribute` method or manually from database.

1. After any change in validations, validate existing values stored in your database.

1. Dockerfile is the best runnable documentation for your app. Even if you don't use docker to deploy your application write a Dockerfile.

1. Use [gitflow](https://datasift.github.io/gitflow/IntroducingGitFlow.html) branching model (master, develop, release/*, feature/*, hotfix/*).

1. Use Continuous Integration, at least to run your tests.

1. Use error monitoring systems (like [errbit](https://github.com/errbit/errbit)).

1. If you care about timezone, do not use `Date` or `Time` data types instead of `DateTime` for your database columns.
