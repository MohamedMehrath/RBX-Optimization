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

### Rendering and Graphics

#### Use Older Collision Geometry System
Opts out of a refactored collision geometry system, reverting to an older version.

*   **Flag:** `DFFlagSimRefactorCollisionGeometry2`
*   **JSON Example (Use Older System):**
    ```json
    {
       "DFFlagSimRefactorCollisionGeometry2": "false"
    }
    ```
*   **Purpose:** Disables the V2 refactoring of the collision geometry system.
*   **Default Value:** `true` (Newer system enabled).
*   **Effects:** Reverts to the previous collision system. Might be used to troubleshoot physics bugs potentially introduced by the V2 refactor, possibly at the cost of performance or other V2 improvements.

#### Disable Shadows/Lighting via Pause Voxelizer
Pauses the voxelizer component, which effectively disables dynamic shadows and potentially other lighting calculations dependent on it.

*   **Flag:** `DFFlagDebugPauseVoxelizer`
*   **JSON Example:**
    ```json
    {
       "DFFlagDebugPauseVoxelizer": "True"
    }
    ```
*   **Purpose:** A debug flag to halt the operation of the voxel-based lighting system.
*   **Default Value:** `False`.
*   **Effects:** Disables features relying on the voxelizer, primarily dynamic shadows (like those from "ShadowMap" or "Future" lighting). This can significantly boost performance in complex lighting scenarios but drastically reduces visual fidelity.

> [!WARNING]
> This completely removes dynamic shadows and potentially other lighting effects, resulting in a very flat and unrealistic look. Use only for performance testing or specific low-fidelity needs.

#### Flags for Skipping Rendering Tasks
These flags control whether certain rendering steps are skipped, potentially improving performance at the cost of visual elements.

*   **Flags:**
    *   `FFlagRenderShadowSkipHugeCulling` (Skips shadow culling for very large objects)
    *   `FFlagRenderSkipReadingShaderData` (Skips reading certain shader data)
    *   `FFlagShoeSkipRenderMesh` (Skips rendering meshes specifically tagged as 'shoes')
*   **JSON Example:**
    ```json
    {
       "FFlagRenderShadowSkipHugeCulling": "true",
       "FFlagRenderSkipReadingShaderData": "false",
       "FFlagShoeSkipRenderMesh": "true" // Example: Enable shoe skipping
    }
    ```
*   **Purpose & Defaults:**
    *   `FFlagRenderShadowSkipHugeCulling`: Default `true`. Optimizes shadow culling for large distant objects. Setting to `false` might force rendering but is likely less performant.
    *   `FFlagRenderSkipReadingShaderData`: Default `true`. Skips reading certain shader data, likely an optimization. Setting to `false` forces reading, potentially for debugging or if the skipping causes issues.
    *   `FFlagShoeSkipRenderMesh`: Default `false`. Setting to `true` specifically prevents shoe meshes from rendering.
*   **Effects:** These offer fine-grained control over rendering skips. Skipping shoe rendering (`true`) can slightly improve performance if many characters are visible, but characters will appear shoeless. Disabling the other skips (`false`) might slightly decrease performance but could potentially fix rare visual glitches if the skipping logic was faulty.

#### Improve Object Detail with Fractal Upsampling
Forces the use of fractal upsampling techniques for grid-based details, potentially enhancing visual sharpness.

*   **Flag:** `FFlagDebugGridForceFractalUpsample`
*   **JSON Example:**
    ```json
    {
       "FFlagDebugGridForceFractalUpsample": "true"
    }
    ```
*   **Purpose:** Enables fractal upsampling algorithms, which can generate more plausible detail when increasing the resolution of grid-based data (like textures or terrain details) compared to simple interpolation.
*   **Default Value:** `false`.
*   **Effects:** May improve the perceived detail and sharpness of textures or other grid-based visual elements, making them look less blurry or stretched when viewed up close or at higher resolutions.

#### Combine Unified Lighting Grid with Specific Shadow Technologies
Allows using the "Unified" lighting system primarily for the light grid while forcing the shadow rendering to use Future, ShadowMap, or Voxel technology explicitly.

*   **Flags:**
    *   `FFlagRenderUnifiedLighting11` / `FFlagRenderUnifiedLighting12` (Enable Unified system)
    *   `FFlagDebugForceFutureIsBrightPhase3` (Force Future shadows)
    *   `FFlagDebugForceFutureIsBrightPhase2` (Force ShadowMap shadows)
    *   `DFFlagDebugRenderForceTechnologyVoxel` (Force Voxel shadows)
*   **JSON Examples:**
    *   **Unified Grid + Future Shadows:**
        ```json
        {
           "FFlagRenderUnifiedLighting12": "true",
           "FFlagDebugForceFutureIsBrightPhase3": "true",
           "FFlagDebugForceFutureIsBrightPhase2": "false",
           "DFFlagDebugRenderForceTechnologyVoxel": "false"
        }
        ```
    *   **Unified Grid + ShadowMap Shadows:**
        ```json
        {
           "FFlagRenderUnifiedLighting12": "true",
           "FFlagDebugForceFutureIsBrightPhase3": "false",
           "FFlagDebugForceFutureIsBrightPhase2": "true",
           "DFFlagDebugRenderForceTechnologyVoxel": "false"
        }
        ```
    *   **Unified Grid + Voxel Shadows:**
        ```json
        {
           "FFlagRenderUnifiedLighting12": "true",
           "FFlagDebugForceFutureIsBrightPhase3": "false",
           "FFlagDebugForceFutureIsBrightPhase2": "false",
           "DFFlagDebugRenderForceTechnologyVoxel": "true"
        }
        ```
*   **Purpose:** Decouples the light grid calculation from the shadow rendering method when Unified lighting is enabled. This allows benefiting from potential Unified light grid optimizations while retaining the specific shadow characteristics of Future, ShadowMap, or Voxel.
*   **Default Behavior:** When only `FFlagRenderUnifiedLighting12` is `True`, the shadow method often defaults to what the game specifies (e.g., ShadowMap), while the light grid uses Unified.
*   **Effects:** Allows mixing and matching. For instance, using Unified Grid + Future Shadows could provide the visual quality of Future's shadows combined with potential performance benefits of the Unified light grid.

> [!NOTE]
> Use `FFlagRenderUnifiedLighting11` or `FFlagRenderUnifiedLighting12` depending on which is currently active in Roblox builds. Set only *one* shadow-forcing flag (`FFlagDebugForceFutureIsBrightPhase3`, `FFlagDebugForceFutureIsBrightPhase2`, `DFFlagDebugRenderForceTechnologyVoxel`) to `True` to select the desired shadow type.

---

### UI and Client Behavior

#### Enable Darker Dark Theme Palettes
Activates newer color palettes intended for UI theming, often resulting in a darker appearance for the "Dark" theme.

*   **Flags:**
    *   `FFlagLuaAppUseUIBloxColorPalettes1`
    *   `FFlagUIBloxUseNewThemeColorPalettes`
*   **JSON Example:**
    ```json
    {
       "FFlagLuaAppUseUIBloxColorPalettes1": "True",
       "FFlagUIBloxUseNewThemeColorPalettes": "True"
    }
    ```
*   **Purpose:** Enables updated color definitions used by the UI framework (UIBlox).
*   **Default Value:** `False` (or potentially `True` via rollout).
*   **Effects:** Changes the specific shades of colors used throughout the Roblox application UI, particularly noticeable in the Dark theme which may appear darker or use different accent colors.

#### Disable Voice Chat Functionality
Completely disables voice chat features within the client.

*   **Flag:** `DFFlagVoiceChat4`
*   **JSON Example:**
    ```json
    {
       "DFFlagVoiceChat4": "False"
    }
    ```
*   **Purpose:** Acts as a master switch to disable the voice chat system.
*   **Default Value:** `True`.
*   **Effects:** Prevents voice chat from functioning, hiding related UI elements (like the microphone icon) and stopping audio transmission/reception, without needing to disable it account-wide via Roblox settings.

#### Redirect Top Bar / VC Badge Link
Redirects the "Learn More" link associated with certain top-bar badges (like the Beta or Voice Chat badge) to a custom URL.

*   **Flags:**
    *   `FFlagTopBarUseNewBadge` (Potentially enables the badge display)
    *   `FStringTopBarBadgeLearnMoreLink` (URL for general top-bar badges)
    *   `FStringVoiceBetaBadgeLearnMoreLink` (URL specifically for the VC Beta badge)
*   **JSON Example (Redirect to Google):**
    ```json
    {
       "FFlagTopBarUseNewBadge": "True",
       "FStringTopBarBadgeLearnMoreLink": "https://google.com",
       "FStringVoiceBetaBadgeLearnMoreLink": "https://google.com"
    }
    ```
*   **Purpose:** Allows customizing the destination of help/info links tied to specific UI badges.
*   **Default Value:** URLs pointing to Roblox help pages.
*   **Effects:** Clicking the "Learn More" link on the relevant badge opens the specified custom URL in the Roblox internal browser. Requires the specific badge to be active/visible (e.g., having VC enabled for the VC Beta badge).

#### Prevent Top Bar UI Opacity Changes
Stops the top-bar UI elements (like the Roblox menu button, chat icon) from becoming fully opaque when the main menu's background transparency is increased.

*   **Flag:** `FFlagChromeUsePreferredTransparency`
*   **JSON Example:**
    ```json
    {
       "FFlagChromeUsePreferredTransparency": "false"
    }
    ```
*   **Purpose:** Normally, the top-bar icons inherit transparency settings from the main escape menu background. Setting this to `false` disconnects that behavior.
*   **Default Value:** `true`.
*   **Effects:** Keeps the top-bar icons at their default semi-transparent state, regardless of the escape menu's background transparency setting. Purely a visual preference.

#### Revert Escape Menu to V4 (No Hamburger/Mic Icons)
Specifically targets the V4 (2023) escape menu appearance, ensuring the newer hamburger menu and microphone icons are *not* shown.

*   **Flag:** `FFlagEnableInGameMenuChromeABTest4`
*   **JSON Example:**
    ```json
    {
       "FFlagEnableInGameMenuChromeABTest4": "False"
    }
    ```
*   **Purpose:** Disables participation in the A/B test that introduced the redesigned top-bar icons (hamburger menu, new mic icon).
*   **Default Value:** `True` (if enrolled) or `False`.
*   **Effects:** If the V4 menu is active (e.g., by setting `FIntNewInGameMenuPercentRollout3` to `0`), this ensures the *original* V4 top-bar icons are used, not the newer ones.

#### Revert Chat Tab UI (Experiment Override)
Forces the chat UI to revert to an older layout by overriding an experiment flag with a non-default value.

*   **Flag:** `FStringNewChatTabExperimentLayerValue`
*   **JSON Example (Force Revert):**
    ```json
    {
       "FStringNewChatTabExperimentLayerValue": "IAmARobloxEngineerFr" // Any value other than default works
    }
    ```
*   **Purpose:** Overrides the layer value controlling the chat tab experiment. The default value is `"ShowNewChatTab"`. Providing any other string reverts the UI.
*   **Default Value:** `"ShowNewChatTab"`.
*   **Effects:** Changes the appearance and layout of the in-game chat interface back to a previous version. The specific string used in the example (`"IAmARobloxEngineerFr"`) is arbitrary; any non-default value should trigger the revert.

> [!NOTE]
> This method relies on providing an *invalid* or *non-default* value to an experiment flag to force a fallback behavior. It might break if Roblox changes how this experiment flag is handled.

#### Re-enable and Customize "Events" Button
Makes the "Events" button visible on the Roblox home page again and allows setting the URL it links to.

*   **Flags:**
    *   `FFlagPlatformEventEnabled2`
    *   `FStringPlatformEventUrl`
