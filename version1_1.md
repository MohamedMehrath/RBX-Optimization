## Roblox FastFlags (FFlags) Overview

### Accessory Adjustment IXP
Enables the in-experience accessory adjustment feature.

*   **Flag:** `FFlagAXAccessoryAdjustmentIXPEnabledForAll`
*   **JSON Example:**
    ```json
    {
          "FFlagAXAccessoryAdjustmentIXPEnabledForAll": "true"
    }
    ```
*   **Purpose:** Activates the user interface and functionality for adjusting accessories directly within a running Roblox experience, if the experience supports it.
*   **Default Value:** Likely `false`.
*   **Effects:** Allows users to modify accessory positions/attachments in-game.

### DPI Scaling Control
Manages how Roblox handles display DPI scaling. Setting these to `False` typically reverts to default or system-managed DPI scaling behavior.

*   **Flags:**
    *   `DFFlagDebugOverrideDPIScale`
    *   `DFFlagDisableDPIScale`
*   **JSON Example:**
    ```json
    {
          "DFFlagDebugOverrideDPIScale": "False",
          "DFFlagDisableDPIScale": "False"
    }
    ```
*   **Purpose:** These flags control overrides related to DPI scaling. `DFFlagDisableDPIScale` likely disables scaling when `True`, so setting it `False` *enables* scaling. `DFFlagDebugOverrideDPIScale` might force a specific debug behavior when `True`. Setting both to `False` aims for standard scaling.
*   **Default Values:** Unknown, but `DFFlagDisableDPIScale` is likely `False` in standard operation.
*   **Effects:** Setting to `False` can help ensure the UI scales correctly on high-DPI displays, preventing blurriness or incorrect sizing.

### Disable Dynamic Head Animations
Disables facial animations on Roblox dynamic heads by manipulating Level of Detail (LOD) settings.

*   **Flags:**
    *   `DFIntAnimationLodFacsDistanceMin`
    *   `DFIntAnimationLodFacsDistanceMax`
    *   `DFIntAnimationLodFacsVisibilityDenominator`
*   **JSON Example:**
    ```json
    {
          "DFIntAnimationLodFacsDistanceMin": "0",
          "DFIntAnimationLodFacsDistanceMax": "0",
          "DFIntAnimationLodFacsVisibilityDenominator": "0"
    }
    ```
*   **Purpose:** These flags control the distances and visibility factors for facial animations (Facs) LOD. Setting them to `0` effectively prevents the animations from ever becoming active.
*   **Default Values:** Non-zero values.
*   **Effects:** Can improve performance slightly by reducing animation computations. Results in static faces on dynamic heads.

### Deterministic Particle Rendering
Forces particle effects to render in a deterministic manner, potentially enabling higher-quality particle visuals regardless of the main graphics quality setting.

*   **Flag:** `FFlagDebugDeterministicParticles`
*   **JSON Example:**
    ```json
    {
          "FFlagDebugDeterministicParticles": "True"
    }
    ```
*   **Purpose:** Makes particle system behavior predictable and potentially less dependent on varying frame rates or simulation steps. Can result in visuals closer to maximum graphics quality settings for particles.
*   **Default Value:** `False`.
*   **Effects:** May provide smoother or more consistent particle effects, especially noticeable at lower graphics quality levels. Potential minor performance impact.

### Customize Experience Guidelines URL
Redirects the "Learn More" link associated with the Experience Guidelines or Age Rating information to a custom URL.

*   **Flag:** `FStringExperienceGuidelinesExplainedPageUrl`
*   **JSON Example:**
    ```json
    {
          "FStringExperienceGuidelinesExplainedPageUrl": "YOUR_CUSTOM_URL_HERE"
    }
    ```
*   **Purpose:** Allows overriding the default destination URL for the guidelines explanation link.
*   **Default Value:** A specific Roblox help page URL.
*   **Effects:** Changes where the "Learn More" button navigates. Replace `"YOUR_CUSTOM_URL_HERE"` with the desired web address.

### Disable Texture Compositor (Gray Avatars)
Setting the number of active jobs for the texture compositor to zero can prevent textures from loading correctly, often resulting in characters appearing gray or untextured.

*   **Flag:** `DFIntTextureCompositorActiveJobs`
*   **JSON Example:**
    ```json
    {
          "DFIntTextureCompositorActiveJobs": "0"
    }
    ```
*   **Purpose:** Controls the number of concurrent jobs the texture compositor can run. Setting this to `0` likely halts or severely limits its operation.
*   **Default Value:** A positive integer (e.g., based on CPU cores).
*   **Effects:** Leads to missing or improperly loaded textures, most visibly causing avatars to appear gray.

> [!WARNING]
> Setting `DFIntTextureCompositorActiveJobs` to `0` will break texture loading and result in gray/untextured avatars and environments. This is not recommended for regular use.

### GUI Toggling Hotkeys (Group Restricted)
Enables keyboard shortcuts to hide different categories of user interface elements, potentially restricted to members of a specific Roblox Group.

*   **Flag:** `DFIntCanHideGuiGroupId`
*   **JSON Example:**
    ```json
    {
          "DFIntCanHideGuiGroupId": "YOUR_GROUP_ID"
    }
    ```
*   **Purpose:** When set to a valid Roblox Group ID, members of that group gain access to hotkeys for toggling GUI visibility:
    *   **Ctrl + Shift + B:** Toggles BillboardGuis, SurfaceGuis (GUIs in 3D space).
    *   **Ctrl + Shift + C:** Toggles game-developer-created ScreenGuis.
    *   **Ctrl + Shift + G:** Toggles Roblox's own CoreGuis (menu, chat, etc.).
    *   **Ctrl + Shift + N:** Toggles player names and other nametag-like BillboardGuis.
*   **Default Value:** `0` or an invalid Group ID (effectively disabled).
*   **Effects:** Useful for developers, testers, or content creators to capture gameplay footage without UI elements. Requires membership in the specified group (replace `YOUR_GROUP_ID` with the actual ID).

> [!NOTE]
> This feature appears to be gated by Roblox Group membership via the provided Group ID. Setting it to `0` or an invalid ID likely disables the hotkeys.

### Grass Motion Control
Adjusts the intensity or completely disables the swaying animation of decorative grass.

*   **Flag:** `FIntGrassMovementReducedMotionFactor`
*   **JSON Examples:**
    *   **Fast Motion:**
        ```json
        {
              "FIntGrassMovementReducedMotionFactor": "500"
        }
        ```
    *   **No Motion:**
        ```json
        {
              "FIntGrassMovementReducedMotionFactor": "0"
        }
        ```
*   **Purpose:** Modifies the factor applied to grass movement calculations. Higher values increase the speed/amplitude of the sway. A value of `0` disables the movement entirely.
*   **Default Value:** `5`.
*   **Effects:**
    *   High values (`999`): Creates exaggerated, fast grass swaying.
    *   `0`: Makes grass static, potentially improving performance slightly in dense grass areas.

### Force Lower Quality Textures
Attempts to force textures to render at a lower quality level, potentially for performance gains.

*   **Flag:** `DFIntPerformanceControlTextureQualityBestUtility`
*   **JSON Example:**
    ```json
    {
          "DFIntPerformanceControlTextureQualityBestUtility": "-1"
    }
    ```
*   **Purpose:** Appears to influence the texture quality selection mechanism, with `-1` potentially forcing the lowest quality or bypassing a certain quality assessment step.
*   **Prerequisite:** May require `DFFlagTextureQualityOverrideEnabled` to be set to `false`.
*   **Default Value:** Unknown, likely a non-negative value.
*   **Effects:** Can reduce texture memory usage and potentially improve performance on systems with limited VRAM, at the cost of visual fidelity (blurrier textures).

> [!NOTE]
> The effectiveness of this flag might be contingent on `DFFlagTextureQualityOverrideEnabled` being set to `false`.

### Modify Connection Timeout Duration
Adjusts the time in milliseconds the client waits before disconnecting after losing connection to the server.

*   **Flag:** `DFIntDefaultTimeoutTimeMs`
*   **JSON Example (Extended Timeout):**
    ```json
    {
          "DFIntDefaultTimeoutTimeMs": "1000000"
    }
    ```
*   **JSON Example (Short Timeout):**
    ```json
    {
          "DFIntDefaultTimeoutTimeMs": "1000"
    }
    ```
*   **Purpose:** Sets the network timeout duration. If no packets are received from the server within this time, the client disconnects.
*   **Default Value:** A moderate value (e.g., 30000ms or 60000ms).
*   **Effects:**
    *   **High Value:** Allows the client to wait longer during temporary network interruptions before disconnecting. Does *not* guarantee reconnection if the interruption is prolonged.
    *   **Low Value:** Causes the client to disconnect very quickly upon connection loss.

### RakNet Resend Buffer Size
Controls the size of the buffer used by RakNet for packet resend operations.

*   **Flag:** `FIntRakNetResendBufferArrayLength`
*   **JSON Example (Default):**
    ```json
    {
          "FIntRakNetResendBufferArrayLength": "512"
    }
    ```
*   **JSON Example (Alternative):**
    ```json
    {
          "FIntRakNetResendBufferArrayLength": "2048"
    }
    ```
*   **Purpose:** Defines the capacity of RakNet's buffer for storing packets that might need to be resent due to network loss. A larger buffer can potentially handle more packet loss or reordering scenarios.
*   **Default Value:** `512`.
*   **Recommendations & Effects:**
    *   **Default (`512`):** Standard setting.
    *   **Low Values (`1` - `~255`):** Strongly discouraged. Can lead to significant network instability, packet loss handling issues, and ping spikes.
    *   **Moderate to High Values (`256` - `4096`+):** Generally considered better for stability, especially on unstable or high-latency connections. May slightly increase memory usage. Values like `256`, `512`, `1024`, `2048` are common starting points.
    *   **Synchronization Myth:** This buffer does *not* directly synchronize with the network adapter's "Receive Buffers" setting found in Device Manager. They operate at different layers (application vs. driver).

> [!WARNING]
> Setting `FIntRakNetResendBufferArrayLength` to extremely low values (e.g., `1`) is known to cause network instability. While higher values may improve stability, excessively large values (approaching integer limits) can lead to crashes or unexpected behavior. Start with the default or moderate increases if experiencing issues potentially related to packet resends.

