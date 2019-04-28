---
title: IRP_MN_QUERY_STOP_DEVICE
description: すべての PnP ドライバーでは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 22f58964-23a0-4307-a748-9c1620e30871
keywords:
- IRP_MN_QUERY_STOP_DEVICE カーネル モード ドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 81dc0f034b028e240b637525b3e5026a5b78b938
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381418"
---
# <a name="irpmnquerystopdevice"></a>IRP\_MN\_クエリ\_停止\_デバイス


すべての PnP ドライバーでは、この IRP を処理する必要があります。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP** ](irp-mj-pnp.md)送信されるときに
---------

PnP マネージャーでは、リソースを再調整するデバイスを停止できるかどうかに、この IRP がクエリを送信します。

Windows 98 で、PnP マネージャーも送信この IRP のデバイスを無効にされているとします。

PnP マネージャーでは、この IRP を送信 IRQL パッシブで\_システム スレッドのコンテキスト内のレベル。

## <a name="input-parameters"></a>入力パラメーター


なし

## <a name="output-parameters"></a>出力パラメーター


なし

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーの設定**Irp -&gt;IoStatus.Status**ステータス\_成功または適切なエラーの状態にします。 ドライバーがデバイスを停止できない場合、ドライバーは設定**Irp -&gt;IoStatus.Status**ステータス\_失敗しました。

バス ドライバーを設定できます**Irp -&gt;IoStatus.Status**ステータス\_リソース\_要件\_成功を示す IRP が要求を PnP マネージャー requery CHANGED停止 IRP を送信する前に、デバイスのリソース要件。

<a name="operation"></a>操作
---------

この IRP では、デバイス スタックの上部にあるドライバーによって最初に処理され、各スタックの下位のドライバーに渡されます。

この IRP に応答して、Windows 2000 およびそれ以降のドライバーを示してのリソースの負荷を分散デバイスを停止しても安全だかどうか。

Windows 98 でリソースが再調整時にだけでなくこの IRP が送信されますがもときに、デバイスは無効化/。 ドライバーがこれら 2 つの状況を識別できないため、デバイスを無効にするのを続行するようにします。 デバイスに開いているハンドルがある場合は、ドライバーはこの IRP に失敗します。 」の説明に従って、ドライバーを続行する開いているハンドルがない場合は、 [IRP の処理\_MN\_クエリ\_停止\_デバイス要求 (Windows 98/Me)](https://msdn.microsoft.com/library/windows/hardware/ff546684)します。

参照してください[プラグ アンド プレイ](https://msdn.microsoft.com/library/windows/hardware/ff547125)処理のための一般的な規則[プラグ アンド プレイ マイナー Irp](plug-and-play-minor-irps.md)します。

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


[**IRP\_MN\_CANCEL\_STOP\_DEVICE**](irp-mn-cancel-stop-device.md)

[**IRP\_MN\_デバイス\_使用状況\_通知**](irp-mn-device-usage-notification.md)

[**IRP\_MN\_START\_DEVICE**](irp-mn-start-device.md)

[**IRP\_MN\_停止\_デバイス**](irp-mn-stop-device.md)

 

 