*   **JSON Example (Link to YouTube):**
    ```json
    {
       "FFlagPlatformEventEnabled2": "True",
       "FStringPlatformEventUrl": "https://www.youtube.com/"
    }
    ```
*   **Purpose:** Re-enables the UI element for platform events (like "The Hunt") and sets its web link destination.
*   **Default Value:** `False` for `FFlagPlatformEventEnabled2`, URL pointing to Roblox event pages for `FStringPlatformEventUrl`.
*   **Effects:** Adds the "Events" button back to the main navigation, linking to the specified URL which opens in the Roblox internal browser. Replace `"https://www.youtube.com/"` with any desired valid URL.

#### Disable Data Sharing Features / UI
Attempts to disable features and UI elements related to Roblox's data sharing policies (CAP - California Privacy Act related).

*   **Flags:**
    *   `FFlagCAP1209EnableDataSharingUI4`
    *   `FFlagCAP1544UseNewDataSharingRollout`
    *   `FIntCAP1209DataSharingRolloutPercentage`
    *   `FIntCAP1209DataSharingTOSVersion`
    *   `FIntCAP1544DataSharingUserRolloutPercentage`
*   **JSON Example:**
    ```json
    {
       "FFlagCAP1209EnableDataSharingUI4": "false",
       "FFlagCAP1544UseNewDataSharingRollout": "false",
       "FIntCAP1209DataSharingRolloutPercentage": "0",
       "FIntCAP1209DataSharingTOSVersion": "0",
       "FIntCAP1544DataSharingUserRolloutPercentage": "0"
    }
    ```
*   **Purpose:** Aims to opt-out of data sharing features and hide related UI prompts or settings by disabling related flags and setting rollout percentages to zero.
*   **Default Values:** Vary depending on user region, account status, and active rollouts.
*   **Effects:** May prevent certain data sharing functionalities or UI elements related to privacy settings (particularly for users under specific regulations like CCPA/CPRA) from appearing or being active.

> [!IMPORTANT]
> The effectiveness of these flags in completely stopping data sharing is uncertain and depends heavily on Roblox's backend implementation and compliance with regulations. They primarily target specific features and UI related to privacy controls.

#### Force V2 Escape Menu via User ID (Alternative)
An alternative method to force the V2 escape menu by specifying a User ID, potentially less reliable than percentage-based flags.

*   **Flag:** `FStringNewInGameMenuForcedUserIds`
*   **JSON Example:**
    ```json
    {
       "FStringNewInGameMenuForcedUserIds": "YOUR_ROBLOX_ID"
    }
    ```
*   **Purpose:** Forces the V2 menu specifically for the user whose ID is listed.
*   **Default Value:** `""` (Empty string).
*   **Effects:** If other menu flags allow, this forces the V2 menu for the specified user.

> [!NOTE]
> This method is generally considered less practical and potentially less reliable than using flags like `FIntNewInGameMenuPercentRollout3`. Requires knowing and inputting the specific User ID.

---

### Telemetry

#### Disable Core Telemetry Components
Disables various core components responsible for collecting and sending telemetry data.

*   **Flags:**
    *   `FFlagDebugDisableTelemetryEphemeralCounter`
    *   `FFlagDebugDisableTelemetryEphemeralStat`
    *   `FFlagDebugDisableTelemetryEventIngest`
    *   `FFlagDebugDisableTelemetryPoint`
    *   `FFlagDebugDisableTelemetryV2Counter`
    *   `FFlagDebugDisableTelemetryV2Event`
    *   `FFlagDebugDisableTelemetryV2Stat`
*   **JSON Example:**
    ```json
    {
       "FFlagDebugDisableTelemetryEphemeralCounter": "True",
       "FFlagDebugDisableTelemetryEphemeralStat": "True",
       "FFlagDebugDisableTelemetryEventIngest": "True",
       "FFlagDebugDisableTelemetryPoint": "True",
       "FFlagDebugDisableTelemetryV2Counter": "True",
       "FFlagDebugDisableTelemetryV2Event": "True",
       "FFlagDebugDisableTelemetryV2Stat": "True"
    }
    ```
*   **Purpose:** Provides switches to turn off different types of telemetry collection (counters, stats, event ingestion).
*   **Default Value:** `False`.
*   **Effects:** Significantly reduces the amount of diagnostic and usage data sent from the client to Roblox servers.

> [!NOTE]
> While these flags disable major telemetry pathways, Roblox may still collect data through other means. This set is considered effective for disabling the bulk of standard telemetry with minimal configuration "bloat".

### Networking and Replication

#### Enable Large Object Replicator (Experimental)
Activates components of a replication system potentially optimized for handling large objects or data streams.

*   **Flags:**
    *   `FFlagLargeReplicatorRead2`
    *   `FFlagLargeReplicatorWrite2`
    *   `FFlagLargeReplicatorEnabled2`
*   **JSON Example:**
    ```json
    {
       "FFlagLargeReplicatorRead2": "True",
       "FFlagLargeReplicatorWrite2": "True",
       "FFlagLargeReplicatorEnabled2": "True"
    }
    ```
*   **Purpose:** Enables specialized read, write, and general functionality pathways within the network replicator, possibly designed for better performance when dealing with large assets or frequent updates of large data chunks.
*   **Default Value:** `false` for all.
*   **Effects:** Could improve network performance and synchronization for experiences that involve replicating large objects (e.g., large models, terrain data streams), potentially reducing latency or visual stutter associated with their replication.

#### Enable RakNet Polling
Activates continuous polling within the RakNet networking library to check for network packets.

*   **Flag:** `DFFlagRakNetEnablePoll`
*   **JSON Example:**
    ```json
    {
       "DFFlagRakNetEnablePoll": "true"
    }
    ```
*   **Purpose:** Enables a mode where the RakNet library actively and frequently checks for incoming/outgoing packets, rather than potentially relying solely on event-driven notifications.
*   **Default Value:** `false`.
*   **Effects:** Can improve network responsiveness and potentially reduce latency by processing packets more immediately. However, this continuous polling might slightly increase CPU usage compared to event-based handling.

> [!TIP]
> Enabling RakNet polling might be beneficial for users seeking the lowest possible network latency, but monitor CPU usage to ensure it doesn't introduce significant overhead.

---

### Client Behavior and UI

#### Improve Inertial Scrolling
Enhances the smoothness and feel of inertial scrolling (momentum-based scrolling) in UI elements.

*   **Flag:** `FFlagUserBetterInertialScrolling`
*   **JSON Example:**
    ```json
    {
       "FFlagUserBetterInertialScrolling": "true"
    }
    ```
*   **Purpose:** Improves the physics and feel of scrolling lists, inventories, or other scrollable frames, making the momentum effect more fluid and natural.
*   **Default Value:** `false`.
*   **Effects:** Results in a smoother scrolling experience, particularly noticeable on touchpads or touchscreens where flick-scrolling is common.

#### Disable Chat Bubbles
Prevents chat messages from appearing in bubbles above player characters' heads.

*   **Flag:** `FFlagEnableBubbleChatFromChatService`
*   **JSON Example:**
    ```json
    {
       "FFlagEnableBubbleChatFromChatService": "False"
    }
    ```
*   **Purpose:** Disables the rendering of chat messages as floating bubbles in the 3D world space.
*   **Default Value:** `True` (Bubble chat enabled).
*   **Effects:** Chat messages will only appear in the standard chat window, not above characters. This can reduce visual clutter, especially in crowded areas.

#### Disable Chinese Policy Compliance Checks (Use with Extreme Caution)
Attempts to bypass checks related to compliance with Chinese government regulations and policies.

*   **Flags:**
    *   `DFFlagPolicyServiceReportIsNotSubjectToChinaPolicies`
    *   `DFFlagPolicyServiceReportDetailIsNotSubjectToChinaPolicies`
    *   `DFIntPolicyServiceReportDetailIsNotSubjectToChinaPoliciesHundredthsPercentage`
    *   `FStringDevPublishChinaRequirementsLink`
*   **JSON Example:**
    ```json
    {
       "DFFlagPolicyServiceReportIsNotSubjectToChinaPolicies": "false",
       "DFFlagPolicyServiceReportDetailIsNotSubjectToChinaPolicies": "false",
       "DFIntPolicyServiceReportDetailIsNotSubjectToChinaPoliciesHundredthsPercentage": "0",
       "FStringDevPublishChinaRequirementsLink": "YesIAmChinese" // Arbitrary string likely ignored when other flags are false
    }
    ```
*   **Purpose:** These flags appear related to Roblox's internal systems for handling policy differences, specifically concerning China. Setting the boolean flags to `false` and the percentage to `0` likely aims to signal that the user *is* subject to these policies or bypasses checks determining applicability.
*   **Default Value:** Varies based on region and other factors. Likely `True` for users outside China.
*   **Effects:** The exact consequences are unclear and likely depend heavily on Roblox's backend systems and the user's actual location and account status. Attempting to manipulate these flags could potentially lead to account issues or unintended behavior.

> [!CAUTION]
> Manipulating flags related to regional policy compliance is highly discouraged. It may violate Roblox's Terms of Service and could have unforeseen consequences on account features or status. The intended effect of the provided example (setting flags to `false`) is ambiguous – it might either falsely signal compliance *or* attempt to disable the checks entirely. The provided GIF link (`nalog` - Russian for "tax") and reactions suggest this is likely intended humorously or for bypassing restrictions, but should be treated with extreme caution.

#### Enable Party Voice Chat Features (Experimental)
Disables filters that might prevent voice chat usage within the Roblox "Party" system.

*   **Flags:**
    *   `FFlagEnablePartyVoiceOnlyForUnfilteredThreads`
    *   `FFlagEnablePartyVoiceOnlyForEligibleUsers`
*   **JSON Example:**
    ```json
    {
       "FFlagEnablePartyVoiceOnlyForUnfilteredThreads": "False",
       "FFlagEnablePartyVoiceOnlyForEligibleUsers": "False"
    }
    ```
*   **Purpose:** Overrides default restrictions that might limit voice chat in parties based on user eligibility or chat filter settings.
*   **Default Value:** `True` (Restrictions enabled).
*   **Effects:** May allow voice chat usage within parties even if users wouldn't normally meet eligibility criteria. Requires voice chat to be enabled account-wide. Uses the default system input device.

> [!IMPORTANT]
> All participants in the party **must** have these flags set to `False` to communicate successfully. It's noted that this might result in "uncensored" communication, likely meaning standard chat filters might not apply as strictly to the voice channel. Use responsibly.

#### Enable Newer UI Theme (Blue/Dark)
Enables the "Foundation Colors V7" theme, providing updated visuals, often with blue accents in the dark theme.

*   **Flag:** `FFlagLuaAppEnableFoundationColors7`
*   **JSON Example:**
    ```json
    {
       "FFlagLuaAppEnableFoundationColors7": "True"
    }
    ```*   **Purpose:** Activates a specific iteration of Roblox's newer UI color palette system.
*   **Default Value:** Variable (may be enabled by default for many users).
*   **Effects:** Updates the appearance of the Roblox desktop application UI. (Duplicate entry, see Supplement 4 for original details).

#### Remove Layered Clothing Visuals
Effectively hides layered clothing items by manipulating the underlying "cage" deformation limits.

*   **Flag:** `DFIntLCCageDeformLimit`
*   **JSON Example:**
    ```json
    {
       "DFIntLCCageDeformLimit": "-1"
    }
    ```
*   **Purpose:** Controls the deformation limit for the invisible "cage mesh" that layered clothing wraps around. Setting it to `-1` (or likely any sufficiently low/invalid value) prevents the cage from forming correctly.
*   **Default Value:** `15`.
*   **Effects:** Layered clothing items (jackets, sweaters, etc.) will not render on avatars, as the underlying structure they rely on is disabled. Base clothing (shirts, pants) and accessories are unaffected. This is primarily a visual preference or potential minor performance tweak.

