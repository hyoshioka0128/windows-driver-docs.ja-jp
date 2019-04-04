---
title: コールバックの同期モードを指定します。
description: コールバックの同期モードを指定します。
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
ms.openlocfilehash: a2fae225abd151ec6b0c6956b720e375c26e3cd1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527872"
---
# <a name="specifying-a-callback-synchronization-mode"></a>コールバックの同期モードを指定します。


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

ドライバーは、フレームワークによってそのコールバック関数の呼び出し方法を指定できます。 ドライバーを同期を指定します (またはロック) を呼び出す前にデバイスのモード、 [ **IWDFDriver::CreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff558899)を作成する方法、[デバイス オブジェクト](framework-device-object.md)デバイス. 同期モードを指定するドライバーを呼び出す必要があります、 [ **IWDFDeviceInitialize::SetLockingConstraint** ](https://msdn.microsoft.com/library/windows/hardware/ff556991)メソッド。 ドライバーへのポインターを受け取る、 [IWDFDeviceInitialize](https://msdn.microsoft.com/library/windows/hardware/ff556965)インターフェイスの場合にその[ **IDriverEntry::OnDeviceAdd** ](https://msdn.microsoft.com/library/windows/hardware/ff554896)システムにデバイスを追加するメソッドが呼び出されます。

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

-   自動のディスパッチのコールバック関数を次のように、 [ **IQueueCallbackRead::OnRead** ](https://msdn.microsoft.com/library/windows/hardware/ff556875)と[ **IQueueCallbackWrite::OnWrite**](https://msdn.microsoft.com/library/windows/hardware/ff556885)します。 詳細については、[I/O キュー イベントのコールバック関数](i-o-queue-event-callback-functions.md)を参照してください。

-   キューの状態を変更するなど、コールバック関数、 [ **IQueueCallbackStateChange::OnStateChange**](https://msdn.microsoft.com/library/windows/hardware/ff556880)します。

-   キャンセル コールバック関数を次のように、要求[ **IRequestCallbackCancel::OnCancel**](https://msdn.microsoft.com/library/windows/hardware/ff556903)します。

-   ファイルのクリーンアップなど、コールバック関数を閉じたり[ **IFileCallbackCleanup::OnCleanupFile** ](https://msdn.microsoft.com/library/windows/hardware/ff554905)と[ **IFileCallbackClose::OnCloseFile** ](https://msdn.microsoft.com/library/windows/hardware/ff554910).

完了コールバック関数の要求 ([**IRequestCallbackRequestCompletion::OnCompletion**](https://msdn.microsoft.com/library/windows/hardware/ff556905)) キューではないをコールバック関数には。 そのため、これらは同期されません。

 

 





