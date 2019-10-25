---
title: IRP_MN_REMOVE_DEVICE
description: すべての PnP ドライバーは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 0d733cbd-2da8-48a5-afc6-e1e6b8f507a1
keywords:
- IRP_MN_REMOVE_DEVICE カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: f8a1fb03be10843ba87d708bff87f524fa9de00e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838561"
---
# <a name="irp_mn_remove_device"></a>IRP\_\_\_デバイスの削除


すべての PnP ドライバーは、この IRP を処理する必要があります。

<a name="major-code"></a>主要なコード
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)送信時
---------

PnP マネージャーは、この IRP を使用して、デバイスのソフトウェア表現 (デバイスオブジェクトなど) を削除するドライバーに指示します。 PnP マネージャは、デバイスが適切な方法で削除されたとき (たとえば、取り外しまたは取り出しハードウェアプログラムのユーザーによって開始された)、驚き (ユーザーが前の警告なしでデバイスをスロットからプルした場合)、またはユーザーが dri を更新するように要求したときに、この IRP を送信します。ver (s)。

Windows 2000 以降のシステムでは、デバイススタック内のいずれかのドライバーで Irp\_が失敗した場合に、デバイスのデバイスに対する\_デバイスの要求を[**開始\_** ](irp-mn-start-device.md)と、この irp も送信されます。

デバイスの削除が正常に行われた場合、PnP マネージャーは、削除 IRP の前に[ **\_デバイスを削除\_、irp\_\_クエリ**](irp-mn-query-remove-device.md)を送信します。 この場合、remove IRP が到着すると、デバイスは削除保留中の状態になります。 Microsoft Windows 2000 以降で突然デバイスを削除した場合、PnP マネージャーは、削除 IRP の前に、予期しない[ **\_削除\_irp\_** ](irp-mn-surprise-removal.md)送信します。 この場合、remove IRP が到着すると、デバイスは突然削除された状態になります。 デバイスを起動する前に、ドライバーが remove IRP を受け取ることもできます。 この場合、IRP が到着すると、デバイスは開始されていない状態になります。

PnP マネージャーは、システムスレッドのコンテキストでこの IRP を IRQL パッシブ\_レベルで送信します。

## <a name="input-parameters"></a>入力パラメーター


なし

## <a name="output-parameters"></a>出力パラメーター


なし

## <a name="io-status-block"></a>I/o 状態ブロック


ドライバーでは、 **Irp&gt;iostatus. status**を STATUS\_SUCCESS に設定する必要があります。 ドライバーは、この IRP を失敗させることはできません。

<a name="operation"></a>操作
---------

この IRP は、デバイススタックの最上位にあるドライバーによって最初に処理され、その後、スタック内の下位の各ドライバーによって処理されます。

この IRP に応答して、ドライバーはデバイスの電源を切る、デバイスのソフトウェア表現 (デバイスオブジェクトなど) を削除し、デバイスのすべてのリソースを解放するなどのタスクを実行します。

この IRP の処理の詳細については、次を参照してください。 [irp\_を処理\_\_デバイスの要求を削除](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-an-irp-mn-remove-device-request)します。 デバイスの削除に関する一般的な情報については、「[デバイスの削除](https://docs.microsoft.com/windows-hardware/drivers/kernel/removing-a-device)」を参照してください。

**この IRP を送信しています**

システム用に予約されています。 ドライバーは、この IRP を送信することはできません。

バスドライバーが、その子デバイス (子 Dos) の1つ (または複数) がコンピューターから物理的に削除されたことを検出した場合、バスドライバーは[**IoInvalidateDeviceRelations**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicerelations)を呼び出して、変更を PnP マネージャーに報告します。 PnP マネージャーは、使用されなくなったすべてのデバイスに対して削除 Irp を送信します。

<a name="requirements"></a>前提条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>ヘッダー</p></td>
<td>Wdm (Wdm .h、Ntddk、または Ntifs を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**IoInvalidateDeviceRelations**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicerelations)

[**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)

[**IRP\_\_キャンセル\_\_デバイスの削除**](irp-mn-cancel-remove-device.md)

[**IRP\_\_クエリ\_\_デバイスの削除**](irp-mn-query-remove-device.md)

[**IRP\_\_驚く\_削除**](irp-mn-surprise-removal.md)

 

 




