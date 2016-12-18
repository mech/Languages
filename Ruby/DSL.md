# Domain Specific Language

```ruby
package 'nginx' do
  action :install
end

service 'nginx' do
  action [:enable, :start]
end
```

```ruby
class DSL
  def package(name, &block)
    pkg = Package.new
    pkg.instance_exec(&block)
    result << ['package', name, pkg.attrs]
  end
  
  def result
    @result ||= []
  end
end

class Package
  def action(actions)
    attrs[:action] = Array(actions)
  end
  
  def attrs
    @attrs ||= {}
  end
end
```

* DSL is an abstraction for a domain-specific purpose