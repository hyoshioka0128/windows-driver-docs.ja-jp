---
title: IRP_MN_CANCEL_REMOVE_DEVICE
description: すべての PnP ドライバーでは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 5cadb1e2-7011-42a5-8e41-6473069b25a6
keywords:
- IRP_MN_CANCEL_REMOVE_DEVICE Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: 8cd7eea40cbe3b1108668c8ca3f61b66ea5dfad5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368404"
---
# <a name="irpmncancelremovedevice"></a>IRP\_MN\_CANCEL\_REMOVE\_DEVICE


すべての PnP ドライバーでは、この IRP を処理する必要があります。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP** ](irp-mj-pnp.md)送信されるときに
---------

PnP マネージャーでは、デバイスは削除されませんをデバイスのドライバーに通知するためには、この IRP を送信します。

PnP マネージャーでは、この IRP を送信 IRQL パッシブで\_システム スレッドのコンテキスト内のレベル。

## <a name="input-parameters"></a>入力パラメーター


なし

## <a name="output-parameters"></a>出力パラメーター


なし

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーを設定する必要があります**Irp -&gt;IoStatus.Status**ステータス\_この IRP の成功します。 ドライバーには、この IRP が失敗した場合、デバイスは一貫性のない状態のままです。

<a name="operation"></a>操作
---------

この IRP は、デバイスの親のバス ドライバー、続いてデバイス スタックの各以上のドライバー最初に処理する必要があります。

この IRP への応答、ドライバーは受信前の状態にデバイスを返す、 **IRP\_MN\_クエリ\_削除\_デバイス**要求。

ドライバーは、この IRP を受信すると、デバイスが既に開始されている場合、ドライバーだけの状態を成功に設定し IRP を次のドライバーに渡します (または IRP を完了する場合は、ドライバーは、バス ドライバー)。 このようなキャンセルと削除 IRP では、関数またはフィルター ドライバーは完了ルーチンを設定しない必要があります。 デバイスではありません、削除保留中状態をたとえば、ドライバーが、以前失敗したため、 **IRP\_MN\_クエリ\_削除\_デバイス**します。

PnP マネージャーでは、いずれかを呼び出す**EventCategoryTargetDeviceChange**通知コールバックの GUID を持つ\_ターゲット\_デバイス\_削除\_の後に取り消さ、 **IRP\_MN\_キャンセル\_削除\_デバイス**要求が完了します。 このようなコールバックは、呼び出すことによって、デバイスに登録された[ **IoRegisterPlugPlayNotification**](https://msdn.microsoft.com/library/windows/hardware/ff549526)します。 PnP マネージャーも呼び出しますユーザー モード コンポーネントを登録したデバイスに通知を呼び出すことによって**RegisterDeviceNotification**します。

デバイスのファイル システムをマウントすると、クエリの削除通知に応答したすべての操作を元に戻す必要があります。

参照してください[プラグ アンド プレイ](https://msdn.microsoft.com/library/windows/hardware/ff547125)削除 Irp の処理の詳細については、すべてを処理するための一般的な規則[プラグ アンド プレイ マイナー Irp](plug-and-play-minor-irps.md)します。

**この IRP を送信します。**

システムの使用に予約されています。 ドライバーは、この IRP を送信する必要があります。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wdm.h (Wdm.h、Ntddk.h、Ntifs.h など)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**IoRegisterPlugPlayNotification**](https://msdn.microsoft.com/library/windows/hardware/ff549526)

[**IRP\_MN\_クエリ\_削除\_デバイス**](irp-mn-query-remove-device.md)

 

 




