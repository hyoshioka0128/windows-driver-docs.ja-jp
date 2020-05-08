---
title: IRP_MN_CANCEL_STOP_DEVICE
description: すべての PnP ドライバーは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 7047c266-84b4-4260-ad75-d56c87c8c9ef
keywords:
- IRP_MN_CANCEL_STOP_DEVICE カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 0bb8725f947a76624611861d7e2e28f78e273ef7
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922532"
---
# <a name="irp_mn_cancel_stop_device"></a>\_IRP\_が\_終了し\_たときにデバイスを停止する


すべての PnP ドライバーは、この IRP を処理する必要があります。

## <a name="value"></a>値

0x06

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>送信時
---------

PnP マネージャーは、 [**\_irp が可能な\_\_クエリの停止\_**](irp-mn-query-stop-device.md)後、ある時点でこの irp を送信し、デバイスが無効にならない (Windows 98/Me のみ) か、リソースの再構成のために停止されていないデバイスをドライバーに通知します。

PnP マネージャーは、システムスレッドのコンテキストで\_この IRP を IRQL パッシブレベルで送信します。

## <a name="input-parameters"></a>入力パラメーター


None

## <a name="output-parameters"></a>出力パラメーター


None

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーでは、この IRP の状態が\_SUCCESS に設定**&gt;され**ている必要があります。 ドライバーがこの IRP に失敗した場合、デバイスは不整合な状態のままになります。

<a name="operation"></a>Operation
---------

この IRP は、デバイスの親バスドライバーによって最初に処理され、その後、デバイススタック内の上位の各ドライバーによって処理される必要があります。

この IRP に応答して、ドライバーはデバイスを開始状態に戻します。 ドライバーは、デバイスが停止保留中の状態にあったときに保持されていたすべての Irp を開始します。

ドライバーがこの IRP を受信したときにデバイスが既にアクティブ状態になっている場合、関数またはフィルタードライバーは単に status を success に設定し、IRP を次のドライバーに渡します。 親バスドライバーが IRP を完了します。 このようなキャンセル停止の IRP の場合、関数またはフィルタードライバーは、完了ルーチンを設定する必要はありません。

停止 Irp の処理の詳細については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。また、すべての[プラグアンドプレイ軽微な irp](plug-and-play-minor-irps.md)を処理するための一般的な規則をご覧ください。

**この IRP を送信しています**

システムで使用するために予約されています。 ドライバーは、この IRP を送信することはできません。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>ヘッダー</p></td>
<td>Wdm.h (Wdm.h、Ntddk.h、Ntifs.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**IRP\_の\_全\_クエリ\_の停止デバイス**](irp-mn-query-stop-device.md)

 

 