---

### Rendering and Performance

#### Enable Lanczos Upsampling for Textures
Activates Lanczos resampling for upscaling textures, aiming for higher quality results than simpler methods.

*   **Flags:**
    *   `DFFlagRenderLanczosUpsampling`
    *   `DFFlagRenderLanczosSeparateAxis`
*   **JSON Example:**
    ```json
    {
       "DFFlagRenderLanczosUpsampling": "true",
       "DFFlagRenderLanczosSeparateAxis": "true"
    }
    ```
*   **Purpose:** Uses the Lanczos algorithm when textures need to be upscaled (e.g., displaying a lower-resolution texture at a larger size). `DFFlagRenderLanczosSeparateAxis` likely enables applying the filter separately on horizontal and vertical axes.
*   **Default Value:** `false`.
*   **Effects:** Can produce sharper and more detailed visuals when upscaling textures compared to bilinear or nearest-neighbor filtering, potentially reducing blurriness at the cost of slightly higher computational effort during the upscaling process.

> [!NOTE]
> Lanczos resampling is known for producing sharper results but can sometimes introduce minor "ringing" artifacts near sharp edges. Its visual benefit is most noticeable when lower-resolution textures are viewed at higher resolutions.

#### Enable CPU Light Culling (FSM)
Forces the use of a specific CPU-based method for light culling (determining which lights affect which objects).

*   **Flag:** `FFlagDebugForceFSMCPULightCulling`
*   **JSON Example:**
    ```json
    {
       "FFlagDebugForceFSMCPULightCulling": "True"
    }
    ```
*   **Purpose:** Explicitly enables a CPU-driven light culling technique, potentially based on Finite State Machines (FSM).
*   **Default Value:** `False` (GPU culling or other methods are typically preferred).
*   **Effects:** May alter performance characteristics of lighting calculations. CPU culling can be less efficient than GPU-based methods on modern hardware but might be used for debugging or as a fallback. (See Supplement 2 for potential interaction with `FFlagNewLightAttenuation`).

#### Force Specific Graphics Quality Level (Render Distance "Fix")
Overrides the Framerate Manager (FRM) quality level to lock graphics settings, allowing manual adjustment of the render distance slider independently.

*   **Flag:** `DFIntDebugFRMQualityLevelOverride`
*   **JSON Example (Lock to Level 1):**
    ```json
    {
       "DFIntDebugFRMQualityLevelOverride": "1"
    }
    ```
*   **Purpose:** Locks the *internal* graphics quality level (affecting textures, lighting details etc.) to the specified value (e.g., `1` for lowest). This prevents the *main* graphics slider in settings from changing these underlying details.
*   **Default Value:** `-1` or `0` (No override).
*   **Effects:** Allows the user to set the main graphics slider in the settings menu to maximum (Level 10) purely to maximize *render distance*, while the actual rendering quality (textures, effects) remains locked at the lower level specified by the FFlag (e.g., Level 1). This provides maximum view distance with potentially very low rendering detail for a performance boost.

> [!TIP]
> This is a technique to decouple render distance from overall graphics quality. Set `DFIntDebugFRMQualityLevelOverride` to the desired *quality* level (e.g., `1` for max FPS), then manually slide the in-game graphics setting to maximum (Level 10) to get the maximum *render distance*. (See Supplement 3 for more general info on this flag).

#### Increase Asset Preloading Limits (Faster Loading)
Sets limits for asset preloading to very high values, potentially speeding up game loading for previously visited experiences.

*   **Flags:**
    *   `DFIntAssetPreloading`
    *   `DFIntNumAssetsMaxToPreload`
    *   `FFlagEnableQuickGameLaunch` (Optional, related)
*   **JSON Example:**
    ```json
    {
       "DFIntAssetPreloading": "2147483647",
       "DFIntNumAssetsMaxToPreload": "2147483647",
       "FFlagEnableQuickGameLaunch": "True" // Optional
    }
    ```
*   **Purpose:** Removes practical limits (`2147483647` is max 32-bit int) on the number of assets the client attempts to preload into memory before they are explicitly needed. `FFlagEnableQuickGameLaunch` enables related quick launch logic.
*   **Default Values:** Lower limits (e.g., `100`) for counts, `False` for quick launch.
*   **Effects:** Can decrease loading times when rejoining games or entering new areas *if* the necessary assets were already encountered and cached/preloaded during previous sessions or earlier in the current session. Requires assets to have been loaded once before.

> [!CAUTION]
> Setting preload limits extremely high can significantly increase initial load times (the first time assets are encountered) and RAM usage as the client tries to keep more assets readily available. Ensure you have sufficient RAM. `DFIntAssetPreloading` was reported as non-functional at one point but later reported as working again; its status might fluctuate.

#### Enable Mesh Preloading
Specifically enables the preloading mechanism for MeshParts.

*   **Flag:** `DFFlagEnableMeshPreloading2`
*   **JSON Example (Enable):**
    ```json
    {
       "DFFlagEnableMeshPreloading2": "True"
    }
    ```
*   **Purpose:** Activates the system responsible for preloading mesh assets.
*   **Default Value:** `False` (according to the source text, though this might change via rollouts).
*   **Effects:** Allows mesh assets to be loaded into memory proactively, potentially reducing stutter or pop-in when meshes first become visible. Works in conjunction with overall asset preloading limits.

#### Adjust Number of Worker Threads
Sets the number of worker threads used by the client's task scheduler for parallel processing.

*   **Flag:** `DFIntRuntimeConcurrency`
*   **JSON Example (Manual Setting):**
    ```json
    {
       "DFIntRuntimeConcurrency": "11" // Example: For a CPU with 12 threads
    }
    ```
*   **Purpose:** Controls how many background threads Roblox can use to parallelize tasks like physics, rendering preparation, etc.
*   **Default Value:** `3` (Reported default on desktop).
*   **Effects:** Increasing the thread count (up to CPU threads - 1 recommended) can significantly improve performance (FPS, loading times) in CPU-bound scenarios by allowing more tasks to run concurrently. Setting it too high (above physical/logical core count) offers no benefit and might add overhead. Setting it lower than default reduces parallelism and likely performance.

> [!IMPORTANT]
> The recommended value is **(Number of CPU Threads) - 1**. To find your CPU thread count, open Task Manager (Ctrl+Shift+Esc), go to the Performance tab, select CPU, and look for "Logical processors". Setting this correctly can be a major performance boost, especially on CPUs with many cores/threads. Monitor CPU temperatures, as increased parallelism can slightly increase load, though usually negligibly.

---

### Physics Simulation

#### Enable Exploding Train Detection (Debug)
Activates a debug feature within the physics simulation solver intended to detect "exploding trains" scenarios.

*   **Flag:** `DFFlagDebugSimSolverDetectExplodingTrains2`
*   **JSON Example:**
    ```json
    {
       "DFFlagDebugSimSolverDetectExplodingTrains2": "true"
    }
    ```
*   **Purpose:** Likely a diagnostic tool for developers to identify physics instability issues where complex constrained systems (like trains) might "explode" due to simulation errors.
*   **Default Value:** `false`.
*   **Effects:** Unlikely to have any noticeable effect for regular players. May add slight overhead to the physics simulation for the detection logic.



## Further Roblox FastFlags (FFlags) - Supplement 8

This document details additional FFlags identified from recent discussions, continuing the series of supplements to the main FFlag overview.

---

### Audio

#### Enable Direct Audio Occlusion
Activates a specific method for calculating audio occlusion (how sounds are muffled or blocked by objects).

*   **Flag:** `FFlagDebugEnableDirectAudioOcclusion2`
*   **JSON Example:**
    ```json
    {
       "FFlagDebugEnableDirectAudioOcclusion2": "True"
    }
    ```
*   **Purpose:** Enables an alternative or updated system ("Direct Audio Occlusion V2") for simulating how sounds are obstructed by geometry in the environment.
*   **Default Value:** `False`.
*   **Effects:** May change how sounds are perceived when objects are between the listener and the sound source, potentially providing more realistic muffling effects.

---

### UI and Client Behavior

#### Custom Disconnect Message
Allows setting a custom reason message displayed when the client disconnects, potentially bypassing the standard reconnect prompt.

*   **Flags:**
    *   `FFlagReconnectDisabled`
    *   `FStringReconnectDisabledReason`
*   **JSON Example:**
    ```json
    {
       "FFlagReconnectDisabled": "True",
       "FStringReconnectDisabledReason": "CUSTOM MESSAGE HERE"
    }
    ```
*   **Purpose:**
    *   `FFlagReconnectDisabled`: When `True`, disables the automatic reconnect attempt/prompt.
    *   `FStringReconnectDisabledReason`: Sets the text displayed on the disconnect screen when reconnecting is disabled by the flag above.
*   **Default Value:** `False` for `FFlagReconnectDisabled`, likely an empty or default reason string.
*   **Effects:** Prevents the "Reconnect" button from appearing upon disconnection and shows the custom message provided in `FStringReconnectDisabledReason` instead. Replace `"CUSTOM MESSAGE HERE"` with your desired text. Setting `FFlagReconnectDisabled` to `False` re-enables the default reconnect behavior.

#### Disable Chrome UI Components
Disables the newer "Chrome" UI elements in the top bar (like the hamburger menu).

*   **Flags:**
    *   `FFlagEnableInGameMenuChrome`
    *   `FFlagEnableInGameMenuChromeABTest4`
*   **JSON Example:**
    ```json
    {
       "FFlagEnableInGameMenuChrome": "False",
       "FFlagEnableInGameMenuChromeABTest4": "False"
    }
    ```
*   **Purpose:** Opts out of both the general Chrome UI feature and a specific A/B test related to it.
*   **Default Value:** `True` (or depends on A/B test enrollment).
*   **Effects:** Reverts the top-bar UI elements to an older style, removing the hamburger menu icon and potentially other associated changes. This provides a more specific way to target the Chrome UI compared to reverting the entire menu version.

#### Disable "Automatic Translation" System Message
Removes the system message that appears in chat upon joining some games, informing the user about automatic chat translation.

*   **Flag:** `FFlagChatTranslationEnableSystemMessage`
*   **JSON Example:**
    ```json
    {
       "FFlagChatTranslationEnableSystemMessage": "False"
    }
    ```
*   **Purpose:** Disables the display of the introductory message regarding chat translation features.
*   **Default Value:** `True`.
*   **Effects:** Prevents the "Roblox automatically translates supported languages in chat" message from appearing in the chat window at the start of a game session. Does not disable the translation feature itself.

#### Use Old Microprofiler Font
Reverts the font used in the Microprofiler overlay (Shift+F1-F5) to an older, potentially less readable version.

*   **Flag:** `FFlagImproveMicroprofilerReadability`
*   **JSON Example:**
    ```json
    {
       "FFlagImproveMicroprofilerReadability": "False"
    }
    ```
*   **Purpose:** Disables changes made to improve the readability of the Microprofiler font.
*   **Default Value:** `True`.
*   **Effects:** The text displayed in the Microprofiler panels will use the older font style. Purely a visual preference for debugging information.

---

### Asset Loading and Preloading

#### Enable Avatar Asset Preloading
Enables preloading of assets specifically related to player avatars.

*   **Flags:**
    *   `DFFlagEnablePreloadAvatarAssets`
    *   `DFIntPreloadAvatarAssets`
*   **JSON Example:**
    ```json
    {
       "DFFlagEnablePreloadAvatarAssets": "True",
       "DFIntPreloadAvatarAssets": "2147483647" // Max 32-bit integer
    }
    ```
