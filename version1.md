# Roblox FFlag Optimization Guide (Based on Flag Forge Discussions)

## What are FFlags?

FFlags (Fast Flags) are experimental configuration variables used internally by Roblox engineers. They allow testing new features, performance tweaks, or different system behaviors without requiring a full client update. Modifying these flags *can* sometimes lead to performance improvements or altered game physics/behavior, but often comes with risks of instability, unexpected bugs, or even game compatibility issues.

> [!WARNING]
> Modifying FFlags is **not officially supported** by Roblox. Doing so may lead to game crashes, visual glitches, unexpected behavior, synchronization issues, or potentially violate game rules if detected as an unfair advantage. Proceed with caution and at your own risk. The information below is based on user discussions and experimentation, not official documentation.

## FFlag Prefixes and Types

FFlags use prefixes to denote their type and behavior:

*   **`F` (Fast):** Static variable initialized once when Roblox starts. Its value remains constant throughout the session and only changes upon restarting the client.
*   **`DF` (Dynamic Fast):** Dynamic variable whose value can be updated by Roblox while the client is running. These typically refresh automatically (e.g., every 5 minutes).
*   **`SF` (Synchronized Fast):** Variable loaded by the server and sent to the client, ensuring consistency across different clients connected to the same server instance.

These prefixes combine with suffixes indicating the data type:

*   **`FFlag` / `DFFlag` / `SFFlag`:** Boolean (`true` or `false`).
*   **`FInt` / `DFInt` / `SFInt`:** Integer (whole number).
*   **`FString` / `DFString` / `SFString`:** String (text, potentially URLs).
*   **`FLog` / `DFLog` / `SFLog`:** Log variable, often used as Boolean or Integer in practice for controlling logging levels or features.

## Data Types and Expected Values

*   **Integer-based Flags (`DFInt`, `FInt`, `SFInt`):**
    *   Expected values: Integers.
    *   Maximum values depend on the underlying integer type used by Roblox (often 32-bit):
        *   *Theoretical* 64-bit integer max: `9,223,372,036,854,775,807`
        *   Common 32-bit integer max: `2,147,483,647`
        *   *Potential* 16-bit integer max: `32,767`
*   **Boolean-based Flags (`FFlag`, `DFFlag`, `SFFlag`):**
    *   Expected values: `true` or `false`.
*   **String-based Flags (`FString`, `DFString`, `SFString`):**
    *   Expected values: Text strings, sometimes URLs.
*   **Log-based Flags (`DFLog`, `FLog`, `SFLog`):**
    *   Expected values: Often `true`/`false` or integer values to control logging verbosity.

---

## Specific FFlags Discussed

Here are details on specific FFlags mentioned in the provided chat logs, along with discussed values and potential effects. Remember the JSON format uses **three spaces** for indentation.

### Task Scheduler Configuration

These flags influence how the Roblox Task Scheduler allocates resources per cycle.

*   **`FIntTaskSchedulerTasksDefaultMaxCountPerCycle`**
    *   **Description:** Sets the maximum number of tasks the scheduler processes in a single cycle. `FInt` means it's set at launch.
    *   **Default:** `16`
    *   **Discussed Value:** `2147483647` (Maximum 32-bit integer)
    *   **Effects:**
        *   *Higher Value:* Allows more tasks per cycle, potentially leading to more responsive gameplay, lower latency, and faster task execution.
        *   *Downside:* Can increase CPU usage and overhead. May be unnecessary or detrimental on lower-end hardware.
    *   **JSON Example:**
        ```json
        {
           "FIntTaskSchedulerTasksDefaultMaxCountPerCycle": "2147483647"
        }
        ```

*   **`FIntTaskSchedulerTasksDefaultMaxTimeMsPerCycle`**
    *   **Description:** Sets the maximum time (in milliseconds) the scheduler spends executing tasks per cycle. `FInt` means it's set at launch.
    *   **Default:** Not explicitly stated, but implied to be non-zero.
    *   **Discussed Value:** `0` or user-tested values.
    *   **Effects:**
        *   *Higher Value:* Allows more tasks to complete within a cycle, potentially improving responsiveness but possibly impacting frame rate if tasks take too long. Might help on high-latency connections if the server is good.
        *   *Lower Value (e.g., `0`):* Might limit execution time per cycle, preventing single long tasks from delaying others. Could reduce task latency but might slow down games needing longer execution times. May cause stutters on low-end PCs.
    *   **JSON Example:**
        ```json
        {
           "FIntTaskSchedulerTasksDefaultMaxTimeMsPerCycle": "0"
        }
        ```
