# ml_challenge

## Introduction

This repo contains Jupyter notebooks investigating a smart scheduling solution for a restaurant. It features a demand forecasting notebook to predict hourly order quantities as well as a staffing solution notebook designed to optimise Orders per labour hour (OPLH) which utilises the outputs of the demand forecasting. 

Several interactive graphs are included within the notebook also that may not display in Github itself, but will show once run within  the notebook. Keep in mind that cells containing training steps can take a considerable amount of time to run compared to other cells. To save time, I have saved the relevant graphs within the plots folder as html files to maintain their interactive nature.

I recommend starting with the Staff Scheduling notebook as it gives a better overview, whereas the Demand Forecasting notebook can be less user friendly. Alternatively, feel free to simply browse the graphs and schedules in the plots folder.


## Installation & Running the Notebook

* Please clone the repo. All commands in this README are run at the repo level.

* To load the project requirements, I recommend using venv. This project was built using Python 3.6.5. The project requirements are found in requirements.txt and can be loaded when inside of the environment. Alternatively tools such as Conda are popular for working with Jupyter notebooks.

```sh
    python3 -m venv venv
    source venv/bin/activate

    pip install -r requirements.txt (alternatively: python -m pip install -r requirements.txt)
```

* To start the notebook please use the following command to open the notebook in your browser.

```sh
    jupyter notebook (alternatively: python -m jupyter notebook)
```

## Challenge Comments

# Measuring Staffing Effectively - Comments & Concerns

* A model based soley on order frequency may not show us the whole story in terms of staffing. Quite a large number of job tasks fall outside of this (cleaning, stock management, accounts, menu planning etc) and will not be reflected here. Noticeably, managers tend to have had more labour hours during quieter order hours which seems to align with this idea.

* Additionally, I have limited my predictive schedules to the opening hours only, as we see few (but not zero) orders outside of opening hours. However, in real life conditions, staff are needed both before and after opening and close and are not captured adequately by these models.

* Sunday through Thursday see a slightly earlier closing time of 30 mins, however as all data is presented at the hour level and we still require staff for the first half of it, I have not treated this timeframe differently. A reduction in orders should be reflected in the staffing requirements.

* We do not have ground truth data to tell us what a 'comfortable' level of staffing is. Understaffing is a real risk, as it would improve on our OPLH metric temporarily, however that would not be sustainable long term. Feedback from customers as to the maintainability / perceived 'comfort' of staffing levels would be great to incorporate.

* I've included schedules on a total staff basis as well as on a per job role basis. Many restaurants have no overlap in job responsibilities, however some do. Here I was thinking of use cases in smaller operations like cafes/delis/smoothie bars/ice cream bars etc where the staff member taking your order is also the one preparing it. For those types of use cases, using a full staff view may allow for a greater reduction in overstaffing. This reduced schedule may also give us some information on lower bounds where we veer towards understaffing.

* The solution does not take into account the fact that shifts may have a minimum time requirement, and so it may not be possible to just schedule a person for one hour, for example.

* The term 'orders' was not completely clear to me (is this an item, a meal, a table etc, is a soft drink the same as a dinner?). If an order could vary the workload greatly for staff, that too may sway results

# General Comments

* I tried to showcase my ML workflow through this challenge as opposed to simply optimising for results. For example, selecting simple, baseline models can allow you to ramp up on the whole project more quickly. This can allow you to start to gather/request any further data at an earlier date, and potentially receive customer feedback more quickly as to what matters in real life scenarios. Iterating on the models themselves for greater accuracy is something I would tackle as a next step, and is also something that benefits from more time due to long training times.

* The challenge took longer than anticipated. In ML, shortcutting on data exploration can be risky as it can have hidden effects through lack of understanding. A model may look good in theory due to a certain metric, but without visualisations you may be optimising for the wrong thing. ML projects tend to be long and can be hard to plan for as accurately as general software projects as they are often dictated by the data itself. It is also costly time wise to train models, particularly more complex ones and especially when working on local devices.

* Code quality, particularly in the forecasting notebook, is something I would improve upon. Due to time constraints there are some shortcuts taken, whereas the notebooks could benefit from more repeatable code, better annotating etc