*   **Purpose:**
    *   `DFFlagEnablePreloadAvatarAssets`: Toggles the avatar preloading feature on/off.
    *   `DFIntPreloadAvatarAssets`: Potentially controls the number or priority of avatar assets to preload. Setting to max integer aims to maximize this.
*   **Default Value:** `False` for the enabling flag.
*   **Effects:** May improve game loading times or reduce stutter when player avatars load into view by preloading their assets (accessories, body parts, clothing textures) beforehand.

> [!IMPORTANT]
> The maximum value for a standard 32-bit signed integer is `2147483647`. Using `2147483648` (as seen in one example) is technically out of bounds and may wrap around to a negative number or cause unexpected behavior. Use `2147483647` for the intended maximum effect. As with other aggressive preloading, monitor RAM usage.

#### Reduce Character Load Time (Humanoid Load Time)
Sets a target time limit (in milliseconds) for loading character appearance (Humanoid).

*   **Flag:** `DFIntCharacterLoadTime`
*   **JSON Example (Target 1ms):**
    ```json
    {
       "DFIntCharacterLoadTime": "1"
    }
    ```
*   **Purpose:** Specifies a desired maximum time allocation for the character loading process.
*   **Default Value:** Unknown, likely a higher value.
*   **Effects:** Setting a very low value (like `1`ms) might prioritize character loading or force it to complete faster, potentially at the cost of other loading tasks or visual fidelity if assets aren't ready.

> [!CAUTION]
> Setting this value extremely low might interfere with proper character appearance loading or cause instability. The user notes setting it to "infinite" breaks games. Experiment with small, reasonable values if desired.

---

### Performance and Optimization

#### Optimize End-of-Frame Update Loop
Enables optimizations related to the tasks performed at the very end of each frame's update cycle.

*   **Flag:** `DFFlagFastEndUpdateLoop`
*   **JSON Example:**
    ```json
    {
       "DFFlagFastEndUpdateLoop": "True"
    }
    ```
*   **Purpose:** Aims to streamline the processing that occurs just before rendering the next frame.
*   **Default Value:** `True`.
*   **Effects:** Intended to potentially reduce frame times slightly or lower input latency. User reports are mixed ("doesn't optimize rather deoptimizes", "does reduce frame times").

> [!NOTE]
> This flag is reported as being enabled (`True`) by default in recent checks. Explicitly setting it may be redundant unless overriding an older `False` value. The actual performance impact seems debatable or situation-dependent.

#### Enable Global Instancing for D3D11
Enables a global instancing rendering technique specifically when using the DirectX 11 renderer.

*   **Flags:** (Potentially alternative names exist)
    *   `FFlagRenderEnableGlobalInstancingD3D11`
    *   `FFlagRenderEnableGlobalInstancing7` (Possible alternative/older version)
*   **JSON Example:**
    ```json
    {
       "FFlagRenderEnableGlobalInstancingD3D11": "true"
       // OR "FFlagRenderEnableGlobalInstancing7": "true"
    }
    ```
*   **Purpose:** Activates GPU instancing on a global scale for D3D11. Instancing allows drawing multiple copies of the same mesh with different properties (position, color) in a single draw call, significantly improving performance when rendering many identical objects.
*   **Default Value:** `true`.
*   **Effects:** Should generally improve rendering performance, especially in scenes with many repeated elements (trees, props, etc.), when using DirectX 11.

> [!NOTE]
> This feature is reported as being enabled (`true`) by default. Explicitly setting it is likely unnecessary.

#### Set Mouse/Keyboard Latency Target Timer
Adjusts internal timers possibly related to input processing latency targets for mouse and keyboard.

*   **Flags:**
    *   `FIntActivatedCountTimerMSKeyboard`
    *   `FIntActivatedCountTimerMSMouse`
*   **JSON Example (Set timers to 0ms):**
    ```json
    {
       "FIntActivatedCountTimerMSKeyboard": "0",
       "FIntActivatedCountTimerMSMouse": "0"
    }
    ```
*   **Purpose:** Modifies timers (in milliseconds) associated with keyboard and mouse input activation counts. The exact function of these timers is unclear, but setting them to `0` might reduce delays or buffering related to input event processing.
*   **Default Value:** Unknown positive integer(s).
*   **Effects:** Potentially reduces input latency by minimizing delays associated with these internal timers. Effect might be subtle. Other related flags exist for Touch and Gamepad inputs (`FIntActivatedCountTimerMSTouch`, `FIntActivatedCountTimerMSGamepad`).

---

### Telemetry and Data Reporting

#### Disable Device Info Reporting
Disables the reporting of device information to Roblox servers.

*   **Flags:**
    *   `FIntReportDeviceInfoRollout` (Controls rollout percentage)
    *   `DFIntReportDeviceInfoRate` (Controls report frequency)
    *   `DFIntReportOutputDeviceInfoEventRateHundredthsPercentage`
    *   `DFIntReportOutputDeviceInfoRateHundredthsPercentage`
    *   `DFIntReportRecordingDeviceInfoEventRateHundredthsPercentage`
    *   `DFIntReportRecordingDeviceInfoRateHundredthsPercentage`
*   **JSON Example (Disable All):**
    ```json
    {
       "FIntReportDeviceInfoRollout": "0",
       "DFIntReportDeviceInfoRate": "0",
       "DFIntReportOutputDeviceInfoEventRateHundredthsPercentage": "0",
       "DFIntReportOutputDeviceInfoRateHundredthsPercentage": "0",
       "DFIntReportRecordingDeviceInfoEventRateHundredthsPercentage": "0",
       "DFIntReportRecordingDeviceInfoRateHundredthsPercentage": "0"
    }
    ```
*   **Purpose:** Sets rollout percentages and reporting rates/frequencies for various device information telemetry events to zero, effectively disabling them.
*   **Default Values:** `100` for rollout, non-zero rates.
*   **Effects:** Prevents the client from sending detailed hardware and device configuration information (potentially including audio devices) to Roblox.

#### Disable Memory Stats Reporting
Disables various telemetry reports related to client memory usage.

*   **Flags:**
    *   `DFFlagReportClientMemoryCat`
    *   `DFFlagReportMemoryAllocStats`
    *   `DFFlagReportMemoryStatsToTelemetryV2`
*   **JSON Example:**
    ```json
    {
       "DFFlagReportClientMemoryCat": "false",
       "DFFlagReportMemoryAllocStats": "false",
       "DFFlagReportMemoryStatsToTelemetryV2": "false"
    }
    ```
*   **Purpose:** Disables specific telemetry flags related to reporting memory statistics, allocation patterns, and general memory categories.
*   **Default Value:** `True`.
*   **Effects:** Reduces the amount of memory-related diagnostic data sent to Roblox.

#### Disable WebView Cookie Synchronization
Prevents cookies from the embedded web view (used for some UI elements like avatar shop previews) from being synchronized or stored by the main Roblox engine.

*   **Flags:**
    *   `FFlagSyncWebViewCookieToEngine2`
    *   `FFlagUpdateHTTPCookieStorageFromWKWebView` (Likely specific to macOS/iOS using WKWebView)
*   **JSON Example (Disable Sync):**
    ```json
    {
       "FFlagSyncWebViewCookieToEngine2": "false",
       "FFlagUpdateHTTPCookieStorageFromWKWebView": "false"
    }
    ```
*   **Purpose:** Disables mechanisms that share or update cookie data between the embedded web browser component and the main Roblox client's HTTP services.
*   **Default Value:** `True`.
*   **Effects:** May enhance privacy slightly by preventing web cookies set within WebView elements from persisting or being accessed outside that specific web context. Likely has minimal impact on functionality unless a feature specifically relies on this cookie sharing.

#### Analytics and Telemetry Disablement (Comprehensive)

This large collection of flags aims to disable a wide range of analytics, telemetry, and event reporting functionalities within the Roblox client. The general approach involves:

1.  **Disabling Services:** Directly turning off analytics-related services (`DFFlagAnalyticsServiceEnabled: false`).
2.  **Setting Rates/Percentages to Zero:** Configuring various integer flags (`DFInt*Percentage`, `DFInt*Rate`, etc.) to `0` to prevent sampling or reporting of data.
3.  **Redirecting Endpoints:** Changing string flags (`DFString*URL`, etc.) that define reporting URLs to non-functional values like `"opt-out"` or `"balls"`, preventing data transmission to Roblox servers.
4.  **Disabling Feature-Specific Analytics:** Setting numerous boolean flags (`DFFlag*`, `FFlag*`) related to specific features (UI elements, physics, networking, voice chat, etc.) to `false` to stop data collection for those features.

*   **Flags:** (Extensive list targeting various analytics components)
    *   `DFFlagAnalyticsServiceEnabled`
    *   `DFFlagAnalyticsServiceCustomEventsEnabled`
    *   `DFIntAnalytics*Percentage` / `DFInt*Rate` / `DFInt*Throttle*`
    *   `DFStringAnalytics*URL` / `DFString*Endpoint`
    *   `FFlag*Analytics*`
    *   `FFlagEnable*Analytics*`
    *   ... and many others as provided in the JSON.
