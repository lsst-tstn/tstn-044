###################
Night Planning Tool
###################

.. abstract::

   This technote describes the design of an integrated night planning tool.
   This is a tool that allows our team to collect a group of Jira tickets describing a set of tests/observations.
   It will also help us organize these into a coherent list that can later be loaded and executed at the summit.

Introduction
============

Test planning and execution for commissioning the Vera Rubin observatory has revolved around using Jira and Confluence to generate a comprehensive plan that can be followed by the night crew.
This process involves a combination of Jira projects:

- SITCOM are used to capture high level tests/verification activities.
  They are usually connected to one or more requirement or some other commissioning activity.
  For example, `SITCOM-1099`_ was created to capture the tests required to validate the operation of the system with the TMA dynamic settings going from 5% all the way to 100% of its requirements.

- DM tickets are used to capture work needed either by a regular contruction deliverable or a commissioning activity.
  DM tickets can be linked to SITCOM tickets when there is work required to accomplish a particular test, but they can also be standalone ticket that are just broadly required.
  For instance, in the example above of `SITCOM-1099`_, we have `DM-39533`_ linked as a related ticket.
  It is not strickly necessary to have this relantionship as `DM-39533`_ represents a broader system functionality, however the issues are linked to demonstrate the relantionship.
  Sometimes a SITCOM ticket might trigger the development of systewide functionality and the relantionship is used to indicate it.

- BLOCK tickets are used to design, plan, execute and track activities at the summit.
  Usually a BLOCK ticket will be linked to a SITCOM ticket.

.. _SITCOM-1099: https://rubinobs.atlassian.net/browse/SITCOM-1099
.. _DM-39533: https://rubinobs.atlassian.net/browse/DM-39533

Up to now, planning activities at the summit have revolved around collecting the BLOCK tickets that will be executed at night and sorting them out in a table with some information about priority and order of execution.
`This page <https://confluence.lsstcorp.org/display/LSSTCOM/2024-04-23+Simonyi+Night+Log>`__ contains the plan for the night of 2024-04-23.

Later, the summit crew adds information to these tables about the execution and are also required to do more detailed logging in LOVE/OLE. 
Gathering information later about task execution and performing traceability under these conditions is taxing.
Users have to peruse the night logs for detailed information and also check the confluence page with the night plan.

In order to improve overal user experience on both sides of the isle; creating and executing the plan, and also to improve metadata extraction for traceability, we propose to introduce a set of new procedures and tools for planning and execution of the summit activities.
 
Planning with Zephyr
====================

We will adopt Jira's Zephyr application to create test cases, test cycles and test plans to organize how tests will be executed and planned.

- BLOCK tickets will be used to describe what the block does, link it to a particular SITCOM ticket and will also aggregate the block configuration.

  See the :external+obsops:ref:`BLOCK project workflow <BLOCK-Jira-Workflow>` documentation for more information.

- Test Cases will have a step by step description of how to execute a particular BLOCK.
  Including instructions to setup/wrap-up.

- Test Cycles will be used to plan a particular night.
  They contain a list of Test Cases, ordered in the same way they should be executed.
  The Environment field is used to separate the Test Cases that will be executed at different parts of the day; Daytime, Afternoon, Early Night, Late Night, etc.

- Test Execution are created for each Test Case to track a particular execution.

- Test Plans contains a collection of Test Cycles and are used for long term planning.

.. figure:: /_static/test_cycle.png
  :name: fig-test-cycle
  :target: ../images/test_cycle.png
  :alt: Test Cycle

  An example Test Cycle showing the planned Test Executions for the Test Cases scheduled for a particular night.
  The Test Executions are sorted in the order they should be executed, sub-divided in two different parts of the day; Late Afternoon and Early Night.

Integration with LOVE
=====================

As an initial fallback mode, we expect the summit crew would be able to interact directly with the Test Cycle in Jira to execute a night plan.
However we have the potential to considerably improve the user experience by integrating the Test Cycle with LOVE.

The idea would be to provide an interface in LOVE similar to that of the Jira Test Player.
Through this interface users would be able to:

- Select the plan for the night.

  This could be a drop down menu that shows the list of Test Cycles from Jira.

  Uppon selection of a particular Test Cycle, users would be presented with the list of Test Executions, ordered like they appear in the Test Cycle.

- Select a Test Execution from the night plan.

  This would present the users with the Test Player interface, showing information about the particular tests and the steps that need to be executed.

- Start and run a Test Execution.

  If the test steps are correctly configured with the required script information, users will be able to send these to the ScriptQueue directly from the test step.
  The test step will also monitor the relevant information and back feed that into the Test Execution.
  This means that, if a block fails to execute, the test step will be marked as failed.

- Log information from a step execution and or the Test Execution.

  Each step in the Test Execution will also have an input text box that can be used to log entries in OLE.
  The system should use metadata provided in the Test Execution to augment the narrative log entry with additional labels, etc.

  The high level Test Execution will also have an input text box to create log entries.

- Feed the information back to Jira.

  All metadata generated at the summit by this tool will be fed back to jira to allow for better traceability.

FAQ
===

.. note::

  This session is to capture any discussion points made while reviewing this document.
  Things here can be deleted afterwards if incorporated to the document or kept for historical reasons.

- On the relantionship between BLOCK tickets and Test Cases:

  - Do we need BLOCK tickets if we have Test Cases?

    - Should we always have a BLOCK ticket associated with a Test Case?

    - What information should go on a BLOCK ticket and what should go in the Test Case?

- What are the values for the "Environment" field we should adopt and how are we going to use it?

  Current suggestion is to use it as a "time block aggregator" with the following values:

  - Time Critical

  - Daytime

  - Late Afternoon

  - Early Night

  - Mid Night

  - Late Night

  - End Night

