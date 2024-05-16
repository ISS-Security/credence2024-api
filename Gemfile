# frozen_string_literal: true

source 'https://rubygems.org'

# Web API
gem 'json'
gem 'puma', '~>6.1'
gem 'roda', '~>3.1'

# Configuration
gem 'figaro', '~>1.2'
gem 'rake', '~>13.0'

# Security
gem 'bundler-audit'
gem 'rbnacl', '~>7.1'

# Database
gem 'hirb', '~>0.7'
gem 'sequel', '~>5.67'

# Encoding
gem 'base64', '~>0.2'

# Testing
group :test do
  gem 'minitest'
  gem 'minitest-rg'
end

# Development
group :development do
  # debugging
  gem 'pry'
  gem 'rerun'
  
  # Quality
  gem 'rubocop'

  # Performance
  gem 'rubocop-performance'
end

group :development, :test do
  # API testing
  gem 'rack-test'

  # Database
  gem 'sequel-seed'
  gem 'sqlite3', '~>1.6'
end