*   **JSON Example (Comprehensive Disable List):**
    ```json
    {
        "DFFlagAnalyticsServiceCustomEventsEnabled": false,
        "DFFlagAnalyticsServiceEnabled": false,
        "DFFlagAnalyticsServiceEnabled_PlaceFilter": false,
        "DFFlagAnalyticsServiceHydrationEnabled": false,
        "DFFlagAnalyticsServiceRelaxedPlayerCheckEnabled": false,
        "DFFlagAnalyticsServiceStudioEnabled_PlaceFilter": false,
        "DFFlagAUMPAnalytics": false,
        "DFFlagConvexDecompCompressionAnalytics": false,
        "DFFlagLegacyRedundantPlayerCheckAnalytics": false,
        "DFFlagLocalizationTableAnalyticsSenderRequeueFailedEntries": false,
        "DFFlagLTAnalyticsIgnoreCoreGui": false,
        "DFFlagNavigationAnalyticsAddPlaceId": false,
        "DFFlagNewPackageAnalytics": false,
        "DFFlagNonBlockingAnalyticsExit": false,
        "DFFlagPath2DAnalytics_ProfilerScope": false,
        "DFFlagPath2DAnalyticsEnabled2": false,
        "DFFlagPlatformServiceCalledAnalytics": false,
        "DFFlagProximityPromptAnalytics": false,
        "DFFlagRealtimeClientAnalyticsPipelineConnectionsSendsSubscriptionStatus": false,
        "DFFlagReportPath2DAnalyticsEnabled_Perf": false,
        "DFFlagSimReportBroadPhasePairCountAnalytics": false,
        "DFFlagTagAnalyticsPointsWithIxpIds": false,
        "DFFlagUseJointAnalytics": false,
        "DFFlagUwpPurchaseAnalytics": false,
        "DFIntAnalyticsCDNProbeInfluxPermyriad": 0,
        "DFIntAnalyticsForXBoxCrash_JoinInfluxHundredthsPercentage": 0,
        "DFIntAnalyticsMaxSendWaitTimeMs": 0,
        "DFIntAnalyticsMaxShutdownWaitTimeMs": 0,
        "DFIntAnalyticsNS1CDNProbeChancePercent": 0,
        "DFIntAnalyticsServiceFiredEventsBudgetMax": 0,
        "DFIntAnalyticsServiceFiredEventsBudgetRefreshInSeconds": 0,
        "DFIntCookieProtocolAnalyticsHundredthsPercentage": 0,
        "DFIntCookieProtocolAnalyticsPriorityHundredthsPercentage": 0,
        "DFIntCoreScriptsAnalyticsHundredthsPercentage": 0,
        "DFIntDragDetectorDragAnalyticsThrottleHundredthsPercent": 0,
        "DFIntEngineDatamodelAnalyticsInfoThrottle": 0,
        "DFIntGuiClassUsageAnalytics_ReportHundredthsPercent": 0,
        "DFIntGuiServiceChromeSignalAPIAnalytics_ReportHundredthsPercent": 0,
        "DFIntInfluxReportingPackageAnalyticsHundrethsPercent": 0,
        "DFIntLocalizationTableAnalyticsSenderClientToHttpMinHundrethsPercent": 0,
        "DFIntLocalizationTableAnalyticsSenderClientToHttpMinHundrethsPercent_PlaceFilter": 0,
        "DFIntLocalizationTableAnalyticsSenderClientToHttpOffset": 0,
        "DFIntLocalizationTableAnalyticsSenderClientToHttpScale": 0,
        "DFIntLocalizationTableAnalyticsSenderClientToServerSampleRateHundrethsPercent": 0,
        "DFIntLocalizationTableAnalyticsSenderClientToServerSampleRateHundrethsPercent_PlaceFilter": 0,
        "DFIntLocalizationTableAnalyticsSenderMaxBytesPerSecondClient": 0,
        "DFIntLocalizationTableAnalyticsSenderMaxBytesPerSecondServer": 0,
        "DFIntLocalizationTableAnalyticsSenderMaxClientQueueSize": 0,
        "DFIntLocalizationTableAnalyticsSenderMaxEntriesPerRemoteEvent": 0,
        "DFIntLocalizationTableAnalyticsSenderMaxPlayerIntegrityListSize": 0,
        "DFIntLocalizationTableAnalyticsSenderMaxPlayerIntegrityListSize_PlaceFilter": 0,
        "DFIntLocalizationTableAnalyticsSenderMaxServerQueueSize": 0,
        "DFIntLocalizationTableAnalyticsSenderMaxToBeProcessedQueueSizeClient": 0,
        "DFIntLocalizationTableAnalyticsSenderMaxToBeProcessedQueueSizeServer": 0,
        "DFIntLocalizationTableAnalyticsSenderServerToHttpSampleRateHundrethsPercent": 0,
        "DFIntLocalizationTableAnalyticsSenderServerToHttpSampleRateHundrethsPercent_PlaceFilter": 0,
        "DFIntLocServicePerformanceAnalyticsHundredthsPercentage": 0,
        "DFIntLTAnalyticsMaxEntrySizeBytes": 0,
        "DFIntPercentApiRequestsRecordGoogleAnalytics": 0,
        "DFIntPhysicsAnalyticsIntervalSec": 0,
        "DFIntProximityPromptAnalyticsSampleRate": 0,
        "DFIntReportAUMPAnalyticsPercentageHundredths": 0,
        "DFIntScreenGuiSafeAreaPropertiesAnalyticsEventIngest_ReportHundredthsPercent": 0,
        "DFIntScreenGuiTopbarSafeInsetsAnalyticsEventIngest_ReportHundredthsPercent": 0,
        "DFIntStudioLexMapChangeDocAnalyticsThrottleHundredthsPercent2": 0,
        "DFIntStudioSyntaxHighlightingOnChangeAnalyticsThrottleHundredthsPercent2": 0,
        "DFIntTeleportV2InvocationsAnalyticsInfluxHundredthsPercentage": 0,
        "DFIntTeleportV2InvocationsAnalyticsInfluxHundredthsPercentage_PlaceFilter": 0,
        "DFIntUIDragDetectorDragAnalyticsThrottleHundredthsPercent": 0,
        "DFLogAnalyticsDeferredEphemeralReportingDiagnostic": 0,
        "DFLogAnalyticsService_PlaceFilter": 0,
        "DFStringAnalyticsEventStreamUrlEndpoint": "opt-out",
        "DFStringAnalyticsNS1BeaconConfig": "https://opt-out.roblox.com",
        "DFStringLocalizationTableAnalyticsSenderImplementationAnalyticsSuffix": "opt-out",
        "DFStringRobloxAnalyticsURL": "https://opt-out.roblox.com",
        "FFlagAddAnalyticsForImprovedPathfinding4": false,
        "FFlagAddAnalyticsForImprovedRasterization4": false,
        "FFlagAddAnalyticsForImprovedSearchStatsPerRequest": false,
        "FFlagAddFriendsMigrateAnalytics_v3": false,
        "FFlagAddRomarkAnalyticsForPathfinding": false,
        "FFlagAddSafeAreaAnalytics2": false,
        "FFlagAlignToolImprovedAnalytics": false,
        "FFlagAnalyticsGlobalVarRefactorV1": false,
        "FFlagAnalyticsGlobalVarRefactorV10": false,
        "FFlagAnalyticsGlobalVarRefactorV2": false,
        "FFlagAnalyticsGlobalVarRefactorV3": false,
        "FFlagAnalyticsGlobalVarRefactorV3b": false,
        "FFlagAnalyticsGlobalVarRefactorV4": false,
        "FFlagAnalyticsGlobalVarRefactorV5": false,
        "FFlagAnalyticsGlobalVarRefactorV5b": false,
        "FFlagAnalyticsGlobalVarRefactorV6": false,
        "FFlagAnalyticsGlobalVarRefactorV7": false,
        "FFlagAnalyticsGlobalVarRefactorV8": false,
        "FFlagAnalyticsGlobalVarRefactorV9": false,
        "FFlagAnalyticsGlobalVarRefactorV9b": false,
        "FFlagAnalyticsServiceForClient_PlaceFilter": false,
        "FFlagAppChatAnalyticsAppChatVisible": false,
        "FFlagAppChatAnalyticsPlaySessionId": false,
        "FFlagAvatarChatCameraTrackerStatusAnalytics": false,
        "FFlagAvatarChatSubsessionAnalyticsV3": false,
        "FFlagAvatarChatSubsessionAnalyticsV4": false,
        "FFlagAXCarouselFixMissingAnalytics2": false,
        "FFlagAXCatalogSearchLandingAnalyticsContext": false,
        "FFlagAXColorPickerErrorAnalytics": false,
        "FFlagAXDoNotSendAnalyticsNoItemType": false,
        "FFlagAXEnableKeywordAnalyticsForSearch": false,
        "FFlagAXSearchRefactorForAnalytics": false,
        "FFlagAXSearchRefactorForAnalytics1": false,
        "FFlagCapturesPerformanceAnalyticsEnabled": false,
        "FFlagCevAnalytics": false,
        "FFlagCEVLowMemoryWarningAnalytics": false,
        "FFlagChatLineAbandonedReportAnalyticsFix": false,
        "FFlagCleanupDUARAnalytics": false,
        "FFlagCollectAnalyticsForSystemMenu": false,
        "FFlagCoreGuiEnableAnalytics": false,
        "FFlagCoreScriptPublishAssetAnalytics": false,
        "FFlagDeepLinkEventReceiverAnalyticsEvent": false,
        "FFlagEnableAnalyticsForCameraDevicePermissions": false,
        "FFlagEnableAnimatorAnalyticsForRetargeting": false,
        "FFlagEnableAppChatAnalyticsReportUserEvent": false,
        "FFlagEnableChromeAnalytics": false,
        "FFlagEnableChromePinAnalytics2": false,
        "FFlagEnableConnectDisconnectAnalytics": false,
        "FFlagEnableConnectDisconnectButtonAnalytics": false,
        "FFlagEnableExpJoinMicPermAnalytics": false,
        "FFlagEnableExplicitSettingsChangeAnalytics": false,
        "FFlagEnableForceOTAAnalytics": false,
        "FFlagEnableForkedChatAnalytics": false,
        "FFlagEnableInExpJoinVoiceAnalytics2": false,
        "FFlagEnableInExpLikelySpeakingAnalytics": false,
        "FFlagEnableInExpMicPermissionsAnalytics": false,
        "FFlagEnableInExpVoiceConsentAnalytics": false,
        "FFlagEnableLeaveGroupDialogAnalytics": false,
        "FFlagEnableLuaVoiceChatAnalyticsV2": false,
        "FFlagEnableNudgeAnalyticsV2": false,
        "FFlagEnableSendCameraAccessAnalytics": false,
        "FFlagEnableTopBarAnalytics": false,
        "FFlagEnableTwoStepCatalogAnalytics": false,
        "FFlagEnableUGCIndividualAssetUploadAnalytics": false,
        "FFlagEnableUGCUploadFlowAnalytics4": false,
        "FFlagEnableVoiceMuteAnalytics": false,
        "FFlagExtendedWidgetAnalytics2": false,
        "FFlagExtendWidgetAnalyticsWithWidgetItemIds": false,
        "FFlagFixChatListCountAnalytics": false,
        "FFlagFixContactRecsCTRAnalytics": false,
        "FFlagFixMissingPermissionsAnalytics": false,
        "FFlagFixResumeSourceAnalytics": false,
        "FFlagFriendsCarouselFixUnverseIdAnalytics": false,
        "FFlagGameInviteModalAnalyticsEmptyEventContextFix": false,
        "FFlagGamepadAnalytics": false,
        "FFlagIGMv1ARFlowExpandedAnalyticsEnabled": false,
        "FFlagInExperienceSettingsRefactorAnalytics": false,
        "FFlagInGameChromeSignalAPIAnalytics": false,
        "FFlagLightgridDependencyExperimentAnalytics": false,
        "FFlagLocServicePerformanceAnalyticsEnabled": false,
        "FFlagLooksAnalyticsEmptyItemsFixes": false,
        "FFlagLooksAnalyticsFixes": false,
        "FFlagLuaAppAbuseReportAnalyticsHasLaunchData": false,
        "FFlagLuaAppFixGameGridAnalyticsUniverseId": false,
        "FFlagLuaAppGameSetTargetIdAnalytics": false,
        "FFlagLuaAppNavigationAnalytics": false,
        "FFlagLuaAppSlpAnalyticsFixes": false,
        "FFlagLuaVoiceChatAnalyticsUseCounterV2": false,
        "FFlagLuaVoiceChatAnalyticsUseEventsV2": false,
        "FFlagMaterialGeneratorCollectAnalytics": false,
        "FFlagMeshLoDAnalyticsFixIsLocalAsset": false,
        "FFlagNavigationAnalyticsImprovement": false,
        "FFlagNewPackageAnalyticsWithRefactor2": false,
        "FFlagOffNetworkAnalytics": false,
        "FFlagPathfindingHighComputeImplTimeAnalytics2": false,
        "FFlagPCSCEVFeasibieAnalytics": false,
        "FFlagRbxAnalyticsExposePlaySessionId": false,
        "FFlagRemoveCLBAnalytics": false,
        "FFlagReportAbuseMenuEntrypointAnalytics": false,
        "FFlagSearchSourceEventAnalytics_1": false,
        "FFlagSendDevicePermissionsModalAnalytics": false,
        "FFlagSendGeometryPhysicsAnalyticsBeforeDMClosing": false,
        "FFlagShareGameSearchBoxFocusAnalytics": false,
        "FFlagShareLinkPrivateServerAnalyticsEnabled": false,
        "FFlagSimEnableEditableAnalytics": false,
        "FFlagSocialAnalyticsFixUpdateInfoAllEvents": false,
        "FFlagSocialAnalyticsSupportTelemetry": false,
        "FFlagSocialAnalyticsTelemetryModule": false,
        "FFlagSocialAnalyticsTelemetrySupportDynamicName": false,
        "FFlagSocialExperienceJoinCustomAnalyticsArgs": false,
        "FFlagSocialLuaAnalyticsAddPlatformValue": false,
        "FFlagSocialLuaAnalyticsAddPlatformValueFix": false,
        "FFlagSocialLuaAnalyticsAddTimestamp": false,
        "FFlagSocialLuaAnalyticsRemoveSocialLibraries": false,
        "FFlagSongbirdChromeWindowAnalytics": false,
        "FFlagSongbirdSendAnalytics": false,
        "FFlagSongbirdWindowAnalyticsUseNonpii": false,
        "FFlagStudioOnboardingExperiment1AdditionalAnalytics": false,
        "FFlagStudioOnboardingStartPageCTAAnalytics": false,
        "FFlagStudioReportChangeAnalytics": false,
        "FFlagThumbnailLoadingAnalyticsMetrics": false,
        "FFlagToastNotificationAnalyticsPlaySessionId": false,
        "FFlagToolboxLinkifyAnalytics": false,
        "FFlagToolboxListviewAnalytics": false,
        "FFlagUGCValidationAnalytics": false,
        "FFlagUpdateContactImporterToUseAnalyticsService": false,
        "FFlagUserDidSignUpAnalyticsFix": false,
        "FFlagUserSearchMoveAnalyticsV2_2": false,
        "FFlagUserSearchTopTabAnalytics": false,
        "FFlagVideoAnalyticsAvoidTempStringConstruction": false,
        "FFlagVideoAnalyticsUseWeakThis": false,
        "FFlagVoiceUpsellNewAnalytics": false,
        "FFlagVoiceUserAgencyAddMuteDecisionAnalytics": false,
        "FFlagVoiceUserAgencyAddMuteDecisionAnalytics_PlaceFilter": false,
        "FFlagXboxAnalyticsTrackTTI2": false,
        "FFlagXboxGamepadUserInfoAnalytics": false,
        "FInt9SliceEditorAnalyticsReportingHundrethsPercent": 0,
        "FIntGraphicsMetalAnalyticsHundredthPercent": 0,
        "FIntGraphicsVulkanAnalyticsHundredthPercent": 0,
        "FIntHSRVersionAnalyticsHundredthPercent": 0,
        "FIntLocalizationAnalyticsSamplesPerMillion": 0,
        "FIntMaterialPickerAnalyticsThrottleHundrethsPercent": 0,
        "FIntPercentReportingLeaveGameAnalytics": 0,
        "FIntPluginLoadingAnalyticsHundredthsPercentage": 0,
        "FIntPluginOTAAnalyticsHundredthsPercentage": 0,
        "FIntPluginOTADeploymentAnalyticsHundredthsPercentage": 0,
        "FIntPluginOTAErrorAnalyticsHundredthsPercentage": 0,
        "FIntProfilePlatformAnalyticsThrottlingThousandths": 0,
        "FIntRenderShaderLoadAnalyticsHundredthPercent": 0,
        "FIntStudioLexMapChangeDocAnalyticsPerKeystrokeThrottleHundredthsPercent": 0,
        "FIntStudioPackagesPublishAnalyticsNumOfTopClassName": 0,
        "FIntStudioSyntaxHighlightingOnChangeAnalyticsPerKeystrokeHundredthsPercent": 0,
        "FIntTeleportMethodAnalyticsHundredthPct": 0,
        "FIntVRAvatarGesturesAnalyticsThrottleHundrethsPercent": 0,
        "DFIntPhysicsAnalyticsHighFrequencyIntervalSec ": 0
    }
    ```
