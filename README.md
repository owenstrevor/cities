# Cities

[![Build Status](https://travis-ci.org/joecorcoran/cities.png?branch=master)](https://travis-ci.org/joecorcoran/cities) [![Code Climate](https://codeclimate.com/github/joecorcoran/cities.png)](https://codeclimate.com/github/joecorcoran/cities)

Every city in the world (according to the MaxMind database).

## Setup

1. Install the gem

```
gem install 'cities', :git => 'https://github.com/owenstrevor/cities.git'
```

2. Download the latest cities data and extract it into your app.

```
$ wget https://s3-us-west-2.amazonaws.com/cities-gem/cities.tar.gz
$ tar -xzf cities.tar.gz
```

3. Create file cities.rb and add it to config/initializers folder. Add the below line.

```ruby
Cities.data_path = '/path/to/cities'
```

## Custom Data

*Added by Owens

I needed reverse lookup for a set of specific cities, so I created a new JSON file called TOP.json (as in "top cities") and added it to the Cities data path. This JSON file is a list of top cities with a country field. I also added the .country method to cities.rb to handle this.

## Usage

Countries are identified by their [ISO 3166-1 alpha-2](http://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) codes.

```ruby
cities = Cities.cities_in_country('GB')
  #=> { "abberley"=> #<City:0x000001049b9ba0>, "abberton"=> #<City:0x000001049b9b50>, ... }

manchester = cities['manchester']
  #=> #<City:0x00000102fb4ea8>

manchester.name
  #=> "Manchester"

manchester.population
  #=> 395516

manchester.latlong
  #=> [53,5, -2.216667]
```

The database is exhaustive and certainly stretches the definition of the word "city".

```ruby
Cities.cities_in_country('GB')['buchlyvie'].population
  #=> 448
```

## Optional: Rails Countries Gem

[Countries gem github page](https://github.com/hexorx/countries)

```
gem install 'countries'
```

Cities gem also adds two new instance methods to the `Country` class from the rails 'countries' gem.

```ruby
us = Country.search('US')
  #=> #<Country:0x000001020cf5f0>

us.cities?
  #=> true

us.cities
  #=> { "abanda" => #<Cities::City:0x00000114b34a38>, ...  }
```

## Caching

Sometimes you may want to not constantly want to read and parse the same large JSON data files.  So by default we cache in memory the parsed JSON.  To turn this off simply set the cache_data flag to false in your initializer file.

```ruby
Cities.cache_data = false
```

## Specs

The default path for data is the following path

```
GEM_ROOT/data/cities
```

Or you can set the environment variable DATA_PATH

To run the specs bundle and run specs
```
=> bundle
=> rake
```

## Credits

Provided under an MIT license by [Joe Corcoran](http://blog.joecorcoran.co.uk). Thanks to [hexorx](https://github.com/hexorx) for the countries gem that brought this idea about.

This product includes data created by MaxMind, available from [http://www.maxmind.com](http://www.maxmind.com). All data &copy; 2008 MaxMind Inc. Read the [MaxMind WorldCities open data license](http://download.maxmind.com/download/geoip/database/LICENSE_WC.txt) for more details.
