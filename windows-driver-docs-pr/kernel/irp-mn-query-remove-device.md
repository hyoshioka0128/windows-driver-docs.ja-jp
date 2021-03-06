---
title: IRP_MN_QUERY_REMOVE_DEVICE
description: すべての PnP ドライバーでは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 95ec9ed8-014f-4d01-bed7-3aeb29cd9e73
keywords:
- IRP_MN_QUERY_REMOVE_DEVICE カーネル モード ドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 1d4e6c8e515785d6629a8281cde1d406aa676305
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370859"
---
# <a name="irpmnqueryremovedevice"></a>IRP\_MN\_クエリ\_削除\_デバイス


すべての PnP ドライバーでは、この IRP を処理する必要があります。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP** ](irp-mj-pnp.md)送信されるときに
---------

PnP マネージャーでは、デバイスは、コンピューターを中断することに、デバイスを削除できるかどうか、およびクエリをコンピューターから削除される直前に、ドライバーに通知するには、この IRP を送信します。 PnP マネージャーは、デバイスのドライバーを更新するユーザーが要求した場合にもこの IRP を送信します。

PnP マネージャーでは、この IRP を送信 IRQL パッシブで\_システム スレッドのコンテキスト内のレベル。

## <a name="input-parameters"></a>入力パラメーター


なし

## <a name="output-parameters"></a>出力パラメーター


なし

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーの設定**Irp -&gt;IoStatus.Status**ステータス\_成功や状態などの適切なエラー状態に\_失敗しました。

<a name="operation"></a>操作
---------

この IRP では、デバイス スタックの上部にあるドライバーによって最初に処理され、各スタックの下位のドライバーに渡されます。

この IRP に応答して、ドライバーは、コンピューターを中断することに、デバイスを削除できるかどうかを示します。

この IRP の処理の詳細については、次を参照してください。 [IRP の処理\_MN\_クエリ\_削除\_デバイス要求](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-an-irp-mn-query-remove-device-request)します。 デバイスの削除のサポートに関する概要については、次を参照してください。[デバイスを削除する](https://docs.microsoft.com/windows-hardware/drivers/kernel/removing-a-device)します。

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


[**IRP\_MN\_CANCEL\_REMOVE\_DEVICE**](irp-mn-cancel-remove-device.md)

[**IRP\_MN\_デバイス\_使用状況\_通知**](irp-mn-device-usage-notification.md)

[**IRP\_MN\_REMOVE\_DEVICE**](irp-mn-remove-device.md)

 

 




