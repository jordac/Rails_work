# Add a declarative step here for populating the DB with movies.

Given /the following movies exist/ do |movies_table|
  movies_table.hashes.each do |movie|
    # each returned element will be a hash whose key is the table header.
    # you should arrange to add that movie to the database here.
    if Movie.find_by_title(movie[:title]).nil?
      Movie.create(title: movie[:title], rating: movie[:rating], release_date: movie[:release_date])
    #flunk "#{movie[:title]} not in movie database"
    end
  end
end

# Make sure that one string (regexp) occurs before or after another one
#   on the same page

Then /I should see "(.*)" before "(.*)"/ do |e1, e2|
  #  ensure that that e1 occurs before e2.
  #  page.body is the entire content of the page as a string.
  #flunk "Unimplemented #{page.body}"
  word_list = page.body.split("\n")
  if word_list.index("<td>#{e1}</td>") > word_list.index("<td>#{e2}</td>")
    flunk "#{e2} occurs before #{e1}"
  end
end

# Make it easier to express checking or unchecking several boxes at once
#  "When I uncheck the following ratings: PG, G, R"
#  "When I check the following ratings: G"

When /I (un)?check the following ratings: (.*)/ do |uncheck, rating_list|
  # HINT: use String#split to split up the rating_list, then
  #   iterate over the ratings and reuse the "When I check..." or
  #   "When I uncheck..." steps in lines 89-95 of web_steps.rb
  r_list = rating_list.split
  if uncheck == "un"
    r_list.each do |rating|
      uncheck "ratings_#{rating}"
    end
  else
    r_list.each do |rating|
      check "ratings_#{rating}"
    end
  end
end

Then /I should see all the movies/ do
  # Make sure that all the movies in the app are visible in the table
  movies = Movie.all
  word_list = page.body.split("\n")
  movies.each do |movie|
    if word_list.include?("<td>#{movie.title}</td>") == false
      flunk "#{movie.title} is not in #{word_list}"
    end
  end 
end
