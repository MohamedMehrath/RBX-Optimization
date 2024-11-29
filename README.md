# RBX-Optimization

## Stable Vulkan
{
"FFlagDebugGraphicsDisableVulkan": false,
"FFlagDebugGraphicsDisableVulkan11": false,
"FFlagDebugGraphicsPreferVulkan": true,
"FFlagDebugVulkanDisablePreRotate": false,
"FFlagGraphicsVulkanBonusMemory": true,
"FFlagRenderEnableGlobalInstancingVulkan": true,
"FFlagDebugGraphicsPreferD3D11": "false"
}

## Blue Theme
{
"FFlagLuaAppEnableFoundationColors7": "True"
} 

## Disable Fullscreen Titlebar
{
    "FIntFullscreenTitleBarTriggerDelayMillis": 3600000
}

## Disable Telemetry
{
  "FFlagDebugDisableTelemetryEphemeralCounter": true,
	"FFlagDebugDisableTelemetryEphemeralStat": true,
	"FFlagDebugDisableTelemetryEventIngest": true,
	"FFlagDebugDisableTelemetryPoint": true,
	"FFlagDebugDisableTelemetryV2Counter": true,
	"FFlagDebugDisableTelemetryV2Event": true,
	"FFlagDebugDisableTelemetryV2Stat": true
}

## Verified User Id
{
"FStringWhitelistVerifiedUserId": "946070340"
}

## Increased Particles on low graphics
{
    "FFlagDebugDeterministicParticles" : "True"
}

## Force Graphics Quality Level
{
    "FIntRomarkStartWithGraphicQualityLevel": "1"
}

### Low Graphics Quality w/ Max Render Distance/FRM Quality Levels
> [!TIP]
> **1-6 Are low graphics, Above 6 are high graphics. Like the 1-21 graphics slider**
```json
{
    "DFIntDebugFRMQualityLevelOverride": "1"
}
```

### Remove Grass
```json
{
    "FIntFRMMinGrassDistance": "0",
    "FIntFRMMaxGrassDistance": "0",
    "FIntRenderGrassDetailStrands": "0",
}
```

### Hide guis
> [!IMPORTANT]
> **Replace "ID" with any group ID that you are in.**

| Key combination   | Action                                                                    |
| ----------------- | ------------------------------------------------------------------------- |
| Ctrl + Shift + B  | Toggles GUIs in 3D space (BillboardGuis, SurfaceGuis, etc)                |
| Ctrl + Shift + C  | Toggles game-defined ScreenGuis                                           |
| Ctrl + Shift + G  | Toggles Roblox CoreGuis                                                   |
| Ctrl + Shift + N  | Toggles player names, and other BillboardGuis that show up above a player |
```json
{
    "DFIntCanHideGuiGroupId": "386736"
}
```

### Possible Super Jump
```json
{
    "DFIntNewRunningBaseGravityReductionFactorHundredth": "1500"
}
```
