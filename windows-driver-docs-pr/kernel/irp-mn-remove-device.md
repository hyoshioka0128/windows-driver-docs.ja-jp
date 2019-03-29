---
title: IRP_MN_REMOVE_DEVICE
description: すべての PnP ドライバーでは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 0d733cbd-2da8-48a5-afc6-e1e6b8f507a1
keywords:
- IRP_MN_REMOVE_DEVICE カーネル モード ドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 54a269203a867f81b2c65eb2e57b330d3a47732a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569761"
---
# <a name="irpmnremovedevice"></a>IRP\_MN\_削除\_デバイス


すべての PnP ドライバーでは、この IRP を処理する必要があります。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP** ](irp-mj-pnp.md)送信されるときに
---------

PnP マネージャーでは、この IRP を使用して、デバイスのソフトウェアの表現 (デバイス オブジェクト、およびなど) を削除するドライバーに指示します。 驚いたことに (ユーザーは、以前の警告なしには、そのスロットから、デバイスを取得) でデバイスが (たとえば、取り外しますプログラム内のユーザーによって開始された)、通常の方法で削除されたときに、または dri を更新するユーザーが要求したときに、PnP マネージャーがこの IRP を送信しますver(s) します。

Windows 2000 およびそれ以降のシステムで、PnP マネージャーも送信この IRP デバイス スタック内のドライバーのいずれかが失敗した場合、 [ **IRP\_MN\_開始\_デバイス**](irp-mn-start-device.md)要求デバイス

PnP マネージャーに送信、正常なデバイスの削除、 [ **IRP\_MN\_クエリ\_削除\_デバイス**](irp-mn-query-remove-device.md) IRP 削除する前にします。 この場合、削除 IRP が到着すると、デバイスは削除保留中の状態は。 突然デバイス削除 Microsoft Windows 2000 またはそれ以降、PnP マネージャー送信、 [ **IRP\_MN\_突然\_削除**](irp-mn-surprise-removal.md) IRP 削除する前にします。 この場合、削除 IRP が到着すると、デバイスは突然削除状態には。 デバイスを開始する前に、ドライバーは IRP の削除 も受信できます。 この場合、IRP が到着すると、デバイスは、開始されていない状態では。

PnP マネージャーでは、この IRP を送信 IRQL パッシブで\_システム スレッドのコンテキスト内のレベル。

## <a name="input-parameters"></a>入力パラメーター


なし

## <a name="output-parameters"></a>出力パラメーター


なし

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーを設定する必要があります**Irp -&gt;IoStatus.Status**ステータス\_成功します。 ドライバーでは、この IRP が失敗する必要があります。

<a name="operation"></a>操作
---------

デバイス スタックの上部にある、ドライバー、続いて各下位のドライバー スタックでこの IRP が最初に処理されます。

この IRP に応答して、ドライバーは、デバイスの電源、デバイスのソフトウェアの表現 (デバイス オブジェクト、およびなど) を削除して、デバイスのすべてのリソースを解放などのタスクを実行します。

この IRP の処理の詳細については、次を参照してください。 [IRP の処理\_MN\_削除\_デバイス要求](https://msdn.microsoft.com/library/windows/hardware/ff546687)します。 デバイスの削除のサポートに関する概要については、次を参照してください。[デバイスを削除する](https://msdn.microsoft.com/library/windows/hardware/ff561046)します。

**この IRP を送信します。**

システムの使用に予約されています。 ドライバーは、この IRP を送信する必要があります。

バス ドライバーを呼び出す場合は、その子デバイス (子 Pdo) のいずれか (または複数) が物理的にコンピューターから削除されて、検出されると、バス ドライバー [ **IoInvalidateDeviceRelations** ](https://msdn.microsoft.com/library/windows/hardware/ff549353)への変更を報告する、PnP マネージャー。 PnP マネージャーし送信削除 Irp が消えているすべてのデバイスにします。

<a name="requirements"></a>必要条件
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


[**IoInvalidateDeviceRelations**](https://msdn.microsoft.com/library/windows/hardware/ff549353)

[**IoRegisterPlugPlayNotification**](https://msdn.microsoft.com/library/windows/hardware/ff549526)

[**IRP\_MN\_CANCEL\_REMOVE\_DEVICE**](irp-mn-cancel-remove-device.md)

[**IRP\_MN\_クエリ\_削除\_デバイス**](irp-mn-query-remove-device.md)

[**IRP\_MN\_SURPRISE\_REMOVAL**](irp-mn-surprise-removal.md)

 

 




