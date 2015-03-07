---
layout: post
title: A (small) critique
date: 2014-05-02 14:53
permalink: a-critique-of-the-design-of-the-clever-api
summary: I explored the Clever API recently while applying for an internship position at the company and I liked how clean, self contained and comprehensive it is.
categories: api review
---

I explored the Clever API recently while applying for an internship position at the company and I liked how clean, self contained and comprehensive it is.

There are 6 kinds of resources that can be accessed using the API - Students, Teachers, Schools, Districts, Sections, Events.

I found that the API supported two verbs GET and PUT. The API is simple enough that a request is very easy to construct. This is the general structure of a request, which when called returns a JSON object: <span class="bg-orange">`/{version-number}/{resource-name}/{id}/{sub-resource}`</span>

So, if you wanted a list of all the students you have access to across all districts you would call - <span class="bg-orange">`/v1.1/students`</span>. And if you wanted a list of all the students that a particular teacher taught you would call - <span class="bg-orange">`/v1.1/teachers/{teacher-id}/students`</span>

###Design Issue###

If there was one thing I found a little puzzling then that would be design of the returned JSON object. For instance in response to <span class="bg-orange">`/v1.1/students`</span> the first field of the data structure is the <span class="bg-orange">`paging`</span> field which contains info about how many pages of data the response has. 

The second field is the <span class="bg-orange">`data`</span> field which contains an array of dictionaries which contain the information about students. Each dictionary key within this array is also called <span class="bg-orange">`data`</span>:

```
{
      "paging": {
          ...
      },
      "data": [                            //<-- These two fields
         {                                    
              "data": {                    //<-- are named the same.
                ...
              },
              "uri": "..."
         },
         {
              "data": {
                ...
              },
              "uri": "..."
         },
        .
        .
        .       
```

Which seems like a missed opportunity. The names of the dictionary keys within the array could have been something else which conveyed some information about the values of those keys.