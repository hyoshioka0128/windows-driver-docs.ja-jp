---
title: ビデオ ポート DDI のサポート
description: Windows 8 以降では、ベースの Windows 2000 のディスプレイ ドライバー モデル (XDDM) でのディスプレイ ドライバーがインストールまたは実行するが GDI アクセシビリティおよびリモート ディスプレイ ドライバーがインストールおよび実行します。
ms.assetid: 87A98A49-B01B-419D-B570-6ECA60E2C7AF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3e12ad56ee5992084db2ba72dfc4ddbb797689a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575103"
---
# <a name="video-port-ddi-support"></a>ビデオ ポート DDI のサポート


ディスプレイに基づいてドライバーを Windows 8 では、以降では、 [Windows 2000 Display Driver Model (XDDM)](windows-2000-display-driver-model-design-guide.md)インストールまたは実行されませんが、 [GDI アクセシビリティ ドライバー](mirror-drivers.md)と[リモート ディスプレイ ドライバー](remote-display-drivers.md)がインストールおよび実行します。 これらのシナリオのビデオ ポート ドライバーによってエクスポートされる関数の一部のみサポートされます。

## <a name="span-idsupportedvideoportddisspanspan-idsupportedvideoportddisspanspan-idsupportedvideoportddisspansupported-video-port-ddis"></a><span id="Supported_Video_Port_DDIs"></span><span id="supported_video_port_ddis"></span><span id="SUPPORTED_VIDEO_PORT_DDIS"></span>サポートされているビデオ ポート Ddi


GDI のアクセシビリティのドライバーとリモート次システムによって実装されるビデオ ポート ドライバーのデバイス ドライバー インターフェイス (Ddi) がまだサポートされている Windows 8 以降では、ドライバーのシナリオを表示します。

-   VideoDebugPrint
-   VideoPortAcquireDeviceLock
-   VideoPortAcquireSpinLock
-   VideoPortAcquireSpinLockAtDpcLevel
-   VideoPortAllocatePool
-   VideoPortClearEvent
-   VideoPortCompareMemory
-   VideoPortCreateEvent
-   VideoPortCreateSpinLock
-   VideoPortDeleteEvent
-   VideoPortDeleteSpinLock
-   VideoPortFlushRegistry
-   VideoPortFreePool
-   VideoPortGetAssociatedDeviceExtension
-   VideoPortGetCurrentIrql
-   VideoPortGetProcAddress
-   VideoPortGetRegistryParameters
-   VideoPortGetVersion
-   VideoPortInterlockedDecrement
-   VideoPortInterlockedExchange
-   VideoPortInterlockedIncrement
-   VideoPortInitialize
-   VideoPortLockBuffer
-   VideoPortLogError
-   VideoPortMoveMemory
-   VideoPortQueryPerformanceCounter
-   VideoPortQueryServices
-   VideoPortQuerySystemTime
-   VideoPortQueueDpc
-   VideoPortReadStateEvent
-   VideoPortReleaseDeviceLock
-   VideoPortReleaseSpinLock
-   VideoPortReleaseSpinLockFromDpcLevel
-   VideoPortSetEvent
-   VideoPortSetRegistryParameters
-   VideoPortSynchronizeExecution
-   VideoPortUnlockBuffer
-   VideoPortWaitForSingleObject
-   VideoPortZeroMemory

## <a name="span-idunsupportedvideoportddisspanspan-idunsupportedvideoportddisspanspan-idunsupportedvideoportddisspanunsupported-video-port-ddis"></a><span id="Unsupported_Video_Port_DDIs"></span><span id="unsupported_video_port_ddis"></span><span id="UNSUPPORTED_VIDEO_PORT_DDIS"></span>サポートされていないビデオ ポート Ddi


GDI アクセシビリティ ドライバーおよびリモート ディスプレイ ドライバーのシナリオについて、Windows 8 以降、次システムによって実装されるビデオ ポート ドライバー Ddi ことはサポートされていません。

アスタリスクでマークされた項目 (\*) は Windows 8 以降ではサポートされなくハードウェア シナリオ用。

-   VideoPortAllocateBuffer
-   VideoPortAllocateCommonBuffer
-   VideoPortAllocateContiguousMemory
-   VideoPortAssociateEventsWithDmaHandle
-   VideoPortCheckForDeviceExistence\*
-   VideoPortCompleteDma\*
-   VideoPortCreateSecondaryDisplay\*
-   VideoPortDDCMonitorHelper\*
-   VideoPortDebugPrint
-   VideoPortDisableInterrupt
-   VideoPortDoDma
-   VideoPortEnableInterrupt
-   VideoPortEnumerateChildren\*
-   VideoPortFreeCommonBuffer
-   VideoPortFreeDeviceBase\*
-   VideoPortGetAccessRanges\*
-   VideoPortGetAgpServices
-   VideoPortGetAssociatedDeviceID\*
-   VideoPortGetBusData\*
-   VideoPortGetBytesUsed
-   VideoPortGetCommonBuffer
-   VideoPortGetDeviceBase\*
-   VideoPortGetDeviceData\*
-   VideoPortGetDmaAdapter\*
-   VideoPortGetDmaContext
-   VideoPortGetMdl
-   VideoPortGetRomImage\*
-   VideoPortGetVgaStatus\*
-   VideoPortInt10\*
-   VideoPortIsNoVesa\*
-   VideoPortLockPages
-   VideoPortMapBankedMemory
-   VideoPortMapDmaMemory
-   VideoPortMapMemory\*
-   VideoPortProtectWCMemory\*
-   VideoPortPutDmaAdapter\*
-   VideoPortReadPortBufferUchar\*
-   VideoPortReadPortBufferUlong\*
-   VideoPortReadPortBufferUshort\*
-   VideoPortReadPortUchar\*
-   VideoPortReadPortUlong\*
-   VideoPortReadPortUshort\*
-   VideoPortReadRegisterBufferUchar
-   VideoPortReadRegisterBufferUlong
-   VideoPortReadRegisterBufferUshort
-   VideoPortReadRegisterUchar
-   VideoPortReadRegisterUlong
-   VideoPortReadRegisterUshort
-   VideoPortRegisterBugcheckCallback
-   VideoPortReleaseBuffer
-   VideoPortReleaseCommonBuffer\*
-   VideoPortRestoreWCMemory\*
-   VideoPortScanRom\*
-   VideoPortSetBusData\*
-   VideoPortSetBytesUsed
-   VideoPortSetDmaContext
-   VideoPortSetTrappedEmulatorPorts\*
-   VideoPortSignalDmaComplete
-   VideoPortStallExecution
-   VideoPortStartDma\*
-   VideoPortStartTimer
-   VideoPortStopTimer
-   VideoPortUnlockPages
-   VideoPortUnmapDmaMemory
-   VideoPortUnmapMemory\*
-   VideoPortVerifyAccessRanges\*
-   VideoPortWritePortBufferUchar\*
-   VideoPortWritePortBufferUlong\*
-   VideoPortWritePortBufferUshort\*
-   VideoPortWritePortUchar\*
-   VideoPortWritePortUlong\*
-   VideoPortWritePortUshort\*
-   VideoPortWriteRegisterBufferUchar
-   VideoPortWriteRegisterBufferUlong
-   VideoPortWriteRegisterBufferUshort
-   VideoPortWriteRegisterUchar
-   VideoPortWriteRegisterUlong
-   VideoPortWriteRegisterUshort
-   VideoPortZeroDeviceMemory\*

 

 





