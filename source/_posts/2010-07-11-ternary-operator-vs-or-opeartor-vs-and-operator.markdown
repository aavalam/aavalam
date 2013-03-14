---
layout: post
title: "Ternary Operator vs Or Operator vs And Operator"
author: Victor Goff
date: 2010-07-11 15:38
comments: true
categories: [Ruby, Ternary, or, and]
---
## The Ternary Operator and the OR Operator
The ternary operator is not reasonable for a situation that returns true or false; if the goal is to get a result of true or false from your decision, it is better to simply evaluate the statement itself. <!-- More -->

For example, if it reduces to this statement:
{% codeblock snippet1.rb %}
some_condition ? true : false
{% endcodeblock %}
then you are better off just simply using `some_condition` by itself, as it will evaluate to either true or false.

If, however, you have a statement that evaluates such as 

{% codeblock snippet2.rb %}
some_condition ? true : (some_action or other value)
{% endcodeblock %}

What you may be asking for and really wanting is the OR Operator, rather than the ternary:

{% codeblock snippet3.rb %}
some_condition || do_this_if_"some_statement"_evaluates_as_false
{% endcodeblock %}

If this doesn't immediately look familiar, look at this:

{% codeblock snippet4.rb %}
assign_this = evaluated_condition ? true : expression_if_evaluated_statement_is_false
{% endcodeblock %}

 Is the same as:

{% codeblock snippet5.rb %}
assign_this = evaluated_statement_if_true or expression_if_evaluated_statement_is_false
{% endcodeblock %}

On the other side of the spectrum, when you have 
{% codeblock snippet6.rb %}
some_statement ? (some_action or other value) : false # or nil
{% endcodeblock %}
You will want to use the AND operator:
{% codeblock snippet7.rb %}
some_condition && do_this_if_some_condition_evaluates_as_true
{% endcodeblock %}

Rather than using the ternary with a false return like:

{% codeblock snippet8.rb %}
assign_this = evaluated_condition ?  (some_action or other value)  : false
{% endcodeblock %}

Remember, the point of either is having an evaluated statement that has the possibility of being false (or nil) as well as the possibility of being true.  

If your evaluated statement never has both possibilities, then these aren't the operators for you at this moment.

In conclusion, we use the ternary operator when we have a simple `if..then` operation that does not return either `true` or `false` itself.  We use the `or` and `and` operator when we need one evaluation or the other.  When using the ternary operator, we don't use it to return `true` or `false`, there are easier ways to do that.

The discussion starts here, but continues in our [Google Plus Post](https://plus.google.com/116568773932133159290/posts/RXLe2TkWEDa)!
