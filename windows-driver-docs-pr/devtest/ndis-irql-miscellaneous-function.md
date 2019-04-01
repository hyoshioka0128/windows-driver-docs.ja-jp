---
title: Irql\_[その他]\_関数ルール (ndis)
description: Irql\_[その他]\_関数の規則は、適切な IRQL レベルで NDIS 関数を呼び出す必要がありますを指定します。
ms.assetid: ae1d0243-1db9-428f-a112-f438e2322ff2
ms.date: 05/21/2018
keywords:
- Irql_Miscellaneous_Function ルール (ndis)
topic_type:
- apiref
api_name:
- Irql_Miscellaneous_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f963047f1e47dcd999725591160a097527837816
ms.sourcegitcommit: 56599ec634b3a731f2d13dff686be3b7b95390e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2019
ms.locfileid: "58419590"
---
# <a name="irqlmiscellaneousfunction-rule-ndis"></a>Irql\_[その他]\_関数ルール (ndis)


Irql\_[その他]\_関数の規則は、適切な IRQL レベルで NDIS 関数を呼び出す必要がありますを指定します。

このルールは、次の機能を確認します。

**KeGetCurrentProcessorNumber**
**NdisAllocateFromNPagedLookasideList**
**NdisAllocateGenericObject**
**NdisAllocateIoWorkItem**
**NdisAllocateMemoryWithTagPriority**
**NdisAnsiStringToUnicodeString**
**NdisCloseConfiguration**
**NdisCloseFile**
**NdisDeleteNPagedLookasideList**
**NdisDeregisterDeviceEx**
**NdisEqualMemory**
**NdisEqualUnicodeString**
**NdisFreeGenericObject**
**NdisFreeIoWorkItem**
**NdisFreeMemory**
**NdisFreeSpinLock**
**NdisFreeString**
**NdisFreeToNPagedLookasideList**
**NdisGeneratePartialCancelId**
**NdisGetCurrentProcessorCounts**
**NdisGetDriverHandle**
**NdisGetRoutineAddress**
**NdisGetSharedDataAlignment**
**NdisGetVersion**
**NdisInitAnsiString**
**NdisInitializeListHead**
**NdisInitializeNPagedLookasideList**
**NdisInitializeSListHead**
**NdisInitializeString**
**NdisInitUnicodeString**
**NdisMapFile**
**NdisOpenConfigurationEx**
**NdisOpenConfigurationKeyByIndex**
**NdisOpenConfigurationKeyByName**
**NdisOpenFile**
**NdisQueryAdapterInstanceName**
**NdisQueryDepthSList**
**NdisQueueIoWorkItem**
**NdisReadConfiguration**
**NdisReadNetworkAddress**
**NdisReEnumerateProtocolBindings**
**NdisSetOptionalHandlers**
**NdisSystemProcessorCount**
**NdisUnicodeStringToAnsiString**
**NdisUnmapFile**
**NdisUpcaseUnicodeString**
**NdisWaitEvent**
**NdisWriteConfiguration**
**NdisWriteErrorLogEntry**
**NdisWriteEventLogEntry**

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コンパイル時</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>Irql_Miscellaneous_Function</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>します。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>対象
----------

