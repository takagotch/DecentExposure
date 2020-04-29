### DecentExposure decent_exposure
---

https://github.com/hashrocket/decent_exposure

```
gem 'decent_exposure', '3.0.0'
bundle
gem install decent_exposure


rails g generate scaffold post title description:text
```

```ruby
class ThingsController < ApplicationController
  expose :thing
end

class ThingsController < ApplicationController
  expose :things, ->{ Thing.all }
  expose :thing
  def create
    if thing.save
      redirect_to thing_path(thing)
    else
      render :new
    end
  end
  def update
    if thing.update(thing_params)
      redirect_to thing_path(thing)
    else
      render :edit
    end
  end
  def destroy
    thing.destroy
    redirect_to things_path
  end
  private
  def thing_params
    params.require(:thing).permit(:foo, :bar)
  end
end


def fetch(scope, id)
  instance = id ? find(id, scope) : build(build_params, scope)
  decorate(instance)
end
def id
  params[:thing_id] || params[:id]
end
def find(id, scope)
  scope.find(id)
end
def build(params, scope)
  scope.new(params) # Thing.new(params)
end
def scope
  model # Thing
end
def model
  exposure_name.classify.constantize # :thing -> Thing
end
def build_params
  if respond_to?(:thing_params, true) && !request.get?
    thing_params
  else
    {}
  end
end
def decorate(thing)
  thing
end


expose :thing, fetch: ->{ get_thing_some_way_or_another }
expose(:thing){ get_thing_some_way_or_another   }
expose :thing, ->{ get_thing_some_way_or_another }
expose :thing, :get_thing_some_way_or_another
expose :comment, from: :post
expose :comments, ->{ post.comments }
expose :thing, id: ->{ params[:thing_id] || params[:id] }
expose :thing, id: ->{ 43 }
expose :thing, id: :custom_thing_id
expose :thing, id: ->{ params[:custom_thing_id] }
expose :thing, id: [:try_this_id, :or_maybe_that_id]
expose :thing, id: ->{ params[:try_this_id] || params[:or_maybe_that_id] }
expose :thing, find: ->(id, scope){ scope.find(id) }
expose :thing, find: ->(id, scope){ scope.find_by!(slug: id) }
expose :thing, find_by: :slug
expose :thing, build: ->(thing_params, scope){ scope.new(thing_params) }
expose :thing, build_params: :custom_thing_params
expose :other_thing, build_params: ->{ { foo: "bar" } }
private
def custom_thing_params
end
expose :thing, scope: ->{ current_user.things }
expose :user, scope: ->{ User.active }
expose :post, scope: ->{ Post.published }
expose :post, scope: :published
expose :post, scope: ->{ Post.published }
expose :thing, parent: :current_user
expose :thing, scope: ->{ current_user.things }
expose :thing, model: ->{ AnotherThing }
expose :thing, model: AnotherThing
expose :thing, model: "AnotherThing"
expose :thing, model: :another_thing
expose :thing, ->{ Thing.all.map{ |thing| ThingDecorator.new(thing) } }
expose :thing, decorate: ->(thing){ ThingDecorator.new(thing) }
exposure_config :cool_find, find: ->{ very_cool_find_code }
exposure_config :cool_build, build: ->{ very_cool_build_code }
expose :thing, with: [:cool_find, :cool_build]
expose :another_things, with: :cool_build

class PostMailer < ApplicationMailer
  expose(:posts, -> { Post.last(10) })
  expose(:post)
  def top_posts
    @greeting = "Top Posts"
    mail to: "to@ex.org"
  end
  def featured_post(id:)
    @greeting = "Featured Post"
    mail to: "to@ex.org"
  en00d
end


config/appliaction.rb
config.generators do |g|
  g.template_engine :erb
end

```

```
```
