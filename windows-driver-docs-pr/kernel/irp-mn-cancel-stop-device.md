---
title: IRP_MN_CANCEL_STOP_DEVICE
description: すべての PnP ドライバーでは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 7047c266-84b4-4260-ad75-d56c87c8c9ef
keywords:
- IRP_MN_CANCEL_STOP_DEVICE Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: 3a077ad80a4c11379ff0e3bfa1751d3793a4faae
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382251"
---
# <a name="irpmncancelstopdevice"></a>IRP\_MN\_キャンセル\_停止\_デバイス


すべての PnP ドライバーでは、この IRP を処理する必要があります。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP** ](irp-mj-pnp.md)送信されるときに
---------

PnP マネージャーでは、この IRP を送信した後は、ある時点で、 [ **IRP\_MN\_クエリ\_停止\_デバイス**](irp-mn-query-stop-device.md)デバイスのドライバーに通知するが、デバイスが無効 (Windows 98/自分のみ) またはリソースの再構成のために停止します。

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

この IRP に応答してでは、ドライバーは、デバイスを開始状態に戻ります。 ドライバーは、デバイスが保留中の停止の状態の中に格納されていた任意の Irp を開始します。

場合は、デバイスがまだアクティブな状態で、ドライバーは、この IRP を受信すると、関数またはフィルター ドライバーは単に状態を成功に設定し、[次へ] のドライバーを IRP を渡します。 親のバス ドライバーは IRP を完了します。 このようなキャンセル停止 IRP では、関数またはフィルター ドライバーは完了ルーチンを設定しない必要があります。

参照してください[プラグ アンド プレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)停止 Irp の処理の詳細については、すべてを処理するための一般的な規則[プラグ アンド プレイ マイナー Irp](plug-and-play-minor-irps.md)します。

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


[**IRP\_MN\_クエリ\_停止\_デバイス**](irp-mn-query-stop-device.md)

 

 




