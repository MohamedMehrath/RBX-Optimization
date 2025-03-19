# Rendering and Graphics FFlags (Generated: 2025-03-18 23:23:00 UTC)

This document outlines the categories and subcategories of Roblox FFlags related to rendering and graphics, along with a brief explanation of each. The JSON snippets below each category allow for easy copying of the flags and their values.

## Rendering

This category encompasses flags directly related to the rendering pipeline and how the game world is drawn.

### General

These flags control core rendering behaviors and settings.

```json
{
  "FFlagDisablePostFx": true,
  "FFlagNewLightAttenuation": true,
  "FFlagRenderFixFog": true,
  "FFlagRenderGpuTextureCompressor": true,
  "FFlagRenderLegacyShadowsQualityRefactor": true,
  "FFlagRenderNoLowFrmBloom": false,
  "FFlagShaderLightingRefactor": false,
  "FFlagRenderCBRefactor2": true,
  "FFlagRenderFixGrassPrepass": false,
  "FFlagRenderSkipReadingShaderData": false,
  "FFlagRemovedRbxRenderingPreProcessor": false,
  "DFIntRenderingThrottleDelayInMS": 20,
  "FIntRenderLocalLightFadeInMs": 0,
  "FIntRenderLocalLightUpdatesMax": 8,
  "FIntRenderLocalLightUpdatesMin": 6,
  "FIntRenderMaxShadowAtlasUsageBeforeDownscale": 250,
  "FIntRenderMeshOptimizeVertexBuffer": 1,
  "FIntRenderShaderLoadAnalyticsHundredthPercent": 0,
  "FIntRenderShadowIntensity": 0,
  "FIntRenderShadowmapBias": 0,
  "FIntDefaultJitterN": 0
}
```

### Vulkan

These flags control the use of the Vulkan graphics API.

```json
{
  "FFlagDebugGraphicsDisableVulkan": false,
  "FFlagDebugGraphicsPreferVulkan": true,
  "FFlagDebugVulkanDisablePreRotate": false,
  "FFlagGraphicsVulkanBonusMemory": true,
  "FFlagRenderEnableGlobalInstancingVulkan": true,
  "FFlagFutureIsBrightPhase3Vulkan": true,
  "FFlagDebugGraphicsDisableVulkan11": false,
  "FFlagDebugGraphicsPreferD3D11": false
}
```

### DirectX

These flags relate to the DirectX graphics API.

```json
{
  "FFlagGraphicsEnableD3D10Compute": true
}
```

### OpenGL

These flags relate to the OpenGL graphics API.

```json
{
  "FFlagGraphicsGLEnableHQShadersExclusion": false,
  "FFlagGraphicsGLEnableSuperHQShadersExclusion": false
}
```

### Shadows

These flags control shadow rendering quality and settings.

```json
{
  "FFlagRenderLegacyShadowsQualityRefactor": true,
  "FIntRenderShadowIntensity": 0,
  "FIntRenderShadowmapBias": 0
}
```

### Particles

These flags control particle effects.

```json
{
  "FFlagFixOutdatedParticles2": false,
  "FFlagFixOutdatedTimeScaleParticles": false,
  "FFlagFixParticleAttachmentCulling": false,
  "FFlagFixParticleEmissionBias2": false,
  "FFlagDebugDeterministicParticles": false
}
```

### Lighting

These flags relate to lighting effects and calculations.

```json
{
  "FFlagNewLightAttenuation": true,
  "FFlagShaderLightingRefactor": false,
  "FIntDirectionalAttenuationMaxPoints": 100,
  "FIntUnifiedLightingBlendZone": 100
}
```

### Atmosphere

These flags control atmospheric effects like fog.

```json
{
  "FFlagRenderFixFog": true
}
```

### Textures

These flags relate to texture handling and settings.

```json
{
  "FFlagGraphicsTextureCopy": true,
  "FIntTerrainOTAMaxTextureSize": 1024,
  "FIntUITextureMaxRenderTextureSize": 1024,
  "FIntUITextureMaxUpdateDepth": 1,
  "FFlagPreloadTextureItemsOption4": true
}
```

### SSAO

These flags control Screen Space Ambient Occlusion.

```json
{
   "FFlagDebugSSAOForce": false,
   "FIntSSAO": 0,
   "FIntSSAOMipLevels": 0
}
```

### Grass

These flags control grass rendering.

```json
{
  "FIntFRMMaxGrassDistance": 0,
  "FIntFRMMinGrassDistance": 0,
  "FIntGrassMovementReducedMotionFactor": 0,
  "FIntRenderGrassDetailStrands": 0,
  "FFlagRenderFixGrassPrepass": false
}
```

## Graphics

This category encompasses flags related to broader graphics settings and optimizations.

### General

These flags control general graphics settings.

```json
{
  "DFFlagDebugOverrideDPIScale": false,
  "DFFlagDisableDPIScale": false,
  "FFlagHighlightOutlinesOnMobile": true,
  "FIntMicroProfilerDpiScaleOverride": 100
}
```

### Performance

These flags are related to graphics performance optimizations.

```json
{
  "DFFlagDebugSkipMeshVoxelizer": true,
  "DFFlagDebugUseOcclusionQueries": true,
  "FFlagFastGPULightCulling3": true,
  "FFlagOcclusionCullingBetaFeature": true,
  "DFFlagGraphicsOptimizationModeMVPExposureEnrollment4": false,
  "DFIntGraphicsOptimizationModeMaxFrameTimeTargetMs": 33
}
```