*   **Purpose:** To comprehensively disable numerous known analytics and telemetry data collection points within the Roblox client.
*   **Default Values:** Typically `true`, non-zero integers, or valid URLs for the respective flags.
*   **Effects:** Significantly reduces the amount of diagnostic, usage, performance, and event data sent to Roblox servers.

> [!IMPORTANT]
> This is an extensive list targeting a wide array of analytics features. While it aims for broad coverage, it's possible some data collection might still occur through other mechanisms or future flags.

> [!CAUTION]
> Disabling analytics might hinder Roblox's ability to diagnose crashes, performance problems, or bugs effectively. Furthermore, flag names and behaviors can change with Roblox updates, potentially rendering parts of this configuration ineffective over time.

---

### Studio Specific

#### Enable Studio Flag State Debugging
Enables a debug feature related to flag states specifically within Roblox Studio.

*   **Flag:** `FFlagDebugStudioFlagState`
*   **JSON Example:**
    ```json
    {
       "FFlagDebugStudioFlagState": "True"
    }
    ```
*   **Purpose:** Activates debugging functionality related to how FastFlags are handled or displayed within the Roblox Studio environment.
*   **Default Value:** `False`.
*   **Effects:** Only affects Roblox Studio. Requires a tool like RSMM (Roblox Studio Mod Manager) to modify Studio flags. The exact functionality enabled is unclear without using it in Studio.

> [!IMPORTANT]
> This flag is **only for Roblox Studio** and requires separate tools (like RSMM) to apply. It has no effect on the regular Roblox player client.

### UI and Client Behavior

#### Bring Back Older Chrome Menu Variations (Using DMP)
Forces the client to load older versions of the UI ("Chrome Menu") by using DataModelPatches (DMP) specific to past Roblox versions, combined with a FastFlag to enable local DMP loading.

*   **Required Flag:**
    ```json
    {
       "FFlagDataModelPatcherForceLocal": "True"
    }
    ```
*   **DataModelPatches (DMP):** Requires downloading and placing specific DMP files (linked in the original source for versions like V615, V611, V610, V608) into the appropriate client directory. These patches contain older UI definitions.
*   **Associated Optional Flags:**
    *   Unpin Chat: `{"FFlagEnableChromePinnedChat": false}`
    *   Hide Playerlist Close Button: `{"FFlagDisablePlayerListDisplayCloseBtn": true}`
    *   Remove Respawn from Unibar: `{"FFlagUnibarRespawn": false}` (Note: Breaks Unibar scrolling)
*   **Purpose:** To load older UI layouts by forcing the client to use patched data models instead of the current live ones.
*   **Effects:** Reverts the appearance of the top bar and potentially other core UI elements to match older versions.

> [!CAUTION]
> *   This method is complex, requiring manual download and placement of external patch files (DMPs). Use files only from trusted sources.
> *   Using outdated DMPs **will break features** that rely on newer UI elements (e.g., Voice Chat UI, newer settings options). The source explicitly mentions VC and Chat Tab are broken.
> *   DMPs are version-specific and will likely stop working or cause crashes after significant Roblox updates. This is an advanced modification primarily for exploring older UI states.

#### Disable Chat System Completely
Disables the in-game chat system entirely.

*   **Flag:** `FFlagDebugForceChatDisabled`
*   **JSON Example:**
    ```json
    {
       "FFlagDebugForceChatDisabled": "True"
    }
    ```
*   **Purpose:** Acts as a master switch to turn off the chat feature.
*   **Default Value:** `False`.
*   **Effects:** Completely disables the chat window and prevents messages from being sent or received. Can provide a minor performance increase in servers with very high chat volume by eliminating chat processing overhead.

#### Disable Non-Chrome UI Rendering (White Screen/Hide GUI)
Disables the rendering of major UI components, potentially leading to a white screen or missing interface elements.

*   **Flags:**
    *   `FFlagDebugDontRenderUI`
    *   `FFlagDebugDontRenderScreenGui`
*   **JSON Example:**
    ```json
    {
       "FFlagDebugDontRenderUI": "True" // Disables broader UI rendering
    }
    ```
    ```json
    {
       "FFlagDebugDontRenderScreenGui": "True" // Specifically targets ScreenGuis
    }
    ```
*   **Purpose:** Debug flags to selectively disable rendering of UI layers.
*   **Default Value:** `False`.
*   **Effects:** Can hide most or all game and core UI elements. `FFlagDebugDontRenderUI` is likely broader than `FFlagDebugDontRenderScreenGui`. Can result in an unplayable state or a white screen.

> [!WARNING]
> These are debug flags that will likely make the game unusable by hiding critical interface elements. Users report setting them to `True` can sometimes prevent Roblox from working correctly. Use `False` to revert.

#### Rename "Charts" Tab to "Discovery" (App UI)
Renames the "Charts" navigation tab in the main Roblox app/website UI to "Discovery".

*   **Flags:**
    *   `FFlagLuaAppChartsPageRename`
    *   `FFlagEnableNavBarLabels3`
*   **JSON Example:**
    ```json
    {
       "FFlagLuaAppChartsPageRename": "false",
       "FFlagEnableNavBarLabels3": "false"
    }
    ```
*   **Purpose:** These flags likely control experiments related to renaming or redesigning the navigation bar. Setting them to `false` might revert to or force an older state where "Discovery" was used instead of "Charts".
*   **Default Value:** `True` (using "Charts" and current labels).
*   **Effects:** Changes the text label of one of the main navigation tabs in the Roblox app/website interface. Purely cosmetic.

---

### Performance and Optimization

#### Disable Data Size Limit for Replicator
Removes the default size limit for data packets handled by the network replicator.

*   **Flag:** `DFFlagReplicatorDisKickSize`
*   **JSON Example:**
    ```json
    {
       "DFFlagReplicatorDisKickSize": "True"
    }
    ```
*   **Purpose:** The replicator normally enforces a maximum size for data chunks being sent over the network to prevent excessively large packets. Setting this to `True` disables this size limit check.
*   **Default Value:** `false`.
*   **Effects:** Allows the client/server to send larger data packets without hitting the default limit.

> [!WARNING]
> Disabling the size limit (`True`) can lead to significantly higher bandwidth usage and potentially network instability or disconnects if extremely large packets are generated and overwhelm the connection or intermediate network hardware. Use with caution.

#### Enable GPU Light Culling
Enables a specific GPU-based light culling technique.

*   **Flag:** `FFlagFastGPULightCulling3`
*   **JSON Example:**
    ```json
    {
       "FFlagFastGPULightCulling3": "True"
    }
    ```
*   **Purpose:** Activates an optimized method for the GPU to determine which lights affect which parts of the scene, reducing the number of light calculations needed.
*   **Default Value:** `false`.
*   **Effects:** Can improve rendering performance, especially in scenes with many light sources, by offloading the culling process to the GPU more effectively.

#### Force Hidden Surface Removal (HSR) Generation
Forces the generation and use of Hidden Surface Removal (HSR) data.

*   **Flag:** `FFlagDebugForceGenerateHSR`
*   **JSON Example:**
    ```json
    {
       "FFlagDebugForceGenerateHSR": "true"
    }
    ```
*   **Purpose:** HSR is an optimization technique that pre-calculates which surfaces are hidden by others, allowing the renderer to skip drawing them. This flag forces the HSR data generation process.
*   **Default Value:** `false` (HSR might be generated automatically based on heuristics or quality settings).
*   **Effects:** Ensures HSR is active, potentially improving rendering performance by reducing the amount of geometry processed, especially in complex scenes with lots of overlapping objects.

> [!NOTE]
> HSR differs from Occlusion Culling. HSR primarily deals with *surfaces* hidden behind other surfaces (like the back faces of an object or parts hidden within a model), often handled during rasterization (e.g., Z-buffering). Occlusion Culling typically works at the *object* level, culling entire objects hidden behind other objects (occluders) earlier in the pipeline. Both aim to reduce rendering workload.

#### Force MSAA (Multisample Anti-Aliasing)
Forces the use of Multisample Anti-Aliasing (MSAA) at a specific sample level.

*   **Flag:** `FIntDebugForceMSAASamples`
*   **JSON Example (Force 4x MSAA):**
    ```json
    {
       "FIntDebugForceMSAASamples": "4"
    }
    ```
*   **Purpose:** Overrides the game's or user's anti-aliasing setting to enforce a specific MSAA sample count (valid values typically 0, 1, 2, 4, 8).
*   **Default Value:** `0` or `1` (effectively no MSAA or minimal).
*   **Effects:** Improves edge smoothness and reduces "jaggies" at the cost of performance. Higher sample counts (e.g., 4x, 8x) provide better quality but have a greater performance impact.