### Enable Performance Debug Mode
Activates a debug mode related to performance monitoring or adjustment.

*   **Flag:** `DFFlagDebugPerfMode`
*   **JSON Example:**
    ```json
    {
          "DFFlagDebugPerfMode": "True"
    }
    ```
*   **Purpose:** Enables an unspecified performance-related debug feature. Could involve displaying metrics, altering internal behavior for profiling, or enabling diagnostic tools.
*   **Default Value:** `False`.
*   **Effects:** Unknown without further context.

### Hide Own Avatar Particles in First Person
Prevents particle effects attached to the player's own avatar items from rendering when the camera is in first-person mode.

*   **Flag:** `FFlagUserHideCharacterParticlesInFirstPerson`
*   **JSON Example:**
    ```json
    {
          "FFlagUserHideCharacterParticlesInFirstPerson": "True"
    }
    ```
*   **Purpose:** Improves visibility in first-person view by hiding potentially obstructive particle effects originating from the player's character.
*   **Default Value:** `False`.
*   **Effects:** Cleans up the first-person view by removing self-generated particle clutter. May slightly improve performance if the particles were intensive.

### Select Graphics Renderer API
Allows manually choosing the graphics rendering API used by Roblox. Only one `Prefer*` flag should be set to `True` at a time.

*   **Flags:**
    *   `FFlagDebugGraphicsPreferOpenGL`: Prefer OpenGL.
    *   `FFlagDebugGraphicsPreferVulkan`: Prefer Vulkan.
    *   `FFlagDebugGraphicsPreferD3D11FL10`: Prefer DirectX 11 Feature Level 10 (effectively DirectX 10).
    *   `FFlagDebugGraphicsPreferD3D11`: Prefer DirectX 11 (Default).
    *   `FFlagDebugGraphicsPreferMetal`: Prefer Metal (macOS only).
*   **JSON Example (Force OpenGL):**
    ```json
    {
          "FFlagDebugGraphicsPreferOpenGL": "True"
    }
    ```
*   **JSON Example (Force DirectX 10):**
    ```json
    {
          "FFlagDebugGraphicsPreferD3D11FL10": "True"
    }
    ```
*   **Purpose:** Overrides the default renderer selection logic to force the use of a specific graphics API.
*   **Default Behavior:** Roblox typically defaults to DirectX 11 on Windows and Metal on macOS.
*   **Effects & Compatibility:**
    *   **DirectX 11 (`FFlagDebugGraphicsPreferD3D11`):** Standard, best balance of performance/compatibility on Windows.
    *   **DirectX 10 (`FFlagDebugGraphicsPreferD3D11FL10`):** May help on very old hardware but lacks "Future" lighting.
    *   **OpenGL (`FFlagDebugGraphicsPreferOpenGL`):** Alternative, performance varies by hardware/driver. No Alt+Enter fullscreen toggle. May lack "Future" lighting.
    *   **Vulkan (`FFlagDebugGraphicsPreferVulkan`):** Can offer performance benefits but is experimental and may cause instability/crashes. No Alt+Enter fullscreen toggle.
    *   **Metal (`FFlagDebugGraphicsPreferMetal`):** Standard on macOS.

> [!WARNING]
> *   Only set **one** `FFlagDebugGraphicsPrefer*` flag to `True`.
> *   Vulkan support is experimental and may cause crashes.
> *   Alt+Enter (fullscreen toggle) does not work with OpenGL or Vulkan.
> *   DirectX 10 (`D3D11FL10`) and potentially OpenGL do not support the "Future" lighting technology.

### Enable Simulation Decomposition Detection (DCD16)
Activates a feature related to decomposition detection within the simulation.

*   **Flag:** `FFlagSimEnableDCD16`
*   **JSON Example:**
    ```json
    {
          "FFlagSimEnableDCD16": "true"
    }
    ```
*   **Purpose:** Enables a specific version (16?) of "Decomposition Detection" in the physics or simulation engine. Exact technical details are unclear.
*   **Default Value:** Potentially `true` by default in newer versions, or the flag may no longer be used.
*   **Effects:** Unknown precise effects. Could relate to how complex assemblies or constraints are handled.

> [!NOTE]
> This flag may have been removed or enabled by default in recent Roblox versions. Its current relevance is uncertain.

### Lighting Adjustments

#### Disable Light Fade-In
Instantly shows local lights instead of having them fade in.

*   **Flag:** `FIntRenderLocalLightFadeInMs`
*   **JSON Example:**
    ```json
    {
          "FIntRenderLocalLightFadeInMs": "0"
    }
    ```
*   **Purpose:** Controls the duration (in milliseconds) of the fade-in effect for newly visible local lights. Setting it to `0` disables the fade effect.
*   **Default Value:** A positive integer (representing the fade duration in ms).
*   **Effects:** Local lights appear instantly when they enter the view or are turned on. May slightly alter visual perception but can make lighting changes more immediate.

#### Fix Chunk Lighting Updates
Applies an experimental fix related to lighting updates across chunk boundaries.

*   **Flag:** `FFlagFixChunkLightingUpdate2`
*   **JSON Example:**
    ```json
    {
          "FFlagFixChunkLightingUpdate2": "True"
    }
    ```
*   **Purpose:** Intended to address potential visual artifacts or inconsistencies in lighting calculations where different world chunks meet.
*   **Default Value:** `False`.
*   **Effects:** May resolve issues like visible seams or abrupt lighting changes between adjacent areas of the map, particularly with dynamic lighting.

#### New Light Attenuation & Culling
Enables a different method for calculating light falloff (attenuation) and related GPU culling optimizations.

*   **Flags:**
    *   `FFlagNewLightAttenuation`
    *   `FFlagFastGPULightCulling3`
    *   `FFlagDebugForceFSMCPULightCulling`
*   **JSON Example:**
    ```json
    {
          "FFlagNewLightAttenuation": "True",
          "FFlagFastGPULightCulling3": "True",
          "FFlagDebugForceFSMCPULightCulling": "True"
    }
    ```
*   **Purpose:**
    *   `FFlagNewLightAttenuation`: Activates an alternative algorithm for how light intensity diminishes over distance.
    *   `FFlagFastGPULightCulling3`: Enables a potentially faster method for the GPU to determine which lights affect the scene.
    *   `FFlagDebugForceFSMCPULightCulling`: Forces a specific type of CPU-based light culling, possibly Finite State Machine related.
*   **Default Values:** `False` for all.
*   **Effects:** Changes the appearance of light sources and their falloff. May improve performance through optimized culling.

> [!WARNING]
> Enabling `FFlagNewLightAttenuation` has been reported to negatively impact the visual appearance of the "Future" lighting technology, potentially making it look undesirable ("ugly").

#### Limit Local Light Updates
Restricts the number of local light sources that can be updated per frame or rendering cycle.

*   **Flags:**
    *   `FIntRenderLocalLightUpdatesMax`
    *   `FIntRenderLocalLightUpdatesMin`
*   **JSON Example:**
    ```json
    {
          "FIntRenderLocalLightUpdatesMax": "1",
          "FIntRenderLocalLightUpdatesMin": "1"
    }
    ```
*   **Purpose:** Sets the minimum and maximum budget for processing updates to local lights (e.g., position changes, brightness changes). Setting both to `1` severely restricts updates.
*   **Default Values:** Higher positive integers.
*   **Effects:** Can significantly improve performance in scenes with numerous dynamic local lights, but may cause noticeable delays or stuttering in how lights react to changes in the environment.

---

### Rendering and Visual Quality

#### Maximum Frame Buffer Size (Further Observations)
Provides additional context on the effects of specific `DFIntMaxFrameBufferSize` values. See the main article for the primary description.

*   **Flag:** `DFIntMaxFrameBufferSize`
*   **JSON Example (Observed Stable):**
    ```json
    {
          "DFIntMaxFrameBufferSize": "4"
    }
    ```
*   **Observed Effects:**
    *   `0`: Reportedly causes a white screen or rendering failure.
    *   `1-3`: May cause other players' movements to appear choppy or "laggy" due to insufficient buffering for interpolation.
    *   `4`: Considered a stable value offering potential performance improvements over the default while maintaining reasonable visual smoothness.
    *   `10` (Default): Standard buffering, generally smooth visuals but potentially higher input/visual latency compared to lower values like `4`.

> [!NOTE]
> The description "less input lag" for the default value `10` might be counterintuitive, as typically *lower* buffer sizes reduce latency. It could refer to a different perceived smoothness or interaction characteristic. `4` is suggested as a balance point for performance gains without excessive visual jitter.

#### Force Low Poly CSG Meshes
Forces Constructive Solid Geometry (CSG) meshes (Unions/Negates) to always render at their lowest level of detail (LOD).

*   **Flags:**
    *   `DFIntCSGLevelOfDetailSwitchingDistance`
    *   `DFIntCSGLevelOfDetailSwitchingDistanceL12`
    *   `DFIntCSGLevelOfDetailSwitchingDistanceL23`
    *   `DFIntCSGLevelOfDetailSwitchingDistanceL34`
*   **JSON Example:**
    ```json
    {
          "DFIntCSGLevelOfDetailSwitchingDistance": "0",
          "DFIntCSGLevelOfDetailSwitchingDistanceL12": "0",
          "DFIntCSGLevelOfDetailSwitchingDistanceL23": "0",
          "DFIntCSGLevelOfDetailSwitchingDistanceL34": "0"
    }
    ```
*   **Purpose:** These flags define the camera distances at which Roblox switches between different LODs for CSG objects. Setting them all to `0` forces the lowest quality LOD (LOD4 presumably) to be used regardless of distance.
*   **Default Values:** Positive integers representing various distance thresholds.
*   **Effects:** Significantly reduces the geometric complexity of CSG meshes, which can lead to substantial performance improvements in scenes heavy with unions/negates, at the cost of visual fidelity (blocky appearance).

#### Control Shadow Atlas Usage
Adjusts the maximum usage threshold for the shadow map atlas before the system considers downscaling shadow resolution.

