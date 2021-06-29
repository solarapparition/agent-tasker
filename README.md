
## Guiding Principles:

### Agents:
- Agents are representatives of a task, i.e. each agent is responsible for tracking and completing a task; any tasks that agents receive beyond its first will get allocated to subagents
- Agents can only send tasks to either its own subagents, or to agents that are explicitly able to receive requests from any agent
- Agents communicate by posting and reading messages
- Agents _can_ post priority and dependency updates to non-subagents
- Agents can also send messages to event boards

### Tasks:
- When splitting tasks, each task must be split into items that are independent of each other

### Messages:
- Messages are posted to the message board by agents; they provide a way to track the communications between agents
- Priority Updates: Increases or decreases priority on tasks

### Bots:
- Unlike agents, bots do not communicate or respond to messages, but to events that are posted on the event board
- Bots act in the background and should not interact much with humans

### Events/Triggers:
- Events represent things of interest that have occurred, and are a way to fulfill triggers, which are things that a bot is on the lookout for
- Events and triggers have their own boards
- Events will be posted every round, and will be archived after a round
- Each trigger on the trigger board will be allocated to a bot that will be on the lookout for events that fulfill the trigger
- Individual bots may also have their own private triggers

### Weavers/Workstreams:
- Workstreams are sequences of tasks created from a source set of task lists through filtering and reordering
- Workstreams are generated by bots called Weavers
- Workstreams can include other workstreams as their source


## Roadmap:

#### v.0.3.12:
- performance: reorder subagents so that older agents are used first

### Minor Updates, Bugs, and Cleanup:
- performance: make it so that not every agent have to read messages in each round
- prod: clean up prod inactive messages
- add ability to set time for task
- bug: dependents being complete outputs an error
- docs: add instructions
- menu: add ability to split tasks and set dependency with same input option
- testing: create debug option in menu
- testing: add tests as option in debug menu
- remove reference to specific human agents (i.e. jcha)
- agents: update save to be async (needs to make sure this doesn't break anything)
- messages: convert message board into swarm system
- messages: optimization: board fetches messages as needed, and saves messages asynchronously
- convert agent runner to be a swarm under Overmind
- add ability to rename task aliases
- add ability to specify time in terms of hours from now
- add ability to send and display notes for tasks
- add ability to display task chain (trace back to parent tasks)

### v.0.x: Workstreams:
- workstreams: create triggers workstream
- agents: create task sequences
- workstreams: create tier-based workstream
- workstreams: create comms stream and plug into overweave (does not include slack)
- workstreams: reorder overweave based on the "all" stream
- workstreams: make next task option pull from overweave instead of all tasks
- workstreams: add 40-min cooldown ability to comms stream
- workstreams: adjust comms cooldown depending on time of day
- workstreams: create documentation stream and plug into overweave
- workstreams: create side weaver (documentation, etc.)
- workstreams: add ability to inactivate workstream based on current time

### v.0.x: Time, Events, and Triggers:
- utils: create isTimeFormat function
- agents: if agent receives task that is in isTimeFormat(), then instead of forwarding it to a human agent, it'll post a request to the triggers board, which will get picked up by a trigger bot
- events: create event board
- events: remove old events at the start of new round
- triggers: create triggers board, where trigger requests get picked up by trigger bots
- bots: bot.act() reads off events every round and checks whether it fulfills one of its triggers
- events: save completed tasks: interfacer posts task completion event after receiving task completion message
- bots: save completed tasks: add task saver bot (save switch is in globals)

### v.0.x: Priority System:
Implement priority system (value = importance/effort, urgency = effort/time, 2-day urgency)
- processing: user can send add_processing_info messages
- processing: user can set keywords during processing
- priority system: user can set importance rating during processing
- priority system: user can set effort rating during processing
- priority system: system can organize tasks by value (undefined first)
- priority system: system can send out next most valuable task
- priority system: system can send out next oldest task
- priority system: user can set target time during processing
- priority system: system can organize tasks by urgency (undefined first)
- priority system: system can send out next most urgent task
- priority system: system automatically switches between modes: urgency -> value -> age

### v.1.0: Origin:
- add ability to execute sequence of tasks (probably via workstream system)
- implement recurring tasks (add new option to mark recurring task as done)
- convert to TypeScript
- create regression test suite

### Backlog:
- implement mental health checkup system
- create system for tracking current mental state, e.g. energy, stress, etc.
- model other humans agents as recipients
- model other humans agents as sources

## Version History:

### v.0.3: Swarms and Bots:

#### v.0.3.11:
- bots: bot.act() now saves bot data automatically to its data file

#### v.0.3.10:
- agents: reordered free subagent list so that it goes from oldest to newest; this should reduce the number of new agents that need to be created and maintained over the long run

#### v.0.3.9:
- bots: updated bots so that they fetch their data during initiation

#### v.0.3.8:
- updated names of files to make more sense for what their actual purposes are
- added tests folder to gitignore (planning to create a different regression suite later)

#### v.0.3.7:
- workstreams: created overweave workstream (currently same as the 'all' workstream)

#### v.0.3.6:
- docs: created roadmap and guiding principles

#### v.0.3.5:
- swarms: updated swarms to use a shared SwarmSystem parent class for shared methods
- tasks: added option in main menu to go to next task

### v.0.2: Human Interface

### v.0.1: Agent Workflow
