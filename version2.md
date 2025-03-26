# Roblox FFlag Optimization Guide

## What are FFlags?
FFlags (Fast Flags) are internal configuration variables used by Roblox engineers to enable, disable, or tune features and systems within the Roblox client and server. They allow for A/B testing, gradual rollouts, and performance experimentation. Modifying these flags *can* alter client behavior, potentially affecting performance, visuals, and network interaction. Use them with caution, as incorrect values can lead to instability, bugs, or unexpected behavior.

---

## Data Types and Expected Values

FFlags come in various types, each expecting a specific kind of value:

**Integer-based Flags:**
*   **Prefixes:** `DFInt`, `FInt`, `SFInt`
*   **Expected values:** Whole numbers (Integers)
*   **Maximum values (typical):**
    *   64-bit integer: `9223372036854775807`
    *   32-bit integer: `2147483647`
    *   16-bit integer: `32767`
> [!NOTE]
> The actual maximum may depend on the specific implementation within Roblox. The 32-bit maximum is commonly encountered.

**Boolean-based Flags:**
*   **Prefixes:** `FFlag`, `DFFlag`, `SFFlag` (can sometimes be boolean)
*   **Expected values:** `true` or `false`

**String-based Flags:**
*   **Prefixes:** `FString`, `DFString`
*   **Expected values:** Text strings, which can include:
    *   URLs
    *   Arbitrary text identifiers

**Log-based Flags:**
*   **Prefixes:** `DFLog`, `FLog`
*   **Expected values:** Often used like Booleans (`true`/`false`) or Integers in practice, though potentially intended for byte-based data.

---

## Types of FastFlags

The prefix of an FFlag indicates its behavior regarding updates and synchronization:

*   **`F` (Fast):** A static variable initialized once when the Roblox session starts. Its value does not change during the session.
*   **`DF` (Dynamic Fast):** A dynamic variable whose value can be changed by Roblox servers during runtime. The client typically checks for updates approximately every 5 minutes.
*   **`SF` (Synchronized Fast):** A variable loaded by the server and sent to the client, ensuring consistency across clients connected to the same server instance.

---

## FFlag Components

The middle part of an FFlag name often indicates the data type:

*   **`Flag`:** Boolean values (`true`/`false`).
*   **`Int`:** Integer values.
*   **`String`:** Text or URL-based string values.
*   **`Log`:** Typically used for Boolean or Integer values related to logging levels or features.

---

## Flag Categories (Implementation Level)

While less relevant for modification, flags can be categorized by where they are primarily implemented:

*   **Lua:** The majority of Roblox flags affect the Lua VM environment and scripts.
*   **C++:** A smaller subset impacts the core C++ engine code.
*   **UserFlag:** A niche category, likely for user-specific experiments or settings.

---

## Discussed FFlags

Below are details on specific FFlags discussed, including their purpose, defaults, and potential effects when modified.

### Task Scheduler Configuration

These flags control the behavior of Roblox's internal task scheduler, which manages various operations per frame cycle.

*   **Flags:**
    *   `FIntTaskSchedulerTasksDefaultMaxCountPerCycle`
    *   `FIntTaskSchedulerTasksDefaultMaxTimeMsPerCycle`

*   **JSON Example:**
    ```json
    {
       "FIntTaskSchedulerTasksDefaultMaxCountPerCycle": "2147483647",
       "FIntTaskSchedulerTasksDefaultMaxTimeMsPerCycle": "0"
    }
    ```

*   **Purpose:**
    *   `MaxCountPerCycle`: Sets the maximum *number* of tasks the scheduler attempts to process in a single cycle.
    *   `MaxTimeMsPerCycle`: Sets the maximum *time* (in milliseconds) the scheduler spends executing tasks within a cycle.

*   **Default Values:**
    *   `MaxCountPerCycle`: `16`
    *   `MaxTimeMsPerCycle`: `10`