[**NdisAllocateFromNPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff560708)  
[**NdisAllocateGenericObject**](https://msdn.microsoft.com/library/windows/hardware/ff561603)  
[**NdisAllocateIoWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff561604)  
[**NdisAllocateMemoryWithTagPriority**](https://msdn.microsoft.com/library/windows/hardware/ff561606)  
[**NdisAnsiStringToUnicodeString**](https://msdn.microsoft.com/library/windows/hardware/ff561619)  
[**NdisCloseConfiguration**](https://msdn.microsoft.com/library/windows/hardware/ff561642)  
[**NdisCloseFile**](https://msdn.microsoft.com/library/windows/hardware/ff561645)  
[**NdisDeleteNPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff561739)  
[**NdisDeregisterDeviceEx**](https://msdn.microsoft.com/library/windows/hardware/ff561741)  
[**NdisEqualMemory**](https://msdn.microsoft.com/library/windows/hardware/ff561760)  
[**NdisEqualString**](https://msdn.microsoft.com/library/windows/hardware/ff561771)  
[**NdisEqualUnicodeString**](https://msdn.microsoft.com/library/windows/hardware/ff561775)  
[**NdisFreeGenericObject**](https://msdn.microsoft.com/library/windows/hardware/ff561850)  
[**NdisFreeIoWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff561855)  
[**NdisFreeMemory**](https://msdn.microsoft.com/library/windows/hardware/ff562577)  
[**NdisFreeString**](https://msdn.microsoft.com/library/windows/hardware/ff562604)  
[**NdisFreeToNPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff562607)  
[**NdisGeneratePartialCancelId**](https://msdn.microsoft.com/library/windows/hardware/ff562623)  
[**NdisGetCurrentProcessorCounts**](https://msdn.microsoft.com/library/windows/hardware/ff562625)  
[**NdisGetRoutineAddress**](https://msdn.microsoft.com/library/windows/hardware/ff562665)  
[**NdisGetSharedDataAlignment**](https://msdn.microsoft.com/library/windows/hardware/ff562671)  
[**NdisGetVersion**](https://msdn.microsoft.com/library/windows/hardware/ff562680)  
[**NdisInitAnsiString**](https://msdn.microsoft.com/library/windows/hardware/ff562730)  
[**NdisInitializeNPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff562736)  
[**NdisInitializeString**](https://msdn.microsoft.com/library/windows/hardware/ff562741)  
[**NdisInitUnicodeString**](https://msdn.microsoft.com/library/windows/hardware/ff562745)  
[**NdisMapFile**](https://msdn.microsoft.com/library/windows/hardware/ff562785)  
[**NdisOpenConfigurationEx**](https://msdn.microsoft.com/library/windows/hardware/ff563717)  
[**NdisOpenConfigurationKeyByIndex**](https://msdn.microsoft.com/library/windows/hardware/ff563721)  
[**NdisOpenConfigurationKeyByName**](https://msdn.microsoft.com/library/windows/hardware/ff563725)  
[**NdisOpenFile**](https://msdn.microsoft.com/library/windows/hardware/ff563728)  
[**NdisQueryAdapterInstanceName**](https://msdn.microsoft.com/library/windows/hardware/ff563745)  
[**NdisQueryDepthSList**](https://msdn.microsoft.com/library/windows/hardware/ff563753)  
[**NdisQueueIoWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff563775)  
[**NdisReadConfiguration**](https://msdn.microsoft.com/library/windows/hardware/ff564511)  
[**NdisReadNetworkAddress**](https://msdn.microsoft.com/library/windows/hardware/ff564512)  
[**NdisReEnumerateProtocolBindings**](https://msdn.microsoft.com/library/windows/hardware/ff564516)  
[**NdisRegisterDeviceEx**](https://msdn.microsoft.com/library/windows/hardware/ff564518)  
[**NdisSetOptionalHandlers**](https://msdn.microsoft.com/library/windows/hardware/ff564550)  
[**NdisSystemProcessorCount**](https://msdn.microsoft.com/library/windows/hardware/ff564579)  
[**NdisUnicodeStringToAnsiString**](https://msdn.microsoft.com/library/windows/hardware/ff564635)  
[**NdisUnmapFile**](https://msdn.microsoft.com/library/windows/hardware/ff564641)  
[**NdisUpcaseUnicodeString**](https://msdn.microsoft.com/library/windows/hardware/ff564644)  
[**NdisWaitEvent**](https://msdn.microsoft.com/library/windows/hardware/ff564651)  
[**NdisWriteConfiguration**](https://msdn.microsoft.com/library/windows/hardware/ff564659)  
[**NdisWriteErrorLogEntry**](https://msdn.microsoft.com/library/windows/hardware/ff564663)  
[**NdisWriteEventLogEntry**](https://msdn.microsoft.com/library/windows/hardware/ff564672)  
[**KeGetCurrentProcessorNumber**](https://msdn.microsoft.com/library/windows/hardware/ff552063)  








