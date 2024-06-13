# Introduction
### The datasets I chose is the "Recipes and Ratings". This project is going to explore the relationship between rating and time consumed and steps required on the recipes. People who are enjoying cooking, might want to know this question. How might time consumed and steps required affect the average rating on a recipe.
### There are two datasets in total, after merging them, there are 234429 rows in total. The col this project going to work on most are these four

<table>
<thead>
<tr>
<th>Column</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>&#39;minutes&#39;</td>
<td>Minutes to prepare recipe</td>
</tr>
<tr>
<td>&#39;n_steps&#39;</td>
<td>Number of steps in recipe</td>
</tr>
<tr>
<td>&#39;n_ingredients</td>
<td>Number of ingredients in recipe</td>
</tr>
<tr>
<td>&#39;submitted&#39;</td>
<td>Date recipe was submitted</td>
</tr>
</tbody>
</table>

# Data Cleaning and Exploratory Data Analysis
## Data Cleaning
### First, as I need to access to all recipes existed in recipe dataset, I read and left merge recipe dataset and interaction dataset(containing rating) respect to the recipe_id. 
### Second, replace rating that equals to zero with np.NaN, because a rate of zero is due to no input of rating.
### Third, using mean of each recipe to fill the missing ratings in the same recipe

<table style="width:100%">
<thead>
<tr>
<th style="text-align:right"></th>
<th style="text-align:left">name</th>
<th style="text-align:right">id</th>
<th style="text-align:right">minutes</th>
<th style="text-align:right">contributor_id</th>
<th style="text-align:left">submitted</th>
<th style="text-align:left">tags</th>
<th style="text-align:left">nutrition</th>
<th style="text-align:right">n_steps</th>
<th style="text-align:left">steps</th>
<th style="text-align:left">description</th>
<th style="text-align:left">ingredients</th>
<th style="text-align:right">n_ingredients</th>
<th style="text-align:right">user_id</th>
<th style="text-align:right">recipe_id</th>
<th style="text-align:left">date</th>
<th style="text-align:right">rating</th>
<th style="text-align:left">review</th>
<th style="text-align:right">rating_filled</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:right">0</td>
<td style="text-align:left">1 brownies in the world    best ever</td>
<td style="text-align:right">333281</td>
<td style="text-align:right">40</td>
<td style="text-align:right">985201</td>
<td style="text-align:left">2008-10-27</td>
<td style="text-align:left">[&#39;60-minutes-or-less&#39;, &#39;time-to-make&#39;, &#39;course&#39;, &#39;main-ingredient&#39;, &#39;preparation&#39;, &#39;for-large-groups&#39;, &#39;desserts&#39;, &#39;lunch&#39;, &#39;snacks&#39;, &#39;cookies-and-brownies&#39;, &#39;chocolate&#39;, &#39;bar-cookies&#39;, &#39;brownies&#39;, &#39;number-of-servings&#39;]</td>
<td style="text-align:left">[138.4, 10.0, 50.0, 3.0, 3.0, 19.0, 6.0]</td>
<td style="text-align:right">10</td>
<td style="text-align:left">[&#39;heat the oven to 350f and arrange the rack in the middle&#39;, &#39;line an 8-by-8-inch glass baking dish with aluminum foil&#39;, &#39;combine chocolate and butter in a medium saucepan and cook over medium-low heat , stirring frequently , until evenly melted&#39;, &#39;remove from heat and let cool to room temperature&#39;, &#39;combine eggs , sugar , cocoa powder , vanilla extract , espresso , and salt in a large bowl and briefly stir until just evenly incorporated&#39;, &#39;add cooled chocolate and mix until uniform in color&#39;, &#39;add flour and stir until just incorporated&#39;, &#39;transfer batter to the prepared baking dish&#39;, &#39;bake until a tester inserted in the center of the brownies comes out clean , about 25 to 30 minutes&#39;, &#39;remove from the oven and cool completely before cutting&#39;]</td>
<td style="text-align:left">these are the most; chocolatey, moist, rich, dense, fudgy, delicious brownies that you&#39;ll ever make.....sereiously! there&#39;s no doubt that these will be your fav brownies ever for you can add things to them or make them plain.....either way they&#39;re pure heaven!</td>
<td style="text-align:left">[&#39;bittersweet chocolate&#39;, &#39;unsalted butter&#39;, &#39;eggs&#39;, &#39;granulated sugar&#39;, &#39;unsweetened cocoa powder&#39;, &#39;vanilla extract&#39;, &#39;brewed espresso&#39;, &#39;kosher salt&#39;, &#39;all-purpose flour&#39;]</td>
<td style="text-align:right">9</td>
<td style="text-align:right">386585</td>
<td style="text-align:right">333281</td>
<td style="text-align:left">2008-11-19</td>
<td style="text-align:right">4</td>
<td style="text-align:left">These were pretty good, but took forever to bake.  I would send it ended up being almost an hour!  Even then, the brownies stuck to the foil, and were on the overly moist side and not easy to cut.  They did taste quite rich, though!  Made for My 3 Chefs.</td>
<td style="text-align:right">4</td>
</tr>
<tr>
<td style="text-align:right">1</td>
<td style="text-align:left">1 in canada chocolate chip cookies</td>
<td style="text-align:right">453467</td>
<td style="text-align:right">45</td>
<td style="text-align:right">1848091</td>
<td style="text-align:left">2011-04-11</td>
<td style="text-align:left">[&#39;60-minutes-or-less&#39;, &#39;time-to-make&#39;, &#39;cuisine&#39;, &#39;preparation&#39;, &#39;north-american&#39;, &#39;for-large-groups&#39;, &#39;canadian&#39;, &#39;british-columbian&#39;, &#39;number-of-servings&#39;]</td>
<td style="text-align:left">[595.1, 46.0, 211.0, 22.0, 13.0, 51.0, 26.0]</td>
<td style="text-align:right">12</td>
<td style="text-align:left">[&#39;pre-heat oven the 350 degrees f&#39;, &#39;in a mixing bowl , sift together the flours and baking powder&#39;, &#39;set aside&#39;, &#39;in another mixing bowl , blend together the sugars , margarine , and salt until light and fluffy&#39;, &#39;add the eggs , water , and vanilla to the margarine / sugar mixture and mix together until well combined&#39;, &#39;add in the flour mixture to the wet ingredients and blend until combined&#39;, &#39;scrape down the sides of the bowl and add the chocolate chips&#39;, &#39;mix until combined&#39;, &#39;scrape down the sides to the bowl again&#39;, &#39;using an ice cream scoop , scoop evenly rounded balls of dough and place of cookie sheet about 1 - 2 inches apart to allow for spreading during baking&#39;, &#39;bake for 10 - 15 minutes or until golden brown on the outside and soft &amp; chewy in the center&#39;, &#39;serve hot and enjoy !&#39;]</td>
<td style="text-align:left">this is the recipe that we use at my school cafeteria for chocolate chip cookies. they must be the best chocolate chip cookies i have ever had! if you don&#39;t have margarine or don&#39;t like it, then just use butter (softened) instead.</td>
<td style="text-align:left">[&#39;white sugar&#39;, &#39;brown sugar&#39;, &#39;salt&#39;, &#39;margarine&#39;, &#39;eggs&#39;, &#39;vanilla&#39;, &#39;water&#39;, &#39;all-purpose flour&#39;, &#39;whole wheat flour&#39;, &#39;baking soda&#39;, &#39;chocolate chips&#39;]</td>
<td style="text-align:right">11</td>
<td style="text-align:right">424680</td>
<td style="text-align:right">453467</td>
<td style="text-align:left">2012-01-26</td>
<td style="text-align:right">5</td>
<td style="text-align:left">Originally I was gonna cut the recipe in half (just the 2 of us here), but then we had a park-wide yard sale, &amp; I made the whole batch &amp; used them as enticements for potential buyers ~ what the hey, a free cookie as delicious as these are, definitely works its magic! Will be making these again, for sure! Thanks for posting the recipe!</td>
<td style="text-align:right">5</td>
</tr>
<tr>
<td style="text-align:right">2</td>
<td style="text-align:left">412 broccoli casserole</td>
<td style="text-align:right">306168</td>
<td style="text-align:right">40</td>
<td style="text-align:right">50969</td>
<td style="text-align:left">2008-05-30</td>
<td style="text-align:left">[&#39;60-minutes-or-less&#39;, &#39;time-to-make&#39;, &#39;course&#39;, &#39;main-ingredient&#39;, &#39;preparation&#39;, &#39;side-dishes&#39;, &#39;vegetables&#39;, &#39;easy&#39;, &#39;beginner-cook&#39;, &#39;broccoli&#39;]</td>
<td style="text-align:left">[194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0]</td>
<td style="text-align:right">6</td>
<td style="text-align:left">[&#39;preheat oven to 350 degrees&#39;, &#39;spray a 2 quart baking dish with cooking spray , set aside&#39;, &#39;in a large bowl mix together broccoli , soup , one cup of cheese , garlic powder , pepper , salt , milk , 1 cup of french onions , and soy sauce&#39;, &#39;pour into baking dish , sprinkle remaining cheese over top&#39;, &#39;bake for 25 minutes or until cheese is lightly browned&#39;, &#39;sprinkle with rest of french fried onions and bake until onions are browned and cheese is bubbly , about 10 more minutes&#39;]</td>
<td style="text-align:left">since there are already 411 recipes for broccoli casserole posted to &quot;zaar&quot; ,i decided to call this one  #412 broccoli casserole.i don&#39;t think there are any like this one in the database. i based this one on the famous &quot;green bean casserole&quot; from campbell&#39;s soup. but i think mine is better since i don&#39;t like cream of mushroom soup.submitted to &quot;zaar&quot; on may 28th,2008</td>
<td style="text-align:left">[&#39;frozen broccoli cuts&#39;, &#39;cream of chicken soup&#39;, &#39;sharp cheddar cheese&#39;, &#39;garlic powder&#39;, &#39;ground black pepper&#39;, &#39;salt&#39;, &#39;milk&#39;, &#39;soy sauce&#39;, &#39;french-fried onions&#39;]</td>
<td style="text-align:right">9</td>
<td style="text-align:right">29782</td>
<td style="text-align:right">306168</td>
<td style="text-align:left">2008-12-31</td>
<td style="text-align:right">5</td>
<td style="text-align:left">This was one of the best broccoli casseroles that I have ever made.  I made my own chicken soup for this recipe. I was a bit worried about the tsp of soy sauce but it gave the casserole the best flavor. YUM!</td>
<td style="text-align:right">5</td>
</tr>
<tr>
<td style="text-align:right"></td>
<td style="text-align:left"></td>
<td style="text-align:right"></td>
<td style="text-align:right"></td>
<td style="text-align:right"></td>
<td style="text-align:left"></td>
<td style="text-align:left"></td>
<td style="text-align:left"></td>
<td style="text-align:right"></td>
<td style="text-align:left"></td>
<td style="text-align:left"></td>
<td style="text-align:left"></td>
<td style="text-align:right"></td>
<td style="text-align:right"></td>
<td style="text-align:right"></td>
<td style="text-align:left"></td>
<td style="text-align:right"></td>
<td style="text-align:left">The photos you took (shapeweaver) inspired me to make this recipe and it actually does look just like them when it comes out of the oven.</td>
<td style="text-align:right"></td>
</tr>
<tr>
<td style="text-align:right"></td>
<td style="text-align:left"></td>
<td style="text-align:right"></td>
<td style="text-align:right"></td>
<td style="text-align:right"></td>
<td style="text-align:left"></td>
<td style="text-align:left"></td>
<td style="text-align:left"></td>
<td style="text-align:right"></td>
<td style="text-align:left"></td>
<td style="text-align:left"></td>
<td style="text-align:left"></td>
<td style="text-align:right"></td>
<td style="text-align:right"></td>
<td style="text-align:right"></td>
<td style="text-align:left"></td>
<td style="text-align:right"></td>
<td style="text-align:left">Thanks so much for sharing your recipe shapeweaver. It was wonderful!  Going into my family&#39;s favorite Zaar cookbook :)</td>
<td style="text-align:right"></td>
</tr>
<tr>
<td style="text-align:right">3</td>
<td style="text-align:left">412 broccoli casserole</td>
<td style="text-align:right">306168</td>
<td style="text-align:right">40</td>
<td style="text-align:right">50969</td>
<td style="text-align:left">2008-05-30</td>
<td style="text-align:left">[&#39;60-minutes-or-less&#39;, &#39;time-to-make&#39;, &#39;course&#39;, &#39;main-ingredient&#39;, &#39;preparation&#39;, &#39;side-dishes&#39;, &#39;vegetables&#39;, &#39;easy&#39;, &#39;beginner-cook&#39;, &#39;broccoli&#39;]</td>
<td style="text-align:left">[194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0]</td>
<td style="text-align:right">6</td>
<td style="text-align:left">[&#39;preheat oven to 350 degrees&#39;, &#39;spray a 2 quart baking dish with cooking spray , set aside&#39;, &#39;in a large bowl mix together broccoli , soup , one cup of cheese , garlic powder , pepper , salt , milk , 1 cup of french onions , and soy sauce&#39;, &#39;pour into baking dish , sprinkle remaining cheese over top&#39;, &#39;bake for 25 minutes or until cheese is lightly browned&#39;, &#39;sprinkle with rest of french fried onions and bake until onions are browned and cheese is bubbly , about 10 more minutes&#39;]</td>
<td style="text-align:left">since there are already 411 recipes for broccoli casserole posted to &quot;zaar&quot; ,i decided to call this one  #412 broccoli casserole.i don&#39;t think there are any like this one in the database. i based this one on the famous &quot;green bean casserole&quot; from campbell&#39;s soup. but i think mine is better since i don&#39;t like cream of mushroom soup.submitted to &quot;zaar&quot; on may 28th,2008</td>
<td style="text-align:left">[&#39;frozen broccoli cuts&#39;, &#39;cream of chicken soup&#39;, &#39;sharp cheddar cheese&#39;, &#39;garlic powder&#39;, &#39;ground black pepper&#39;, &#39;salt&#39;, &#39;milk&#39;, &#39;soy sauce&#39;, &#39;french-fried onions&#39;]</td>
<td style="text-align:right">9</td>
<td style="text-align:right">1.19628e+06</td>
<td style="text-align:right">306168</td>
<td style="text-align:left">2009-04-13</td>
<td style="text-align:right">5</td>
<td style="text-align:left">I made this for my son&#39;s first birthday party this weekend. Our guests INHALED it! Everyone kept saying how delicious it was. I was I could have gotten to try it.</td>
<td style="text-align:right">5</td>
</tr>
<tr>
<td style="text-align:right">4</td>
<td style="text-align:left">412 broccoli casserole</td>
<td style="text-align:right">306168</td>
<td style="text-align:right">40</td>
<td style="text-align:right">50969</td>
<td style="text-align:left">2008-05-30</td>
<td style="text-align:left">[&#39;60-minutes-or-less&#39;, &#39;time-to-make&#39;, &#39;course&#39;, &#39;main-ingredient&#39;, &#39;preparation&#39;, &#39;side-dishes&#39;, &#39;vegetables&#39;, &#39;easy&#39;, &#39;beginner-cook&#39;, &#39;broccoli&#39;]</td>
<td style="text-align:left">[194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0]</td>
<td style="text-align:right">6</td>
<td style="text-align:left">[&#39;preheat oven to 350 degrees&#39;, &#39;spray a 2 quart baking dish with cooking spray , set aside&#39;, &#39;in a large bowl mix together broccoli , soup , one cup of cheese , garlic powder , pepper , salt , milk , 1 cup of french onions , and soy sauce&#39;, &#39;pour into baking dish , sprinkle remaining cheese over top&#39;, &#39;bake for 25 minutes or until cheese is lightly browned&#39;, &#39;sprinkle with rest of french fried onions and bake until onions are browned and cheese is bubbly , about 10 more minutes&#39;]</td>
<td style="text-align:left">since there are already 411 recipes for broccoli casserole posted to &quot;zaar&quot; ,i decided to call this one  #412 broccoli casserole.i don&#39;t think there are any like this one in the database. i based this one on the famous &quot;green bean casserole&quot; from campbell&#39;s soup. but i think mine is better since i don&#39;t like cream of mushroom soup.submitted to &quot;zaar&quot; on may 28th,2008</td>
<td style="text-align:left">[&#39;frozen broccoli cuts&#39;, &#39;cream of chicken soup&#39;, &#39;sharp cheddar cheese&#39;, &#39;garlic powder&#39;, &#39;ground black pepper&#39;, &#39;salt&#39;, &#39;milk&#39;, &#39;soy sauce&#39;, &#39;french-fried onions&#39;]</td>
<td style="text-align:right">9</td>
<td style="text-align:right">768828</td>
<td style="text-align:right">306168</td>
<td style="text-align:left">2013-08-02</td>
<td style="text-align:right">5</td>
<td style="text-align:left">Loved this.  Be sure to completely thaw the broccoli.  I didn&#039;t and it didn&#039;t get done in time specified.  Just cooked it a little longer though and it was perfect.  Thanks Chef.</td>
<td style="text-align:right">5</td>
</tr>
</tbody>
</table>


## Univariate Analysis
<iframe
  src="assets/histogram_of_cooking n_steps.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

# Assessment of Missingness

# Hypothesis Testing

# Framing a Prediction Problem

# Baseline Model

# Final Model

# Fairness Analysis