> [!IMPORTANT]
> *   Valid sample values are powers of 2 (0, 1, 2, 4, 8).
> *   Values above `4` (i.e., `8`) are reported to cause **visual bugs** with decals or other viewport elements.
> *   Setting a value higher than `8` (e.g., `2048`) will still cap the actual MSAA level at `8x` internally.
> *   **`4` is generally considered the maximum stable value.** The visual difference between 4x and 8x is often minimal, while the performance cost of 8x is significantly higher and may introduce bugs.

#### Induce Lag/Stutter via Garbage Collection Settings
Intentionally causes stuttering, particularly when jumping, by setting Lua garbage collection parameters to extreme values.

*   **Flags:**
    *   `DFIntLuaGcMaxKb` (Max memory before forced GC cycle)
    *   `DFIntLuauGcStepSizeKb` (Amount of work per GC step)
*   **JSON Example (Induce Stutter):**
    ```json
    {
       "DFIntLuaGcMaxKb": "2147483647",
       "DFIntLuauGcStepSizeKb": "2147483647"
    }
    ```
*   **Purpose:** Setting these to maximum integer values likely disrupts the normal incremental garbage collection process, causing infrequent but massive GC pauses when the memory limit is hit, leading to noticeable freezes or stutters.
*   **Default Values:** Moderate values tuned for balanced performance.
*   **Effects:** Creates intentional performance drops and stuttering.

> [!WARNING]
> This is a "troll flag" configuration designed to deliberately worsen performance and induce lag spikes. It serves no practical optimization purpose. Use `0` or default values for normal operation.

---

### Networking

#### Limit Data Sender Bandwidth (Ping Increase/Fix)
Sets a very low maximum bandwidth limit for the client's data sender, potentially increasing perceived ping or fixing specific network issues related to excessive bandwidth usage.

*   **Flag:** `DFIntDataSenderMaxBandwidthBps`
*   **JSON Example (Very Low Limit):**
    ```json
    {
       "DFIntDataSenderMaxBandwidthBps": "150"
    }
    ```
*   **Purpose:** Limits the maximum bytes per second the client's general data sender attempts to use.
*   **Default Value:** Likely a much higher value (e.g., related to `DFIntPhysicsSenderMaxBandwidthBps` default of 38760 or higher).
*   **Effects:** Severely restricts outgoing data rate. This will likely increase latency and cause lag ("increase your ping") due to data queuing up.

> [!NOTE]
> While presented as potentially increasing ping for trolling, the user also notes it might be used "for a fix people have". This could imply it's a workaround for rare scenarios where the client might incorrectly attempt to send too much data, causing issues on very limited connections. However, for most users, this will significantly degrade network performance.

#### Disable Timeout Disconnect Message
Prevents the standard disconnect message/screen from appearing when a network timeout occurs.

*   **Flag:** `DFFlagDebugDisableTimeoutDisconnect`
*   **JSON Example:**
    ```json
    {
       "DFFlagDebugDisableTimeoutDisconnect": "True"
    }
    ```
*   **Purpose:** Disables the client's action upon detecting a network timeout.
*   **Default Value:** `False`.
*   **Effects:** The client might simply freeze or hang indefinitely upon losing connection instead of showing the usual "You have been disconnected" message.

> [!NOTE]
> Considered "kinda useless" as it doesn't prevent the disconnect itself, only the notification. It might mask connection issues rather than solving them. Possibly used alongside other flags (`DFIntDefaultTimeoutTimeMs`) to experiment with connection handling.

#### Fix RakNet Bandwidth Collapse Issue
Enables a fix within the RakNet networking library related to potential bandwidth estimation collapse.

*   **Flag:** `DFFlagRakNetFixBwCollapse`
*   **JSON Example:**
    ```json
    {
       "DFFlagRakNetFixBwCollapse": "true"
    }
    ```
*   **Purpose:** Addresses a specific issue where RakNet's bandwidth detection/congestion control mechanism might incorrectly reduce the available bandwidth estimate ("collapse").
*   **Default Value:** `false`.
*   **Effects:** May improve network stability and performance, especially on connections prone to fluctuations, by preventing the bandwidth from being unnecessarily throttled due to this specific collapse issue.

---

### Telemetry and Logging

#### Remove DM (Direct Message?) Logging
Disables logging related to "DM"s (potentially Direct Messages or Data Model interactions).

*   **Flag:** `FFlagAddDMLogging`
*   **JSON Example:**
    ```json
    {
       "FFlagAddDMLogging": "false"
    }
    ```
*   **Purpose:** Turns off a specific logging mechanism labeled "DM". The exact scope (chat DMs, internal DataModel logs) is unclear but implied to be related to privacy.
*   **Default Value:** `True`.
*   **Effects:** Reduces logging, potentially enhancing privacy by not recording certain interactions.

> [!NOTE]
> This likely does *not* affect moderation or banning systems, which operate based on server-side data and reports, not client-side logs that this flag might disable.

---

### Audio and Sound

#### Use Velocity for Sound Effects (Doppler)
Enables sound properties to be affected by the physical velocity of the sound source and listener, simulating effects like Doppler shift.

*   **Flags:**
    *   `FFlagSoundsUsePhysicalVelocity`
    *   `FFlagUserSoundsUseRelativeVelocity2`
*   **JSON Example:**
    ```json
    {
       "FFlagSoundsUsePhysicalVelocity": "True",
       "FFlagUserSoundsUseRelativeVelocity2": "True"
    }
    ```
*   **Purpose:**
    *   `FFlagSoundsUsePhysicalVelocity`: Makes sound emitters consider their physical velocity.
    *   `FFlagUserSoundsUseRelativeVelocity2`: Enables Doppler effect calculations based on the relative velocity between the sound source and the listener.
*   **Default Value:** `False` for both.
*   **Effects:** Adds realism to sounds by making their pitch shift based on movement (Doppler effect - e.g., a siren changing pitch as it passes). Can potentially sound glitchy if velocities are extreme or erratic. `FFlagUserSoundsUseRelativeVelocity2` is noted as potentially improving the stability when `FFlagSoundsUsePhysicalVelocity` is enabled.

---

### Character Appearance

#### Fix Temporary Hair Order Property
Enables a temporary fix related to the rendering order or properties of hair accessories.

*   **Flag:** `DFFlagTEMPFixHairOrderProperty`
*   **JSON Example:**
    ```json
    {
       "DFFlagTEMPFixHairOrderProperty": "true"
    }
    ```
*   **Purpose:** Applies a specific, likely temporary, fix to address issues with how hair accessories are layered or rendered.
*   **Default Value:** `false`.
*   **Effects:** May resolve visual glitches or incorrect layering involving multiple hair accessories.

### Graphics and Rendering (Vulkan Specific)

#### Vulkan Rendering Optimizations and Fixes
This collection of flags targets various aspects of the experimental Vulkan renderer, aiming to apply fixes, adjust behavior, and manage resources.

*   **Flags:** (Includes numerous Vulkan-specific flags)
    *   `FFlagGraphicsVulkanSampleCountFix`
    *   `FFlagGraphicsVulkanSwapchainImagesFix`
    *   `FFlagGraphicsVulkanSwapchainCount`
    *   `FFlagGraphicsVulkanBufferWaw`
    *   `FStringGraphicsVulkanVertexOutputsBufferLimitMiB`
    *   `FFlagGraphicsVulkanYuvTexturesSamplers5`
    *   `FFlagGraphicsVulkanFixInputBindingGaps2`
    *   `FFlagGraphicsVulkanDescriptorSetBindFix`
    *   `FFlagGraphicsVulkanDescriptorSetBindCSFix`
    *   `FFlagGraphicsVulkanClampSurfaceSize`
    *   `FFlagGraphicsVulkanBufferUploadBarrier`
    *   `DFFlagRecategorizeVulkanDeviceLostCrashes`
    *   `FStringGraphicsVulkanVaryingBufferLimitMiB`
    *   `FFlagGraphicsVulkanDeviceLostCrash`
    *   `FFlagUseConstantBufferViewsVulkan2`
    *   `FFlagVulkanAlwaysLogLayersAndExtensions` (Logging)
    *   `FIntGraphicsVulkanAnalyticsHundredthPercent` (Analytics)
    *   `FFlagSetDbgInfoVulkan` (Debug Info)
    *   `FStringGraphicsVulkanBlacklist*` (Device Blacklisting)
    *   `FIntEnableFIB3VulkanHundredthPercent` (Future Is Bright Rollout for Vulkan)
    *   `FIntGraphicsVulkanMinDriverVersionPVR` (Driver Version Check)
    *   `FStringVulkanBuggyRenderpassList` (Buggy Render Pass List)
    *   `FFlagHandleAltEnterFullscreenManually` (Fullscreen Handling)
*   **JSON Example (Combined):**
    ```json
    {
        "FFlagGraphicsVulkanSampleCountFix": "True",
        "FFlagVulkanAlwaysLogLayersAndExtensions": "False",
        "FIntGraphicsVulkanAnalyticsHundredthPercent": "0",
        "FFlagSetDbgInfoVulkan": "False",
        "FFlagGraphicsVulkanSwapchainImagesFix": "True",
        "FFlagGraphicsVulkanSwapchainCount": "True",
        "FFlagGraphicsVulkanBufferWaw": "False",
        "FStringGraphicsVulkanVertexOutputsBufferLimitMiB": "0x13B6:.\\u002B:.\\u002B=256",
        "FFlagGraphicsVulkanBlacklistIDs2": "False",
        "FStringGraphicsVulkanBlacklistVendorIDs": "",
        "FFlagGraphicsVulkanBlacklistIDs": "False",
        "FFlagGraphicsVulkanYuvTexturesSamplers5": "True",
        "FFlagGraphicsVulkanImageViewName": "False",
        "FFlagGraphicsVulkanFixInputBindingGaps2": "True",
        "FFlagGraphicsVulkanDescriptorSetBindFix": "True",
        "FFlagGraphicsVulkanDescriptorSetBindCSFix": "True",
        "FFlagGraphicsVulkanClampSurfaceSize": "False",
        "FFlagGraphicsVulkanBufferUploadBarrier": "True",
        "DFFlagRecategorizeVulkanDeviceLostCrashes": "True",
        "FStringGraphicsVulkanBlacklistVendorDeviceDriverIDs": "",
        "FStringGraphicsVulkanBlacklistDeviceIDs": "",
        "FIntEnableFIB3VulkanHundredthPercent": "16003",
        "FFlagGraphicsVulkanDeviceLostCrash": "True",
        "FFlagUseConstantBufferViewsVulkan2": "True",
        "FStringGraphicsVulkanBlacklist": "",
        "FStringGraphicsVulkanFutureGPUNameBlacklist": "",
        "FStringGraphicsVulkanVaryingBufferLimitMiB": "0x13B6:.\\u002B:.\\u002B=256;0x5143:.\\u002B:.\\u002B=256",
        "FStringVulkanBuggyRenderpassList": "",
        "FIntGraphicsVulkanMinDriverVersionPVR": "0",
        "FFlagHandleAltEnterFullscreenManually": "False"
    }
    ```
*   **Purpose:** This extensive set of flags fine-tunes the Vulkan renderer, addressing potential bugs (swapchain issues, binding gaps, device loss), managing resources (buffer limits, blacklisting problematic GPUs/drivers), controlling features (YUV textures, constant buffer views), and configuring logging/analytics specific to Vulkan.
*   **Default Values:** Vary widely; many fixes/features might be `False` by default. Blacklists are typically empty.
*   **Effects:** Aims to improve stability, performance, and visual correctness when using the Vulkan rendering API. Disables unnecessary logging and analytics. Configures buffer limits and specific feature rollouts (like Future is Bright).

