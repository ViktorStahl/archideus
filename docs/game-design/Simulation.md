The game runs a simulation loop on the server which is 60 ticks per second (60 Hz). Ticks is the base unit of all time in the game. That does not mean that everything is updated every tick, instead the different functions in the game operate at different frequencies:

| System                            | Frequency |
| --------------------------------- | --------- |
| Heartbeat                         | 60 Hz     |
| Core                              | 20 Hz     |
| Agent engine                      | 1 Hz      |
| Calendar                          | 1/8 Hz    |
| Multiplayer Core Synchronization  | 1/5 Hz    |
| Multiplayer Agent Synchronization | 1 Hz      |
The simulation normally runs with a 1x time scale but the game supports 2x, 4x and 8x as well.
## Heartbeat Frequency
The heartbeat is the games maximum frequency at which it checks for state updates. It is not possible to run cyclic functions more often the heartbeat frequency.
At the moment no function runs at the heartbeat frequency except recording elapsed ticks.
## Core Frequency
Most of the game simulation happens at the core frequency. Systems that run at this speed include:
- Labour availability - Updates the available [Labour](Labour.md) based on families and 
- Construction - Uses available labour to progress construction as detailed in [Construction](Buildings.md#Progress).
## The Calendar Simulation
The game has an annual cycle with 12 months a year and 30 days a months. A day is 480 ticks (8 seconds) and a month 14400 ticks (4 minutes) on 1x time scale.

Each day, resource stockpiles are updated according to the production and consumption levels in the city, see [Consumption and Production](#Consumption%20and%20Production).
## Multiplayer Synchronization
The game uses a separate network timer that is unaffected by time scale to not overload the network with traffic. Most of the simulation is predicted by the clients to make the game run smoothly while keeping the bandwidth requirement down but some states are transmitted by the server to the clients at the multiplayer synchronization frequency.

Important simulation updates are also sent as events to the clients so they can update the local state as soon as they receive the update.
### Core
Synchronization of core game simulation. See [Core frequency](#Core%20frequency).
### Agents
Agent synchronization calls are more frequent to reduce "rubber banding". These updates are path based and can conceptually look like:
```json
{
    "agent_id": 42,
    "path": [
        Vector2(10, 20),
        Vector2(15, 20),
        Vector2(15, 30),
        Vector2(25, 30)
    ],
    "speed": 2.0,
    "start_tick": 15000
}
```