*   **Flag:** `FIntRenderMaxShadowAtlasUsageBeforeDownscale`
*   **JSON Example (Default):**
    ```json
    {
          "FIntRenderMaxShadowAtlasUsageBeforeDownscale": "650"
    }
    ```
*   **JSON Example (Performance Focused):**
    ```json
    {
          "FIntRenderMaxShadowAtlasUsageBeforeDownscale": "300" // Example lower value
    }
    ```
*   **Purpose:** Defines how much of the shadow atlas texture can be utilized before Roblox attempts to reduce shadow quality to save resources.
*   **Default Value:** `650`.
*   **Effects:**
    *   Higher values: Maintain shadow quality longer, potentially using more VRAM and performance.
    *   Lower values: Trigger shadow quality reduction sooner, potentially saving VRAM and boosting FPS, especially in scenes with many shadow-casting lights, at the cost of shadow resolution/detail.

#### Deterministic Rendering Mode
Enables a deterministic mode for rendering, potentially simplifying or stabilizing the rendering process.

*   **Flag:** `FFlagDebugRenderingSetDeterministic`
*   **JSON Example:**
    ```json
    {
          "FFlagDebugRenderingSetDeterministic": "True"
    }
    ```
*   **Purpose:** Likely forces the renderer to operate in a more predictable, possibly simplified manner, perhaps disabling certain dynamic effects or optimizations.
*   **Default Value:** `False`.
*   **Effects:** May alter visual output (e.g., simpler shading, fewer effects) and could potentially increase performance by reducing rendering complexity.

#### Remove Terrain Textures
Disables the loading and rendering of detailed terrain material textures.

*   **Flags:**
    *   `FStringTerrainMaterialTablePre2022`
    *   `FStringTerrainMaterialTable2022`
    *   `FIntTerrainArraySliceSize`
*   **JSON Example:**
    ```json
    {
          "FStringTerrainMaterialTablePre2022": "",
          "FStringTerrainMaterialTable2022": "",
          "FIntTerrainArraySliceSize": "0"
    }
    ```
*   **Purpose:** By providing empty strings for the material table definitions and setting the slice size to zero, these flags effectively prevent the client from loading and applying standard terrain materials.
*   **Default Values:** Non-empty strings (pointing to material definition assets) and a positive integer.
*   **Effects:** Terrain appears with basic colors/shading but lacks detailed textures like grass, rock, sand patterns. Can significantly improve performance and reduce memory usage in experiences with large terrains.

#### Remove Textures via Mipmap Skipping
Forces the texture manager to load significantly lower-resolution versions of textures by skipping mipmap levels.

*   **Flag:** `FIntDebugTextureManagerSkipMips`
*   **JSON Example (Aggressive):**
    ```json
    {
          "FIntDebugTextureManagerSkipMips": "8"
    }
    ```
*   **Purpose:** Instructs the texture loader to skip the specified number of higher-resolution mipmap levels for *all* textures.
*   **Default Value:** `0`.
*   **Effects:**
    *   `1-4`: Textures become progressively blurrier.
    *   `5-7`: Textures become very low quality; classic studs on baseplates may disappear.
    *   `8`: Extreme effect, textures are almost entirely removed or reduced to basic colors. UI elements and icons are also affected.
*   **Impact:** Drastically reduces texture memory usage and can improve performance on VRAM-limited systems, but severely degrades visual quality.

#### Force Shiny Avatars / Materials
Manipulates material rendering properties to make surfaces appear extremely shiny or metallic.

*   **Flags:**
    *   `DFIntRenderClampRoughnessMax`
    *   `DFIntDebugFRMQualityLevelOverride`
*   **JSON Example:**
    ```json
    {
          "DFIntRenderClampRoughnessMax": "-640000000",
          "DFIntDebugFRMQualityLevelOverride": "6"
    }
    ```
*   **Purpose:**
    *   `DFIntRenderClampRoughnessMax`: Clamps the maximum roughness value of materials. Setting this to a large negative number likely forces roughness towards zero (very smooth/shiny).
    *   `DFIntDebugFRMQualityLevelOverride`: Overrides a quality level possibly related to Fidelity/Roughness/Metalness (PBR properties). The value `6` might force a specific high-reflectivity preset.
*   **Default Values:** Non-negative roughness clamp, likely no override (`-1` or `0`).
*   **Effects:** Causes materials, particularly on avatars using PBR textures, to appear unnaturally shiny, reflective, or metallic.

---

### Client Behavior and UI

#### Optimize Login Page Images
Enables the use of optimized PNG images on the Roblox login screen.

*   **Flag:** `FFlagLoginPageOptimizedPngs`
*   **JSON Example:**
    ```json
    {
          "FFlagLoginPageOptimizedPngs": "true"
    }
    ```
*   **Purpose:** Instructs the client to load potentially smaller or faster-parsing versions of image assets used on the login page.
*   **Default Value:** `False`.
*   **Effects:** May lead to slightly faster loading times for the login screen or reduced initial memory footprint.

#### Smoother Trackpad Scrolling
Improves the scrolling behavior when using a laptop trackpad in Roblox UI elements.

*   **Flag:** `FFlagBetterTrackpadScrolling`
*   **JSON Example:**
    ```json
    {
          "FFlagBetterTrackpadScrolling": "True"
    }
    ```
*   **Purpose:** Enables a scrolling mode better suited for the continuous input from trackpads, avoiding the large, discrete steps typical of standard mouse wheel emulation.
*   **Default Value:** `False`.
*   **Effects:** Provides a noticeably smoother, more fluid scrolling experience in lists and scrollable frames when using a trackpad. Has minimal to no effect when using a standard external mouse wheel.

#### Set Initial Graphics Quality Level
Forces Roblox to start with a specific graphics quality level (1-10).

*   **Flag:** `FIntRomarkStartWithGraphicQualityLevel`
*   **JSON Example (Force Level 1):**
    ```json
    {
          "FIntRomarkStartWithGraphicQualityLevel": "1"
    }
    ```
*   **Purpose:** Overrides the automatic graphics quality detection or the last used setting upon client startup, forcing it to initialize at the specified level.
*   **Default Value:** `-1` or `0` (indicating automatic detection).
*   **Effects:** Ensures Roblox always launches at a chosen graphics setting, useful for consistency or forcing low settings on underpowered machines.

#### Enable Preferred Text Size Options (Beta)
Activates a suite of beta features allowing users to adjust the text size across various parts of the Roblox UI.

*   **Flags:** (Includes numerous related flags)
    *   `FFlagEnablePreferredTextSizeGuiService`
    *   `FFlagEnablePreferredTextSizeScale`
    *   `FFlagEnablePreferredTextSizeSettingInMenus2`
    *   `FIntPreferredTextSizeSettingBetaFeatureRolloutPercent`
    *   `FFlagEnablePreferredTextSizeStyleFixesInAppShell3`
*   **JSON Example:**
    ```json
    {
       "FFlagEnablePreferredTextSizeGuiService": true,
       "FFlagEnablePreferredTextSizeScale": true,
       "FFlagEnablePreferredTextSizeSettingInMenus2": true,
       "FIntPreferredTextSizeSettingBetaFeatureRolloutPercent": 100,
       "FFlagEnablePreferredTextSizeStyleFixesInAppShell3": true
    }
    ```
*   **Purpose:** Collectively enables an accessibility feature allowing users to select a preferred text size, which then scales text in supported UI elements like menus, player lists, prompts, etc.
*   **Default Values:** `False` for most enabling flags, `0` for rollout percent.
*   **Effects:** Adds a text size slider or option within the Roblox settings menu, allowing users to increase or decrease text size for better readability. Requires enabling multiple related flags to function correctly across different UI components.

### UI and Menu Customization

#### Cleaner Escape Menu
Removes several options and toggles from the standard Roblox Escape Menu for a less cluttered appearance.

*   **Flags:**
    *   `FIntV1MenuLanguageSelectionFeaturePerMillageRollout`
    *   `FFlagAlwaysShowVRToggleV3`
    *   `FFlagEnableTFFeedbackModeEntryCheck`
    *   `FFlagDisableFeedbackSoothsayerCheck`
    *   `FFlagAddHapticsToggle`
    *   `FFlagChatTranslationSettingEnabled3`
*   **JSON Example:**
    ```json
    {
       "FIntV1MenuLanguageSelectionFeaturePerMillageRollout": "0",
       "FFlagAlwaysShowVRToggleV3": "False",
       "FFlagEnableTFFeedbackModeEntryCheck": "False",
       "FFlagDisableFeedbackSoothsayerCheck": "False",
       "FFlagAddHapticsToggle": "False",
       "FFlagChatTranslationSettingEnabled3": "False"
    }
    ```
*   **Purpose:** Each flag disables a specific feature or UI element within the Escape Menu:
    *   `FIntV1MenuLanguageSelectionFeaturePerMillageRollout`: Disables rollout of a language selection feature.
    *   `FFlagAlwaysShowVRToggleV3`: Hides the VR toggle.
    *   `FFlagEnableTFFeedbackModeEntryCheck`, `FFlagDisableFeedbackSoothsayerCheck`: Disable feedback-related options.
    *   `FFlagAddHapticsToggle`: Hides the Haptics toggle.
    *   `FFlagChatTranslationSettingEnabled3`: Disables the chat translation setting entry.
*   **Default Values:** Varies, typically enabling these features (`1000` rollout, `True` for flags).
*   **Effects:** Results in a simplified Escape Menu by hiding less commonly used or beta features.

> [!NOTE]
> To retain the Chat Translation setting while applying other cleanup flags, simply remove `"FFlagChatTranslationSettingEnabled3": "False"` from the JSON configuration.

#### Revert to Older In-Game Menu Versions
Forces the client to use specific older versions of the In-Game Escape Menu UI.

*   **Flags:**
    *   `FIntNewInGameMenuPercentRollout3`
    *   `FFlagEnableInGameMenuChromeABTest4`
    *   (Possibly others like `FFlagEnableInGameMenuControls`, `FFlagDisableNewIGMinDUA`, `FFlagEnableInGameMenuChrome` depending on the specific version desired and current client state).
