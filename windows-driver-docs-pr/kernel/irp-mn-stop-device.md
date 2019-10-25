---
title: IRP_MN_STOP_DEVICE
description: すべての PnP ドライバーは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: a5c81db0-e753-4d91-97e4-c58ea05f5ce8
keywords:
- IRP_MN_STOP_DEVICE カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 03bc3143324d86265bac7855dc3a7727d2569b7f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827949"
---
# <a name="irp_mn_stop_device"></a>IRP\_\_\_デバイスの停止


すべての PnP ドライバーは、この IRP を処理する必要があります。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)送信時
---------

PnP マネージャーは、この IRP を送信してデバイスを停止し、デバイスのハードウェアリソースを再構成できるようにします。

Windows 2000 以降のシステムでは、PnP マネージャーがこの IRP を送信するのは、前の[**irp\_\_クエリ\_\_デバイスの停止**](irp-mn-query-stop-device.md)が正常に完了した場合のみです。

Windows 98/Me では、デバイスが無効になっている場合や、デバイススタックが Irp\_に失敗した場合に、デバイスの要求 **\_開始\_** ことによって、この irp も送信されます。 開始に失敗した場合は、PnP マネージャーがこの IRP を送信する前に、前の[**irp\_を\_クエリ\_\_デバイス**](irp-mn-query-stop-device.md)要求を停止します。

PnP マネージャーは、システムスレッドのコンテキストでこの IRP を IRQL パッシブ\_レベルで送信します。

## <a name="input-parameters"></a>入力パラメーター


なし

## <a name="output-parameters"></a>出力パラメーター


なし

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーでは、 **Irp&gt;iostatus. status**を STATUS\_SUCCESS に設定する必要があります。

<a name="operation"></a>操作
---------

この IRP は、デバイススタックの一番上にあるドライバーによって最初に処理され、スタック内の下位の各ドライバーに渡されます。

この IRP に応答して、Windows 2000 以降のドライバーは、デバイスを停止し、i/o ポートや割り込みなど、デバイスによって使用されているハードウェアリソースを解放します。

Windows 2000 以降では、stop IRP は、デバイスのハードウェアリソースを解放して再構成できるようにするためだけに使用されます。 リソースが再構成されると、デバイスが再起動されます。 Stop IRP は、remove IRP の前段階ではありません。 PnP Irp がデバイスに送信される順序の詳細については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。

Windows 98/Me では、stop IRP は、開始に失敗した場合と、デバイスが無効になっている場合にも使用されます。 これらのオペレーティングシステムで実行されている WDM ドライバーは、デバイスを停止し、入力 i/o を失敗させ、ユーザーモードインターフェイスを無効にして登録解除する必要があります。

ドライバーは、この IRP を失敗させることはできません。 ドライバーがデバイスのハードウェアリソースを解放できない場合は、前のクエリ停止 IRP を失敗させる必要があります。

停止 Irp の処理の詳細については[、「デバイスの停止](https://docs.microsoft.com/windows-hardware/drivers/kernel/stopping-a-device)」を参照してください。

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


[**IRP\_\_クエリ\_\_デバイスの停止**](irp-mn-query-stop-device.md)

[ **\_デバイスを起動\_IRP\_** ](irp-mn-start-device.md)

[**IoSetDeviceInterfaceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacestate)

[**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)

 

 