> [!IMPORTANT]
> This configuration is specifically for users forcing the Vulkan renderer (`FFlagDebugGraphicsPreferVulkan: "True"`). Vulkan itself is experimental on Roblox and may cause instability regardless of these flags. The `FLogNetwork: "7"` flag seems unrelated to Vulkan and might be an error in the original list. The blacklist strings are empty, meaning no devices are blacklisted by this configuration.

---

### Networking

#### Disable CDN Usage for UWP Client Updates
Prevents the UWP (Microsoft Store) version of Roblox from using Content Delivery Networks (CDNs) when checking for or downloading updates.

*   **Flag:** `FFlagUWPUpgradeUseCDN`
*   **JSON Example:**
    ```json
    {
       "FFlagUWPUpgradeUseCDN": "false"
    }
    ```
*   **Purpose:** Forces the UWP client to fetch update data directly from Roblox servers instead of potentially faster, geographically distributed CDN nodes.
*   **Default Value:** `true`.
*   **Effects:** Specific to the UWP client. Disabling CDN usage (`false`) will likely result in **slower update checks and downloads**.

> [!CAUTION]
> Disabling CDN usage is **not recommended** as it typically slows down downloads. This might only be useful for troubleshooting very specific network issues where CDN access is problematic.

---

### Graphics and Rendering

#### Enable Dynamic Resolution Scaling
Enables a feature where the game's rendering resolution is dynamically adjusted (usually lowered) to maintain a target framerate.

*   **Flag:** `FFlagRenderDynamicResolutionScale12`
*   **JSON Example (Disable):**
    ```json
    {
       "FFlagRenderDynamicResolutionScale12": "false"
    }
    ```
*   **Purpose:** Allows the engine to render the game at a lower resolution during heavy scenes and upscale it to the native display resolution, aiming to keep performance stable.
*   **Default Value:** `true`.
*   **Effects:** When enabled (`true`, default), helps maintain smoother FPS on lower-end hardware by sacrificing resolution temporarily. Disabling (`false`) forces rendering at the native selected resolution, which might provide a consistently sharper image but can lead to lower FPS in demanding situations.

> [!NOTE]
> This feature is reported as **enabled by default** (`true`) in recent Roblox versions. Setting it to `false` explicitly disables dynamic resolution.

---

### Physics and Simulation

#### Configure "Exploding Train" Detection (Place Filter)
Configures the rollout percentage for the "exploding train" physics detection feature, but only for specific Place IDs (games).

*   **Flag:** `DFIntSimExplodingTrainHundredthsPercentage_PlaceFilter`
*   **JSON Example:**
    ```json
    {
       "DFIntSimExplodingTrainHundredthsPercentage_PlaceFilter": "10000;18973473972;6214255393;7027922660;9133022367;5177561496;6927810595;10082031223;4119848102;6458393580;6510504476;13295432657"
    }
    ```
*   **Purpose:** Sets the rollout percentage (first value, `10000` = 100%) for the "exploding train" detection feature, but *only* activates it within the listed Place IDs (which are noted as being train-related games).
*   **Default Value:** Likely empty or `0`.
*   **Effects:** Enables the physics stability detection specifically in the listed games. This is likely used by Roblox developers to target testing or fixes for physics issues known to occur in those experiences.

> [!NOTE]
> This complements `DFFlagDebugSimSolverDetectExplodingTrains2` by controlling *where* the detection is active based on Place ID filtering.

---

### Networking and Bandwidth

#### Adjust Cluster Sender Bandwidth Limits (Fake 0 KB/s)
Sets various bandwidth limits related to cluster replication (potentially used for streaming or large world data) to maximum values.

*   **Flags:**
    *   `DFIntClusterSenderMaxJoinBandwidthBps`
    *   `DFIntClusterSenderMaxUpdateBandwidthBps`
    *   `DFIntClusterSenderMaxJoinBandwidthBpsScaling`
    *   `DFIntInitialCacheClustersBandwidthKBpS`
    *   `DFIntMaxClusterKBPerSecond`
*   **JSON Example (Maximize Limits):**
    ```json
    {
       "DFIntClusterSenderMaxJoinBandwidthBps": "2147483647",
       "DFIntClusterSenderMaxUpdateBandwidthBps": "2147483647",
       "DFIntClusterSenderMaxJoinBandwidthBpsScaling": "2147483647",
       "DFIntInitialCacheClustersBandwidthKBpS": "2147483647",
       "DFIntMaxClusterKBPerSecond": "2147483647"
    }
    ```
*   **Purpose:** Controls various bandwidth allocations (Bytes per second or Kilobytes per second) for sending cluster data. Setting them to the maximum 32-bit integer value effectively removes any practical limit.
*   **Default Values:** Moderate integer values.
*   **Effects:** By removing bandwidth limits, this might allow cluster data to transmit faster if the network allows. The user associated this with achieving a "Fake 0 kb cluster" display in some network monitoring tool, likely because the unlimited rate prevents throttling that would normally show up as KB/s usage in the monitor.

> [!NOTE]
> Similar to other bandwidth limit removals, this could lead to network instability or higher actual bandwidth usage if the system tries to send extremely large amounts of cluster data at once.

#### Induce Fake 0 Ping (Negative Bandwidth Limit)
Attempts to create a "fake 0 ping" display by setting the data sender bandwidth limit to a large negative number.

*   **Flag:** `DFIntDataSenderMaxBandwidthBps`
*   **JSON Example:**
    ```json
    {
       "DFIntDataSenderMaxBandwidthBps": "-2147483647"
    }
    ```
*   **Purpose:** Sets the maximum bandwidth for the general data sender to an invalid negative value.
*   **Default Value:** A positive integer.
*   **Effects:** Likely causes the bandwidth limiting mechanism to malfunction or disable entirely due to the invalid input. This might interfere with how ping or network stats are calculated or displayed, potentially resulting in a `0` or nonsensical reading. It does not actually improve the connection quality.

> [!CAUTION]
> This is purely manipulating a display value by providing invalid input. It does not grant actual 0 ping and may cause underlying network instability or errors. Setting the value to a high *positive* number, conversely, was noted to potentially create a *fake high ping* display.

#### Set Maximum Camera Zoom Distance (Infinite Zoom)
Overrides the maximum distance the camera can be zoomed out.

*   **Flag:** `FIntCameraMaxZoomDistance`
*   **JSON Example (Effectively Infinite):**
    ```json
    {
       "FIntCameraMaxZoomDistance": "2147483647"
    }
    ```
*   **Purpose:** Controls the upper limit for the camera's zoom distance.
*   **Default Value:** A moderate value (e.g., 400 or similar).
*   **Effects:** Setting to a very high value (max 32-bit integer) allows zooming the camera out extremely far, much further than normally allowed.

> [!IMPORTANT]
> This only works in games where the developer has *not* explicitly set their own `CameraMaxZoomDistance` limit in their scripts. If the game enforces its own limit, this flag will be overridden.

#### Adjust Mouse Input Queue/Debounce Time
Modifies an internal timer related to mouse input processing, potentially affecting debounce or queueing.

*   **Flag:** `FIntCLI20390_2`
*   **JSON Example (Set to 0ms):**
    ```json
    {
       "FIntCLI20390_2": "0"
    }
    ```
*   **Purpose:** Interpreted as controlling a debounce time (in milliseconds) between registered mouse clicks or the size/timing of an input queue.
*   **Default Value:** `16` (milliseconds).
*   **Effects:** Setting to `0` removes the default 16ms delay/debounce. This could make rapid clicks register more quickly, potentially useful in spam-clicking scenarios (e.g., specific games like Blade Ball mentioned). Higher values would introduce delays.

> [!NOTE]
> The default value of `16` likely exists to prevent accidental double clicks from registering due to minor physical switch bounce in mice. Setting to `0` may make inputs feel slightly more responsive for rapid clicks but could potentially lead to unintended double inputs depending on the mouse hardware.

#### Set Network Quality Responder Max Wait Time
Adjusts the maximum time the network quality responder waits.

*   **Flag:** `DFIntNetworkQualityResponderMaxWaitTime`
*   **JSON Example (Very Low Wait Time):**
    ```json
    {
       "DFIntNetworkQualityResponderMaxWaitTime": "1"
    }
    ```
*   **Purpose:** Controls a timeout related to network quality assessment or response mechanisms.
*   **Default Value:** `20` (likely milliseconds).
*   **Effects:** Lowering the wait time might make network quality adjustments or responses happen faster.

> [!CAUTION]
> The user suggests lowering this value *only* for "HIGH END" systems/connections. Setting it too low (`1`) might cause network instability or issues if the system doesn't have enough time to properly assess or respond under normal network conditions.

#### Enable New Escape Menu Settings Layout (Reorder)
Activates an experimental variant of the in-game Settings menu with reordered items.

*   **Flag:** `FFlagInExperienceMenuReorderFirstVariant2`
*   **JSON Example:**
    ```json
    {
       "FFlagInExperienceMenuReorderFirstVariant2": "true"
    }
    ```
*   **Purpose:** Enables a specific experimental layout ("First Variant 2") for the Settings section within the escape menu.
*   **Default Value:** `false`.
*   **Effects:** Changes the order or grouping of options within the Settings menu. Purely a UI layout change.

#### Prevent Task Scheduler Sleep/Yielding
Forces the client's task scheduler to avoid entering sleep or yield states, potentially keeping worker threads more active.

*   **Flags:**
    *   `DFFlagTaskSchedulerAvoidSleep`
    *   (Related mentioned: flags for `AvoidYieldInBackground`, `TaskCycles`)
*   **JSON Example:**
    ```json
    {
       "DFFlagTaskSchedulerAvoidSleep": "true"
    }
    ```
*   **Purpose:** Prevents the task scheduler from pausing or reducing activity, ensuring worker threads remain active even when there might be brief idle periods.
*   **Default Value:** `false`.
*   **Effects:** Can potentially boost FPS or responsiveness by reducing latency associated with waking threads up. However, it **will likely increase CPU usage** as threads remain active instead of sleeping.

> [!WARNING]
> Enabling this (`True`) is noted to increase CPU usage. While it might improve performance, monitor CPU temperatures and overall system stability. Related flags controlling yielding and task cycles might offer further tuning but were not detailed.

#### Physics Sender Rate Explanation (Reiteration)
Provides context on the `DFIntS2PhysicsSenderRate` flag, emphasizing its role in synchronization.

*   **Flag:** `DFIntS2PhysicsSenderRate`
*   **JSON Example (Default):**
    ```json
    {
       "DFIntS2PhysicsSenderRate": "15"
    }
    ```
*   **Purpose:** Controls how often (times per second, Hz) the client sends physics state updates (position, velocity, jumping, etc.) to the server.
*   **Default Value:** `15` (Hz).
*   **Effects:**
    *   **Increasing Value:** Sends updates more frequently, improving client-to-server synchronization. Player movements appear smoother and more accurate on the server and to other players, reducing perceived latency (makes actions feel like they happen at lower ping).
    *   **Decreasing Value:** Sends updates less frequently, saving upstream bandwidth but worsening synchronization. Can lead to desync exploits or visual lag where actions appear delayed or jerky to others.
*   **Misconception:** Noted that some communities mistakenly call this "Fast Dash" in certain games; it does not inherently speed up actions but improves their synchronization.

> [!TIP]
> Increasing `DFIntS2PhysicsSenderRate` (e.g., to `30` or `60`, ensuring `DFIntPhysicsSenderMaxBandwidthBps` is also sufficient) can make interactions feel more responsive, especially in physics-heavy games, provided the network connection can handle the increased data rate.
