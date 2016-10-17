# Contents
##### [Part 1: Creating your Xcode Project](./part1.md)
##### [Part 2: Setting up your Table View in Interface Builder](./part2.md)
##### [Part 3: Setting up your Custom Table View Cell](./part3.md)
##### [Part 4: Implementing your Table View Delegate](./part4.md)
##### [Part 5: Subclassing UITableViewCell](./part5.md)
##### [Bonus: Explaining @IBOutlets](./part50.md)
##### [Part 6: Populating your Table View Cells](./part6.md)
##### [Part 7: Adding User Interaction](./part7.md)

# How to port this to Legacy GT iOS Website
1. Move all of the contents in `assets/tableview/` to `app/assets/images/tableview/` in the rails-site
2. Move all of the tutorials .md files (part*.md) to `app/assets/tutorials/tableview/`
3. `rm -rf public` when in the root directory of the rails-site
4. `rake assets:precompile` to compile the assets
5. `rails s` to run the server on `localhost:3000`
6. To push to heroku, git add, git commit, and then `git push heroku master` if you have permission.