*   **JSON Examples:**
    *   **V2 Menu:**
        ```json
        {
           "FIntNewInGameMenuPercentRollout3": "100",
           "FFlagEnableInGameMenuChromeABTest4": "False"
           // Add "FFlagEnableInGameMenuControls": "False", "FFlagDisableNewIGMinDUA": "True" if needed
        }
        ```
    *   **V4 Menu (No Chrome UI):**
        ```json
        {
           "FIntNewInGameMenuPercentRollout3": "0",
           "FFlagEnableInGameMenuChromeABTest4": "False"
           // Add "FFlagEnableInGameMenuControls": "False", "FFlagDisableNewIGMinDUA": "True" if needed
        }
        ```
    *   **V4 Menu with New Chrome UI (Hamburger/Mic icons):**
        ```json
        {
           "FIntNewInGameMenuPercentRollout3": "0",
           "FFlagEnableInGameMenuChromeABTest4": "True"
           // Add "FFlagEnableInGameMenuChrome": "True" if needed
        }
        ```
*   **Purpose:** Overrides the default menu version determined by Roblox rollouts. `FIntNewInGameMenuPercentRollout3` controls participation in the *newest* menu rollout (setting to `0` opts out), while `FFlagEnableInGameMenuChromeABTest4` controls a specific A/B test for the top-bar "Chrome" UI elements.
*   **Default Values:** Usually `0` for rollout (meaning latest stable), `False` for AB test flags unless user is enrolled.
*   **Effects:** Changes the visual appearance and layout of the Escape Menu to match older designs (V2, V4). Functionality remains largely the same.

> [!NOTE]
> The exact flags required may change over time as Roblox updates the menu system. Conflicting menu-related flags can prevent these overrides from working correctly. Some games might also force a specific menu version. The method using `FStringNewInGameMenuForcedUserIds` is generally not recommended due to complexity.

#### Refactor Experience Menu (Experimental/Buggy)
Enables an experimental refactoring of the in-experience game settings menu.

*   **Flag:** `FFlagRefactorInExpGameSettings2`
*   **JSON Example:**
    ```json
    {
       "FFlagRefactorInExpGameSettings2": "true"
    }
    ```
*   **Purpose:** Activates a redesigned or internally restructured version of the settings panel accessible from the Escape Menu.
*   **Default Value:** `False`.
*   **Effects:** Changes the appearance and potentially the organization of the Settings menu.

> [!WARNING]
> This flag is noted as potentially buggy. Use with caution, as it might lead to UI issues or instability within the settings panel.

---

### Rendering and Graphics

#### Disable Highlights
Disables the rendering of the "Highlight" instance effect, which adds outlines or overlays to objects.

*   **Flag:** `DFFlagRenderHighlightManagerPrepare`
*   **JSON Example:**
    ```json
    {
       "DFFlagRenderHighlightManagerPrepare": "true" // Setting to true seems to *disable* rendering
    }
    ```
*   **Purpose:** Appears to control a preparation step for rendering highlights. Setting it to `true` might cause this step to bypass the actual rendering, effectively disabling them.
*   **Default Value:** `False`.
*   **Effects:** Objects with Highlight instances applied will no longer display the outline/overlay effect. Can potentially improve performance slightly if highlights are used extensively.

#### Draw Test Image on Items/Icons
Replaces item icons, UI images, and potentially other textures with a default white or red test image.

*   **Flag:** `FFlagDebugTestImageDrawItem`
*   **JSON Example:**
    ```json
    {
       "FFlagDebugTestImageDrawItem": "true"
    }
    ```
*   **Purpose:** A debug flag to test image loading or rendering paths by substituting a standard test pattern.
*   **Default Value:** `False`.
*   **Effects:** Most icons in the UI (inventory, menus, etc.) become plain white squares. May cause other visual artifacts like full-screen red flashes during certain events (e.g., taking damage).

> [!WARNING]
> This is a debug flag and severely impacts usability by obscuring icons. Not intended for regular use.

#### Fix Potential Graphics Bug
Disables enrollment in a specific graphics optimization experiment, potentially fixing related visual bugs.

*   **Flag:** `DFFlagGraphicsOptimizationModeMVPExposureEnrollment4`
*   **JSON Example:**
    ```json
    {
       "DFFlagGraphicsOptimizationModeMVPExposureEnrollment4": "False"
    }
    ```
*   **Purpose:** Opts the user out of a specific A/B test or experimental graphics optimization feature (`MVPExposure`).
*   **Default Value:** `True` (if user is enrolled in the experiment) or `False`.
*   **Effects:** Reverts graphics behavior to the non-experimental path, which might resolve visual glitches or performance issues introduced by the experiment.

#### Force Gray Skybox
Replaces the current game's skybox with a plain gray color.

*   **Flag:** `FFlagDebugSkyGray`
*   **JSON Example:**
    ```json
    {
       "FFlagDebugSkyGray": "True"
    }
    ```
*   **Purpose:** A debug flag to force a simple, untextured gray sky, likely for testing lighting or performance without skybox influence.
*   **Default Value:** `False`.
*   **Effects:** Removes the visual skybox, replacing it with a uniform gray. May slightly improve performance by reducing texture load and rendering complexity related to the sky.

#### Use Legacy Shaders
Forces the client to use older shader programs for lighting calculations.

*   **Flag:** `FFlagShaderLightingRefactor`
*   **JSON Example:**
    ```json
    {
       "FFlagShaderLightingRefactor": "false"
    }
    ```
*   **Purpose:** Disables a newer, refactored lighting shader system, reverting to a previous implementation.
*   **Default Value:** `True` (enabling the refactored shaders).
*   **Effects:** Changes the appearance of lighting and shadows. May offer a performance boost on some hardware or resolve visual bugs present in the newer shaders, potentially at the cost of visual fidelity or features.

#### Optimize Vertex Buffer Technique
Enables an alternative technique for optimizing mesh vertex buffers.

*   **Flag:** `FIntRenderMeshOptimizeVertexBuffer`
*   **JSON Example (Enable Option 1):**
    ```json
    {
       "FIntRenderMeshOptimizeVertexBuffer": "1"
    }
    ```
*   **JSON Example (Android Default):**
    ```json
    {
       "FIntRenderMeshOptimizeVertexBuffer": "3"
    }
    ```
*   **Purpose:** Selects a specific method (indicated by the integer value) for optimizing vertex buffer data associated with meshes. Different values likely represent different optimization strategies.
*   **Default Value:** `0` (likely no specific optimization or a baseline method on PC), `3` on Android.
*   **Effects:** Potentially improves rendering performance by reducing the amount of vertex data processed by the GPU or optimizing its format/layout. The impact may vary depending on the hardware and the specific optimization technique selected (value `1`).

---

### Performance and System

#### Threading Control (Experimental)
Includes flags for debugging render threading and setting thread limits for the task scheduler.

*   **Flags:**
    *   `FFlagDebugCheckRenderThreading`
    *   `FFlagRenderDebugCheckThreading2`
    *   `FIntRuntimeMaxNumOfThreads`
    *   `FIntTaskSchedulerThreadMin`
*   **JSON Example:**
    ```json
    {
       "FFlagDebugCheckRenderThreading": "True",
       "FFlagRenderDebugCheckThreading2": "True",
       "FIntRuntimeMaxNumOfThreads": "2400", // Likely excessive, use caution
       "FIntTaskSchedulerThreadMin": "0"
    }
    ```
*   **Purpose:**
    *   `FFlagDebugCheckRenderThreading`, `FFlagRenderDebugCheckThreading2`: Enable diagnostic checks related to multi-threaded rendering.
    *   `FIntRuntimeMaxNumOfThreads`: Sets a potential upper limit on the total number of threads the runtime might attempt to use.
    *   `FIntTaskSchedulerThreadMin`: Sets the minimum number of threads maintained by the task scheduler.
*   **Default Values:** `False` for debug flags, system-determined thread counts.
*   **Effects:** Enabling debug flags may add performance overhead. Modifying thread counts can significantly impact performance and stability.

> [!WARNING]
> Modifying thread count flags like `FIntRuntimeMaxNumOfThreads` with extremely high values is highly experimental and can lead to severe instability, high resource usage, or crashes. Default values are usually determined based on system hardware (CPU cores). Setting `FIntTaskSchedulerThreadMin` to `0` might be reasonable, allowing the scheduler more flexibility. Use extreme caution with these flags.

#### Limit Console Message Length
Truncates long messages printed to the developer console.

*   **Flag:** `FIntStandardOutputMaximumCharacterLength`
*   **JSON Example (Truncate to 100 chars):**
    ```json
    {
       "FIntStandardOutputMaximumCharacterLength": "100"
    }
    ```
*   **Purpose:** Sets the maximum number of characters allowed for a single message logged to the standard output (developer console). Longer messages will be cut short and appended with `[trimmed]`.
*   **Default Value:** `100000` (100k characters).
*   **Effects:** Can make the developer console less cluttered by shortening very long log entries, especially repetitive ones. Does not bypass the absolute maximum message size limit (around 16k).

#### Optimize Friends List Cache (Experimental)
Enables an optimization technique for caching the friends list.

*   **Flag:** `DFIntFriendsListCacheOptimizationRolloutPercentage`
*   **JSON Example:**
    ```json
    {
       "DFIntFriendsListCacheOptimizationRolloutPercentage": "100"
    }
    ```
*   **Purpose:** Fully enables (at 100% rollout) an experimental optimization for how the client caches and retrieves friend data.
*   **Default Value:** `0`.
*   **Effects:** May improve performance related to loading or interacting with the friends list.

> [!WARNING]
> This flag has been reported to potentially cause client crashes. Enable with caution and disable if instability occurs.

#### Aggressive Asset Preloading
Enables a wide range of flags aimed at preloading various asset types (meshes, sounds, textures, fonts) more aggressively, potentially reducing loading hitches during gameplay or teleports, while disabling related telemetry.

*   **Flags:** (Includes numerous related flags for different asset types and contexts)
    *   `DFFlagEnableMeshPreloading2`
    *   `DFFlagEnableSoundPreloading`
    *   `DFFlagEnableTexturePreloading`
    *   `DFFlagTeleportClientAssetPreloadingEnabled9`
    *   `DFIntNumAssetsMaxToPreload`
    *   `FFlagPreloadAllFonts`
    *   `DFIntContentProviderPreloadHangTelemetryHundredthsPercentage`
    *   `FFlagContentProviderPreloadHangTelemetry`
    *   ... (and many others)
