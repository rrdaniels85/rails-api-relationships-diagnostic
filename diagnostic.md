# Rails API Relationships Diagnostic

Place your responses inside the fenced code-blocks where indivated by comments.

1.  Describe a reason why a join tables may be valuable.

  ```md
It allows you to extract data from multiple tables that have relationships.
  ```

1.  Provide a database table structure and explain the Entity Relationship that
  describes a many-to-many relationship for `Profiles`, `Movies` and `Favorites`
  (Think of Netflix). A `Profile` has a `given_name`, `surname` and `email` and a
  `Movies` have `title`, `release_date`, and `length` and `Favorites` would be the
  join table with references to `Movies` and `Profiles`.

  ```md
Profiles to Favorites - One to Many relationship
Movies to Favorites - Many to many relationship

Profile - Columns: given_name, surname, email
Movies - Columns: title, release_date, length
Favorites - Columns: Movies, Profiles

  ```

1.  For the above example, what needs to be added to the Model files?

  ```rb
  class Profile < ActiveRecord::Base
  has_many :movies, through: :favorites
  has_many :favorites
  end
  ```

  ```rb
  class Movie < ActiveRecord::Base
  has_many:profiles, through :favorites
  has_many:favorites

  end
  ```

  ```rb
  class Favorite < ActiveRecord::Base
  has_many :movies
  has_many :profiles
  end
  ```

1.  What is the purpose of a serializer? What would our `Profile` serializer look
like to show all movies favorited by a profile on
`http://localhost:3000/profiles/1`

  ```md
The Serializer allows you to control the format that your data is returned and shown
in the browser.
  ```

  ```rb
  class ProfileSerializer < ActiveModel::Serializer
    attributes :id
    has_manu :
  attributes :id, :date
  has_one :doctor
  has_one :patient

  end
  ```

1.  What would the command be to _scaffold_ out a **join table** for Favorites from
the above `Movies` and `Profiles`.

  ```sh
generate scaffold Favorite profile:references movie:references
  ```

1.  What is `Dependent: Destroy` and where/why would we use it?

  ```md
It tells tells the table to destroy the dependent item in the join table if the item
in the model tied to that dependent item in the join table is destroyed. In this case, we would
put it in the movie or profie models. For the profile model, it might look something like this:
has_many :favorites, dependent: :destroy

  ```

1.  Think of **ANY** example where you would have a one-to-many relationship as well
as a many-to-many relationship in an application. You only need to list the
description about the resources and how they relate to one another.

  ```md
  ```
