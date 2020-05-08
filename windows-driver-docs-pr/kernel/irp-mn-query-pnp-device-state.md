---
title: IRP_MN_QUERY_PNP_DEVICE_STATE
description: 関数、フィルター、およびバスドライバーは、この要求を処理できます。
ms.date: 08/12/2017
ms.assetid: 24362a20-9e9d-4566-bc95-ce52b91056af
keywords:
- IRP_MN_QUERY_PNP_DEVICE_STATE カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 681a754f044eb28b51f55759b855d9bfe06a061d
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922595"
---
# <a name="irp_mn_query_pnp_device_state"></a>IRP\_の\_全\_クエリ\_の\_PNP デバイスの状態


関数、フィルター、およびバスドライバーは、この要求を処理できます。

## <a name="value"></a>値

0x14

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>送信時
---------

PnP マネージャーは、デバイスのドライバーが最初に起動されたときに送信された[**\_irp\_の\_開始デバイス**](irp-mn-start-device.md)の要求から成功を返した後に、この irp を送信します。 この IRP は、リソースの再配分の停止後に開始時に送信されません。 また、デバイスのドライバーが[**IoInvalidateDeviceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicestate)を呼び出すと、この IRP が送信されます。

PnP マネージャーは、任意のスレッドのコンテキスト\_で、この IRP を IRQL パッシブレベルで送信します。

## <a name="input-parameters"></a>入力パラメーター


None

## <a name="output-parameters"></a>出力パラメーター


I/o 状態ブロックで返されました。

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーは、 **Irp-&gt;iostatus**を、status が\_SUCCESS に設定されているか、状態\_が "失敗" などの適切なエラー状態に設定されています。

成功した場合、ドライバーは**Irp&gt;-Iostatus**を[**\_PNP\_デバイスの状態**](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-an-irp-mn-surprise-removal-request#about-pnpdevicestate)ビットマスクに設定します。


関数またはフィルタードライバーがこの IRP を処理しない場合は、 [**Ioskipfinalentifinallocation**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を呼び出し、 [*iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定せずに、irp を次のドライバーに渡します。 このようなドライバーでは、 **irp&gt;-iostatus**を変更しないでください。 irp を完了することはできません。

バスドライバーがこの IRP を処理しない場合は、 **irp-&gt;iostatus**をそのままにして、irp を完了します。

<a name="operation"></a>Operation
---------

この IRP は、デバイススタックの最上位にあるドライバーによって最初に処理され、次にスタック内の1つ下のドライバーによって処理されます。

ドライバーは、デバイスの PnP 状態に関する情報を持っている場合、この IRP を処理します。 ドライバーは、PNP\_デバイス\_の状態ビットマスクのフラグを設定または解除できます。 別のドライバーによって、\_ **Irp-&gt;IOSTATUS. 情報**に PNP デバイス\_の状態が設定されている場合、ドライバーは、構造体全体を上書きするのではなく、そのビットマスクのフラグを変更する必要があります。

[プラグアンドプレイの小さな irp](plug-and-play-minor-irps.md)を処理するための一般的な規則については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。

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


[**IoInvalidateDeviceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicestate)

[**PNP\_デバイス\_の状態**](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-an-irp-mn-surprise-removal-request#about-pnpdevicestate)
