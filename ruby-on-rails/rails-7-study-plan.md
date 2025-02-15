# Rails 7 Study List

## 1. **Rails Basics**

- [x] Install Ruby, Rails, and Database (PostgreSQL, MySQL, etc.)
- [x] Learn Rails Directory Structure
- [x] Understanding MVC (Model-View-Controller)
- [x] Creating a New Rails Application
- [x] Basic CRUD operations (Create, Read, Update, Delete)

## 2. **Rails Models**

- [x] ActiveRecord Basics
- rails-active-record.md
- [x] Validations
- rails-active-record.md
- [x] Associations (has_many, belongs_to, has_one, etc.)
- rails-active-record.md
- [x] Scopes -
- rails-active-record.md
- [x] Migrations and Schema Changes
- rails-active-record.md

## 3. **Rails Views**

- [x] Using Embedded Ruby (ERB) Templates
- [x] Layouts and Partials
- [ ] Helper Methods
- [ ] Rendering JSON Responses
- [ ] Turbo and Hotwire Basics

## 4. **Rails Controllers**

- [x] Understanding Controllers
- [ ] RESTful Routes
- [x] Action Methods (index, show, new, create, edit, update, destroy)
- [ ] Redirects and Renders
- [ ] Strong Parameters

## 5. **Authentication and Authorization**

- [ ] Implementing User Authentication (Devise or custom solution)
- [ ] **JWT Authentication** (Implementing token-based authentication for APIs)
      https://www.youtube.com/watch?v=MWuRHY5XF40&list=PL6SEI86zExmvGeaquocN_umlbhJVhijqG
- [ ] Authorization with Pundit or CanCanCan
- [ ] Role-based Access Control (RBAC)

## 6. **Testing**

- [ ] Unit Tests with RSpec or Minitest
- [ ] Request Specs
- [ ] Integration Tests
- [ ] Test Coverage with SimpleCov
- [ ] Test-driven Development (TDD)

## 7. **Routing and URL Generation**

- [ ] Rails Routing: Understanding `resources`, `member`, `collection`, and custom routes
- [ ] Path Helpers: Generating paths with helper methods
- [ ] Nested Routes: Working with nested resources and URLs
- [ ] Named Routes: Using `as:` for custom URL names

## 8. **Background Jobs**

- [ ] ActiveJob: Understanding Rails' background job system
- [ ] Sidekiq: Using Sidekiq for real-time job processing
- [ ] Job Queues: Understanding how to manage and scale job processing
- [ ] Job Scheduling: Scheduling tasks with tools like `whenever` or `sidekiq-scheduler`

## 9. **Action Cable (Real-time Features)**

- [ ] WebSockets: Understanding how WebSockets work in Rails
- [ ] Action Cable: Setting up channels for real-time data updates
- [ ] Streaming: Sending updates to clients in real time (e.g., chat apps, live feeds)

## 10. **Front-End Integration**

- [ ] Turbo: Using Turbo for optimizing page loads and navigation
- [ ] Stimulus: Enhancing pages with minimal JavaScript using Stimulus controllers
- [ ] Webpacker: Managing JavaScript, CSS, and other assets with Webpack
- [ ] Tailwind CSS: Using Tailwind CSS for utility-first styling in Rails apps
- [ ] Hotwire: Building real-time, fast applications with Turbo + Stimulus

## 11. **ActiveStorage**

- [ ] File Uploads: Handling file uploads and attachments (images, PDFs, etc.)
- [ ] Service Backends: Using cloud storage (AWS S3, Google Cloud Storage) with ActiveStorage
- [ ] Variant Generation: Creating image variants for different resolutions and sizes

## 12. **Action Mailer**

- [ ] Email Setup: Sending emails from your Rails app with ActionMailer
- [ ] HTML and Plain-text Emails: Creating both HTML and text-based email templates
- [ ] Email Preview: Previewing emails in the development environment
- [ ] Attachments: Sending file attachments via email

## 13. **Caching**

- [ ] Page Caching: Caching entire pages for better performance
- [ ] Action Caching: Caching controller actions for faster responses
- [ ] Fragment Caching: Caching partials to reduce load times
- [ ] Low-level Caching: Using Rails cache store (e.g., Memcached, Redis) for complex objects

## 14. **Localization and Internationalization (i18n)**

- [ ] Rails Localization: Setting up `config/locales` for translations
- [ ] Dynamic Translations: Using translation helpers (`t`) in views and controllers
- [ ] Pluralization and Gender Handling: Managing plural and gendered words in translations
- [ ] Locale Switching: Allowing users to change their locale dynamically

## 15. **Performance Optimization**

- [ ] Query Optimization: Using `EXPLAIN` to analyze slow queries
- [ ] Database Indexing: Creating and managing indexes for faster queries
- [ ] Eager Loading: Avoiding N+1 query problems with `includes` and `joins`
- [ ] Caching Strategies: Using caching at various levels (page, action, fragment, low-level)

## 16. **Deployment**

- [ ] Capistrano: Deploying Rails applications using Capistrano
- [ ] Heroku: Deploying and managing Rails apps on Heroku
- [ ] Docker: Containerizing Rails apps using Docker
- [ ] CI/CD: Setting up Continuous Integration and Continuous Deployment pipelines (e.g., GitHub Actions, CircleCI)

## 17. **Other Tools**

- [ ] Rails Console: Mastering Rails' interactive console for debugging and testing
- [ ] Rails Debugging: Using `byebug` and `pry` for debugging code
- [ ] Database Schema: Understanding and managing your database schema with `db:schema`
- [ ] Ruby Gems: Using popular gems like `Devise`, `Kaminari`, `Pundit`, `Sidekiq`, etc.

## Useful Gems

gem 'rack-mini-profiler'

## Gem from this project

gem 'rails-ujs'
gem 'toastr-rails'
gem 'kaminari'
https://github.com/kaminari/kaminari
gem 'faker'
gem 'kaminari-bootstrap', '~> 4.0.0'
