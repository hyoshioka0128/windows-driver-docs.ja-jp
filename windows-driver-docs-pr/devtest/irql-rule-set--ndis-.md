---
title: IRQL の規則セット (NDIS)
description: これらの規則を使用すると、ドライバーが必要な IRQL で DDI 呼び出しを行うことを確認します。IRQL の規則に従っていないドライバーは、デッドロック状態またはコンピューターがクラッシュする可能性のある操作中に重大な問題を発生することができます。
ms.assetid: EEFEF8E3-8AB8-46AD-A3BD-DA676F8FA786
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4befa47c1344c34329372af6135fe338d563f161
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570530"
---
# <a name="irql-rule-set-ndis"></a>IRQL の規則セット (NDIS)


これらの規則を使用すると、ドライバーが必要な IRQL で DDI 呼び出しを行うことを確認します。

IRQL の規則に従っていないドライバーは、デッドロック状態またはコンピューターがクラッシュする可能性のある操作中に重大な問題を発生することができます。

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="ndis-flags-irql.md" data-raw-source="[&lt;strong&gt;Flags_Irql&lt;/strong&gt;](ndis-flags-irql.md)"><strong>Flags_Irql</strong></a></p></td>
<td align="left"><p><a href="ndis-flags-irql.md" data-raw-source="[&lt;strong&gt;Flags_Irql&lt;/strong&gt;](ndis-flags-irql.md)"> <strong>Flags_Irql</strong> </a>ルールを指定する<strong>KeGetCurrentIrql</strong>しないを示すディスパッチ レベルのフラグ パラメーターを持つコールバック関数内で呼び出す必要があります、現在の IRQL します。</p>
<p>ディスパッチのレベルのフラグの正しい使用では、IRQL を設定しようと不要なを回避できます。 このフラグを使用する方法の詳細については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/hardware/ff546448" data-raw-source="[Dispatch IRQL Tracking](https://msdn.microsoft.com/library/windows/hardware/ff546448)">ディスパッチ IRQL 追跡</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-irql-callmanager-function.md" data-raw-source="[&lt;strong&gt;Irql_CallManager_Function&lt;/strong&gt;](ndis-irql-callmanager-function.md)"><strong>Irql_CallManager_Function</strong></a></p></td>
<td align="left"><p><a href="ndis-irql-callmanager-function.md" data-raw-source="[&lt;strong&gt;Irql_CallManager_Function&lt;/strong&gt;](ndis-irql-callmanager-function.md)"> <strong>Irql_CallManager_Function</strong> </a>ルールでは、適切な IRQL レベルで NDIS CallManager の NDIS 関数を呼び出す必要がありますを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-irql-connection-function.md" data-raw-source="[&lt;strong&gt;Irql_Connection_Function&lt;/strong&gt;](ndis-irql-connection-function.md)"><strong>Irql_Connection_Function</strong></a></p></td>
<td align="left"><p><a href="ndis-irql-connection-function.md" data-raw-source="[&lt;strong&gt;Irql_Connection_Function&lt;/strong&gt;](ndis-irql-connection-function.md)"> <strong>Irql_Connection_Function</strong> </a>ルールでは、適切な IRQL レベル プロトコル ドライバーの NDIS 接続関数を呼び出す必要がありますを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-irql-filter-driver-function.md" data-raw-source="[&lt;strong&gt;Irql_Filter_Driver_Function&lt;/strong&gt;](ndis-irql-filter-driver-function.md)"><strong>Irql_Filter_Driver_Function</strong></a></p></td>
<td align="left"><p>Irql_Filter_Driver_Function ルールでは、適切な IRQL レベルでフィルター ドライバーの NDIS 関数を呼び出す必要がありますを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-irql-gather-dma-function.md" data-raw-source="[&lt;strong&gt;Irql_Gather_DMA_Function&lt;/strong&gt;](ndis-irql-gather-dma-function.md)"><strong>Irql_Gather_DMA_Function</strong></a></p></td>
<td align="left"><p>Irql_Gather_DMA_Function ルールには、NDIS スキャッター/ギャザー DMA 関数は、適切な IRQL レベルで呼び出す必要がありますを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-irql-im-function.md" data-raw-source="[&lt;strong&gt;Irql_IM_Function&lt;/strong&gt;](ndis-irql-im-function.md)"><strong>Irql_IM_Function</strong></a></p></td>
<td align="left"><p>Irql_IM_Function ルールでは、適切な IRQL レベルで中間 (IM) ドライバーの NDIS 関数を呼び出す必要がありますを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-irql-interfaces-function.md" data-raw-source="[&lt;strong&gt;Irql_Interfaces_Function&lt;/strong&gt;](ndis-irql-interfaces-function.md)"><strong>Irql_Interfaces_Function</strong></a></p></td>
<td align="left"><p>Irql_Interfaces_Function ルールでは、適切な IRQL レベルで NDIS ネットワーク インターフェイスの関数を呼び出す必要がありますを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-irql-interrupt-function.md" data-raw-source="[&lt;strong&gt;Irql_Interrupt_Function&lt;/strong&gt;](ndis-irql-interrupt-function.md)"><strong>Irql_Interrupt_Function</strong></a></p></td>
<td align="left"><p>Irql_Interrupt_Function ルールでは、適切な IRQL レベルでの割り込みの NDIS 関数を呼び出す必要がありますを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-irql-irqlsetting-function.md" data-raw-source="[&lt;strong&gt;Irql_IrqlSetting_Function&lt;/strong&gt;](ndis-irql-irqlsetting-function.md)"><strong>Irql_IrqlSetting_Function</strong></a></p></td>
<td align="left"><p>Irql_IrqlSetting_Function ルールでは、適切な IRQL レベルで NDIS 割り込みマクロを呼び出す必要があることを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-irql-mcm-function.md" data-raw-source="[&lt;strong&gt;Irql_MCM_Function&lt;/strong&gt;](ndis-irql-mcm-function.md)"><strong>Irql_MCM_Function</strong></a></p></td>
<td align="left"><p><a href="ndis-irql-mcm-function.md" data-raw-source="[&lt;strong&gt;Irql_MCM_Function&lt;/strong&gt;](ndis-irql-mcm-function.md)"> <strong>Irql_MCM_Function</strong> </a>ルールでは、適切な IRQL レベルでのドライバーの NDIS MCM 関数を呼び出す必要がありますを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-irql-mco-function.md" data-raw-source="[&lt;strong&gt;Irql_MCO_Function&lt;/strong&gt;](ndis-irql-mco-function.md)"><strong>Irql_MCO_Function</strong></a></p></td>
<td align="left"><p><a href="ndis-irql-mco-function.md" data-raw-source="[&lt;strong&gt;Irql_MCO_Function&lt;/strong&gt;](ndis-irql-mco-function.md)"> <strong>Irql_MCO_Function</strong> </a>ルールでは、適切な IRQL レベルでのミニポート ドライバーの NDIS MCO Ddi を呼び出す必要があることを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-irql-miniport-driver-function.md" data-raw-source="[&lt;strong&gt;Irql_Miniport_Driver_Function&lt;/strong&gt;](ndis-irql-miniport-driver-function.md)"><strong>Irql_Miniport_Driver_Function</strong></a></p></td>
<td align="left"><p>Irql_Miniport_Driver_Function ルールでは、適切な IRQL レベルでのミニポート ドライバーの NDIS 関数を呼び出す必要がありますを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-irql-miscellaneous-function.md" data-raw-source="[&lt;strong&gt;Irql_Miscellaneous_Function&lt;/strong&gt;](ndis-irql-miscellaneous-function.md)"><strong>Irql_Miscellaneous_Function</strong></a></p></td>
<td align="left"><p>Irql_Miscellaneous_Function ルールでは、適切な IRQL レベルで NDIS 関数を呼び出す必要がありますを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-irql-netbuffer-function.md" data-raw-source="[&lt;strong&gt;Irql_NetBuffer_Function&lt;/strong&gt;](ndis-irql-netbuffer-function.md)"><strong>Irql_NetBuffer_Function</strong></a></p></td>
<td align="left"><p>Irql_NetBuffer_Function ルールでは、適切な IRQL レベルで NET_BUFFER 関連の関数を呼び出す必要がありますを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-irql-oid-function.md" data-raw-source="[&lt;strong&gt;Irql_OID_Function&lt;/strong&gt;](ndis-irql-oid-function.md)"><strong>Irql_OID_Function</strong></a></p></td>
<td align="left"><p><a href="ndis-irql-oid-function.md" data-raw-source="[&lt;strong&gt;Irql_OID_Function&lt;/strong&gt;](ndis-irql-oid-function.md)"> <strong>Irql_OID_Function</strong> </a>ルールでは、適切な IRQL レベルで NDIS OID 要求 Ddi を呼び出す必要があることを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-irql-protocol-driver-function.md" data-raw-source="[&lt;strong&gt;Irql_Protocol_Driver_Function&lt;/strong&gt;](ndis-irql-protocol-driver-function.md)"><strong>Irql_Protocol_Driver_Function</strong></a></p></td>
<td align="left"><p>Irql_Protocol_Driver_Function ルールでは、適切な IRQL レベルにいる CoNDIS クライアントの NDIS 関数を呼び出す必要がありますを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-irql-sendrcv-function.md" data-raw-source="[&lt;strong&gt;Irql_SendRcv_Function&lt;/strong&gt;](ndis-irql-sendrcv-function.md)"><strong>Irql_SendRcv_Function</strong></a></p></td>
<td align="left"><p><a href="ndis-irql-sendrcv-function.md" data-raw-source="[&lt;strong&gt;Irql_SendRcv_Function&lt;/strong&gt;](ndis-irql-sendrcv-function.md)"> <strong>Irql_SendRcv_Function</strong> </a>ルールでは、ことを指定します、送信と受信機能を適切な IRQL レベルで NDIS ドライバーを呼び出す必要があるのです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-irql-statusindication-function.md" data-raw-source="[&lt;strong&gt;Irql_StatusIndication_Function&lt;/strong&gt;](ndis-irql-statusindication-function.md)"><strong>Irql_StatusIndication_Function</strong></a></p></td>
<td align="left"><p>Irql_StatusIndication_Function ルールでは、適切な IRQL レベルとフィルターのミニポート ドライバーの NDIS 状態を示す値関数を呼び出す必要がありますを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-irql-synch-function.md" data-raw-source="[&lt;strong&gt;Irql_Synch_Function&lt;/strong&gt;](ndis-irql-synch-function.md)"><strong>Irql_Synch_Function</strong></a></p></td>
<td align="left"><p><a href="ndis-irql-synch-function.md" data-raw-source="[&lt;strong&gt;Irql_Synch_Function&lt;/strong&gt;](ndis-irql-synch-function.md)"> <strong>Irql_Synch_Function</strong> </a>ルール NDIS 割り込みと同期 Ddi する必要があります呼び出すように指定適切な IRQL レベル。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-irql-timer-function.md" data-raw-source="[&lt;strong&gt;Irql_Timer_Function&lt;/strong&gt;](ndis-irql-timer-function.md)"><strong>Irql_Timer_Function</strong></a></p></td>
<td align="left"><p>Irql_Timer_Function ルールでは、適切な IRQL レベルで NDIS タイマー サービスの関数を呼び出す必要がありますを指定します。</p></td>
</tr>
</tbody>
</table>

 

**Irql ルールを選択するには、次のように設定します。**

1.  Microsoft Visual Studio で、ドライバーのプロジェクト (.vcxProj) を選択します。 **ドライバー**  メニューのをクリックして**Static Driver Verifier を起動しています**.

2.  をクリックして、**ルール**タブ。**規則セット**、 **Irql**します。

    Visual Studio の開発者コマンド プロンプト ウィンドウから既定のルールを選択するには、次のように指定します。 **Irql.sdv**で、 **/check**オプション。 以下に例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:Irql.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、次を参照してください。[ドライバーで障害を検出する Static Driver Verifier を使用して](https://msdn.microsoft.com/library/windows/hardware/hh454281)と[Static Driver Verifier のコマンド (MSBuild)](https://msdn.microsoft.com/library/windows/hardware/hh466459)します。

 

 





