---
layout: post
title: Blocipedia
thumbnail-path: "img/blocipedia/myblocipedia.png"
short-description: An application that allows users to create their own wikis.

---

{:.center}
![]({{ site.baseurl }}/img/blocipedia/myblocipedia.png)

## Summary
Blocipedia is a web application built on Ruby on Rails, and structured similarly to Wikipedia. Users can create their own public wikis while premium users can create private ones, and invite collaborators to contribute.

## Technologies Used

- Rails
- Heroku
- Bootstrap
- Devise
- Pundit
- Rolify
- Stripe
- SendGrid
- RedCarpet
- RSpec
- Shoulda
- Faker
- Factory Girl
- Figaro

[Click here to view the GitHub repo](https://github.com/thejonlee/blocipedia)

## Explanation
The end goal for Blocipedia was to create a Wikipedia clone using Ruby on Rails with this set of functionality:

1. Log-in/Sign-up using email and password with email confirmation
2. Create three levels of users: standard, premium, and admin
3. Standard and premium users are able to create, read, and destroy personal public wikis
4. Ability to create private wikis for premium users
5. Admin users have access and control over all wikis, public or private
6. Premium users are charged using Stripe for upgraded accounts
7. Premium users are able to add collaborators for wiki topics
8. All users are able to create and preview wikis using markdown syntax

## Problem
The initial implementation of user sign-up, and logging users in and out were fairly simple using Devise. User sign up requires an e-mail address and verification, and that was completed utilizing SendGrid. Implementing CRUD operations was also relatively straightforward. Creating three different roles for users, however - standard, admin, and premium - proved to be more of a challenge.

Standard users should be allowed to create public wikis and topics, but premium users should also be allowed to make wikis private while also inviting other collaborators to contribute. Admin users would not be restricted access to any wikis, public or private.

## Solution
[The Rolify gem](https://github.com/RolifyCommunity/rolify) combined with Devise greatly simplified the process of creating the roles of standard, admin, and premium. I was able to search in order to find a streamlined solution to this problem, and implement it to great effect in Blocipedia. Queries are able to be completed from Rails console.

In the User model, after adding the Rolify gem, I assigned a default role of standard to all users using the after_initialize method.

{% highlight ruby %}
  after_initialize :assign_default_role

  def assign_default_role
    self.add_role(:standard) if self.roles.blank?
  end
{% endhighlight %}

## Results
After assigning all users the default standard role, all operations work as expected. I established the relationship between users, wikis, and collaborators, and later integrated Stripe to handle payments for upgraded accounts.

Index of Wikis
{:.center}
![]({{ site.baseurl }}/img/blocipedia/indexwikis.png)

Wiki Edit Page
{:.center}
![]({{ site.baseurl }}/img/blocipedia/editwikis.png)

User Upgrade Page
{:.center}
![]({{ site.baseurl }}/img/blocipedia/upgradewiki.png)

Stripe Integration for Payments
{:.center}
![]({{ site.baseurl }}/img/blocipedia/stripeintegration.png)


## Conclusion
This was my first experience building a fully formed application using Rails, and was surprised at how (relatively) simple it was. The built-in generators along with powerful gems like Devise, Pundit, Stripe, and Rolify can make complicated tasks much simpler and easier to implement.

While building an application like this from the ground up was by no means easy, it did demonstrate the power of the right tools to help create an application with great functionality. It also made me excited to continue learning more about Rails and what other great things it can do.
