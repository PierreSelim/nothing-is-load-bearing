# Jargon index

Over 400 terms, grouped by the domain each one borrows its picture from. For every entry:
what the metaphor literally depicts, and what to write instead.

The middle column matters more than it looks. Naming the source image is what
makes the emptiness visible: "the foundation is solid but there is plumbing to
do" is two building metaphors in one sentence, and once you see that, you see
the sentence contains no engineering.

A term in this index is not banned. Run the three questions in SKILL.md first —
several entries below are genuine terms of art inside their own domain, marked
**(term of art in X)**, and inside X they stay.

## Contents

1. [Construction and structural engineering](#1-construction-and-structural-engineering)
2. [Demolition, weapons, and war](#2-demolition-weapons-and-war)
3. [Freight, logistics, and shipping](#3-freight-logistics-and-shipping)
4. [Gates, valves, and control panels](#4-gates-valves-and-control-panels)
5. [Water and hydraulics](#5-water-and-hydraulics)
6. [Physics and mechanics](#6-physics-and-mechanics)
7. [Geometry and space](#7-geometry-and-space)
8. [Medicine, biology, and hygiene](#8-medicine-biology-and-hygiene)
9. [Finance and accounting](#9-finance-and-accounting)
10. [Cooking and food](#10-cooking-and-food)
11. [Sport and games](#11-sport-and-games)
12. [Mining, digging, and diving](#12-mining-digging-and-diving)
13. [Navigation and altitude](#13-navigation-and-altitude)
14. [Animals](#14-animals)
15. [Hands, feet, and bodies](#15-hands-feet-and-bodies)
16. [Theatre, magic, and performance](#16-theatre-magic-and-performance)
17. [Roads and traffic](#17-roads-and-traffic)
18. [Electricity, heat, and fire](#18-electricity-heat-and-fire)
19. [Filler, hedges, and throat-clearing](#19-filler-hedges-and-throat-clearing)
- [Narration: text about the text](#narration)
20. [Corporate strategy vocabulary](#20-corporate-strategy-vocabulary)
21. [Sentence shapes that signal the same problem](#21-sentence-shapes-that-signal-the-same-problem)

---

## 1. Construction and structural engineering

The most common family in Claude's technical prose, and the one that gives this
skill its name. The picture is a building: some parts hold weight, some are
decoration, and removing the wrong wall brings down the roof. Software has
dependencies, not weight.

| Phrase | The picture | Write instead |
|---|---|---|
| load-bearing | a wall carrying the floor above | which callers depend on it, and what breaks if it changes |
| nothing is load-bearing | a structure with no structural members | nothing else reads this value; it can be deleted |
| the load-bearing assumption | one wall holding up the house | the design assumes arrivals are monotonic; out-of-order events produce negative delays |
| foundation / foundational | concrete poured first | which later work requires it, and in what order |
| bedrock | rock under the soil | the fact everything else is derived from, stated plainly |
| scaffolding | temporary frame around a build | temporary code, removed when X lands |
| structural change | moving walls | which modules are renamed, split, or deleted |
| brittle | material that snaps | fails when input is empty; three call sites assume non-empty |
| solid / rock-solid | masonry | has tests for all four branches and has run six months without a fault |
| shaky / on shaky ground | bad ground under a building | the claim rests on one unmeasured assumption |
| cracks are showing | masonry failure | three bugs this month, all from the same shared cache |
| plumbing | pipes inside walls | the wiring code that passes the config from CLI to handler |
| wiring / wire up | electrical install | register the handler with the dispatcher |
| girder / backbone | main beam | the module every request passes through |
| the house of cards | unstable stack | each layer assumes the one below validated its input; none does |
| paper over | wallpaper hiding a crack | the fix suppresses the error without correcting the cause |
| papering over the cracks | same | the retry hides a duplicate write |
| green-field / brown-field | undeveloped vs built-on land | new service with no existing callers / existing service with 12 callers |
| blueprint | architect's drawing | the design, the schema, or the plan — say which |
| building blocks | children's bricks | the four components and what each one does |
| bolt on / bolted on | hardware fastening | added after the fact, with no shared type between it and the core |
| retrofit | fitting new parts to an old building | add the field to the existing table and backfill |
| tear down / rebuild from scratch | demolition | delete the module and write a replacement with the same interface |
| cornerstone | first stone laid | the component the rest is designed around |
| pillar | column | one of the three required properties — name them |
| keystone | arch stone | the part whose removal breaks the rest — name what breaks |
| under the hood | car body panel (adjacent) | internally, the function does X |

## 2. Demolition, weapons, and war

The picture is an explosion spreading damage outward by distance, or an army
defending a perimeter. Both are wrong about software: failures travel along
dependency edges, not through space, and systems do not have fronts.

| Phrase | The picture | Write instead |
|---|---|---|
| blast radius | a bomb's damage circle | which services stop working, and which keep working |
| limit the blast radius | containing an explosion | the failure stops at the queue; consumers keep serving stale data |
| nuke it / nuke the table | a nuclear weapon | drop and recreate the table |
| shoot yourself in the foot | self-inflicted gunshot | the API lets a caller pass a landing time before its takeoff |
| footgun | a gun aimed at your foot | the parameter is easy to pass in the wrong order; both are strings |
| battle-tested | survived combat | has run in production for two years under 5k messages/s |
| war room | military command post | a scheduled call during the migration |
| war story | combat anecdote | the incident on 12 March and what it showed |
| fire drill | emergency rehearsal | an unplanned interruption that produced no change |
| firefighting | emergency response | responding to incidents instead of fixing their causes |
| hardened | armoured | input is validated and the service runs without privileges |
| attack surface | exposed flank | **(term of art in security)** — keep; elsewhere, list the exposed endpoints |
| defence in depth | layered fortification | **(term of art in security)** — keep |
| shields up / lock it down | raising defences | restrict the endpoint to authenticated callers |
| kill switch | weapon abort control | a flag that stops the consumer without a deploy |
| tripwire | ambush trigger | an alert that fires when queue depth exceeds 10k |
| in the trenches | infantry position | doing the implementation |
| bulletproof | armour | handles all four documented failure cases |
| take fire / under fire | being shot at | the service is receiving more traffic than it can serve |
| rally the troops | military muster | ask the team |
| scorched earth | burning retreating land | delete everything and start over |
| silver bullet | werewolf-killing ammunition | there is no single fix; here are the three partial ones |
| smoking gun | murder evidence | the log line proving the cause |
| collateral damage | civilian casualties | what else broke, named |
| pick your battles | combat choice | which of these to fix now, and which to leave |

## 3. Freight, logistics, and shipping

The picture is cargo moved through warehouses and docks. Occasionally apt;
usually a way to avoid naming an order of operations.

| Phrase | The picture | Write instead |
|---|---|---|
| front-load | loading weight at the front of a truck | do X before Y, and why that order matters |
| back-load / defer the weight | loading at the rear | do X after Y |
| heavy lifting | cargo handling | which specific work the component does |
| lift and shift | moving cargo intact | copy the service to the new host with no code change |
| pipeline | oil or assembly line | **(term of art in data and CI)** — keep; otherwise name the stages |
| bottleneck | narrow bottle neck | the slowest step, with its measured time |
| throughput | goods per hour | **(term of art)** — keep, with a number and a unit |
| in-flight | cargo in transit | requests sent but not yet answered |
| hand-off | passing a parcel | which component takes over, and what it receives |
| throw it over the wall | tossing cargo to the next yard | the producing team delivers the file with no schema and no contact |
| ship it / shipping | cargo leaving the dock | deploy it / release it |
| the long pole | the longest tent pole | the step with the longest duration — name it and its estimate |
| critical path | project scheduling | **(term of art in planning)** — keep, with the chain named |
| warehouse | storage building | **(term of art in data)** — keep |
| last mile | final delivery leg | the remaining work between the API and the user's screen |
| conveyor belt | factory line | the sequence of steps, named |
| freight train | heavy train | a large change; say how large in files or lines |
| unblock / blocked on | a blocked loading bay | waiting for the schema from team X |

## 4. Gates, valves, and control panels

The picture is a machine operator at a panel of knobs, or a guard at a gate.
These usually hide the actual condition being checked.

| Phrase | The picture | Write instead |
|---|---|---|
| gate (verb) | a gate in a fence | do not deploy until the integration suite passes |
| gate (noun) / quality gate | a checkpoint | the check that must pass, and what it checks |
| gating factor | the thing holding the gate shut | the condition that is not yet met |
| ungate / open the gate | removing the barrier | enable the feature for all accounts |
| lever | a mechanical lever | the one setting that changes the outcome — name it and its range |
| dial / turn the dial | a radio dial | the parameter, with its current and proposed values |
| knob | a control knob | the configuration option, named |
| guardrails | highway barriers | the constraint, and what rejects what |
| escape hatch | submarine exit | a documented way to bypass the check — say who may use it |
| throttle | engine valve | limit to 100 requests per second per client |
| backpressure | pressure against flow | **(term of art in streaming)** — keep |
| circuit breaker | electrical safety device | **(term of art for the pattern)** — keep |
| safety valve | pressure release | what sheds load, and at what threshold |
| rubber stamp | an unread approval | approved without review |
| gatekeeper | a guard | the person or check that must approve |
| single source of truth | one authoritative register | the table that holds the value; everything else derives from it |
| source of truth drift | registers disagreeing | two tables hold the same field and disagree after an update |
| feature flag | a signal flag | **(term of art)** — keep |

## 5. Water and hydraulics

The picture is liquid flowing downhill through channels. The most invisible
family, because so much of it has become ordinary. Some entries are now plain
English; the ones to cut are the decorative ones.

| Phrase | The picture | Write instead |
|---|---|---|
| upstream / downstream | a river | the producer / the consumer, named |
| flows through | current in a channel | which function passes the value to which |
| firehose | fire-fighting hose | 40k events per second with no filter |
| drinking from the firehose | an impossible volume | more events than the consumer can process |
| drain the queue | emptying a tank | process all pending messages before shutdown |
| leak | a leaking pipe | **(term of art: memory leak, connection leak)** — keep; otherwise say what escapes where |
| cascade / cascading failure | a waterfall in steps | **(term of art)** — keep, with the chain named |
| ripple effect | rings on water | what else changes, named |
| trickle in | slow drip | arrives over several minutes rather than at once |
| flood / flooded | water overflowing | receives more requests than it can serve |
| siphon off | drawing liquid out | route 5% of traffic to the new consumer |
| watertight | sealed vessel | the proof covers all four cases |
| sink and source | plumbing fittings | **(term of art in dataflow)** — keep |
| stem the tide | holding back water | stop the growth; say of what, and by what means |
| swamped | flooded land | has more work queued than it can clear |
| a sea of | an ocean | a count: 400 of them |

## 6. Physics and mechanics

The picture is forces, friction, and momentum. Attractive because it sounds
rigorous. Rigour comes from the number, not from the word.

| Phrase | The picture | Write instead |
|---|---|---|
| friction | surfaces rubbing | the three manual steps a user must do |
| frictionless | no resistance | no sign-in and no configuration needed |
| inertia | mass resisting change | nobody has changed the module in two years; nobody knows its tests |
| momentum | mass in motion | the team shipped four of six planned items |
| gravity / centre of gravity | mass attraction | the part of the system most work concentrates in |
| escape velocity | orbital threshold | the point past which the project continues without extra staffing |
| orthogonal | perpendicular axes | **(term of art in mathematics)** — keep there; otherwise: independent, and say in what way |
| impedance mismatch | electrical/acoustic mismatch | the object model has inheritance; the table does not |
| coupling / tightly coupled | joined parts | **(term of art in design)** — keep, naming the dependency |
| degrees of freedom | mechanics/statistics | **(term of art)** — keep; otherwise, which parameters a caller may vary |
| entropy | thermodynamic disorder | the module has gained four unused parameters since its last review |
| phase change / step function | state transition | the behaviour changes discontinuously at N = 1000 |
| critical mass | fission threshold | the number of users at which the effect appears |
| activation energy | chemistry | the setup work needed before the first useful result |
| moving parts | a mechanism | the six components, named |
| machinery | engine | the code that does it |
| lossy / lossless | signal theory | **(term of art)** — keep |
| signal and noise | signal theory | which measurements are informative, and which vary at random |

## 7. Geometry and space

The picture is shapes with area and edges. Used to suggest measurement where
none happened.

| Phrase | The picture | Write instead |
|---|---|---|
| surface area | the outside of a solid | the API exposes 14 public methods; 9 have no external caller |
| reduce the surface area | shrinking a shape | remove the six unused endpoints |
| sharp edges | a dangerous object | the two known failure cases, named |
| rough edges | unfinished surface | the three defects still open |
| corner case | a shape's corner | the specific input: empty list with a non-null cursor |
| edge case | a shape's edge | the specific condition — always name it |
| in the shape of | silhouette | the signature is `(str, int) -> Result` |
| cross-cutting | a cut across layers | **(term of art in aspect-oriented design)** — keep there; otherwise: authentication appears in all six handlers |
| vertical slice | cutting through layers | one feature implemented through API, service, and store |
| horizontal / across the board | spatial direction | affecting all nine services |
| fan-out / fan-in | a folding fan | **(term of art in messaging and task graphs)** — keep, with the number; otherwise name the recipients |
| wide vs deep | dimensions | 200 call sites with one line each / one call site with 200 lines |
| flatten | geometry | remove the nesting; the result is a list of 40 records |
| bounded / unbounded | limits | has a maximum of 1000; has no maximum |
| lands on / lands in | an object coming to rest | is assigned to, is written to, is routed to |
| falls out of | gravity | follows from X, or is produced by X |
| shakes out | sieving | the result once X is measured |
| slots in / drops in | fitting a part | replaces X without changing its callers |
| sits on top of | stacking | calls X; X does not call it |
| lives in / lives at | residence | is stored in `table`, is defined in `module.py` |

## 8. Medicine, biology, and hygiene

The picture is a body that can be healthy, infected, or dying. Hidden cost:
it moralises. "Unhealthy code" invites shame rather than a change list.

| Phrase | The picture | Write instead |
|---|---|---|
| healthy / unhealthy | a body | passing its checks / failing check X |
| health check | medical exam | **(term of art in operations)** — keep |
| heartbeat | pulse | **(term of art in protocols)** — keep |
| anemic | low haemoglobin | **(term of art: anemic domain model)** — keep there; otherwise, say what is missing |
| bloat / bloated | swelling | the bundle is 4 MB; 2.6 MB is unused |
| hygiene / code hygiene | handwashing | formatting, naming, and dead-code removal — name which |
| sanitize | disinfecting | **(term of art for input handling)** — keep |
| toxic | poison | say the behaviour: the function mutates its argument |
| metastasize | cancer spreading | the pattern has been copied into nine files |
| cancer / rot / rotting | disease, decay | the module has no tests and no current owner |
| DNA | genetic code | the design decision made at the start that still constrains it |
| immune to | immunology | unaffected by X, because Y |
| contagion / infected | disease spread | the bad value is copied into every derived record |
| viral | epidemiology | each user invites on average 1.4 others |
| bleeding edge | a cut | released three weeks ago; API not yet stable |
| diagnosis / symptom | clinical terms | the observed failure / the cause |
| triage | emergency sorting | **(term of art in incident work)** — acceptable; otherwise, order the three items |
| post-mortem | autopsy | **(term of art for incident reviews)** — keep |
| organic growth | plant growth | usage grew without a plan; say by how much |
| cross-pollinate | botany | share the approach between the two teams |
| low-hanging fruit | fruit within reach | the three changes that each take under an hour |
| seeds of | planting | the first version already assumed X |
| pruning | gardening | delete the 12 unused flags |
| green shoots | new growth | the first two measurements improved |
| in the weeds | overgrown ground | discussing implementation detail before the interface is settled |

## 9. Finance and accounting

The picture is a ledger with debts, interest, and investments. Mostly
comprehensible, but "debt" has become a way of describing problems without
listing them.

| Phrase | The picture | Write instead |
|---|---|---|
| tech debt / technical debt | borrowed money | the module has no tests and two copies of the retry loop |
| pay down the debt | repayment | add tests to the four untested branches |
| accruing interest | compound interest | each new caller adds another place to change |
| invest in / investment | capital outlay | spend two days on X to save Y |
| ROI / return | investment return | the saving, with a number |
| cost / expensive / cheap | prices | the measured time, memory, or money — give the unit |
| budget | spending limit | **(term of art: error budget, latency budget)** — keep, with the number |
| amortized | spreading a cost | **(term of art in algorithms)** — keep |
| place a bet on | gambling | choose X, accepting that Y becomes hard if it is wrong |
| priced in | market pricing | already accounted for in the estimate |
| bang for the buck | value for money | the change takes a day and removes 60% of the errors |
| sunk cost | unrecoverable spend | **(term of art in economics)** — keep when it is the actual argument |
| free / comes for free | no price | needs no extra code, because X already does it |
| expensive to undo | cost of reversal | reversing it requires a data migration |
| one-way door / two-way door | reversibility | reversible: a flag flip. Irreversible: a schema change with backfill |
| write it off | accounting | stop maintaining it; it has no users |
| opportunity cost | economics | the two weeks spent here are not spent on X |

## 10. Cooking and food

The picture is a kitchen. Rarely says anything; almost always deletable.

| Phrase | The picture | Write instead |
|---|---|---|
| bake in / baked in | baking an ingredient into dough | the value is fixed at build time and cannot be changed later |
| half-baked | underdone | the design does not cover the duplicate-delivery case |
| secret sauce | a proprietary recipe | the specific algorithm — or say it is undocumented |
| boil the ocean | an impossible task | the scope as written covers all nine services; start with one |
| recipe | cooking instructions | the procedure, as numbered steps |
| ingredients | recipe parts | the inputs, named |
| vanilla | plain ice cream | with no modifications to the default configuration |
| flavours of | varieties | the three variants, named |
| bread and butter | staple food | the common case, which is 95% of requests |
| meat of it | the main part | the part that matters: X |
| marinate / let it sit | soaking in sauce | decide after the migration finishes |
| soup to nuts | a full dinner | from receipt of the event to the stored delay |
| cherry-pick | selecting fruit | **(term of art in git)** — keep; otherwise, say which items and why |
| dogfooding | eating one's own dog food | the team uses it for its own work |
| a slice of | portioning | a subset: the 200 flights in one region |
| spoon-feed | feeding a child | the API requires the caller to pass each field separately |
| sandwich | layered food | between X and Y |
| alphabet soup | a jumble of letters | the four acronyms, expanded |

## 11. Sport and games

The picture is a match with rules, scores, and goals. Frequently combined with
corporate strategy vocabulary and doubly empty.

| Phrase | The picture | Write instead |
|---|---|---|
| table stakes | minimum poker bet | required; without it the feature is unusable because X |
| moving the goalposts | changing a pitch mid-game | the requirement changed after the design was agreed |
| level playing field | a flat pitch | the same limits apply to all clients |
| home run / slam dunk | baseball, basketball | say the measured result |
| punt on it | kicking downfield | defer it; say until when and what decides |
| own goal | scoring against yourself | the change caused the failure it was meant to prevent |
| ball is in their court | tennis | waiting for team X to reply |
| play ball | agreeing to a game | agree to X |
| in our court / out of our hands | tennis | ours to decide / theirs to decide |
| par for the course | golf | typical; say what the typical value is |
| the ball is rolling | momentum in play | the first step is done |
| quick win | easy point | a change that takes under an hour and removes X |
| endgame | chess | the final state, described |
| zero-sum | game theory | **(term of art)** — keep when it is the actual argument |
| playbook | a team's set plays | the written procedure |
| goalpost / north star metric | goal markers | the metric, with its target number |
| raise the bar | high jump | the new minimum requirement, stated |
| skin in the game | a wager | they bear the cost of the failure too |
| hail mary | desperate pass | an attempt with no expectation of success — say why it is tried |

## 12. Mining, digging, and diving

The picture is going below a surface to extract something. Signals effort
rather than describing it.

| Phrase | The picture | Write instead |
|---|---|---|
| deep dive | a diver going down | measured X over seven days / read all 40 call sites |
| dig into | excavation | read, measure, or trace — say which |
| drill down | boring into rock | break the number down by region |
| surface (verb) | bringing to the surface | show the error in the response, with its code |
| unearth | digging up | found |
| mine the logs | ore extraction | search the logs for X |
| rabbit hole | a burrow | the investigation ran four hours with no result |
| tip of the iceberg | hidden mass | the two visible cases, with N more suspected — give N or say unknown |
| gold mine / goldmine | rich ore | the dataset contains X, which answers Y |
| excavate | archaeology | read the history to find when X changed |
| peel back the layers | onion (adjacent) | trace the call from handler to store |
| scratch the surface | superficial | this covers 2 of the 9 cases |

## 13. Navigation and altitude

The picture is a map and a vantage point. "Zoom out" and "altitude" are the
Claude tics in this family.

| Phrase | The picture | Write instead |
|---|---|---|
| north star | polar navigation | the goal, stated as a measurable target |
| roadmap | a route map | the planned work, with dates or order |
| compass / true north | navigation instrument | the decision rule, stated |
| zoom out / zoom in | camera or map scale | state the broader claim, or the specific one |
| 10,000-foot view / bird's-eye view | aerial height | the summary, in one sentence |
| at a higher altitude | flight level | more general: say the general claim |
| lay of the land | terrain survey | what exists now, listed |
| line of sight | visibility | a path from here to X, with the steps |
| off the beaten path | an untrodden route | an uncommon configuration; say which |
| uncharted territory | an unmapped region | no prior example; the risk is X |
| course correct | changing heading | change the plan: do X instead of Y |
| in the loop / out of the loop | circuit (adjacent) | informed / not informed — name who |
| on track / off track | railways | ahead of or behind the stated date |
| waypoint / milestone | route markers | the dated checkpoint, with its exit condition |
| the map is not the territory | cartography aphorism | the schema does not match the stored data; here is the difference |

## 14. Animals

The picture is livestock, pests, or wildlife. A few are established names for
real phenomena; most are decoration.

| Phrase | The picture | Write instead |
|---|---|---|
| canary | a mine canary | **(term of art: canary release)** — keep |
| thundering herd | stampeding cattle | **(term of art)** — keep: all consumers retry at the same instant |
| herding cats | an impossible task | coordinating nine teams with no shared schedule |
| bikeshedding | arguing over a bike shed | the review spent its time on naming and not on the retry logic |
| yak shaving | an absurd prerequisite chain | the change needs three unrelated upgrades first — list them |
| elephant in the room | an ignored obvious thing | the unaddressed problem: X |
| white whale | Moby-Dick | the long-pursued goal that keeps failing — say why it failed |
| unicorn | a mythical animal | a case that may not exist; say whether it has been observed |
| dogpile | dogs swarming | all clients retry at once, multiplying load |
| straw man | a scarecrow | a deliberately weak version, offered for comparison |
| swarm on it | insects | several people work on it at once |
| cash cow | dairy farming | the product that earns most of the revenue |
| chicken and egg | the old puzzle | X needs Y and Y needs X; break it by Z |
| boiling the frog | a folk claim about frogs | the value grew 2% a week and nobody noticed |
| rat's nest | tangled rodent nest | 14 modules import each other in a cycle |
| squirrelled away | hoarding | stored in an undocumented place: X |
| bikeshed-free | as above | the review covered the retry logic |

## 15. Hands, feet, and bodies

The picture is a person doing manual work. Mild, and often invisible for that
reason.

| Phrase | The picture | Write instead |
|---|---|---|
| hand-wavy / hand-wave | waving a hand | the argument skips the step where X is proven |
| hand-rolled | made by hand | written here rather than taken from the library |
| hands-off / hands-on | touching | automatic / requires a person to run it |
| heavy lifting | lifting weight | the specific work done — see §3 |
| headroom | space above the head | the system runs at 40% of its measured capacity |
| legwork | walking | the preparation, named |
| muscle memory | motor learning | the team already knows the pattern from X |
| skeleton / skeletal | bones | a version with the interfaces and no implementations |
| backbone | spine | the component every request passes through |
| nerve centre | nervous system | the coordinator, named |
| arm's length | distance | separate: no shared types between them |
| finger on the pulse | taking a pulse | monitoring X; name the measurement |
| shoulder the cost | bearing weight | which component pays the cost, in what unit |
| bend over backwards | contortion | the workaround takes four extra steps |
| rule of thumb | thumb measurement | the heuristic, stated, with its error range |
| elbow grease | manual effort | two days of manual work |
| sleight of hand | conjuring | the step that hides the real cost: X |

## 16. Theatre, magic, and performance

The picture is a show with hidden mechanics. Useful signal that an explanation
is missing.

| Phrase | The picture | Write instead |
|---|---|---|
| magic / it just works | conjuring | what actually happens, in one sentence |
| magic number / magic string | conjuring | the literal 3600, which means one hour — name it as a constant |
| smoke and mirrors | stage illusion | the demonstration used fixed data, not live input |
| behind the curtain | backstage | internally, X happens |
| dog and pony show | a novelty act | a demonstration with no measurement |
| waving a wand | magic | the step with no implementation yet |
| dial it up to eleven | a film joke | the setting's maximum value, which is X |
| break a leg | theatre superstition | — delete |
| the big reveal | stage climax | the result: X |
| showstopper | an act that halts a show | a defect that blocks release; name it |
| curtain call | end of a show | the final step |
| choreographed | dance | the ordered sequence, listed |
| orchestration | conducting | **(term of art in deployment)** — keep |

## 17. Roads and traffic

The picture is vehicles on a road network. Overlaps with logistics; the
distinguishing image is lanes and junctions.

| Phrase | The picture | Write instead |
|---|---|---|
| on-ramp / off-ramp | motorway junctions | how a new user starts / how they stop |
| paved road / paved path | a made road | the supported configuration, documented |
| golden path / happy path | an easy route | one in-order sequence with all fields present |
| sad path / unhappy path | the hard route | the error cases, each named |
| swim lanes | pool markings (adjacent) | who does which part |
| fast lane / slow lane | traffic lanes | priority queue for X; everything else in the default queue |
| roadblock | a barrier | what is blocking it, and who can clear it |
| detour / workaround | an alternative route | the temporary route: X, until Y lands |
| speed bump | a traffic calming device | a step that adds a day |
| merge conflict | traffic merging | **(term of art in version control)** — keep |
| rubber meets the road | tyres on tarmac | in the running system, X happens |
| drive-by | passing vehicle | a small unrelated change in the same commit |
| wheels coming off | vehicle failure | the measured failure: X |
| in the driver's seat | driving | who decides |
| hit the brakes | braking | stop the rollout |

## 18. Electricity, heat, and fire

The picture is current, temperature, and combustion.

| Phrase | The picture | Write instead |
|---|---|---|
| hot path / cold path | heat from use | the code run on every request / the code run rarely |
| hot spot | heat concentration | the function with 60% of measured CPU time |
| cold start | an unwarmed engine | the first request after deploy takes 900 ms |
| warm up / warming the cache | heating | prefill the cache before taking traffic |
| burn down / burn rate | combustion | the remaining work, with the rate it is being completed |
| on fire | burning | failing: say which component and how |
| fan the flames | fire tending | the retry makes the overload worse |
| short-circuit | electrical fault | return early, before X runs |
| wired / plugged in | electrical connection | connected to X via Y |
| power user | electrical power | a user who uses X and Y; say which features |
| spark joy | a tidying slogan | — delete |
| light a fire under | urgency | set a date |
| smouldering | slow fire | an unfixed problem that produces one failure a week |

## 19. Filler, hedges, and throat-clearing

Claude's most frequent tic in technical documents. Each phrase announces that a
point is coming rather than making it. Deleting them changes nothing, which is
the proof.

| Phrase | Write instead |
|---|---|
| it is worth noting that | — delete; state the fact |
| it is important to note | — delete |
| crucially | — delete |
| fundamentally | — delete |
| at its core | — delete |
| essentially | — delete |
| in essence | — delete |
| the key insight is | — delete; state the insight |
| the crux of it is | — delete |
| that said / that being said | but, or delete |
| to be clear | — delete |
| arguably | — delete, or give the argument |
| in many ways | — delete |
| truly / genuinely / really | — delete |
| quite / rather / fairly | — delete, or give the number |
| a number of | the count |
| various | the list |
| several considerations | the considerations, listed |
| there are trade-offs here | the trade-off: X costs Y |
| this is a balance | the two things balanced, and the chosen point |
| depends on your use case | the rule: use X when Y, otherwise Z |
| broadly speaking | — delete |
| by design | the design decision, stated |
| for free | needs no extra code, because X |
| needless to say | — delete |
| as we all know | — delete |
| in today's landscape | — delete |
| at the end of the day | — delete |
| when all is said and done | — delete |
| moving forward | from now on, or delete |
| going forward | as above |
| in order to | to |
| the fact of the matter is | — delete |
| let me be precise | — delete; be precise |
| I should mention | — delete; mention it |

## Narration: text about the text <a id="narration"></a>

The text announces, previews, or summarises itself instead of saying the thing.
The announcement can always be deleted; the sentence after it is the content.

| Phrase | Write instead |
|---|---|
| This section describes / explains / covers X | — delete; start with X |
| In this document we will | — delete |
| Let's walk through / dive into / unpack | — delete; walk through it |
| Below we outline / The following explains | — delete |
| As we will see / as discussed above / as mentioned earlier | — delete, or link the section |
| Here's how it works: | — delete; say how it works |
| Let me explain | — delete; explain |
| In summary / To recap / In conclusion / Overall | — delete; the summary is the first paragraph |
| The goal of this section is to | — delete |
| Now that we have covered X, let's turn to Y | — delete; start Y |
| It's worth walking through | — delete |
| What follows is | — delete |

## 20. Corporate strategy vocabulary

Borrowed from management decks. In a technical document it reads as evasion,
because it names actions without naming actors or objects.

| Phrase | Write instead |
|---|---|
| leverage (verb) | use, or read from, or call |
| unlock | with this in place, X becomes possible — name X |
| enable / empower | lets the user do X |
| align / alignment | agree; say who agreed to what |
| socialise the idea | send the design to X for comment |
| circle back | return to this on a date |
| touch base | ask them |
| drive / drive forward | do it, or name who is responsible |
| double down | continue with X, adding Y |
| best practice | the practice, with its source |
| synergy | the specific shared component or saved work |
| low-hanging fruit | the three changes that each take under an hour |
| quick wins | as above |
| holistic | covering all of X, Y, Z — name them |
| end-to-end | from receipt of the event to the stored result |
| strategic | the goal it serves, stated |
| mission-critical | what stops if it stops |
| game-changer | the measured difference |
| paradigm shift | what changed, in one sentence |
| north-star metric | the metric and its target |
| stakeholder | the named team or person |
| actionable | the action, stated |
| deliverable | the artefact: a document, a service, a dataset |
| bandwidth (of people) | available time: two days this week |
| wear many hats | does X and Y |
| tiger team | the three people assigned |
| shift left | run the check earlier: at commit, not at release |
| day 2 operations | the operational work after launch: upgrades, backups, on-call |
| single wringable neck | the one named owner |
| disagree and commit | decided against X's objection; X is implementing it |
| boil it down | summarise |
| at scale | at the stated load: 5k messages/s |
| future-proof | survives change X without a rewrite — name X |
| 10x | the measured factor |

## 21. Sentence shapes that signal the same problem

Beyond single phrases, some sentence patterns are empty by construction. They
appear in Claude's technical writing often enough to be worth naming.

| Shape | Example | What to do |
|---|---|---|
| The X does the heavy lifting | "The scheduler does the heavy lifting here." | List the work: resolves aliases, applies offsets, writes the row. |
| X is doing a lot of work | "That one line is doing a lot of work." | Say what the line does, and why it is surprising. |
| X is what makes Y possible / X is what lets us Y | "The per-source map is what makes the precedence rules work." | Name the mechanism: "Rules 3 and 4 compare two sources' reports, so both must be stored." This is *load-bearing* turned inside out — see the note below the table. |
| X is essential / critical / key to Y | "Ordering is critical to correctness." | Say what goes wrong without it: "out-of-order messages produce negative delays." |
| This buys us X | "This buys us flexibility." | Name the specific later change it permits. |
| Cheap to do, expensive to undo | — | State the cost of each, in days or in migrations. |
| It is not that X, it is that Y | "It's not that it's slow, it's that it's unpredictable." | Keep only if you then give both numbers. |
| Rule-of-three list of adjectives | "simple, fast, and reliable" | Replace each with its measurement, or drop the ones you cannot measure. |
| X, but Y — and that is the point | — | Delete the flourish; keep the claim. |
| The real question is | — | Ask the question. |
| There are two kinds of X | — | Keep only if the division is exhaustive and useful; otherwise it is a rhetorical frame. |
| Think of it as a Y | "Think of the queue as a conveyor belt." | Keep only for teaching an unfamiliar reader, and only once; never as the definition. |
| Everything is a trade-off | — | Delete. Then state this trade-off. |

The common thread: each shape promises a payoff in the next clause and then
does not deliver one. When you catch yourself writing one, the sentence after
it is the one that was supposed to be the document.

### Where the banned word goes

Removing a metaphor does not remove the missing claim — it relocates it. Someone
who has stopped writing "the config loader is load-bearing" will write "the
config loader is what makes the retry path work", which asserts exactly as
little. The emptiness moves out of the adjective and into the justification
clause.

So after a pass over the term list, read the document again for sentences whose
job is to explain *why* a choice was made. Each one should contain a mechanism —
a call, a comparison, a stored value, a failure — and not just a claim of
importance. This is the most common way a document passes a jargon check and
still says nothing.
