---
title: IRP_MN_CANCEL_REMOVE_DEVICE
description: すべての PnP ドライバーは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 5cadb1e2-7011-42a5-8e41-6473069b25a6
keywords:
- IRP_MN_CANCEL_REMOVE_DEVICE カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 23a193598412103f347ad07066ae6027a6f741f1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828081"
---
# <a name="irp_mn_cancel_remove_device"></a>IRP\_\_キャンセル\_\_デバイスの削除


すべての PnP ドライバーは、この IRP を処理する必要があります。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)送信時
---------

PnP マネージャーは、デバイスが削除されないことをデバイスのドライバーに通知するために、この IRP を送信します。

PnP マネージャーは、システムスレッドのコンテキストでこの IRP を IRQL パッシブ\_レベルで送信します。

## <a name="input-parameters"></a>入力パラメーター


なし

## <a name="output-parameters"></a>出力パラメーター


なし

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーでは、 **irp&gt;IoStatus. status**\_を、この IRP の正常な状態に設定する必要があります。 ドライバーがこの IRP に失敗した場合、デバイスは不整合な状態のままになります。

<a name="operation"></a>操作
---------

この IRP は、デバイスの親バスドライバーによって最初に処理され、その後、デバイススタック内の上位の各ドライバーによって処理される必要があります。

この IRP への応答として、ドライバーは、\_デバイスの要求を削除\_ために、 **irp\_\_クエリ**を受信する前の状態にデバイスを返します。

ドライバーがこの IRP を受信したときにデバイスが既に起動している場合、ドライバーは単に status を success に設定し、IRP を次のドライバーに渡します (または、ドライバーがバスドライバーの場合は IRP を完了します)。 このような削除を行う IRP の場合、関数またはフィルタードライバーは、完了ルーチンを設定する必要はありません。 デバイスが保留中の状態になっていない可能性があります。たとえば、ドライバーが以前の**IRP\_完了した\_クエリ\_\_デバイスを削除**しようとした場合などです。

PnP マネージャーは、すべての**Eventdeviceid Targetdevicechange**通知コールバックを呼び出します。 GUID\_ターゲット\_デバイス\_削除\_IRP\_完了後に取り消され\_**デバイス\_削除\_** 要求が完了します。 このようなコールバックは、 [**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)を呼び出すことによってデバイスに登録されました。 また、PnP マネージャーは、 **RegisterDeviceNotification**を呼び出すことによって、デバイスで通知するために登録されたユーザーモードのコンポーネントも呼び出します。

ファイルシステムがデバイスにマウントされている場合は、クエリ削除通知に応答して実行した操作を元に戻す必要があります。

削除 Irp の処理の詳細については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。また、すべての[プラグアンドプレイ軽微な irp](plug-and-play-minor-irps.md)を処理するための一般的なルールについては、

**この IRP を送信しています**

システム用に予約されています。 ドライバーは、この IRP を送信することはできません。

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
<td>Wdm (Wdm .h、Ntddk、または Ntifs を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)

[**IRP\_\_クエリ\_\_デバイスの削除**](irp-mn-query-remove-device.md)

 

 




