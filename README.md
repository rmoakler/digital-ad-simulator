# Digital Advertising Simulator
Author: Robert Moakler `<rmoakler@stern.nyu.edu>`

## Purpose
Online advertising campaigns and the environments they run in are becoming increasingly complex. Advertisers are building sophisticated targeting algorithms. Users are spreading their Internet browsing behavior across multiple devices. The various problems we may be interested in solving can be difficult or impossible without having rich (but clean) data to analyze and test out models and algorithms on. While there is a vast amount of real world advertising data that we can use, it is often beneficial to use simulated data to explore many possible settings. In some fields, such as causal inference, simulation can be the only possible way of teasing out causal effects in certain scenarios. Current digital advertising literature often relies on aggregate level simulation or on overly simplistic simulations.

The goal of this project is to build a method for creating simulated data that is granular and highly adjustable. Instead of simulating the results of a single advertising campaign, we simulate all users and advertisers at the individual level. By adjusting the various details of all different players in simulation we can provide data that will allow us to test complex hypotheses in a variety of fields such as causal inference or user identification.

## High level overview
Simulation is done by modeling the behavior of three main players: users, advertising campaigns, and advertising strategies.

- Users are individuals that browse the Internet on any type(s) of device. They have descriptive characteristics (covariates) that can be customized. They can  browse in any number of patterns, e.g., sleeping at night and browsing heavily on weekends.
- Advertising campaigns can be thought of as companies that are advertising a particular product or service. They have a particular goal in mind for each campaign. They also have a time range where they would like to run their campaign and some limits on the number of ads they want to serve to the population/each user.
- Advertising strategies consider user covariates, campaign limits, and potential outcomes when deciding how much they value a particular user.

Simulation begins at `t_0`.

1. For all users we determine and queue up their next event by taking into account the state of the world and their individual characteristics. They may choose to visit a web page, convert, or change device.
2. We process the time-sorted event queue and execute each event and update the state of the user and world. We then generate the user's next event and insert it into the queue.
3. Step 2 continues until all new events fall out side some specified time `T`.

All interactions and player details are defined and customized before runtime. This allows for rich control of the advertising world: simple setups consisting of a handful of users with uniform browsing on a single device and one ad campaign, or complex settings with millions of users, dozens of competing campaigns, complex covariate settings and dependencies, mobile and desktop browsing, and holiday and time effects.

## Technical implementation
All simulation is done in Python with a strong focus on minimizing run time.