*   **Recommendations & Effects:**
    *   **`MaxCountPerCycle`:**
        *   **Higher Value (e.g., `2147483647`):** Allows more tasks per cycle, potentially increasing responsiveness and reducing task execution latency. Generally recommended unless encountering issues.
        *   **Lower Value:** Limits tasks per cycle, which can introduce delays if many tasks are pending, but may reduce CPU load variation.
    *   **`MaxTimeMsPerCycle`:**
        *   **Higher Value:** Allows more time for tasks within a cycle, potentially improving throughput for task completion but could increase the latency for tasks waiting for the *next* cycle if one cycle takes the full allowed time. May help responsiveness in games with demanding tasks.
        *   **Lower Value (e.g., `0` effectively removing time limit, needs testing):** Prevents individual cycles from taking too long due to demanding tasks, potentially leading to smoother frame rates by distributing work more evenly, but might delay completion of longer tasks. Game-dependent and requires individual testing.


> [!WARNING]
> Increasing `MaxCountPerCycle` can increase CPU overhead. Setting `MaxTimeMsPerCycle` inappropriately (too high or too low for the system/game) can potentially cause stutters or slowdowns. Benchmarking is difficult; effects are often judged by perceived visual latency and smoothness.

*   **Related Links:**
    *   [Roblox Task Scheduler Documentation](https://create.roblox.com/docs/reference/engine/classes/TaskScheduler)
    *   [Roblox Microprofiler Task Scheduler](https://create.roblox.com/docs/studio/microprofiler/task-scheduler)

### Network Bandwidth Management

These flags influence how Roblox manages outgoing network bandwidth, particularly throttling different data streams.

*   **Flags:**
    *   `DFIntBandwidthManagerDataSenderMaxWorkCatchupMs`
    *   `DFIntBandwidthManagerApplicationDefaultBps`

*   **JSON Example:**
    ```json
    {
       "DFIntBandwidthManagerDataSenderMaxWorkCatchupMs": "10",
       "DFIntBandwidthManagerApplicationDefaultBps": "128000"
    }
    ```

*   **Purpose:**
    *   `ApplicationDefaultBps`: Sets a baseline bandwidth budget (Bytes per second) for application-level data (e.g., `RemoteEvent` traffic, shown as "Out Data" in Shift+F3). Helps prevent application data from consuming all bandwidth needed for core physics replication ("Out Physics").
    *   `DataSenderMaxWorkCatchupMs`: Defines the maximum time (in milliseconds) the network sender can spend processing backlogged data in one go if it falls behind. This acts as a throttle to prevent massive data bursts after a pause, smoothing network output.

*   **Default Values:**
    *   `ApplicationDefaultBps`: `64000`
    *   `DataSenderMaxWorkCatchupMs`: `20`

*   **Recommendations & Effects (`DataSenderMaxWorkCatchupMs`):**
    *   **Lower Value:** Reduces the potential size of catch-up bursts, leading to smoother network output generally, but might take longer to fully catch up after a significant delay (less stable recovery).
    *   **Higher Value:** Allows larger catch-up bursts, enabling faster recovery after delays (more stable recovery), but these bursts could potentially cause temporary bandwidth saturation or perceived lag spikes.
    *   **Value `0`:** Reportedly causes significant ping increases and is not recommended.


> [!WARNING]
> Setting `DataSenderMaxWorkCatchupMs` to `0` drastically increases ping. Setting it too high may cause noticeable lag spikes during catch-up periods.

### Connection MTU Size

This flag adjusts the Maximum Transmission Unit size used by the Roblox client.

*   **Flag:** `DFIntConnectionMTUSize`

*   **JSON Example:**
    ```json
    {
       "DFIntConnectionMTUSize": "1472"
    }
    ```

*   **Purpose:** Sets the largest network packet size (in bytes) that Roblox attempts to send without fragmentation. This includes data payload and protocol headers.

*   **Default Value:** `1396`

*   **Recommendations & Effects:**
    *   The optimal MTU depends heavily on the network path between the client and Roblox servers.
    *   **Testing:** Use `ping www.roblox.com -f -l <value>` (Windows Command Prompt) or tools like TCP Optimizer to find the largest value that doesn't result in "Packet needs to be fragmented but DF set" errors. Start high (e.g., 1472) and decrease until pings succeed.
    *   **Good Connection:** Values closer to the path MTU (often around 1472-1500, but `1472` is suggested as a safe upper limit for the flag itself) are generally preferred. Higher MTU allows more data per packet, potentially improving overall data throughput and effective latency even if raw ping (ms) slightly increases.
    *   **Poor Connection:** Lower values (e.g., 700-900) might be necessary to avoid fragmentation issues on unstable networks.


> [!WARNING]
> Setting the value *too high* for your network path will cause packet fragmentation or loss, potentially breaking game connectivity or causing severe lag. Recommended maximum for the flag seems to be around `1472`; exceeding this might trigger internal issues regardless of path MTU.

*   **Related Links:**
    *   [Netgear KB on MTU Ping Test](https://kb.netgear.com/19863/Ping-Test-to-determine-Optimal-MTU-Size-on-Router)

### Frame Buffer and Interpolation

These flags control animation buffering and the interpolation applied between character states, affecting visual smoothness versus latency.

*   **Flags:**
    *   `DFIntMaxFrameBufferSize`
    *   `FIntInterpolationAwareTargetTimeLerpHundredth`
    *   `DFIntMaxAverageFrameDelayExceedFactor`

*   **JSON Example:**
    ```json
    {
       "DFIntMaxFrameBufferSize": "3",
       "FIntInterpolationAwareTargetTimeLerpHundredth": "100",
       "DFIntMaxAverageFrameDelayExceedFactor": "0"
    }
    ```

*   **Purpose:**
    *   `MaxFrameBufferSize`: Controls the number of frames buffered for animations. Larger buffer = smoother animation playback but higher visual latency. Smaller buffer = lower latency but potential jitter.
    *   `InterpolationAwareTargetTimeLerpHundredth`: Controls the aggressiveness of interpolation (smoothing) between character network updates. Value is 0-100 (representing 0% to 100%). Higher values interpolate more strongly towards the target state.
    *   `MaxAverageFrameDelayExceedFactor`: A multiplier used with the target frame time. If the average frame delay exceeds `(Target Frame Time * Factor)`, the system may take corrective action.

*   **Default Values:**
    *   `MaxFrameBufferSize`: `10`
    *   `InterpolationAwareTargetTimeLerpHundredth`: `13` (13%)
    *   `MaxAverageFrameDelayExceedFactor`: `3`

*   **Recommendations & Effects:**
    *   **Low Latency Setup (Potential Jitter):**
        *   Set `MaxFrameBufferSize` low (e.g., `1` to `3`).
        *   Set `InterpolationAwareTargetTimeLerpHundredth` high (e.g., `100`) to compensate for the lack of buffering with stronger interpolation.
        *   Set `MaxAverageFrameDelayExceedFactor` low (e.g., `0` or `1`) for less aggressive frame delay correction.
        *   *Effect:* Lowest visual latency (what you see is closer to the actual state), but character movements (especially others') may appear jittery or teleporty ("lag ball" effect).
    *   **Smoother Animation Setup (Higher Latency):**
        *   Keep `MaxFrameBufferSize` at default (`10`) or slightly lower (`4`-`10`).
        *   Keep `InterpolationAwareTargetTimeLerpHundredth` at default (`13`) or lower.
        *   Keep `MaxAverageFrameDelayExceedFactor` at default (`3`).
        *   *Effect:* Smoother, more fluid animations, but with increased delay between the actual game state and what is displayed.


> [!WARNING]
> Low `MaxFrameBufferSize` causes visual jitter/stutter. High `InterpolationAwareTargetTimeLerpHundredth` can cause unnatural "teleporting" movement for other players, which may be disorienting, especially in fast-paced games like FPS. Some games might consider extreme values for these flags (especially in combination with modified physics rates or MTU) as cheating. Setting `MaxAverageFrameDelayExceedFactor` low (0-1) can also contribute to jitter.

### Physics Simulation Timestep

This flag relates to the physics engine's timing and stability.

*   **Flag:** `DFIntTimestepArbiterThresholdCFLThou`

*   **JSON Example:**
    ```json
    {
       "DFIntTimestepArbiterThresholdCFLThou": "300"
    }
    ```

*   **Purpose:** Influences the "Arbiter," which manages trade-offs between rendering, simulation updates (including physics), and overall timing stability. The exact mechanism is complex (related to CFL condition).

*   **Default Value:** `1000`

*   **Recommendations & Effects:**
    *   **Higher Value (e.g., default `1000` or max int):** Promotes stability in simulation and rendering timing. May result in a visually "sharper" or more stable image, potentially at the cost of responsiveness if updates are less frequent. Some users prefer max value.
    *   **Lower Value (e.g., `100` or `300`):** May allow for more frequent or less constrained physics/timing updates, potentially improving responsiveness or perceived latency for physics interactions. Often suggested for "movement fixes."
    *   **Value `0`:** Reportedly results in jittery behavior.
    *   **Value `-1`:** Reportedly causes crashes.


> [!WARNING]
> Setting the value to `-1` will likely crash the client. Setting it to `0` or very low values can cause significant visual jitter in physics and movement. There is user disagreement on whether lower or higher values are optimal for latency.

### Raycasting Limits

These flags control parameters related to raycasting operations.

*   **Flags:**
    *   `DFIntRaycastMaxDistance`
    *   `DFIntVisibilityCheckRayCastLimitPerFrame` (Less discussed)

*   **JSON Example:**
    ```json
    {
       "DFIntRaycastMaxDistance": "15000"
    }
    ```

*   **Purpose:**
    *   `RaycastMaxDistance`: Defines the maximum distance (in studs) a single `WorldRoot:Raycast()` operation can travel.

*   **Default Values:**
    *   `RaycastMaxDistance`: `15000` (updated from 5000 in 2021)
    *   `VisibilityCheckRayCastLimitPerFrame`: `2`

*   **Recommendations & Effects:**
    *   The default `15000` is generally sufficient. Modification is usually unnecessary unless encountering specific issues related to raycast distance limits (which is rare after the default increase).


> [!NOTE]
> Raycasting is a local computation and doesn't directly cause network latency. However, game logic using raycast results (e.g., server-side hit detection) will still be subject to network RTT. Excessive raycasting can impact performance (FPS).
> [!WARNING]
> Setting `RaycastMaxDistance` to a very low value (reportedly below `3`) can break character leg collision or other raycast-dependent game mechanics.

*   **Related Links:**
    *   [Roblox Raycasting Documentation](https://create.roblox.com/docs/workspace/raycasting)
    *   [DevForum: Upgraded Raycasts](https://devforum.roblox.com/t/upgraded-improved-and-faster-raycasts/1420368)
    *   [DevForum: Raycast Performance Discussion](https://devforum.roblox.com/t/raycast-performance/233503)

### CFrame Optimization and Replication

These flags aim to optimize or alter how CFrames (Coordinate Frames: position and orientation) are handled and replicated.

*   **Flags:**
    *   `FFlagOptimizeCFrameUpdates`
    *   `FFlagOptimizeCFrameUpdates2`
    *   `DFFlagPreciseCFrameReplication`

*   **JSON Example:**
    ```json
    {
       "FFlagOptimizeCFrameUpdates": true,
       "FFlagOptimizeCFrameUpdates2": true,
       "DFFlagPreciseCFrameReplication": true
    }
    ```

*   **Purpose:**
    *   `OptimizeCFrameUpdates` / `OptimizeCFrameUpdates2`: Enable internal optimizations related to CFrame calculations or updates.
    *   `PreciseCFrameReplication`: Aims to replicate CFrame changes over the network with higher precision.

*   **Default Values:**
    *   `OptimizeCFrameUpdates`: `false`
    *   `OptimizeCFrameUpdates2`: `false`
    *   `PreciseCFrameReplication`: Originally `false`, but reported to be `true` by default later (as of early 2025).

*   **Recommendations & Effects:**
    *   Setting the `Optimize` flags to `true` *might* offer performance benefits in CFrame-heavy scenarios, but comes with significant compatibility risks.
    *   `PreciseCFrameReplication` being default `true` means manual setting is likely unnecessary.


> [!WARNING]
> `FFlagOptimizeCFrameUpdates` (and likely `2`) are known to cause significant bugs in games that rely on specific or older CFrame behaviors (e.g., spawning issues in Arsenal, out-of-bounds glitches in Nico's Nextbots). Use with extreme caution, highly game-dependent.

> [!NOTE]
> Initial concerns about bugs with `DFFlagPreciseCFrameReplication` were later potentially attributed to interactions with `DFIntS2PhysicsSenderRate`. As it's likely default `true`, modifying it is generally not needed.

*   **Related Links:**
    *   [Roblox CFrame Documentation](https://create.roblox.com/docs/reference/engine/datatypes/CFrame)
    *   [Roblox CFrames Usage Guide](https://create.roblox.com/docs/workspace/cframes)

### Physics Sender Rate

Controls the frequency of sending client physics updates to the server.

*   **Flag:** `DFIntS2PhysicsSenderRate`

*   **JSON Example:**
    ```json
    {
       "DFIntS2PhysicsSenderRate": "60"
    }
    ```

*   **Purpose:** Determines how many times per second the client sends its physics state (position, velocity, inputs like jumping/walking) to the server. This directly impacts server-client synchronization for movement.

*   **Default Value:** `15` (updates per second)

*   **Recommendations & Effects:**
    *   **Higher Value (e.g., `60`, `128`):** Sends physics updates more frequently. Improves synchronization between client actions and server state, making movement appear more precise to the server and other clients. Can reduce the feeling of server-side latency (e.g., making anti-shove mechanics feel more responsive). `60` was reported as a stable value offering smoothness with fewer bugs than default.
    *   **Lower Value:** Sends updates less frequently. Increases desynchronization between client and server, which can lead to rubber-banding, delayed hit registration, and appearing laggy to others. Generally disadvantageous, though potentially exploitable in niche ways (not recommended).
    *   **Very High Values (e.g., `1000+` or `2147483647`):** Historically, max int values were usable, potentially offering maximum sync but also causing issues. This capability was reportedly patched or limited around March 2025 due to abuse potential (crashing/bugging games). Values above `~512` or `~1000` might cause unregistered server positions or other bugs in certain games/contexts.


> [!WARNING]
> Lowering the value significantly degrades gameplay experience due to desync. Setting the value excessively high (`1000+` or previously max int) can cause bugs, performance issues, or unregistered positions, and may be detected as cheating by some games. The ability to use extremely high values appears to be patched. Stick to moderately increased values (e.g., `30`-`128`) for potential benefits.

> [!NOTE]
> This flag is sometimes incorrectly referred to as "Fast Dash" in specific games like The Strongest Battlegrounds. It does not inherently speed up actions but improves the *synchronization* of those actions with the server. Pairing with `DFIntPhysicsSenderMaxBandwidthBps` might allow higher rates to function more stably by providing adequate bandwidth.

### Debugging Flags

*   **`FLogDebugShowFlagState` / `FStringDebugShowFlagState`**
    *   **Description:** Enables an overlay or log output showing the current state (values) of active FFlags. Useful for verifying if your overrides are being applied. `FLog`/`FString` implies static setting at launch.
    *   **JSON Example (using FLog as boolean):**
        ```json
        {
           "FLogDebugShowFlagState": "DFIntS2PhysicsSenderRate"
        }
        ```
> [!NOTE]
> A video explaining this was linked: `https://www.youtube.com/watch?v=USzEqHQ_87g`

### UI Cosmetic Changes

These flags alter minor visual elements of the Roblox client UI.

*   **Flags:**
    *   `FFlagEnableNavBarLabels3`
    *   `FFlagLuaAppChartsPageRename`

*   **JSON Example:**
    ```json
    {
       "FFlagEnableNavBarLabels3": "False",
       "FFlagLuaAppChartsPageRename": "False"
    }
    ```

*   **Purpose:** Primarily cosmetic UI tweaks. `FFlagEnableNavBarLabels3` set to `False` removes text labels from the main navigation sidebar icons, reverting it to an older appearance.

*   **Default Value:** `true` (Labels enabled)

*   **Recommendations & Effects:** Set to `False` for the visual change if desired.


> [!NOTE]
> These flags are purely cosmetic and have no impact on performance or network latency. Any claims of ping changes related to these flags are likely jokes or misconceptions.