> [!NOTE]
> Benchmarking Task Scheduler changes is difficult. Effects are often perceived through visual latency or measured via increased CPU usage in microprofilers. Optimal values heavily depend on hardware and the specific game. Requires individual testing.

### Network Bandwidth Management

These flags relate to how Roblox manages outgoing network traffic.

*   **`DFIntBandwidthManagerApplicationDefaultBps`**
    *   **Description:** Sets the baseline bandwidth budget (Bytes per second) used for throttling application-level data (e.g., `RemoteEvent` traffic) to prevent it from starving core physics replication traffic. `DFInt` means it can change dynamically.
    *   **Default:** `64000`
    *   **JSON Example:**
        ```json
        {
           "DFIntBandwidthManagerApplicationDefaultBps": "64000"
        }
        ```

*   **`DFIntBandwidthManagerDataSenderMaxWorkCatchupMs`**
    *   **Description:** Maximum time (in milliseconds) the network data sender will spend in one go trying to "catch up" if it falls behind on sending updates. Limits packet bursts after a lag/pause. `DFInt` means it can change dynamically.
    *   **Default:** `20`
    *   **Effects:**
        *   *Lower Value:* Smoother network output, prevents large bursts, but catch-up might be less stable or take longer.
        *   *Higher Value:* More stable/faster catch-up after delays, but can cause larger packet bursts and potential perceived lag spikes. Extreme stability desired = higher value.
        *   *Setting to `0`:* Reported to cause ping to increase significantly.
    *   **JSON Example:**
        ```json
        {
           "DFIntBandwidthManagerDataSenderMaxWorkCatchupMs": "20"
        }
        ```
> [!NOTE]
> Roblox's network debug overlay (Shift+F3) shows `Out Data` (application) and `Out Physics` (replication) traffic and potential throttling based on budgets like `DFIntBandwidthManagerApplicationDefaultBps`.

### Connection MTU Size

*   **`DFIntConnectionMTUSize`**
    *   **Description:** Sets the Maximum Transmission Unit size (in bytes) for network packets. Larger packets carry more data but might take slightly longer to transmit (higher raw ms ping). `DFInt` means it can change dynamically.
    *   **Default:** `1396`
    *   **Discussed Values:** `700-900` (for poor connections), `1472` (recommended max for good connections).
    *   **Effects:**
        *   *Higher Value (up to ~1472):* Sends more data per packet. Can improve *effective* throughput and reduce perceived latency even if raw ping increases slightly (e.g., 1472 bytes @ 30ms > 900 bytes @ 22ms in terms of data/sec).
        *   *Lower Value:* May be necessary for unstable connections prone to packet loss with larger packets.
        *   *Values > ~1472:* Risk causing packet fragmentation, which can severely degrade performance or break connectivity.
    *   **Testing:** Use `ping www.roblox.com -f -l <size>` (or a game server IP if known) in Command Prompt (as admin) to find the largest size that doesn't fragment ("Packet needs to be fragmented but DF set"). Add 28 bytes (IP/ICMP headers) to the working `-l` size for the router/system MTU, but for the `DFIntConnectionMTUSize` flag, use the tested payload size directly (e.g., test up to `1472`). TCP Optimizer can also help test.
    *   **JSON Example:**
        ```json
        {
           "DFIntConnectionMTUSize": "1472"
        }
        ```
> [!WARNING]
> Setting `DFIntConnectionMTUSize` too high (generally above 1472 for standard Ethernet) can cause significant network issues due to fragmentation. Test carefully. Pinging websites is only an estimate; optimal game server MTU might differ.

### Frame Buffering and Delay Management

These flags influence animation smoothing and frame timing.

*   **`DFIntMaxFrameBufferSize`**
    *   **Description:** Controls the size of the buffer used for smoothing animations. `DFInt` means it can change dynamically.
    *   **Default:** `10`
    *   **Discussed Values:** `1-3` (low latency, potentially jittery), `4-10` (smoother, default range).
    *   **Effects:**
        *   *Higher Value (4-10):* Smoother animations, less jitter, as the client has more frames buffered to play back.
        *   *Lower Value (1-3):* Less animation buffering, potentially lower visual latency (what you see is closer to the actual state), but can cause noticeable stuttering or jittery movements, especially without other smoothing flags.
    *   **JSON Example:**
        ```json
        {
           "DFIntMaxFrameBufferSize": "3"
        }
        ```

