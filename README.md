# mongoid-paranoia [![Build Status](https://travis-ci.org/haihappen/mongoid-paranoia.png)](https://travis-ci.org/haihappen/mongoid-paranoia)

**Important:** This gem is an extraction of [Mongoid::Paranoia](http://mongoid.github.io/en/mongoid/docs/extras.html#paranoia) from the official [mongoid](http://mongoid.org) gem.
Since Mongoid::Paranoia was removed in the `4.0.0` release of Mongoid, this gem re-enables the functionality of paranoid documents.

**Please submit only bug and security fixes**. Neither I will accept new features nor changes to existing APIs.

**Attention:** There are two similarly named gems out there: `mongoid-paranoia` and `mongoid_paranoia`

* `mongoid-paranoia`'s (this one) goal is to stay API compatible, which comes at the cost of (breaking) API changes to be rejected. If you're updating a Mongoid 3.x app to Mongoid 4+ and you depend on `Mongoid::Paranoia` this gem is recommended for continuity.

* However if your code is working and you want new features, for example a `*_restore` callback, you should head over to @simi's `mongoid_paranoia` gem at https://github.com/simi/mongoid_paranoia. He is doing a great job there and is willing to accept your PRs ;)

---

There may be times when you don't want documents to actually get deleted from the database, but "flagged" as deleted. Mongoid provides a Paranoia module to give you just that.

## Installation

In your Gemfile:

```ruby
gem 'mongoid-paranoia'
```

## Usage

```ruby
class Person
  include Mongoid::Document
  include Mongoid::Paranoia
end

person.delete   # Sets the deleted_at field to the current time, ignoring callbacks.
person.delete!  # Permanently deletes the document, ignoring callbacks.
person.destroy  # Sets the deleted_at field to the current time, firing callbacks.
person.destroy! # Permanently deletes the document, firing callbacks.
person.restore  # Brings the "deleted" document back to life.
```

The documents that have been "flagged" as deleted (soft deleted) can be accessed at any time by calling the deleted class method on the class.

```ruby
Person.deleted # Returns documents that have been "flagged" as deleted.
```

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Added some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

## Copyright

(The MIT license)

Copyright (c) 2013-2015 Mario Uher

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
"Software"), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE
LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION
WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
