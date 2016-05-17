 rails new rapi --api
 
 rake middleware
 
 use Rack::Sendfile
 use ActionDispatch::Static
 use ActionDispatch::Executor
 use ActiveSupport::Cache::Strategy::LocalCache::Middleware
 use Rack::Runtime
 use ActionDispatch::RequestId
 use Rails::Rack::Logger
 use ActionDispatch::ShowExceptions
 use ActionDispatch::DebugExceptions
 use ActionDispatch::RemoteIp
 use ActionDispatch::Reloader
 use ActionDispatch::Callbacks
 use ActiveRecord::Migration::CheckPending
 use Rack::Head
 use Rack::ConditionalGet
 use Rack::ETag
 use ActionView::Digestor::PerRequestDigestCacheExpiry
 run Rapi::Application.routes
 
 The API does not have:
 
 use Rack::MethodOverride
 use WebConsole::Middleware
 use ActionDispatch::Cookies
 use ActionDispatch::Session::CookieStore
 use ActionDispatch::Flash
 
 
 application_controller.rb:
 
 class ApplicationController < ActionController::API
 end
 
 rails g scaffold article title content 
 
 gem 'active_model_serializers'
 bundle
 
 rails g serializer article
 
 class ArticleSerializer < ActiveModel::Serializer
   attributes :id, :title, :content
 end
 
 rails db:migrate
 
 seeds.rb
 
 Article.create! title: "Superman", content: "Superman is a fictional comic book superhero appearing in publications by DC Comics, widely considered to be an American cultural icon. Created by American writer Jerry Siegel and Canadian-born American artist Joe Shuster in 1932 while both were living in Cleveland, Ohio, and sold to Detective Comics, Inc."
 Article.create! title: "Krypton", content: "Krypton is a fictional planet in the DC Comics universe, and the native world of the super-heroes Superman and, in some tellings, Supergirl and Krypto the Superdog."
 Article.create! title: "Batman & Robin", content: "Batman is a fictional character created by the artist Bob Kane and writer Bill Finger. A comic book superhero, Batman first appeared in Detective Comics #27 (May 1939), and since then has appeared primarily in publications by DC Comics.)"
 
 rails s
 
 curl http://localhost:3000/articles
  
 [{"id":1,"title":"Superman","content":"Superman is a fictional comic book superhero appearing in publications by DC Comics, widely considered to be an American cultural icon. Created by American writer Jerry Siegel and Canadian-born American artist Joe Shuster in 1932 while both were living in Cleveland, Ohio, and sold to Detective Comics, Inc. (later DC Comics) in 1938, the character first appeared in Action Comics #1 (June 1938) and subsequently appeared in various radio serials, television programs, films, newspaper strips, and video games. (from Wikipedia)"},{"id":2,"title":"Krypton","content":"Krypton is a fictional planet in the DC Comics universe, and the native world of the super-heroes Superman and, in some tellings, Supergirl and Krypto the Superdog. Krypton has been portrayed consistently as having been destroyed just after Superman's flight from the planet, with exact details of its destruction varying by time period, writers and franchise. Kryptonians were the dominant people of Krypton. (from Wikipedia)"},{"id":3,"title":"Batman \u0026 Robin","content":"Batman is a fictional character created by the artist Bob Kane and writer Bill Finger. A comic book superhero, Batman first appeared in Detective Comics #27 (May 1939), and since then has appeared primarily in publications by DC Comics. Originally referred to as The Bat-Man and still referred to at times as The Batman, he is additionally known as The Caped Crusader, The Dark Knight, and the World's Greatest Detective, among other titles. (from Wikipedia)"}]
 
 def index
   @articles = Article.all

   render json: @articles
 end
 
 http://sourcey.com/building-the-prefect-rails-5-api-only-app/
 https://blog.codeship.com/building-a-json-api-with-rails-5/