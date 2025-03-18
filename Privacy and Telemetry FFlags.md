# Privacy and Telemetry FFlags (Generated: 2025-03-18 22:48:36 UTC)

This document outlines the categories and subcategories of Roblox FFlags related to privacy and telemetry, along with a brief explanation of each. The JSON snippets below each category allow for easy copying of the flags and their values.

## Privacy

This category encompasses flags related to user privacy and data handling.

### Opt-Out URLs

These flags define the URLs used for opting out of various data collection and analytics services. These URLs typically point to Roblox's privacy settings or external services used for data collection.

```json
{
  "DFStringAltHttpPointsReporterUrl": "https://opt-out.roblox.com",
  "DFStringAnalyticsEventStreamUrlEndpoint": "opt-out",
  "DFStringAnalyticsNS1ApplicationId": "opt-out",
  "DFStringAnalyticsNS1BeaconConfig": "https://opt-out.roblox.com",
  "DFStringCrashUploadToBacktraceBaseUrl": "https://opt-out.roblox.com",
  "DFStringCrashUploadToBacktraceMacPlayerToken": "opt-out",
  "DFStringCrashUploadToBacktraceTestingToken": "opt-out",
  "DFStringCrashUploadToBacktraceWindowsPlayerToken": "opt-out",
  "DFStringHttpPointsReporterUrl": "https://opt-out.roblox.com",
  "DFStringLightstepHTTPTransportUrlHost": "https://opt-out.roblox.com",
  "DFStringLightstepHTTPTransportUrlPath": "/opt-out",
  "DFStringLightstepToken": "opt-out",
  "DFStringLmsRecipeEndpoint": "/opt-out",
  "DFStringLmsReportEndpoint": "/opt-out",
  "DFStringRobloxAnalyticsSubDomain": "opt-out",
  "DFStringRobloxAnalyticsURL": "https://opt-out.roblox.com",
  "DFStringTelemetryV2Url": "https://opt-out.roblox.com",
  "FStringCoreScriptBacktraceErrorUploadToken": "opt-out",
  "FStringErrorUploadToBacktraceBaseUrl": "https://opt-out.roblox.com",
  "FStringPerformanceSendMeasurementAPISubdomain": "opt-out"
}
```

## Telemetry

This category includes flags that affect the telemetry aspects of the Roblox engine, such as data collection and reporting.

### General Telemetry

These flags control the collection and reporting of various telemetry data.

```json
{
  "DFFlagAddPlaySessionIdTelemetry": false,
  "DFFlagAddStreamingEnabledTagEventIngest": false,
  "DFFlagAudioDeviceTelemetry": false,
  "DFFlagBrowserTrackerIdTelemetryEnabled": false,
  "DFFlagCollectAudioPluginTelemetry": false,
  "DFFlagDSTelemetryV2ReplaceSeparator": false,
  "DFFlagESGamePerfMonitorEnabled": false,
  "DFFlagEmitSafetyTelemetryInCallbackEnable": false,
  "DFFlagEnableExtraUnreachableTelemetry": false,
  "DFFlagEnableFmodErrorsTelemetry": false,
  "DFFlagEnableHumanoidStateChangeTelemtry": false,
  "DFFlagEnableHumanoidStateChangeTelemtryOldStateDuration": false,
  "DFFlagEnablePercentileTelemetry": false,
  "DFFlagEnableTelemetryV2FRMStats": false,
  "DFFlagEphemeralCounterInfluxReportingEnabled": false,
  "DFFlagFrameTimeStdDev": false,
  "DFFlagGpuVsCpuBoundTelemetry": false,
  "DFFlagGraphicsQualityUsageTelemetry": false,
  "DFFlagLegacyRedundantPlayerCheckAnalytics": false,
  "DFFlagProximityPromptAnalytics": false,
  "DFFlagRccLoadSoundLengthTelemetryEnabled": false,
  "DFFlagRemoveTelemetryFlushOnJobClose": false,
  "DFFlagReportAssetRequestV1Telemetry": false,
  "DFFlagReportRenderDistanceTelemetry": false,
  "DFFlagRobloxTelemetryAddDeviceRAM": false,
  "DFFlagRobloxTelemetryAddDeviceRAMPointsV2": false,
  "DFFlagRobloxTelemetryV2PointEncoding": false,
  "DFFlagSendRenderFidelityTelemetry": false,
  "FFlagAvatarChatIncludeSelfViewOnTelemetry": false,
  "FFlagDebugDisableTelemetryEphemeralCounter": true,
  "FFlagDebugDisableTelemetryEphemeralStat": true,
  "FFlagDebugDisableTelemetryEventIngest": true,
  "FFlagDebugDisableTelemetryPoint": true,
  "FFlagDebugDisableTelemetryV2Counter": true,
  "FFlagDebugDisableTelemetryV2Event": true,
  "FFlagDebugDisableTelemetryV2Stat": true,
  "FFlagContentProviderPreloadHangTelemetry": false,
  "DFFlagGraphicsOptimizationModeMVPExposureEnrollment4": false
}
```

### Performance Telemetry

These flags control the collection of performance-related telemetry data.

```json
{
  "DFFlagEnablePerfDataCoreCategoryTimersCollection2": false,
  "DFFlagEnablePerfDataCoreTimersCollection2": false,
  "DFFlagEnablePerfDataCountersCollection": false,
  "DFFlagEnablePerfDataGatherTelemetry2": false,
  "DFFlagEnablePerfDataMainThread": true,
  "DFFlagEnablePerfDataReportThermals": false,
  "DFFlagEnablePerfDataSubsystemTimersCollection2": false,
  "DFFlagEnablePerfDataSummaryMode": false,
  "DFFlagEnablePerfRenderStatsCollection2": false,
  "DFFlagEnablePerfStatsCollection3": false,
  "DFFlagGpuVsCpuBoundTelemetry": false
}
```

### HTTP Telemetry

These flags control HTTP-related telemetry.

```json
{
  "DFIntHttpInfluxHundredthsPercentage": 0,
  "DFIntHttpInfluxReportsPerMillion": 0,
  "DFLogHttpTrace": 0,
  "DFLogHttpTraceError": 0,
  "DFIntSendJoinHttpBytesToDiag_HundredthsPercentage": 0
}
```

### Crash Reporting

These flags control crash reporting functionality.

```json
{
  "DFFlagAttachmentCrashReport": false,
  "DFFlagStoreUniqueIdInferredCrashSystem": false,
  "DFIntCrashReportingHundredthsPercentage": 0,
  "DFIntCrashUploadToBacktracePercentage": 0,
  "FFlagEnableBacktraceAttachmentsV3": false,
  "FFlagEnableBacktraceConnectionDidFailHandler": false,
  "FFlagEnableBacktraceMissingLogReport": false,
  "FFlagEnableBacktraceResponseHandler": false,
  "FFlagRolloutFlagCrashDataMacClient": false,
  "FFlagUserAgentInBacktraceReports": false,
  "FFlagWin32BacktraceWindowsLaunchType": false,
  "FIntLuaAppBacktraceErrorReportPercentage": 0
}
```

### Loopback Redirection (Telemetry Related)

These flags control loopback redirection, potentially used in the context of telemetry or analytics.  Directing traffic to loopback addresses can be used for internal testing or monitoring.

```json
{
    "DFStringAltTelegrafAddress": "127.0.0.1",
    "DFStringTelegrafAddress": "127.0.0.1"
}
```
