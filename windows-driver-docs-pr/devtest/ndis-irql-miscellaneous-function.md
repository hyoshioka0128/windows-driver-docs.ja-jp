---
title: Irql\_その他の\_関数規則 (ndis)
description: Irql\_その他の\_関数規則は、正しい IRQL レベルで NDIS 関数を呼び出す必要があることを指定します。
ms.assetid: ae1d0243-1db9-428f-a112-f438e2322ff2
ms.date: 05/21/2018
keywords:
- Irql_Miscellaneous_Function rule (ndis)
topic_type:
- apiref
api_name:
- Irql_Miscellaneous_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a5c23e6b01b65a6d8c1fe1dced6456993751e795
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840108"
---
# <a name="irql_miscellaneous_function-rule-ndis"></a>Irql\_その他の\_関数規則 (ndis)


Irql\_その他の\_関数規則は、正しい IRQL レベルで NDIS 関数を呼び出す必要があることを指定します。

このルールは、次の機能を検証します。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>Irql_Miscellaneous_Function</strong>規則を指定します。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">コードを準備します (ロールの種類の宣言を使用します)。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">静的ドライバー検証ツールを実行します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">結果を表示して分析します。</a></li>
</ol>
<p>詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">Static Driver Verifier を使用したドライバーの欠陥の検出</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

[**NdisAllocateFromNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatefromnpagedlookasidelist)  
[**NdisAllocateGenericObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocategenericobject)  
[**NdisAllocateIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocateioworkitem)  
[**NdisAllocateMemoryWithTagPriority**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatememorywithtagpriority)  
[**NdisAnsiStringToUnicodeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisansistringtounicodestring)  
[**NdisCloseConfiguration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseconfiguration)  
[**NdisCloseFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclosefile)  
[**NdisDeleteNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisdeletenpagedlookasidelist)  
[**NdisDeregisterDeviceEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisderegisterdeviceex)  
[**NdisEqualMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisequalmemory)  
[**NdisEqualString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisequalstring)  
[**NdisEqualUnicodeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisequalunicodestring)  
[**NdisFreeGenericObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreegenericobject)  
[**NdisFreeIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreeioworkitem)  
[**NdisFreeMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreememory)  
[**NdisFreeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreestring)  
[**NdisFreeToNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreetonpagedlookasidelist)  
[**NdisGeneratePartialCancelId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgeneratepartialcancelid)  
[**NdisGetCurrentProcessorCounts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetcurrentprocessorcounts)  
[**NdisGetRoutineAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetroutineaddress)  
[**NdisGetSharedDataAlignment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetshareddataalignment)  
[**NdisGetVersion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetversion)  
[**NdisInitAnsiString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisinitansistring)  
[**NdisInitializeNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisinitializenpagedlookasidelist)  
[**NdisInitializeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisinitializestring)  
[**NdisInitUnicodeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisinitunicodestring)  
[**NdisMapFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismapfile)  
[**NdisOpenConfigurationEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenconfigurationex)  
[**NdisOpenConfigurationKeyByIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenconfigurationkeybyindex)  
[**NdisOpenConfigurationKeyByName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenconfigurationkeybyname)  
[**NdisOpenFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenfile)  
[**NdisQueryAdapterInstanceName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisqueryadapterinstancename)  
[**NdisQueryDepthSList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisquerydepthslist)  
[**NdisQueueIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisqueueioworkitem)  
[**NdisReadConfiguration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreadconfiguration)  
[**NdisReadNetworkAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreadnetworkaddress)  
[**NdisReEnumerateProtocolBindings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreenumerateprotocolbindings)  
[**NdisRegisterDeviceEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterdeviceex)  
[**NdisSetOptionalHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)  
[**NdisSystemProcessorCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissystemprocessorcount)  
[**NdisUnicodeStringToAnsiString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisunicodestringtoansistring)  
[**NdisUnmapFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisunmapfile)  
[**NdisUpcaseUnicodeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisupcaseunicodestring)  
[**NdisWaitEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiswaitevent)  
[**NdisWriteConfiguration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiswriteconfiguration)  
[**NdisWriteErrorLogEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiswriteerrorlogentry)  
[**NdisWriteEventLogEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiswriteeventlogentry)  
[**KeGetCurrentProcessorNumber**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-kegetcurrentprocessornumber)  








