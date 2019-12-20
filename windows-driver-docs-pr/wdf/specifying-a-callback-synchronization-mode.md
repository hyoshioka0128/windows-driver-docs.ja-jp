---
title: コールバック同期モードの指定
description: コールバック同期モードの指定
ms.assetid: 3e041493-1095-47cb-b9a7-879a4cf1bd2e
keywords:
- コールバック同期 WDK UMDF
- WDK の同期の UMDF
- キューコールバック関数 WDK UMDF
- コールバック関数 WDK UMDF
- I/o キュー WDK UMDF
- WDK の UMDF をロックする
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8a461ffece59f2890abab078372a938d551b243
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209950"
---
# <a name="specifying-a-callback-synchronization-mode"></a>コールバック同期モードの指定


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

ドライバーは、そのコールバック関数がフレームワークによってどのように呼び出されるかを指定できます。 ドライバーは、 [**Iwdfdriver:: CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)メソッドを呼び出してデバイスの[デバイスオブジェクト](framework-device-object.md)を作成する前に、デバイスの同期 (またはロック) モードを指定します。 同期モードを指定するには、ドライバーは[**Iwdfdeviceinitialize:: Setロック制約**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize-setlockingconstraint)メソッドを呼び出す必要があります。 ドライバーは、デバイスをシステムに追加するために、 [**Idriverentry:: OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)メソッドが呼び出されたときに、 [Iwdfdeviceinitialize](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdeviceinitialize)インターフェイスへのポインターを受け取ります。

ドライバーは、 **Iwdfdeviceinitialize:: SetWDF 制約**の*LockType*パラメーターで、次のいずれかの\_\_値を指定して、ロックモードを識別できます。 指定された制約の種類 (またはロック) は、ハードウェアデバイスが利用できる並列処理の量と、ドライバーが処理できる量によって異なります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>なし</strong>(0)</p></td>
<td align="left"><p>ドライバーへのコールバック関数が同期されていないことを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>WdfDeviceLevel</strong> (1)</p></td>
<td align="left"><p>ドライバーへのすべてのキューコールバック関数が同期されることを示します。</p></td>
</tr>
</tbody>
</table>

 

  **なお**、ドライバーが**Iwdfdeviceinitialize:: setWdfDeviceLevel 制約**を呼び出して値を指定していない場合、フレームワークはこのプロパティの既定値を**** に設定します。

 

制約は、キューコールバック関数にのみ適用され、プラグアンドプレイ (PnP) および電源管理コールバック関数には適用されません。 キューコールバック関数には、次のものがあります。

-   、 [**Iqueuecallbackread:: OnRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackread-onread) 、 [**Iqueuecallbackread:: onread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackwrite-onwrite)などの自動ディスパッチコールバック関数。 詳細については、「 [I/o キューイベントコールバック関数](i-o-queue-event-callback-functions.md)」を参照してください。

-   キュー状態変更コールバック関数 ( [**IQueueCallbackStateChange:: OnStateChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackstatechange-onstatechange)など)。

-   、 [**Irequestcallback cancel:: OnCancel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-irequestcallbackcancel-oncancel)などのキャンセルコールバック関数を要求します。

-   [**IFileCallbackCleanup:: OnCleanupFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ifilecallbackcleanup-oncleanupfile)や[**IFileCallbackClose:: oncleanupfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ifilecallbackclose-onclosefile)など、ファイルのクリーンアップと終了のコールバック関数。

要求の完了コールバック関数 ([**Irequestcallback Requestcompletion:: OnCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-irequestcallbackrequestcompletion-oncompletion)) は、キューのコールバック関数ではありません。 そのため、同期されません。

 

 





