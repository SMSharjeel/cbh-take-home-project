# Ticket Breakdown
We are a staffing company whose primary purpose is to book Agents at Shifts posted by Facilities on our platform. We're working on a new feature which will generate reports for our client Facilities containing info on how many hours each Agent worked in a given quarter by summing up every Shift they worked. Currently, this is how the process works:

- Data is saved in the database in the Facilities, Agents, and Shifts tables
- A function `getShiftsByFacility` is called with the Facility's id, returning all Shifts worked that quarter, including some metadata about the Agent assigned to each
- A function `generateReport` is then called with the list of Shifts. It converts them into a PDF which can be submitted by the Facility for compliance.

## You've been asked to work on a ticket. It reads:

**Currently, the id of each Agent on the reports we generate is their internal database id. We'd like to add the ability for Facilities to save their own custom ids for each Agent they work with and use that id when generating reports for them.**


Based on the information given, break this ticket down into 2-5 individual tickets to perform. Provide as much detail for each ticket as you can, including acceptance criteria, time/effort estimates, and implementation details. Feel free to make informed guesses about any unknown details - you can't guess "wrong".


You will be graded on the level of detail in each ticket, the clarity of the execution plan within and between tickets, and the intelligibility of your language. You don't need to be a native English speaker, but please proof-read your work.

## Your Breakdown Here

### (Ticket-1) Update An Agent Table ( to allow custom Ids)

As an admin user, I want to update the Agent table to allow Facilities to save their own ids for each agent they work with, so that we can use that id when generating reports for them.

- Acceptance Benchmarks:
  - A new column called `facility_agent_id` must be added to the Agent Table to store custom ids
  - Update Agents Apis to allow the custom id to be set or updated by the Facilities
  - Ensure custom id is unique and is being stored in a database

- Time estimation : 4-5 hours

- Implementation details:
  - Use database migration to add `facility_agent_id` column to Agent Table
  - Modify Agent Api to  accept custom id as input and update  `facility_agent_id` in Agent Table
  - Create a method to generate a unique id such as (contain alphanumeric unique characters of certain length)
 
### (Ticket-2) Modify the Shifts Table to use CustomId

As an admin user, I want to modify the Shifts Table to use the custom id for Agents that was set by Facilities so that we can generate reports for them with the custom id.

- Acceptance Benchmark:
  - Modify the Shifts table to reference the `facility_agent_id` column in the Agent table instead of the id column
  - Modify the `getShiftsByFacility` function to return the custom id for each Agent assigned to each Shift
  - Ensure that the report generation function (generateReport) uses the custom id instead of the internal database id

- Time  estimation: 4 hours

- Implementation details:
  - Use a database migration to modify the Shifts Table to reference the `facility_agent_id` column in the Agent table.
  - Update the `getShiftsByFacility` function to ( join if SQL / include if NOSQL ) the Agent table and return the `facility_agent_id` column instead of the id column for each Agent assigned to each Shift.
  - Modify the `generateReport` function to use the custom id instead of the internal database id when generating the report.

### (Ticket-3) Modify the report interface to display custom id

As a Facility User, I want to see the custom id of each Agent on the report Ui so that I can submit the report with the correct information.

- Acceptance Benchmark:
  - Modify the report (Ui) to display the custom id of each Agent with respect to their name
  - Make sure that the custom id is displayed in an appropriate readable way.
  - Testing will need to be done to ensure that the report UI accurately displays the correct agent ids on the report

- Time estimation: 2 hours

- Implementation details:
  - Modify the report (Ui) to display the custom id of each Agent with respect to their name
  - Make sure that the custom id is displayed in an appropriate readable way.


### (Ticket-4) Update the Report API to accept Custom id Parameter

As a facility User, i want to submit reports using the custom id of each Agent instead of their internal database id so that the report is accurate.

- Acceptance Benchmark:
  - Modify the report API to accept the custom id of each Agent instead of their internal database id
  - Update the report generation function `generateReport` to accept the custom id as input instead of the internal database id

- Time estimation: 4 hours  

- Implementation details:
  - Modify the report API (GET, PUT, POST, DELETE) to accept the custom id of each Agent instead of their internal database id
  - Update the report generation function `generateReport` to accept the custom id as input instead of the internal database id


