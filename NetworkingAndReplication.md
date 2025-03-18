# Networking and Replication FFlags (Generated: 2025-03-18 23:00:00 UTC)

This document outlines the categories and subcategories of Roblox FFlags related to networking and replication, along with a brief explanation of each. The JSON snippets below each category allow for easy copying of the flags and their values.

## Networking

This category encompasses flags related to the networking aspects of the Roblox engine, such as data communication and network quality.

### General Networking

These flags control general networking behavior and settings.

```json
{
  "DFFlagClampIncomingReplicationLag": true,
  "DFFlagNetworkUseZstdWrapper": false,
  "DFFlagNextGenRepRollbackOverbudgetPackets": true,
  "DFFlagRakNetCalculateApplicationFeedback2": false,
  "DFFlagRakNetDetectNetUnreachable": true,
  "DFFlagRakNetDetectRecvThreadOverload": true,
  "DFFlagRakNetEnablePoll": true,
  "DFFlagRakNetUnblockSelectOnShutdownByWritingToSocket": true,
  "DFFlagRakNetUseSlidingWindow4": true,
  "DFFlagSampleAndRefreshRakPing": true,
  "DFIntClientPacketExcessMicroseconds": 1000,
  "DFIntClientPacketHealthyAllocationPercent": 20,
  "DFIntClientPacketMaxDelayMs": 1,
  "DFIntClientPacketMaxFrameMicroseconds": 200,
  "DFIntCodecMaxIncomingPackets": 100,
  "DFIntCodecMaxOutgoingFrames": 1000,
  "DFIntConnectionMTUSize": 1464,
  "DFIntMaxDataPacketPerSend": 100000,
  "DFIntMaxReceiveToDeserializeLatencyMilliseconds": 10,
  "DFIntMegaReplicatorNetworkQualityProcessorUnit": 10,
  "DFIntNetworkQualityResponderMaxWaitTime": 10,
  "DFIntNetworkQualityResponderUnit": 10,
  "DFIntRakNetApplicationFeedbackMaxSpeedBPS": 0,
  "DFIntRakNetApplicationFeedbackScaleUpFactorHundredthPercent": 0,
  "DFIntRakNetApplicationFeedbackScaleUpThresholdPercent": 0,
  "DFIntRakNetClockDriftAdjustmentPerPingMillisecond": 100,
  "DFIntRakNetLoopMs": 1,
  "DFIntRakNetMinAckGrowthPercent": 0,
  "DFIntRakNetNakResendDelayMs": 1,
  "DFIntRakNetNakResendDelayMsMax": 1,
  "DFIntRakNetNakResendDelayRttPercent": 50,
  "DFIntRakNetResendRttMultiple": 1,
  "DFIntRakNetSelectTimeoutMs": 1,
  "DFIntRaknetBandwidthInfluxHundredthsPercentageV2": 1000,
  "DFIntRaknetBandwidthPingSendEveryXSeconds": 1,
  "DFIntTimeBetweenSendConnectionAttemptsMS": 200
}
```

### Audio

These flags relate to audio-specific networking aspects, such as volumetric panning.

```json
{
  "DFFlagAudioDeviceTelemetry": false,
  "DFFlagCollectAudioPluginTelemetry": false,
  "DFFlagAudioEnableVolumetricPanningForMeshes": false,
  "DFFlagAudioEnableVolumetricPanningForPolys": false,
  "DFFlagAudioUseVolumetricPanning": true
}
```

## Replication

This category includes flags that affect how data is replicated between the server and clients.

### General

These flags control the general behavior of the replication system.

```json
{
  "DFFlagReplicateCreateToPlayer": true,
  "DFFlagReplicatorCheckReadTableCollisions": true,
  "DFFlagReplicatorDisKickSize": true,
  "DFFlagReplicatorSeparateVarThresholds": true,
  "FFlagLargeReplicatorEnabled3": true,
  "FFlagLargeReplicatorRead2": true,
  "FFlagLargeReplicatorWrite2": true,
  "DFFlagDebugLargeReplicatorDisableCompression": true,
  "DFFlagDebugLargeReplicatorForceFullSend": true,
  "FFlagDebugNextGenReplicatorEnabledWriteCFrameColor": true,
  "DFIntMegaReplicatorNumParallelTasks": 4,
  "DFIntReplicationDataCacheNumParallelTasks": 4
}
```

### Next Gen Replication

These flags are specific to the next generation replication system.

```json
{
  "DFFlagNextGenRepRollbackOverbudgetPackets": true,
  "FFlagNextGenReplicatorEnabledRead2": true,
  "FFlagNextGenReplicatorEnabledWrite2": true
}
```
