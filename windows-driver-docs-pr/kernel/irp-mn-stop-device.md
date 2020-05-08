---
title: IRP_MN_STOP_DEVICE
description: すべての PnP ドライバーは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: a5c81db0-e753-4d91-97e4-c58ea05f5ce8
keywords:
- IRP_MN_STOP_DEVICE カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 34e33779bd4965696f599fdbacb1cb221ead4796
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922515"
---
# <a name="irp_mn_stop_device"></a>IRP\_の\_全\_停止デバイス


すべての PnP ドライバーは、この IRP を処理する必要があります。

## <a name="value"></a>値

0x04

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>送信時
---------

PnP マネージャーは、この IRP を送信してデバイスを停止し、デバイスのハードウェアリソースを再構成できるようにします。

Windows 2000 以降のシステムでは、この IRP は、前の[**\_irp の完全な\_クエリ\_\_**](irp-mn-query-stop-device.md)が正常に終了した場合にのみ、この irp を送信します。

Windows 98/Me では、デバイスが無効になっている場合や、デバイススタックが**irp\_\_\_** を使用した開始デバイスの要求に失敗した場合にも、PnP マネージャーがこの IRP を送信します。 開始に失敗した場合、この IRP は、前の[**irp\_を使用し\_た\_クエリ\_停止デバイス**](irp-mn-query-stop-device.md)要求なしでこの irp を送信します。

PnP マネージャーは、システムスレッドのコンテキストで\_この IRP を IRQL パッシブレベルで送信します。

## <a name="input-parameters"></a>入力パラメーター


None

## <a name="output-parameters"></a>出力パラメーター


None

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーでは、 **Irp-&gt;iostatus**を設定する必要\_があります。状態は SUCCESS に設定されます。

<a name="operation"></a>Operation
---------

この IRP は、デバイススタックの一番上にあるドライバーによって最初に処理され、スタック内の下位の各ドライバーに渡されます。

この IRP に応答して、Windows 2000 以降のドライバーは、デバイスを停止し、i/o ポートや割り込みなど、デバイスによって使用されているハードウェアリソースを解放します。

Windows 2000 以降では、stop IRP は、デバイスのハードウェアリソースを解放して再構成できるようにするためだけに使用されます。 リソースが再構成されると、デバイスが再起動されます。 Stop IRP は、remove IRP の前段階ではありません。 PnP Irp がデバイスに送信される順序の詳細については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。

Windows 98/Me では、stop IRP は、開始に失敗した場合と、デバイスが無効になっている場合にも使用されます。 これらのオペレーティングシステムで実行されている WDM ドライバーは、デバイスを停止し、入力 i/o を失敗させ、ユーザーモードインターフェイスを無効にして登録解除する必要があります。

ドライバーは、この IRP を失敗させることはできません。 ドライバーがデバイスのハードウェアリソースを解放できない場合は、前のクエリ停止 IRP を失敗させる必要があります。

停止 Irp の処理の詳細については[、「デバイスの停止](https://docs.microsoft.com/windows-hardware/drivers/kernel/stopping-a-device)」を参照してください。

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

[**IRP\_の\_全\_開始デバイス**](irp-mn-start-device.md)

[**IoSetDeviceInterfaceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacestate)

[**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)

 

 




