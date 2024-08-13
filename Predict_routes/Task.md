## Task description
**Background**

Uber serves hundreds of thousands of journeys every day. When a journey is requested, but before it takes place, we need to set a price for it. Pricing in Uber is calculated based on the routes’ distance and duration estimated by our routing engine. To guarantee that we are offering a fair price, we must make sure that these estimates are accurate.

**Proposal**

Uber’s Data Science team understands that in this context, “accurate” means that the estimated and real routes are very similar (the driver followed the route we predicted). We can use humans to label which routes are similar and which routes are different, as it is easy for humans to look at a map of the two routes and understand what is happening. But Uber serves millions of journeys, so the team is considering setting up a system to do it automatically.

We want to build a model that, given a pair of routes, assesses whether they are different or not. As a preliminary step, we ran a labeling project to provide the ground truth for a sample of routes on which the model can be trained. The steps were the following:

* 5,000 journeys were randomly selected.
* For each journey, estimated and real routes were plotted on a map.
* Several people (annotators) visually assess, according to their own perception, if the routes are equal, different or if they are not able to tell (annotations).

Routes examples, the magenta route is the real route while black route is the estimated route.

![Routes_example](Predict_routes/Routes_example.png)


**Data description**

With the labeling project we obtained a json file where each object represents an annotator's assessment of the similarity of an estimated/real routes pair, with the following attributes:

* journey_id: an identifier for each journey.
* annotator: an identifier for each evaluator.
* annotation: selected label for the estimated/actual route pair (“Both are the same”, “They differ” and “I don’t know”).
* estimated_route: coordinates pairs (lat-lon) of the estimated route.
* real_route: coordinates pairs (lat-lon) of the real route.

Example:

```
{
    "journey_id": "9cd6cd52-54c5-11ec-ae0a-0d030544d074",
    "annotator": 3,
    "annotation": "Both are the same",
    "estimated_route": [
        [
            -12.11249,
            -77.04655
        ],
        [
            -12.11245,
            -77.04661
        ],
        [
            -12.11239,
            -77.04664
        ],
        ...
    ],
    "real_route": [
        [
            -12.11197,
            -77.04775
        ],
        [
            -12.11193,
            -77.04736
        ],
        [
            -12.11181,
            -77.04722
        ],
        ...
    ]
}
```

### Task

The main purpose of this exercise is to create a model that distinguishes between similar and different paths. Using the provided dataset, perform the following tasks:

* Create any additional variables you think necessary.
* Build a model with them to predict when two routes are identical or different (according to human evaluation).
* Evaluate the model’s performance.

Hint: Note that each journey may have more than one annotation, as it may have been viewed by more than one annotator, and these annotations may be different.