*   **JSON Example (Combined & Updated):**
    ```json
    {
        "DFFlagEnableMeshPreloading2": "true",
        "DFFlagEnableSoundPreloading": "true",
        "DFFlagEnableTexturePreloading": "true",
        "DFFlagTeleportClientAssetPreloadingDoingExperiment2": "true",
        "DFFlagTeleportClientAssetPreloadingEnabled9": "true",
        "DFFlagTeleportClientAssetPreloadingEnabledIXP": "true",
        "DFFlagTeleportClientAssetPreloadingEnabledIXP2": "true",
        "DFFlagTeleportPreloadingMetrics5": "true", // Note: This might enable metrics/telemetry despite other flags
        "DFIntContentProviderPreloadHangTelemetryHundredthsPercentage": "0",
        "DFIntNumAssetsMaxToPreload": "2147483647",
        "FFlagAssetPreloadingIXP": "true",
        "FFlagContentProviderPreloadHangTelemetry": "false",
        "FFlagPreloadAllFonts": "true",
        "FFlagPreloadTextureItemsOption4": "true",
        "DFIntTeleportClientAssetPreloadingHundredthsPercentage": "100000",
        "DFIntTeleportClientAssetPreloadingHundredthsPercentage2": "100000",
        "DFFlagTeleportClientAssetPreloadingDoingExperiment": "True"
        // Flags like FFlagLuaAppGamesPagePreloadingDisabled: false, FFlagRemoveRedundantFontPreloading: true etc. can also be included from the original list.
    }
    ```
*   **Purpose:** Forces the client to preload a wider variety and potentially larger number of game assets before they are needed (e.g., during loading screens, before teleports). Flags also attempt to disable telemetry related to preloading hangs or performance metrics. `DFIntNumAssetsMaxToPreload` set to max 32-bit integer effectively removes the limit on preload count.
*   **Default Values:** `False` or `0` for most, limiting preloading.
*   **Effects:** Can potentially reduce in-game stuttering or loading times when encountering new assets or teleporting, by having them already loaded into memory. May increase initial loading times and memory usage significantly.

> [!WARNING]
> Enabling such aggressive preloading with an essentially unlimited asset count (`DFIntNumAssetsMaxToPreload`) can lead to very high memory consumption and potentially client instability or crashes, especially on systems with limited RAM. Some telemetry flags (`DFFlagTeleportPreloadingMetrics5`) might still be active despite others being disabled. Use with caution and monitor resource usage.

### Rendering and Visual Effects

#### Brighter Visuals / Fog Adjustment
Applies a fix related to fog rendering, which can result in brighter visuals or altered atmospheric effects.

*   **Flag:** `FFlagRenderFixFog`
*   **JSON Example:**
    ```json
    {
       "FFlagRenderFixFog": "True"
    }
    ```
*   **Purpose:** Intended to correct issues with fog calculations or rendering.
*   **Default Value:** `False`.
*   **Effects:** Often makes the scene appear brighter by reducing the density or impact of distance fog. However, it can introduce a noticeable blue tint to the overall image or reduce the visibility of effects like sunrays (god rays) in certain environments. The visual outcome heavily depends on the specific game's lighting and fog settings.

> [!NOTE]
> While this can increase visibility in foggy conditions, the potential blue tint and impact on other atmospheric effects might be undesirable depending on the game and user preference.

#### Disable Grass Rendering
Completely disables the rendering of decorative grass details.

*   **Flags:**
    *   `FIntFRMMinGrassDistance`
    *   `FIntFRMMaxGrassDistance`
    *   `FIntRenderGrassDetailStrands`
*   **JSON Example:**
    ```json
    {
       "FIntFRMMinGrassDistance": "0",
       "FIntFRMMaxGrassDistance": "0",
       "FIntRenderGrassDetailStrands": "0"
    }
    ```
*   **Purpose:** Controls the distance range and density (strands) for rendering grass. Setting these values to `0` effectively prevents grass from being drawn.
*   **Default Values:** Positive integers defining the standard grass rendering parameters.
*   **Effects:** Removes all decorative grass from the terrain. Can provide a noticeable performance increase in environments with dense grass coverage, at the cost of visual detail.

#### Disable Highlights (Vulkan/OpenGL Specific)
May disable or alter the rendering of Highlight instances when using Vulkan or OpenGL graphics APIs.

*   **Flag:** `FFlagHighlightOutlinesOnMobile`
*   **JSON Example:**
    ```json
    {
       "FFlagHighlightOutlinesOnMobile": "True"
    }
    ```
*   **Purpose:** Ostensibly controls highlight outlines on mobile platforms. However, it has been reported to have a side effect of disabling or affecting Highlight instance rendering when using Vulkan or OpenGL on PC.
*   **Default Value:** `False`.
*   **Effects:** If using Vulkan or OpenGL, setting this to `True` might prevent Highlight outlines/overlays from appearing.

> [!NOTE]
> The intended purpose of this flag seems different from its reported effect on Vulkan/OpenGL rendering. Its behavior might be unintentional or change in future updates. This likely does *not* affect DirectX rendering.

#### Override FRM Quality Level
Allows manual override of the internal quality level used by the Framerate Manager (FRM), affecting various rendering details.

*   **Flag:** `DFIntDebugFRMQualityLevelOverride`
*   **JSON Example (Force Low Quality):**
    ```json
    {
       "DFIntDebugFRMQualityLevelOverride": "1"
    }
    ```
*   **Purpose:** Forces the engine to use a specific internal quality profile, bypassing automatic adjustments based on performance.
*   **Default Value:** `-1` or `0` (indicating no override).
*   **Effects:** Can force lower or higher levels of detail for various rendering features managed by the FRM. The mapping between the override value and the internal quality level is complex (e.g., Low: 1->3, 2->2, 3->6; High: 4->7, 5->11, 6->14, etc.). Allows for fine-tuning or forcing consistency in rendering quality.

#### Low Render Distance (Streaming Enabled)
Forces a significantly reduced render distance for objects managed by Roblox's streaming system.

*   **Flag:** `DFIntDebugRestrictGCDistance`
*   **JSON Example (Very Short Distance):**
    ```json
    {
       "DFIntDebugRestrictGCDistance": "1"
    }
    ```
*   **Purpose:** Sets the distance at which streamed-in objects are rendered and potentially garbage collected (unloaded). Lower values mean shorter distances.
*   **Default Value:** A higher integer representing the standard render distance.
*   **Effects:** Objects will load/appear much closer to the camera and unload more quickly when moving away. This can drastically improve performance in large games that utilize `StreamingEnabled`, but severely limits visual range, causing noticeable pop-in/out.

> [!IMPORTANT]
> This flag only has an effect in experiences where `StreamingEnabled` is turned on by the developer. You can check this by opening the Developer Console (Shift+F3) in-game.

#### Enable Newer CSG Implementation (V4)
Enables features related to an updated Constructive Solid Geometry (CSG) system (V4) and its API.

*   **Flags:**
    *   `FFlagSimCSG4EnableMesh`
    *   `FFlagNewCSGAPIBetaFeature` (Potentially Studio-only)
    *   `FFlagCSG4StudioBetaFeature` (Potentially Studio-only)
*   **JSON Example:**
    ```json
    {
       "FFlagSimCSG4EnableMesh": "True",
       "FFlagNewCSGAPIBetaFeature": "True",
       "FFlagCSG4StudioBetaFeature": "True"
    }
    ```
*   **Purpose:** Opts into a newer engine backend for handling CSG operations (unions, negations). `FFlagSimCSG4EnableMesh` is likely the primary flag affecting the client simulation.
*   **Default Value:** `False` for all.
*   **Effects:** May improve performance or reliability of CSG operations, potentially fixing bugs present in the older system.

> [!NOTE]
> The `BetaFeature` flags might only affect Roblox Studio. Enabling just `FFlagSimCSG4EnableMesh` might be sufficient for client-side changes. As with any major system change, this could potentially introduce new or different bugs.

#### Highlight Specific Font Usage (Debug)
Renders all text using a specified font family in red for debugging purposes.

*   **Flag:** `FStringDebugHighlightSpecificFont`
*   **JSON Example (Highlight BuilderSans):**
    ```json
    {
       "FStringDebugHighlightSpecificFont": "rbxasset://fonts/families/BuilderSans.json"
    }
    ```
*   **Purpose:** Used to visually identify where a particular font is being applied in the UI.
*   **Default Value:** `""` (Empty string, disabled).
*   **Effects:** All text rendered with the font specified in the value (e.g., `BuilderSans.json`) will appear bright red. Requires the client to be using the specified font (often the default Roblox font).

> [!CAUTION]
> This is purely a visual debugging tool. It can make text hard to read and may appear glitchy in certain UI elements like the settings menu.

#### Display Unthemed Instances (Debug - Rainbow Text)
Highlights UI elements that are not correctly using the current UI theme with cycling rainbow colors.

*   **Flag:** `FFlagDebugDisplayUnthemedInstances`
*   **JSON Example:**
    ```json
    {
       "FFlagDebugDisplayUnthemedInstances": "True"
    }
    ```
*   **Purpose:** Helps UI developers identify instances that don't adhere to the active theme (e.g., color scheme).
*   **Default Value:** `False`.
*   **Effects:** Unthemed elements, often including text labels, will flash or cycle through bright colors, creating a "rainbow" effect.

> [!CAUTION]
> This is a debug flag that makes the UI very distracting and unusable for normal gameplay.

---

### Networking and Data Transmission

#### Adjust Data/Physics Send Rates
Controls the frequency at which general game data and physics updates are sent from the client to the server.

*   **Flags:**
    *   `DFIntDataSenderRate` (Default: 60 Hz)
    *   `DFIntS2PhysicsSenderRate` (Default: 15 Hz)
    *   `DFIntPhysicsSenderMaxBandwidthBps` (Default: 38760 Bps)
*   **JSON Example (Increased Rates within Default Bandwidth):**
    ```json
    {
       "DFIntDataSenderRate": "38760",
       "DFIntS2PhysicsSenderRate": "38760"
    }
    ```