*   **`DFIntMaxAverageFrameDelayExceedFactor`**
    *   **Description:** A multiplier used with the target frame time. If the *average* frame delay exceeds `TargetFrameTime * Factor`, the system takes corrective action. `DFInt` means it can change dynamically.
    *   **Default:** `3`
    *   **Discussed Values:** `0`, `1`, `2`, `3`.
    *   **Effects:**
        *   *Lower Value (e.g., 0 or 1):* More aggressive correction of frame delays. Can potentially reduce perceived latency but might cause jittery movement for other players. Works in conjunction with low `DFIntMaxFrameBufferSize`. `0` might attempt indefinite running without correction?
        *   *Higher Value (Default 3):* More tolerant of frame delay variations before correcting.
    *   **JSON Example:**
        ```json
        {
           "DFIntMaxAverageFrameDelayExceedFactor": "1"
        }
        ```

### Raycasting Limits

*   **`DFIntRaycastMaxDistance`**
    *   **Description:** Defines the maximum distance (in studs) a single raycast operation can travel. `DFInt` means it can change dynamically.
    *   **Default/Current Max:** `15000` (Updated from 5000 previously).
    *   **Effects:** Primarily impacts developers using raycasts. Higher values allow longer checks without chaining multiple rays. Raycasting itself is local; perceived latency comes from client-server communication *about* raycast results. High frequency/intensity raycasting can impact frame rate.
    *   **JSON Example:**
        ```json
        {
           "DFIntRaycastMaxDistance": "15000"
        }
        ```
*   **`DFIntVisibilityCheckRayCastLimitPerFrame`**
    *   **Description:** Likely limits the number of raycasts used for visibility checks per frame. Details not provided in logs.
    *   **Default:** `2`
    *   **JSON Example:**
        ```json
        {
           "DFIntVisibilityCheckRayCastLimitPerFrame": "2"
        }
        ```
> [!CAUTION]
> One user reported that setting `DFIntRaycastMaxDistance` below `3` broke leg collision in their testing. Use default or higher values unless you have a specific reason and understand the consequences.

### Timestep Arbiter

*   **`DFIntTimestepArbiterThresholdCFLThou`**
    *   **Description:** Influences the "Arbiter," which manages trade-offs between rendering, simulation updates, physics, and timing. Seems related to timestep stability. `DFInt` means it can change dynamically.
    *   **Default:** `1000`
    *   **Discussed Values:** `0`, `100-300`, `1000` (default), Max integer.
    *   **Effects:**
        *   *Higher Value:* Stabilizes updates, potentially making the screen feel "sharper" due to potentially less frequent but more consistent updates. Some users prefer max value.
        *   *Lower Value (e.g., 100-300):* Suggested by some for lower latency or as a "movement fix," but can cause jitteriness.
        *   *Value `0` or `-1`:* Reported to potentially cause crashes or jitter.
    *   **JSON Example:**
        ```json
        {
           "DFIntTimestepArbiterThresholdCFLThou": "300"
        }
        ```
> [!NOTE]
> There are conflicting opinions on the optimal value for latency vs. stability. Lower values might reduce latency but increase jitter, while higher values increase stability potentially at the cost of update frequency. Requires testing.

### Interpolation Awareness

*   **`FIntInterpolationAwareTargetTimeLerpHundredth`**
    *   **Description:** Controls the aggressiveness of frame interpolation (smoothing/predicting movement between received states). Value is a percentage (0-100). `FInt` means it's set at launch.
    *   **Default:** `13` (13%)
    *   **Discussed Values:** `100` (100%).
    *   **Effects:**
        *   *Higher Value (e.g., 100):* More aggressive interpolation. Can potentially smooth out movement when used with very low `DFIntMaxFrameBufferSize` (1-3). However, can also cause overcorrections, leading to characters appearing to teleport or stand still instead of moving smoothly. Nicknamed "lag ball" by some.
        *   *Lower Value (Default 13):* Less aggressive smoothing.
    *   **User Experience:** Divisive. Some feel high values give more predictable movement/lower visual latency, others find the teleporting effect detrimental, especially in FPS games.
    *   **JSON Example:**
        ```json
        {
           "FIntInterpolationAwareTargetTimeLerpHundredth": "100"
        }
        ```
> [!WARNING]
> Some users reported concerns that certain games might detect high interpolation values (or low frame buffer sizes) as cheating. Use with extreme caution.

