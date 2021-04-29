# Credence API

API to store and retrieve confidential development files (configuration, credentials)

## Vulnerabilities

This branch (1_demo_db_vulnerabilities) allows mass assignment and SQL injection. It does not prevent the above attacks and loosens some of Roda's built-in precautions for demonstration purposes.

### Mass assignment

Conduct mass assignment via POST request:

```ruby
$ rake console
# type these within console:
req_header = { 'CONTENT_TYPE' => 'application/json' }
req_body = { name: 'Bad Date', created_at: '1900-01-01' }.to_json
post '/api/v1/projects', req_body, req_header
```

Conduct mass assignment in code:

```ruby
Credence::Project.create(
  name: 'Future Project',
  repo_url: 'http://github.com/fakeproject',
  created_at: Time.new(1900, 01, 01)
)
```

### SQL Injection

Conduct SQL injection via GET request vector:

```bash
http GET http://localhost:9292/api/v1/projects/2%20or%20id%3D1
```

Intent of attack is to cause code using naked SQL code to execute a maninpulated SQL query as follows:

```ruby
app.DB['SELECT * FROM projects WHERE id=2 or id=1'].all.to_json
```

## Routes

All routes return Json

- GET  `/`: Root route shows if Web API is running
- GET  `api/v1/projects/[proj_id]/documents/[doc_id]`: Get a document
- GET  `api/v1/projects/[proj_id]/documents`: Get list of documents for project
- POST `api/v1/projects/[ID]/documents`: Upload document for a project
- GET  `api/v1/projects/[ID]`: Get information about a project
- GET  `api/v1/projects`: Get list of all projects
- POST `api/v1/projects`: Create new project

## Install

Install this API by cloning the *relevant branch* and use bundler to install specified gems from `Gemfile.lock`:

```shell
bundle install
```

Setup development database once:

```shell
rake db:migrate
```

## Execute

Run this API using:

```shell
puma
```

## Test

Setup test database once:

```shell
RACK_ENV=test rake db:migrate
```

Run the test specification script in `Rakefile`:

```shell
rake spec
```

## Release check

Before submitting pull requests, please check if specs, style, and dependency audits pass:

```shell
rake release?
```