*   **JSON Example (Exceeding Default Bandwidth - Requires Limit Increase):**
    ```json
    {
       "DFIntPhysicsSenderMaxBandwidthBps": "60000", // Increased bandwidth limit
       "DFIntS2PhysicsSenderRate": "60000"         // New rate at or below the limit
    }
    ```
*   **Purpose:** Higher sender rates mean more frequent updates sent to the server, potentially reducing perceived latency for actions and movement. `DFIntPhysicsSenderMaxBandwidthBps` limits the bandwidth allocated specifically for physics updates.
*   **Effects:** Increasing rates can make gameplay feel more responsive *if* the network connection can handle the increased traffic. Setting rates higher than the `DFIntPhysicsSenderMaxBandwidthBps` limit *without* increasing the limit itself will cause severe desynchronization ("ghost mode"), where your character moves locally but is stuck or invisible on the server.

> [!WARNING]
> Setting `DFIntDataSenderRate` or `DFIntS2PhysicsSenderRate` above the value of `DFIntPhysicsSenderMaxBandwidthBps` (default 38760) will cause major desync issues unless `DFIntPhysicsSenderMaxBandwidthBps` is also increased accordingly. Increasing these rates significantly increases upstream bandwidth usage. Test carefully. Use the linked "Desync Playground" game to visualize effects.

---

### UI and Client Behavior

#### Enable Blue UI Theme
Activates a specific color palette ("Foundation Colors") for the Roblox desktop application UI, often resulting in blue accents.

*   **Flag:** `FFlagLuaAppEnableFoundationColors7`
*   **JSON Example:**
    ```json
    {
       "FFlagLuaAppEnableFoundationColors7": "True"
    }
    ```
*   **Purpose:** Enables a specific version or iteration of the "Foundation Colors" theme system.
*   **Default Value:** Variable; may be `False` or `True` depending on Roblox rollouts and account age.
*   **Effects:** Changes the color scheme of the main Roblox application window and its UI elements, frequently introducing more blue.

> [!NOTE]
> This flag might already be enabled by default for many users or newer accounts as part of Roblox's ongoing UI updates.

#### Revert Chat Icon
Restores the older, classic chat bubble icon in the top-left corner of the screen during gameplay.

*   **Flag:** `FFlagAppChatRebrandIconUpdates`
*   **JSON Example:**
    ```json
    {
       "FFlagAppChatRebrandIconUpdates": "False"
    }
    ```
*   **Purpose:** Disables the updated/rebranded chat icon, reverting to the previous design.
*   **Default Value:** `True` (enabling the newer icon).
*   **Effects:** Replaces the newer chat icon with the more traditional speech bubble design. Purely a cosmetic change based on user preference.

#### Revert Builder Font Mapping
Opts out of an A/B test related to font name mappings, potentially reverting changes to the default "BuilderSans" font.

*   **Flag:** `FFlagEnableNewFontNameMappingABTest2`
*   **JSON Example:**
    ```json
    {
       "FFlagEnableNewFontNameMappingABTest2": "False"
    }
    ```
*   **Purpose:** Disables participation in an experiment that might alter how font names are resolved or which font file is used for standard text.
*   **Default Value:** `True` (if enrolled in the A/B test) or `False`.
*   **Effects:** If the A/B test caused visual changes to the default font, setting this to `False` may revert those changes.

---

### Audio

#### Adjust Voice Chat Volume
Allows increasing or decreasing the incoming voice chat volume beyond standard limits.

*   **Flag:** `DFIntVoiceChatVolumeThousandths`
*   **JSON Example (860% Volume):**
    ```json
    {
       "DFIntVoiceChatVolumeThousandths": "8600"
    }
    ```
*   **Purpose:** Sets the multiplier for incoming voice chat audio volume, where `1000` represents 100% or default volume.
*   **Default Value:** `1000`.
*   **Effects:** Useful for making quiet teammates louder or reducing the volume of loud ones beyond the normal settings slider. Values are in thousandths, so `8600` means 8.6x the default volume.

> [!TIP]
> Start with moderate adjustments (e.g., `1500` for 150%, `2000` for 200%) and increase as needed. Very high values like `8600` can be extremely loud.

---

### VR Specific

#### Optimize Mouse Movement in VR
Enables an optimization for handling physical mouse input while in a VR session.

*   **Flag:** `FFlagVRMouseMoveOptimization`
*   **JSON Example:**
    ```json
    {
       "FFlagVRMouseMoveOptimization": "true"
    }
    ```
*   **Purpose:** Aims to improve the performance or smoothness of mouse cursor movement within the Roblox VR environment when using a traditional mouse.
*   **Default Value:** `False`.
*   **Effects:** May provide a better experience when interacting with UI elements using a mouse in VR. Has no effect outside of VR sessions.

> [!NOTE]
> This flag is only relevant for users playing Roblox in Virtual Reality mode.

### Performance and Telemetry

#### Disable Performance Data Capture Interval
Disables the periodic capture of performance counters by setting the interval to zero.

*   **Flag:** `CaptureCountersIntervalInMinutes` (Note: This is a C++ variable, not a standard FFlag prefix, but can sometimes be set via client settings)
*   **JSON Example:**
    ```json
    {
       "CaptureCountersIntervalInMinutes": "0"
    }
    ```
*   **Purpose:** Controls how often, in minutes, the client gathers and potentially reports performance metrics. Setting it to `0` disables this timed capture.
*   **Default Value:** `5` (Capture every 5 minutes).
*   **Effects:** Prevents the client from periodically collecting performance data, which might reduce extremely minor background overhead.

> [!NOTE]
> This variable originates from C++ code (`FVariables.txt`) and might require manual addition to the `ClientAppSettings.json` file if not directly supported by FFlag editors like Bloxstrap. It doesn't use standard `F`/`DF`/`SF` prefixes. Bloxstrap and similar tools might need specific handling or manual JSON editing for such variables.

#### Disconnect Unrequired Input Connections
Enables an optimization to disconnect input-related event connections when they are no longer needed.

*   **Flag:** `FFlagUserUpdateInputConnections`
*   **JSON Example:**
    ```json
    {
       "FFlagUserUpdateInputConnections": "True"
    }
    ```
*   **Purpose:** Allows the system to clean up (disconnect) connections related to user input processing when they become redundant.
*   **Default Value:** `True`.
*   **Effects:** Potentially improves memory management and reduces minor overhead by ensuring unused input listeners are properly removed.

> [!NOTE]
> This flag appears to be enabled (`True`) by default in recent Roblox versions, so explicitly setting it may not be necessary unless trying to override a potential `False` state from an older configuration.

#### Faster Game Loading (Player Image Timeout)
Adjusts the timeout duration for fetching player images during the game loading process.

*   **Flag:** `FStringGetPlayerImageDefaultTimeout`
*   **JSON Example (Faster Timeout):**
    ```json
    {
       "FStringGetPlayerImageDefaultTimeout": "5"
    }
    ```
*   **JSON Example (Very Fast Timeout):**
    ```json
    {
       "FStringGetPlayerImageDefaultTimeout": "1"
    }
    ```
*   **Purpose:** Sets the maximum time (likely in seconds, despite being `FString`) the client waits for player thumbnails/images during the initial game join sequence. Lower values make it give up faster if images are slow to load.
*   **Default Value:** `"12"`.
*   **Effects:** Setting a lower value (e.g., `1` to `5`) can significantly speed up the transition from the loading screen into the actual game environment, especially if player image fetching is a bottleneck. The game will proceed without waiting long for slow-loading images.

> [!CAUTION]
> While lower values speed up *joining* the game, they don't necessarily speed up the overall asset loading within the game itself. Setting it too low might lead to player thumbnails appearing blank initially more often. Some users noted it might increase resource usage slightly during the faster load phase, potentially because other loading steps are less interleaved with waiting for images.

#### Enable Memory Probing (Optimization)
Enables a memory probing feature intended to optimize memory usage, particularly for systems with limited RAM.

*   **Flag:** `DFFlagPerformanceControlEnableMemoryProbing3`
*   **JSON Example (Enable):**
    ```json
    {
       "DFFlagPerformanceControlEnableMemoryProbing3": "True"
    }
    ```
*   **Purpose:** Activates a system that monitors memory usage and potentially makes adjustments to reduce the client's memory footprint.
*   **Default Value:** `False`.
*   **Effects:** When enabled (`True`), it may help reduce RAM usage, which could improve stability and performance on low-memory devices.

> [!TIP]
> Consider enabling this (`True`) if you are experiencing crashes or performance issues related to high memory usage, especially on PCs with 8GB of RAM or less.

#### Enable Luau Native Code Generation (Codegen)
Allows the Luau virtual machine to compile scripts directly into native machine code for potentially faster execution.

*   **Flag:** `FFlagLuauCodegen`
*   **JSON Example:**
    ```json
    {
       "FFlagLuauCodegen": "True"
    }
    ```
*   **Purpose:** Instead of interpreting Luau bytecode, this enables the Just-In-Time (JIT) compiler to translate frequently run script portions into native CPU instructions.
*   **Default Value:** `False` (Client-side execution typically uses the interpreter).
*   **Effects:** Can significantly improve the performance of computationally intensive Luau scripts. However, its effectiveness depends heavily on whether game developers have optimized their server-side scripts for codegen and the nature of the client-side scripts. It might slightly increase load times or memory usage for storing the compiled code.

> [!NOTE]
> This primarily benefits server-side script performance when enabled by developers. While setting it `True` client-side *might* apply to certain client scripts, many games may not see a noticeable difference. If a script is incompatible, Luau automatically falls back to the interpreter. Check the Developer Console (F9) for messages related to codegen status if enabled. The flag `FIntLuauCodeGenMaxTotalSize` can limit the amount of memory used for compiled code.

#### Disable Zstandard Compression for Client Settings
Disables the use of the Zstandard compression algorithm for the `ClientSettings` data.

*   **Flags:**
    *   `FFlagEnableZstdDictionaryForClientSettings`
    *   `FFlagEnableZstdForClientSettings`
*   **JSON Example (Disable):**
    ```json
    {
       "FFlagEnableZstdDictionaryForClientSettings": "false",
       "FFlagEnableZstdForClientSettings": "false"
    }
    ```
