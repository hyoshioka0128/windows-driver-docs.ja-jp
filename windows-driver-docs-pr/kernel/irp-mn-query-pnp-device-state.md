---
title: IRP_MN_QUERY_PNP_DEVICE_STATE
description: 関数、フィルター、およびバスドライバーは、この要求を処理できます。
ms.date: 08/12/2017
ms.assetid: 24362a20-9e9d-4566-bc95-ce52b91056af
keywords:
- IRP_MN_QUERY_PNP_DEVICE_STATE カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: a5a10868d8a153fff60cd1f7e10658473cea04e9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838569"
---
# <a name="irp_mn_query_pnp_device_state"></a>IRP\_\_クエリ\_PNP\_デバイス\_状態


関数、フィルター、およびバスドライバーは、この要求を処理できます。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)送信時
---------

PnP マネージャーは、デバイスのドライバーが\_正常に復帰した後に、デバイスが最初に起動されたときに送信された[ **\_デバイスの要求\_開始**](irp-mn-start-device.md)するように、この irp を送信します。 この IRP は、リソースの再配分の停止後に開始時に送信されません。 また、デバイスのドライバーが[**IoInvalidateDeviceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicestate)を呼び出すと、この IRP が送信されます。

PnP マネージャーは、任意のスレッドのコンテキストで、この IRP を IRQL パッシブ\_レベルで送信します。

## <a name="input-parameters"></a>入力パラメーター


なし

## <a name="output-parameters"></a>出力パラメーター


I/o 状態ブロックで返されました。

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーは、 **Irp&gt;iostatus. status**を STATUS\_SUCCESS に設定します。または、状態\_失敗など、適切なエラー状態に設定します。

成功すると、ドライバーは**Irp&gt;IoStatus**を設定します。[**デバイス\_状態**](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-an-irp-mn-surprise-removal-request#about-pnpdevicestate)のビットマスク\_ます。


関数またはフィルタードライバーがこの IRP を処理しない場合は、 [**Ioskipfinalentifinallocation**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を呼び出し、 [*iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定せずに、irp を次のドライバーに渡します。 このようなドライバーでは、 **irp&gt;IoStatus**を変更しないでください。 irp を完了することはできません。

バスドライバーがこの IRP を処理しない場合は、 **irp&gt;iostatus**がそのままの状態になり、irp が完了します。

<a name="operation"></a>操作
---------

この IRP は、デバイススタックの最上位にあるドライバーによって最初に処理され、次にスタック内の1つ下のドライバーによって処理されます。

ドライバーは、デバイスの PnP 状態に関する情報を持っている場合、この IRP を処理します。 ドライバーは、PNP\_デバイス\_状態ビットマスクのフラグを設定または解除できます。 別のドライバーによって、 **Irp&gt;IoStatus. 情報**で PNP\_デバイス\_状態が設定されている場合、ドライバーは、構造体全体を上書きするのではなく、そのビットマスクのフラグを変更する必要があります。

[プラグアンドプレイの小さな irp](plug-and-play-minor-irps.md)を処理するための一般的な規則については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。

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


[**IoInvalidateDeviceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicestate)

[**PNP\_デバイスの\_状態**](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-an-irp-mn-surprise-removal-request#about-pnpdevicestate)
