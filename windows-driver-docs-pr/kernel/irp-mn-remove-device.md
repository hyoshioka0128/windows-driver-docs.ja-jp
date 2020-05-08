---
title: IRP_MN_REMOVE_DEVICE
description: すべての PnP ドライバーは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 0d733cbd-2da8-48a5-afc6-e1e6b8f507a1
keywords:
- IRP_MN_REMOVE_DEVICE カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 158226ca3f23da1322446d57bc765424df447daf
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922559"
---
# <a name="irp_mn_remove_device"></a>IRP\_の\_すべて\_のデバイスの削除


すべての PnP ドライバーは、この IRP を処理する必要があります。

## <a name="value"></a>値

0x02

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>送信時
---------

PnP マネージャーは、この IRP を使用して、デバイスのソフトウェア表現 (デバイスオブジェクトなど) を削除するドライバーに指示します。 PnP マネージャーは、デバイスが適切な方法で削除されたとき (たとえば、デバイスを取り外しまたは取り出しているプログラムのユーザーによって開始された場合)、突然 (ユーザーが前の警告なしでデバイスをスロットからプルした場合)、またはユーザーがドライバーの更新を要求したときに、この IRP を送信します。

Windows 2000 以降のシステムでは、デバイススタック内のいずれかのドライバーがデバイスに対する[**\_irp\_の\_開始デバイス**](irp-mn-start-device.md)の要求に失敗した場合にも、PnP マネージャーによってこの irp が送信されます。

デバイスの削除が正常に行われると、PnP マネージャーは、削除 IRP の前に[**デバイスを\_削除\_\_\_する irp**](irp-mn-query-remove-device.md)を実行するクエリを送信します。 この場合、remove IRP が到着すると、デバイスは削除保留中の状態になります。 Microsoft Windows 2000 以降で驚くほどデバイスが削除される場合、PnP マネージャーは、削除の IRP の前に、 [**irp\_\_の\_突然の削除**](irp-mn-surprise-removal.md)を送信します。 この場合、remove IRP が到着すると、デバイスは突然削除された状態になります。 デバイスを起動する前に、ドライバーが remove IRP を受け取ることもできます。 この場合、IRP が到着すると、デバイスは開始されていない状態になります。

PnP マネージャーは、システムスレッドのコンテキストで\_この IRP を IRQL パッシブレベルで送信します。

## <a name="input-parameters"></a>入力パラメーター


None

## <a name="output-parameters"></a>出力パラメーター


None

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーでは、 **Irp-&gt;iostatus**を設定する必要\_があります。状態は SUCCESS に設定されます。 ドライバーは、この IRP を失敗させることはできません。

<a name="operation"></a>Operation
---------

この IRP は、デバイススタックの最上位にあるドライバーによって最初に処理され、その後、スタック内の下位の各ドライバーによって処理されます。

この IRP に応答して、ドライバーはデバイスの電源を切る、デバイスのソフトウェア表現 (デバイスオブジェクトなど) を削除し、デバイスのすべてのリソースを解放するなどのタスクを実行します。

この IRP の処理の詳細については、「 [\_irp\_の\_処理後のデバイスの削除要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-an-irp-mn-remove-device-request)」を参照してください。 デバイスの削除に関する一般的な情報については、「[デバイスの削除](https://docs.microsoft.com/windows-hardware/drivers/kernel/removing-a-device)」を参照してください。

**この IRP を送信しています**

システムで使用するために予約されています。 ドライバーは、この IRP を送信することはできません。

バスドライバーが、その子デバイス (子 Dos) の1つ (または複数) がコンピューターから物理的に削除されたことを検出した場合、バスドライバーは[**IoInvalidateDeviceRelations**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicerelations)を呼び出して、変更を PnP マネージャーに報告します。 PnP マネージャーは、使用されなくなったすべてのデバイスに対して削除 Irp を送信します。

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


[**IoInvalidateDeviceRelations**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicerelations)

[**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)

[**\_IRP\_を終了\_する\_デバイスの削除**](irp-mn-cancel-remove-device.md)

[**IRP\_を\_実行\_する\_クエリデバイスの削除**](irp-mn-query-remove-device.md)

[**IRP\_の\_突然\_の削除**](irp-mn-surprise-removal.md)

 

 




