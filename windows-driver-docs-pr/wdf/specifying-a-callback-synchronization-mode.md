---
title: コールバック同期モードの指定
description: コールバック同期モードの指定
ms.assetid: 3e041493-1095-47cb-b9a7-879a4cf1bd2e
keywords:
- コールバック同期 WDK UMDF
- WDK UMDF の同期
- queue WDK UMDF のコールバック関数
- WDK UMDF のコールバック関数
- WDK UMDF の I/O キュー
- ロックの WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: caa43943f6925481bf4527a58da4266dbf3444a8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376181"
---
# <a name="specifying-a-callback-synchronization-mode"></a>コールバック同期モードの指定


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

ドライバーは、フレームワークによってそのコールバック関数の呼び出し方法を指定できます。 ドライバーを同期を指定します (またはロック) を呼び出す前にデバイスのモード、 [ **IWDFDriver::CreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdriver-createdevice)を作成する方法、[デバイス オブジェクト](framework-device-object.md)デバイス. 同期モードを指定するドライバーを呼び出す必要があります、 [ **IWDFDeviceInitialize::SetLockingConstraint** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdeviceinitialize-setlockingconstraint)メソッド。 ドライバーへのポインターを受け取る、 [IWDFDeviceInitialize](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdeviceinitialize)インターフェイスの場合にその[ **IDriverEntry::OnDeviceAdd** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)システムにデバイスを追加するメソッドが呼び出されます。

ドライバーは、WDF から、次のいずれかの値を指定できます\_コールバック\_で列挙型の制約、 *LockType*パラメーターの**IWDFDeviceInitialize::SetLockingConstraint**ロック モードを識別します。 制約 (またはロック) の指定された型はどの程度の並列処理にハードウェア デバイスを悪用できるし、量、ドライバーを処理できます。

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
<td align="left"><p><strong>None</strong> (0)</p></td>
<td align="left"><p>ドライバーにコールバック関数が同期されないことを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>WdfDeviceLevel</strong> (1)</p></td>
<td align="left"><p>ドライバーにすべてのキューのコールバック関数が同期されていることを示します。</p></td>
</tr>
</tbody>
</table>

 

**注**  ドライバーが要求されていない場合**IWDFDeviceInitialize::SetLockingConstraint**フレームワークには、このプロパティの既定値の設定値を指定する**WdfDeviceLevel**.

 

制約は、キューのコールバック関数にのみ、プラグ アンド プレイ (PnP) と電源管理のコールバック関数が適用されます。 キューのコールバック関数を以下に示します。

-   自動のディスパッチのコールバック関数を次のように、 [ **IQueueCallbackRead::OnRead** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iqueuecallbackread-onread)と[ **IQueueCallbackWrite::OnWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iqueuecallbackwrite-onwrite)します。 詳細については、次を参照してください。 [I/O キュー イベントのコールバック関数](i-o-queue-event-callback-functions.md)します。

-   キューの状態を変更するなど、コールバック関数、 [ **IQueueCallbackStateChange::OnStateChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iqueuecallbackstatechange-onstatechange)します。

-   キャンセル コールバック関数を次のように、要求[ **IRequestCallbackCancel::OnCancel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-irequestcallbackcancel-oncancel)します。

-   ファイルのクリーンアップなど、コールバック関数を閉じたり[ **IFileCallbackCleanup::OnCleanupFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ifilecallbackcleanup-oncleanupfile)と[ **IFileCallbackClose::OnCloseFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ifilecallbackclose-onclosefile).

完了コールバック関数の要求 ([**IRequestCallbackRequestCompletion::OnCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-irequestcallbackrequestcompletion-oncompletion)) キューではないをコールバック関数には。 そのため、これらは同期されません。

 

 





