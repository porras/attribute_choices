# AttributeChoices

AttributeChoices is a plugin that simplifies the common pattern of mapping a set of discreet values for an ActiveRecord model attribute, to a set of display values for human consumption.

# Installation

## Rails 3

  In your `Gemfile` add
  
    gem 'attribute_choices'

## Rails 2

  In `environment.rb` add:
    
    config.gem 'attribute_choices'

# Usage

Define your model:

    class User < ActiveRecord::Base
      attribute_choices :gender,  { 'm' => "Male", 'f' => 'Female'}, :validate => true
      attribute_choices :age_group,  [
        ['18-24', '18 to 24 years old'], 
        ['25-45', '25 to 45 years old']
      ]
    end

Then try this in the console:

    >> @john # User.new :gender => 'm', :age_group => '18-24', :name => 'John'
    >> @john.gender
    => 'm'
    >> @john.gender_display
    => 'Male'
    >> User.gender_choices
    => [["Male", 'm'], ['Female', 'f']]

    >> @john.valid?
    => true
    >> @john.gender # 'o'
    >> @john.valid?
    => false

    => I18n.locale # :es
    >> @john.gender_display
    => "translation missing: es, Male"
 
    >> @john.age_group_display
    => '18 to 24 years old'
    >> User.age_group_choices
    => [['18-24', '18 to 24 years old], ['25-45', '25 to 45 years old']]
    
# ToDo

* Validate absence of _display and _choices methods
* Consider the usefulness of _choices# method


Copyright (c) 2009-2011 Christos Zisopoulos, released under the MIT license