*   **Purpose:** These flags control whether Zstandard compression (potentially with a shared dictionary) is used for transmitting or storing client settings. Disabling forces the use of an older or no compression method.
*   **Default Value:** `True` (Zstd compression is enabled by default in recent versions).
*   **Effects:** Disabling Zstd might slightly increase the size of client settings data transmitted or stored, but could potentially resolve rare issues if Zstd decompression was causing problems. Generally, leaving it enabled (`True`) is recommended for efficiency.

> [!IMPORTANT]
> Zstandard compression is generally efficient. Disabling it (`false`) is typically unnecessary unless troubleshooting specific issues potentially related to settings loading or decompression. The default is now `True`.

---

### UI and Visuals

#### Fake Verified Icon (Self Only)
Adds the "Verified" checkmark icon next to your own username in various UI elements (client-side only).

*   **Flag:** `FStringWhitelistVerifiedUserId`
*   **JSON Example:**
    ```json
    {
       "FStringWhitelistVerifiedUserId": "YOUR_ROBLOX_ID"
    }
    ```
*   **Purpose:** Whitelists a specific Roblox User ID to display the verified icon next to their name.
*   **Default Value:** `""` (Empty string).
*   **Effects:** Purely cosmetic; adds the blue checkmark next to your name as seen by you. Replace `"YOUR_ROBLOX_ID"` with your actual numerical Roblox User ID.

> [!TIP]
> You can find your Roblox User ID by visiting your profile page on the Roblox website; the ID is the number in the URL (e.g., `roblox.com/users/12345678/profile` -> ID is `12345678`).

#### Fake Verified Icon (Everyone)
Forces the "Verified" checkmark icon to display next to *everyone's* username (client-side only).

*   **Flag:** `DFFlagUserRespectsVerifiedBadgeEnabled`
*   **JSON Example (from attached file):**
    ```json
    {
       "DFFlagUserRespectsVerifiedBadgeEnabled": false
    }
    ```
*   **Purpose:** This flag likely controls whether the client respects the actual verification status provided by the server/API. Setting it to `false` might bypass this check and apply the badge visual indiscriminately.
*   **Default Value:** `True`.
*   **Effects:** Causes the blue checkmark icon to appear next to every player's name in lists, chat, etc., as seen by you. Creates a visually confusing but potentially amusing effect.

> [!CAUTION]
> This modifies the visual display for *all* users, making it impossible to distinguish genuinely verified users. It's purely a client-side visual gag.

#### Faster Catalog Item Loading
Includes flags potentially related to optimizing the loading speed and display of items in the Roblox Catalog/Avatar Shop.

*   **Flags:**
    *   `FFlagEnableCatalogTileLoadingLatencyV2`
    *   `FFlagAXFixOutfitLoadingAfterPurchase`
*   **JSON Example:**
    ```json
    {
       "FFlagEnableCatalogTileLoadingLatencyV2": "true",
       "FFlagAXFixOutfitLoadingAfterPurchase": "True"
    }
    ```
*   **Purpose:**
    *   `FFlagEnableCatalogTileLoadingLatencyV2`: Likely enables optimizations related to how catalog item tiles (thumbnails) are loaded and displayed, possibly improving perceived speed.
    *   `FFlagAXFixOutfitLoadingAfterPurchase`: Addresses issues where the user's avatar might not update correctly immediately after purchasing an item and equipping it.
*   **Default Value:** `True` for both (in recent versions).
*   **Effects:** Aims to make browsing the avatar shop smoother and ensure avatar previews update promptly after purchases.

> [!NOTE]
> These flags are likely enabled (`True`) by default in current Roblox versions. Setting them explicitly might only be relevant if using an older configuration or if they were somehow disabled.

#### Revert Chrome UI Elements (Legacy - Patched)
Attempted to revert various top-bar UI elements (like the hamburger menu icon) to older designs.

*   **Flags:** (Included various flags like `FFlagEnableHamburgerIcon`, `FFlagEnableUnibarV4IA`, etc.)
*   **JSON Example (Historical):**
    ```json
    {
      "FFlagEnableHamburgerIcon": "False",
      "FFlagEnableUnibarV4IA": "False",
      // ... other flags ...
    }
    ```
*   **Status:** No longer effective.

> [!IMPORTANT]
> These flags related to reverting the "Chrome UI" (top bar elements) are reported as **no longer working** or patched out by Roblox updates. Attempting to use them will likely have no effect.

#### Disable Automatic Graphics Option in Settings
Removes the "Automatic" graphics quality option from the in-game settings menu.

*   **Flag:** `FFlagClientFRMManualToAutoExperimentCheck2`
*   **JSON Example:**
    ```json
    {
       "FFlagClientFRMManualToAutoExperimentCheck2": "false"
    }
    ```
*   **Purpose:** Disables an experiment or check related to switching between manual and automatic graphics settings, which seems to have the side effect of hiding the "Automatic" toggle/option.
*   **Default Value:** `True`.
*   **Effects:** Simplifies the Graphics Quality setting by removing the "Automatic" choice, forcing the user to select a specific manual level (1-10).

#### Disable Chrome UI Analytics
Disables analytics/telemetry specifically related to the top-bar "Chrome UI".

*   **Flag:** `FFlagEnableChromeAnalytics`
*   **JSON Example:**
    ```json
    {
       "FFlagEnableChromeAnalytics": "False"
    }
    ```
*   **Purpose:** Opts out of data collection regarding usage and performance of the main UI top bar elements.
*   **Default Value:** `True`.
*   **Effects:** Reduces the amount of telemetry data sent to Roblox related to UI interactions.

---

### Graphics and Rendering

#### Blacklist GPU for Unaligned DXT
Prevents the use of unaligned DXT texture compression formats on a specified GPU, potentially as a workaround for driver bugs or on low-end hardware.

*   **Flag:** `FStringGraphicsDisableUnalignedDxtGPUNameBlacklist`
*   **JSON Example:**
    ```json
    {
       "FStringGraphicsDisableUnalignedDxtGPUNameBlacklist": "NVIDIA GeForce GTX 1650" // Replace with your GPU name
    }
    ```
*   **Purpose:** Forces the graphics engine to avoid using potentially problematic "unaligned" DXT texture formats if the specified GPU name matches the system's GPU. DXT is a standard texture compression; "unaligned" might refer to specific non-standard variants or memory layouts.
*   **Default Value:** `""` (Empty string, no blacklist).
*   **Effects:** May prevent rendering artifacts or crashes on specific GPUs (especially older or lower-end ones) that have issues with certain DXT implementations, potentially at a minor performance cost or slight increase in VRAM usage if less efficient formats are used instead.

> [!IMPORTANT]
> You need to replace `"NVIDIA GeForce GTX 1650"` with the exact name of your graphics card as reported by tools like **Task Manager** (Performance tab -> GPU). Only use this if experiencing texture corruption or crashes potentially related to texture formats.

#### Enable Unified Lighting Technology (Experimental)
Forces the use of an experimental "Unified" lighting system.

*   **Flag:** `FFlagRenderUnifiedLighting12`
*   **JSON Example:**
    ```json
    {
       "FFlagRenderUnifiedLighting12": "True"
    }
    ```
*   **Purpose:** Enables a newer, potentially more advanced or optimized lighting rendering pipeline named "Unified".
*   **Default Value:** `False`.
*   **Effects:** Changes how lighting and potentially shadows are rendered. May offer performance improvements or different visual characteristics compared to "Future" or other lighting modes. Visual differences might be subtle depending on the game's lighting setup.

> [!NOTE]
> This is likely an experimental feature. Check the `Shift+F2` rendering stats menu to confirm if "Unified" is active. It might offer better performance than "Future" lighting in some scenarios.

### Rendering and Graphics Quality

#### Initialize Shadowmaps for Better Shadows
Enables an initialization process for shadow maps, potentially improving their quality at the cost of increased loading time.

*   **Flag:** `FFlagRenderInitShadowmaps`
*   **JSON Example:**
    ```json
    {
       "FFlagRenderInitShadowmaps": "true"
    }
    ```
*   **Purpose:** Activates a specific initialization step for shadow maps when rendering starts.
*   **Default Value:** `false`.
*   **Effects:** May result in visually better or more stable shadows. Users report potentially longer initial game loading times when enabled.

#### Shadowmap Bias Adjustment
Adjusts the depth bias applied to shadow maps, which can influence shadow accuracy and prevent artifacts like "shadow acne" or "peter-panning".

*   **Flag:** `FIntRenderShadowmapBias`
*   **JSON Example:**
    ```json
    {
       "FIntRenderShadowmapBias": "75"
    }
    ```
*   **Purpose:** Controls an offset used during shadow map rendering to reduce self-shadowing artifacts or gaps.
*   **Default Value:** Likely `0` or a small integer.
*   **Effects:** Modifying the bias can fine-tune shadow appearance. Higher values push shadows further away from the surface, potentially fixing acne but causing shadows to detach (peter-panning). Lower values do the opposite. Finding an optimal value often depends on the specific game's lighting and geometry. The value `75` is provided as an example.

> [!TIP]
> Adjusting shadow bias can be a way to improve shadow quality, particularly reducing artifacts on surfaces under "Future" or "ShadowMap" lighting technologies. Experimentation might be needed to find the best value for specific scenarios.

#### Fix Skybox Texture Blurriness
Attempts to fix issues causing skybox textures to appear blurry.

*   **Flag:** `DFFlagFixSkyBoxTextureBlurrines`
*   **JSON Example:**
    ```json
    {
       "DFFlagFixSkyBoxTextureBlurrines": "true"
    }
    ```
*   **Purpose:** Addresses potential rendering problems that lead to reduced sharpness in skybox textures.
*   **Default Value:** `false`.
*   **Effects:** When enabled, skybox textures may appear sharper and less blurry, improving visual fidelity of the game's sky.

#### Optimize Mesh Scaling Quality
Enables fixes or improvements related to how mesh parts are scaled, potentially improving visual quality.

*   **Flag:** `DFFlagFixMeshScale2`
*   **JSON Example (Enable Fix):**
    ```json
    {
       "DFFlagFixMeshScale2": "true"
    }
    ```
