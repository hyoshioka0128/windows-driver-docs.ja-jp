---
title: IRP_MN_CANCEL_REMOVE_DEVICE
description: すべての PnP ドライバーは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 5cadb1e2-7011-42a5-8e41-6473069b25a6
keywords:
- IRP_MN_CANCEL_REMOVE_DEVICE カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 68e3c96f910d47b093dc0fa75aefe9b9bf7b7d38
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922537"
---
# <a name="irp_mn_cancel_remove_device"></a>\_IRP\_を終了\_する\_デバイスの削除


すべての PnP ドライバーは、この IRP を処理する必要があります。

## <a name="value"></a>値

0x03

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>送信時
---------

PnP マネージャーは、デバイスが削除されないことをデバイスのドライバーに通知するために、この IRP を送信します。

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

この IRP への応答として、ドライバーは、 **irp\_\_が "デバイスの\_削除\_** " 要求を受け取る前の状態にデバイスを返します。

ドライバーがこの IRP を受信したときにデバイスが既に起動している場合、ドライバーは単に status を success に設定し、IRP を次のドライバーに渡します (または、ドライバーがバスドライバーの場合は IRP を完了します)。 このような削除を行う IRP の場合、関数またはフィルタードライバーは、完了ルーチンを設定する必要はありません。 デバイスが保留中の状態にならない可能性があります。たとえば、ドライバーが前の**IRP\_\_\_\_** を完了したクエリを削除すると、デバイスが削除されないことがあります。

PnP マネージャーは、任意**の Eventカテゴリ Targetdevicechange**通知コールバック\_を\_呼び出し\_ます\_。 GUID ターゲットデバイスの**削除要求\_が\_\_\_** 完了した後、削除は取り消されました。 このようなコールバックは、 [**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)を呼び出すことによってデバイスに登録されました。 また、PnP マネージャーは、 **RegisterDeviceNotification**を呼び出すことによって、デバイスで通知するために登録されたユーザーモードのコンポーネントも呼び出します。

ファイルシステムがデバイスにマウントされている場合は、クエリ削除通知に応答して実行した操作を元に戻す必要があります。

削除 Irp の処理の詳細については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。また、すべての[プラグアンドプレイ軽微な irp](plug-and-play-minor-irps.md)を処理するための一般的なルールについては、

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


[**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)

[**IRP\_を\_実行\_する\_クエリデバイスの削除**](irp-mn-query-remove-device.md)

 

 




