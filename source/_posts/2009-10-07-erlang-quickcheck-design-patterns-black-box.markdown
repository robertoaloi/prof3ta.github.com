--- 
layout: post
title: "Erlang Quickcheck Design Patterns - Black Box"
date: 2009-10-07 00:00
categories: [erlang, software engineering, quickcheck, testing]
---
<h3>Name</h3>

Black Box

<h3>Also Known As</h3>

ETS Driven Testing

<h3>Intent</h3>

When writing _Quickcheck_ unit tests for an Erlang application, it
usually happens that you require to stub some external application,
since you're not interested in _system tests_, but you want to test
your application as a mere _black box_.

<h3>Motivation</h3>

You want complete control on the results provided by your stubs, so
that you can successfully check the properties you need for your
application.

<h3>Sample Code</h3>

In your quickcheck module, just define in your state the results you
need, together with their default value:

<pre>-record(state, {stub_result = true}).</pre>

Define the initial state as follows:

<pre>
initial_state() -&gt;
    init.

initial_state_data() -&gt;
    #state{}.
</pre>

In your property, create an ETS table containing the results (don't forget to delete it after running the tests) and call the _run_commands_ function by passing an extra parameter:

<pre>
prop_commands() -&gt;
    ?FORALL({Cmds, State}, custom_commands(),
            ?TRAPEXIT(begin
                          results = ets:new(results, [named_table, set, public]),
                          ets:insert(results, {stub_result, State#state.stub_result}),
                          {H,S,Res} = eqc_fsm:run_commands(?MODULE, Cmds, [{var, stub_result}]),
                          true = ets:delete(results),
                          ...
</pre>

The _custom_commands_ function is the place where you set the list of available results:
<pre>
custom_commands() -&gt;
    ?LET(State,
         #state{stub_result = oneof([true, false])},
         {more_commands(100, eqc_fsm:commands(?MODULE, {init, State})), State}).
</pre>

You can check the result in your postconditions, as follows:
<pre>
postcondition(_From, _To, S, {call, _, _, _}, R) -&gt;
    S#state.stub_result == R.
</pre>

Obviously, your stubs need to contain something like:
<pre>
stubbed_function() -&gt;
    ets:lookup_element(results, stub_result, 2).
</pre>

<h3>Consequences</h3>
Your tests will be able to cover a bigger number of code lines (<a target="_blank" href="http://en.wikipedia.org/wiki/Lemmings_(video_game)">lemmings</a>).

<h3>Thanks</h3>
Thanks to _Master_ Magnus Henoch for his suggestions.
