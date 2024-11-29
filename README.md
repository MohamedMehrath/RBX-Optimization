# RBX-Optimization

## Stable Vulkan
```json
{
"FFlagDebugGraphicsDisableVulkan": false,
"FFlagDebugGraphicsDisableVulkan11": false,
"FFlagDebugGraphicsPreferVulkan": true,
"FFlagDebugVulkanDisablePreRotate": false,
"FFlagGraphicsVulkanBonusMemory": true,
"FFlagRenderEnableGlobalInstancingVulkan": true,
"FFlagDebugGraphicsPreferD3D11": "false"
}
```

### - DirectX10:
```json
{
    "FFlagDebugGraphicsPreferD3D11": "false",
    "FFlagDebugGraphicsPreferD3D11FL10": "true",
    "FFlagGraphicsEnableD3D10Compute": "true",
    "FFlagRenderEnableGlobalInstancingD3D10": "true",
    "FFlagRenderEnableGlobalInstancingD3D11": "false"
}
```
> [!TIP]
>## - You cant use future lightining with dx10!

## Blue Theme
```json
{
"FFlagLuaAppEnableFoundationColors7": "True"
} 
```

## Disable Fullscreen Titlebar
```json
{
    "FIntFullscreenTitleBarTriggerDelayMillis": 3600000
}
```

## Disable Telemetry
```json
{
  "FFlagDebugDisableTelemetryEphemeralCounter": true,
	"FFlagDebugDisableTelemetryEphemeralStat": true,
	"FFlagDebugDisableTelemetryEventIngest": true,
	"FFlagDebugDisableTelemetryPoint": true,
	"FFlagDebugDisableTelemetryV2Counter": true,
	"FFlagDebugDisableTelemetryV2Event": true,
	"FFlagDebugDisableTelemetryV2Stat": true
}
```

## Verified User Id
```json
{
"FStringWhitelistVerifiedUserId": "946070340"
}
```

## Increased Particles on low graphics
```json
{
    "FFlagDebugDeterministicParticles" : "True"
}
```

## Force Graphics Quality Level
```json
{
    "FIntRomarkStartWithGraphicQualityLevel": "1"
}
```

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