### Debugging Flags

*   **`FLogDebugShowFlagState` / `FStringDebugShowFlagState`**
    *   **Description:** Enables an overlay or log output showing the current state (values) of active FFlags. Useful for verifying if your overrides are being applied. `FLog`/`FString` implies static setting at launch.
    *   **JSON Example (using FLog as boolean):**
        ```json
        {
           "FLogDebugShowFlagState": "1"
        }
        ```
> [!NOTE]
> A video explaining this was linked: `https://www.youtube.com/watch?v=USzEqHQ_87g`

### UI Customization

*   **`FFlagEnableNavBarLabels3` / `FFlagLuaAppChartsPageRename`**
    *   **Description:** These seem to control UI elements, specifically removing labels from the main navigation bar for a cleaner look (reverting to an older style). `FFlag` means static setting at launch.
    *   **Discussed Value:** `False`
    *   **Effects:** Purely visual change to the Roblox client UI. Unlikely to have any significant performance impact (jokes about "50.70ms ping" are likely sarcastic).
    *   **JSON Example:**
        ```json
        {
           "FFlagEnableNavBarLabels3": "False",
           "FFlagLuaAppChartsPageRename": "False"
        }
        ```

### CFrame Optimization and Replication

CFrames define position and orientation in 3D space. These flags relate to how they are updated and synchronized.

*   **`FFlagOptimizeCFrameUpdates` / `FFlagOptimizeCFrameUpdates2`**
    *   **Description:** Attempts to optimize the processing of CFrame updates. `FFlag` means static setting at launch.
    *   **Default:** `false`
    *   **Discussed Value:** `true`
    *   **Effects:** Intended to improve performance related to CFrame calculations.
    *   **JSON Example:**
        ```json
        {
           "FFlagOptimizeCFrameUpdates": true,
           "FFlagOptimizeCFrameUpdates2": true
        }
        ```
> [!WARNING]
> These flags can cause compatibility issues. Example: Reported to cause spawning bugs in Arsenal, potentially because the game uses older or specific CFrame methods incompatible with the optimization. Use with caution, test per game.

*   **`DFFlagPreciseCFrameReplication`**
    *   **Description:** Aims to make the network replication of CFrames more precise. `DFFlag` means dynamic.
    *   **Default:** `false` (though one user mentioned it might be `true` by default later)
    *   **Discussed Value:** `true`
    *   **Effects:** Intended to improve synchronization of object positions/orientations. However, users reported potential for bugs and bad gameplay in some games. Issues might be related to physics sender settings.
    *   **JSON Example:**
        ```json
        {
           "DFFlagPreciseCFrameReplication": true
        }
        ```

### Physics Sender Rate

*   **`DFIntS2PhysicsSenderRate`**
    *   **Description:** Controls how frequently the client sends physics updates (movement, jumping, etc.) to the server. Measured in updates per second (?). `DFInt` means dynamic.
    *   **Default:** `15`
    *   **Discussed Values:** `60` (stable), `64`, `128`, `512`, `1000`, `38760`, Max integer.
    *   **Effects:**
        *   *Higher Value:* Sends updates more frequently. Improves client-to-server synchronization, making your movements appear more accurate and responsive on the server and to other players. Can reduce the feeling of server-side lag (e.g., better anti-shove, less likely to be hit behind cover). Misleadingly called "Fast Dash" in some communities - it's about sync, not speed.
        *   *Lower Value:* Sends updates less frequently. Causes desynchronization between client and server. Can lead to exploits or bugs (e.g., appearing laggy, potentially avoiding hits unfairly, or getting hit unfairly due to server lag compensation). **Not recommended.**
        *   *Very High Values (>512/1000):* Can cause issues in some games, potentially unregistered server positions or desync, according to some tests. Effects might plateau. Max possible values (like 38760+) were reported as potentially patched or capped later due to crash/bug concerns, possibly related to official tournaments.
    *   **Testing:** The game "Desync Playground" (`https://www.roblox.com/games/11746390170/Desync-Playground`) was mentioned for visualizing client vs. server positions.
    *   **JSON Example (using a commonly suggested stable value):**
        ```json
        {
           "DFIntS2PhysicsSenderRate": "60"
        }
        ```
> [!WARNING]
> Setting this value too low causes desync and is generally detrimental. Setting it extremely high might cause instability, game-specific bugs, or may no longer work as expected due to Roblox patches/caps. Values like 60-128 are often considered safer increases over the default 15.
