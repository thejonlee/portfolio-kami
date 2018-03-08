---
layout: post
title: Kele Client
thumbnail-path: "img/kele.png"
short-description: Kele is a ruby gem client built to access the Bloc API.

---

{:.center}
![]({{ site.baseurl }}/img/kele.png)


##Summary
Kele is a Ruby Gem API client built to access the [Bloc API](https://blocapi.docs.apiary.io/#). It handles the details  of requests and responses allowing Bloc students easy access to their information from the command line.

##Explanation
The Kele client allows Bloc students to do the following:
1. Initialize and authorize client using user log-in
2. Retrieve personal user information
3. Retrieve mentor schedule and availability
4. Retrieve roadmaps and checkpoints
5. Retrieve message threads, respond to message, and create new ones
6. Submit assignments for grading

##Problem
The main problem with this project was creating functionality for each of the user stories without the codebase becoming unnecessarily complicated or unwieldy.

##Solution
This was easily achieved by separating out the checkpoint submissions, roadmap access, and messaging functionality into their own separate files, and requiring them individually in the main kele.rb file.

{% highlight ruby %}

require 'httparty'
require 'json'
require_relative './roadmap'
require_relative './messages'
require_relative './checkpoints'

class Kele
  include HTTParty
  include Roadmap
  include Messages
  include Checkpoints
  base_uri 'https://www.bloc.io/api/v1/'
{% endhighlight %}

##Results
Once set up, the Kele client is fairly simple to use to retrieve student information from the command line and works as expected. All of the information can be called from the command line, and returned as a JSON blob.

##Conclusion
This was one of my first experiences with an API, and manipulating information using cURL commands from the command line. It was very educational to learn how to translate information into readable JSON, and make calls to pull the desired data.

[Click here](https://github.com/thejonlee/Kele) to access the code repository on Github.
