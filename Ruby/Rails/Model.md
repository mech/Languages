# Rails Model

* [7 Design Patterns to Refactor MVC Components in Rails](https://www.sitepoint.com/7-design-patterns-to-refactor-mvc-components-in-rails/)
* [7 Patterns to Refactor Fat ActiveRecord Models](http://blog.codeclimate.com/blog/2012/10/17/7-ways-to-decompose-fat-activerecord-models/)
* [Rails Database Practices](http://blog.carbonfive.com/2016/11/16/rails-database-best-practices/)
* [Gourmet Service Objects](http://brewhouse.io/blog/2014/04/30/gourmet-service-objects.html)
* [Service objects in Rails will help you design clean and maintainable code. Here's how.](https://www.netguru.co/blog/service-objects-in-rails-will-help)
* [The World Needs Another Post About Dependency Injection in Ruby](http://solnic.eu/2013/12/17/the-world-needs-another-post-about-dependency-injection-in-ruby.html)
* [Testing Network Services in Ruby Is Easier Than You Think](http://www.justinweiss.com/articles/testing-network-services-in-ruby//)
* [Composition by James Dabbs](https://www.youtube.com/watch?v=zwo7ZTHS8Wg)

---

1. Service Object
2. Form Object
3. Value object
4. Query Object
5. View Object
6. Policy Object
7. Decorator

## Service Object

> Service layers are all about verbs.

* Define application boundary that establishes a set of available operations.
* Encapsulate cross-cutting operations. Involves several models.
* Encapsulate a single process of the business logic. Describe one business rule only.
* Is functional, don't store any states. Services get input and produce output.

In Rails, controller is the boundary we want to separate. Service Object is the bridge between controller boundary and domain object. Controller's `params` acts as input and Service Object's output determine result (`render` or `redirect`).

```ruby
def create
  form = TimesheetService::Form.new(params)
  
  # Form object can quickly bailout if it is not even valid
  if form.valid?
    result = TimesheetService::Save.new(form)
    # result = TimesheetService.save(self)
    
    # Result is the next deeper level of bailout when
    # contract with third-party service
    result.success? ? render_ok(result) : render_error(result)
  else
    render_error(form)
  end
rescue ServiceError => e
  Audit::Exceptional.error(e)
end
```

Most Services use the `call()` so you can use a closure as well.

## Form Object

* [18 Con-Struct Attributes Gems](http://idiosyncratic-ruby.com/18-con-struct-attributes.html)
* [Form Objects with Virtus](http://hawkins.io/2014/01/form_objects_with_virtus/)
* [Creating Form Objects with ActiveModel and Virtus](https://webuild.envato.com/blog/creating-form-objects-with-activemodel-and-virtus/)

Encapsulate logic related to validating and persisting data.

You can move validation to Form Object, but your model still need it just in case.

> So this isn't a SRP violation, they are two different responsibilities and relate to different chapters in the lifecycle of information.

## Value Object

Simple, small object that represents certain value-ness instead of an identity. Examples are money values in various currencies, temperatures, etc.

Conversion and comparison of values is one of the function Value object can perform reliably.

Anytime you need to do immutable conversion or comparison, you can consider encapsulate those logics into Value object.

```ruby
class Temperature
  include Comparable
  SCALES = %w(:kelvin :celsius)
  
  attr_reader :degrees, :scale, :kelvin_degrees
  
  def initialize(degrees, scale = :kelvin)
    @degrees = degrees.to_f
    @scale = case scale
    when *SCALES then scale
    else :kelvin
    end
    
    @kelvin_degrees = case @scale
    when :kelvin
      @degrees
    when :celsius
      @degrees + 273.15
    end
  end
  
  def self.from_celsius(degrees)
    new(degrees, :celsius)
  end
  
  def self.from_kelvin(degrees)
    new(degrees, :kelvin)
  end
  
  def <=>(other)
    kelvin_degrees <=> other.kelvin_degrees
  end
end
```

## Query Object

As much as possible use ActiveRecord scopes or class methods to generate query. Do not do the query inside controller.

> I find that scopes are best used when they're simple and don't do too much. I think of them as reusable building blocks. If I need to do something more complicated, I used a Query class to encapsulate the potentially gnarly query.

```ruby
class VolunteersNotMemberQuery
  def initialize(year:)
    @year = year
  end
  
  def relation
    volunteer_ids = GroupMembership.select(:person_id).school_year(@year)
    pta_member_ids = PtaMembership.select(:person_id).school_year(@year)
    
    Person
      .active
      .adults
      .where(id: volunteer_ids) # Will become sub-query
      .where.not(id: pta_member_ids)
      .order(:last_name)
  end
end
```

## View Object

* [Draper](https://github.com/drapergem/draper)

A.k.a Serializer or Presenter

Good when you want to represent JSON response or HTML view. This is especially helpful when you have controller and model information like `articles_path` URL to show to the user.

## Policy Object

If you want to enforce policy like who has permission to create resources, how many resources can be created, who can view what, you need Policy Object. Policy Objects are interchangeable. They can be replaced depending on access level or other context.

Move the policy checking out of the controller and model.

```ruby
class CreateInvoicePolicy
  def initialize(user)
    @user = user
  end
  
  def allowed?
    @user.finance? && !blocked
  end
  
  private
  
  def blocked
  end
end

class InvoiceController < ApplicationController
  def create
    if policy.allowed?
      InvoiceService.new(invoice_params)
    else
      head :unauthorized
    end
  end
  
  private
  
  def policy
    CreateInvoicePolicy.new(current_user)
  end
end
```

## Decorator

* [Strategy vs Decorator](https://www.google.com.sg/webhp?sourceid=chrome-instant&ion=1&espv=2&ie=UTF-8#q=decorator%20vs%20strategy)

---

* If you have many actions to cover
* When you want to add more auxiliary behavior to individual object without affecting other objects of the same class
* Format complex data for display