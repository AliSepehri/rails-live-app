# My experiences in a live Rails application

- Idempotency for `seed files`, `rake tasks` and `background jobs`.

- Do not ignore `schema.rb` file in Git. Use `rake db:schema:load` instead of `rake db:migrate` to initialize database (for example when you clone a new project).

- Use just a single way to define environment variables in your app.

- Don’t ignore `Gemfile.lock` file.

- You need both of application layer validations and database layer constraints. For example if you’re using multi process/thread app-servers(like `unicorn`, `puma`, …) in addtion to model uniqueness validation, also define database uniqueness constraint to protect againist race condition. Read [this](https://robots.thoughtbot.com/validation-database-constraint-or-both) great article.

- As far as possible don’t use `Rails.env.production?`, `Rails.env.development?` or any same conditions in your code. Sometimes you need them in config files.

- Put your data changes in migration files. For example if you want to add a column and store concatenation of two another columns into it, in this case after creation of new column iterate all rows and update it in your new migration file (and then delete old columns). Also before goieng live, test your data migration functions with your existing live database in your development environment (if it is possible).

- Don’t bypass model validations to save specific data by `update_attribute` method or manually from database.

- After any change in validations, validate existing values stored in your database.

- Dockerfile is the best runnable documentation for your app. Even if you don't use docker to deploy your application write a Dockerfile.

- Use [gitflow](https://datasift.github.io/gitflow/IntroducingGitFlow.html) branching model (master, develop, release/*, feature/*, hotfix/*).

- Use Continuous Integration, at least to run your tests.

- Use error monitoring systems (like [errbit](https://github.com/errbit/errbit)).