*   **Purpose:** Activates code intended to address issues or enhance the quality of rendering when MeshParts are scaled non-uniformly.
*   **Default Value:** `false`.
*   **Effects:** May result in better-looking meshes when they are scaled, reducing visual artifacts or distortion.

#### Optimize Texture Atlas for Lighting Grid
Enables an optimization for updating the texture atlas used by the lighting grid, potentially improving lighting quality.

*   **Flag:** `FFlagRenderLightGridEfficientTextureAtlasUpdate`
*   **JSON Example:**
    ```json
    {
       "FFlagRenderLightGridEfficientTextureAtlasUpdate": "true"
    }
    ```
*   **Purpose:** Activates a more efficient method for updating the texture atlas related to the light grid system (used for local light rendering).
*   **Default Value:** `false`.
*   **Effects:** Could lead to performance improvements in lighting updates or potentially enhance the visual quality and accuracy of local lighting effects.

---

### Physics and Animation

#### Custom Physics Steps Per Second (Studio Debug Feature)
Sets the number of physics simulation steps per second.

*   **Flag:** `FIntPhysicsStepsPerSecond`
*   **JSON Example:**
    ```json
    {
       "FIntPhysicsStepsPerSecond": "240" // Example value
    }
    ```
*   **Purpose:** (Intended for Studio) Allows developers to change the physics simulation frequency for debugging purposes.
*   **Default Value:** Typically `240` (for 240Hz simulation).
*   **Effects:** Modifying this value client-side is **not recommended** and likely **has no effect** or may cause severe physics desynchronization.

> [!WARNING]
> This flag is primarily a Roblox Studio debugging tool, as discussed in the linked DevForum post. It allows developers to step through physics simulation frames. Using it on the live client is unlikely to provide any benefit and might break physics synchronization with the server. It's also reported to be an 8-bit integer flag, limiting its potential range anyway. Avoid modifying this flag for regular gameplay.

#### Enable Interpolation Correction During FK Retargeting
Improves animation quality by applying interpolation corrections when retargeting animations using Forward Kinematics (FK).

*   **Flag:** `DFFlagAnimatorRetargetInterpolateFKCorrection`
*   **JSON Example:**
    ```json
    {
       "DFFlagAnimatorRetargetInterpolateFKCorrection": "true"
    }
    ```
*   **Purpose:** Fixes potential inaccuracies or awkward movements that can occur when an animation designed for one rig is applied (retargeted) to another rig with potentially different bone structures or proportions.
*   **Default Value:** `false`.
*   **Effects:** Leads to smoother and more visually correct animation playback on characters, especially when using animations not originally designed for that specific character model.

#### Fix Humanoid Root Part Raycasts
Applies fixes related to raycasts originating from the HumanoidRootPart, potentially affecting grounding and height calculations.

*   **Flag:** `DFFlagFixHumanoidRootPartRaycasts`
*   **JSON Example:**
    ```json
    {
       "DFFlagFixHumanoidRootPartRaycasts": "True"
    }
    ```
*   **Purpose:** Addresses potential issues or inaccuracies in the raycasts used by the Humanoid for detecting ground, calculating height, etc.
*   **Default Value:** `False`.
*   **Effects:** May change how humanoids interact with the ground or slopes. Also noted to affect the behavior of related flags like `DFIntMaxAltitudePDStickHipHeightPercent`.

> [!CAUTION]
> Users have reported that enabling this flag (`True`) **breaks camera behavior**. Use with caution, as it may negatively impact gameplay.

#### Optimize CFrame Updates
Enables optimizations for how CFrame (Coordinate Frame - position and rotation) updates are handled.

*   **Flag:** `FFlagOptimizeCFrameUpdates`
*   **JSON Example:**
    ```json
    {
       "FFlagOptimizeCFrameUpdates": "true"
    }
    ```
*   **Purpose:** Activates a more optimized code path for processing changes to the position and orientation of objects (Parts, Models).
*   **Default Value:** `false`.
*   **Effects:** May provide performance improvements, especially in scenarios with many moving parts or frequent CFrame manipulations, by reducing the computational overhead of these updates.

#### Real-Time Animation Refactor
Enables a refactored system for handling real-time animations.

*   **Flag:** `FFlagRealTimeAnimationEnableRefactor`
*   **JSON Example:**
    ```json
    {
       "FFlagRealTimeAnimationEnableRefactor": "true"
    }
    ```
*   **Purpose:** Activates a newer, potentially restructured backend for processing animations that update in real-time.
*   **Default Value:** `False`.
*   **Effects:** Might improve animation performance or behavior, but comes with a warning that it *can increase CPU load*.

> [!WARNING]
> Enabling this flag may lead to higher CPU usage. Monitor performance if you choose to enable it.

---

### Networking

#### Enable Next-Generation Replicator (V2)
Activates components of an updated network replication system ("Next Gen Replicator V2").

*   **Flags:**
    *   `FFlagNextGenReplicatorEnabledWrite2`
    *   `FFlagNextGenReplicatorEnabledRead2`
    *   `DFFlagNextGenRepRollbackOverbudgetPackets`
*   **JSON Example:**
    ```json
    {
       "FFlagNextGenReplicatorEnabledWrite2": "True",
       "FFlagNextGenReplicatorEnabledRead2": "True",
       "DFFlagNextGenRepRollbackOverbudgetPackets": "True"
    }
    ```
*   **Purpose:** Enables newer code paths for serializing (Write) and deserializing (Read) data being replicated over the network. Also enables logic for rolling back packet processing if budget limits are exceeded.
*   **Default Value:** `False` for all.
*   **Effects:** Aims to improve the efficiency and performance of network data transfer between the client and server, potentially leading to faster reads/writes of replicated data and better handling of network packets.

> [!TIP]
> Enabling this newer replication system could potentially reduce network latency or improve synchronization, especially in complex scenarios.

---

### Client Behavior and UI

#### Improve UWP JSON Parsing for Update Checks
Enables better JSON parsing specifically during the update check process for the UWP (Universal Windows Platform / Microsoft Store) version of Roblox.

*   **Flag:** `FFlagUWPBetterJsonParsingInUpdateCheck`
*   **JSON Example:**
    ```json
    {
       "FFlagUWPBetterJsonParsingInUpdateCheck": "true"
    }
    ```
*   **Purpose:** Implements improved or more robust JSON parsing logic used when the UWP client checks for updates.
*   **Default Value:** `false`.
*   **Effects:** Specific to the UWP version of Roblox. May make the update checking process more reliable or slightly faster if the previous parsing method had inefficiencies.

> [!NOTE]
> This flag only affects the Roblox client downloaded from the Microsoft Store (UWP version), not the standard web-downloaded desktop client.

#### Optimize Camera Movement Input Tracking
Disables tracking of the last input type used for camera control, potentially reducing minor stutters.

*   **Flag:** `FFlagUserCameraControlLastInputTypeUpdate`
*   **JSON Example:**
    ```json
    {
       "FFlagUserCameraControlLastInputTypeUpdate": "false"
    }
    ```
*   **Purpose:** This flag normally tracks whether the last input came from Keyboard, Mouse, Gamepad, etc. Disabling this tracking might slightly reduce processing overhead during camera movements.
*   **Default Value:** `true`.
*   **Effects:** Setting to `false` might lead to smoother camera movement by eliminating the minor overhead of constantly updating the last input type state. The effect is likely subtle.

#### Set Maximum Developer Console Log History
Controls the maximum number of messages retained in the Developer Console (F9).

*   **Flag:** `FIntNewDevConsoleMaxLogCount`
*   **JSON Example (Default):**
    ```json
    {
       "FIntNewDevConsoleMaxLogCount": "500"
    }
    ```
*   **JSON Example (Reduced History):**
    ```json
    {
       "FIntNewDevConsoleMaxLogCount": "100"
    }
    ```
*   **Purpose:** Defines the maximum number of log entries the Developer Console will store and display. Once the limit is reached, the oldest messages are removed as new ones arrive.
*   **Default Value:** `500`.
*   **Effects:** Allows increasing or decreasing the console's history buffer. Lower values reduce memory usage slightly but limit how far back you can scroll. Higher values allow retaining more history.

> [!WARNING]
> Setting `FIntNewDevConsoleMaxLogCount` to `0` will completely disable the Developer Console, preventing it from opening with F9 and stopping all message logging to it.

---

### Memory Management

#### Configure Memory Utility Curve Parameters
Adjusts parameters used by the engine's memory utility calculations, influencing how memory usage is evaluated and potentially managed.

*   **Flags:**
    *   `DFIntMemoryUtilityCurveBaseHundrethsPercent`
    *   `DFIntMemoryUtilityCurveNumSegments`
    *   `DFIntMemoryUtilityCurveTotalMemoryReserve`
*   **JSON Example (Aggressive Usage Assumption):**
    ```json
    {
       "DFIntMemoryUtilityCurveBaseHundrethsPercent": "10000",
       "DFIntMemoryUtilityCurveNumSegments": "100",
       "DFIntMemoryUtilityCurveTotalMemoryReserve": "0"
    }
    ```
*   **Purpose:**
    *   `BaseHundrethsPercent`: Sets the baseline assumption for memory utilization (10000 = 100%). High values assume memory is fully utilized.
    *   `NumSegments`: Defines the granularity of the utility curve used for calculations (more segments = potentially more accurate but more calculations).
    *   `TotalMemoryReserve`: Specifies an amount of memory to reserve, preventing the system from using it (0 = no reserve).
*   **Default Values:** Unknown, but likely represent less aggressive assumptions.
*   **Effects:** The provided example configuration (100% base, 100 segments, 0 reserve) forces the system to assume memory is always fully utilized and reserves no extra space. User testing suggests this configuration *increases* actual RAM usage (e.g., up to 4-5GB or more in some games).

> [!CAUTION]
> While potentially intended for tuning memory management, the example configuration appears to lead to significantly *higher* memory consumption. This might be beneficial on systems with ample RAM (e.g., 16GB+, especially 32GB) by allowing Roblox to utilize more memory freely, potentially reducing cache misses or loading, but could cause instability or performance issues on systems with less RAM (e.g., 8GB). Use with caution and monitor memory usage. Disabling Resizable BAR in NVIDIA settings was mentioned as a separate, potentially related tweak for memory management on newer GPUs.
