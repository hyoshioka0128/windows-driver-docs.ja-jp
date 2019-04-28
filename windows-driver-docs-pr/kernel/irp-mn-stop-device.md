---
title: IRP_MN_STOP_DEVICE
description: すべての PnP ドライバーでは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: a5c81db0-e753-4d91-97e4-c58ea05f5ce8
keywords:
- IRP_MN_STOP_DEVICE カーネル モード ドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: d51e1856e9bb4b97d93a56cb59cba07c3fe58577
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381403"
---
# <a name="irpmnstopdevice"></a>IRP\_MN\_停止\_デバイス


すべての PnP ドライバーでは、この IRP を処理する必要があります。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP** ](irp-mj-pnp.md)送信されるときに
---------

PnP マネージャーでは、デバイスのハードウェア リソースを再構成できるようにデバイスを停止するには、この IRP を送信します。

Windows 2000 およびそれ以降のシステムで、PnP マネージャー送信場合にのみ、この IRP 前[ **IRP\_MN\_クエリ\_停止\_デバイス**](irp-mn-query-stop-device.md)完了正常にします。

Windows 98/、PnP マネージャーも送信この IRP 無効になり、デバイス スタックが失敗した場合、デバイスがされているときに、 **IRP\_MN\_開始\_デバイス**要求。 PnP マネージャー失敗した開始の場合は、最初に指定しないでこの IRP を送信します[ **IRP\_MN\_クエリ\_停止\_デバイス**](irp-mn-query-stop-device.md)要求。

PnP マネージャーでは、この IRP を送信 IRQL パッシブで\_システム スレッドのコンテキスト内のレベル。

## <a name="input-parameters"></a>入力パラメーター


なし

## <a name="output-parameters"></a>出力パラメーター


なし

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーを設定する必要があります**Irp -&gt;IoStatus.Status**ステータス\_成功します。

<a name="operation"></a>操作
---------

この IRP では、デバイス スタックの上部にあるドライバーによって最初に処理され、各スタックの下位のドライバーに渡されます。

この IRP、Windows 2000 以降のドライバーを応答では、デバイスを停止し、I/O ポートと割り込みなど、デバイスで使用されている、ハードウェア リソースを解放します。

Windows 2000 以降、stop IRP を再構成するために、デバイスのハードウェア リソースを解放するためだけに使用されます。 リソースの再構成後、デバイスが再起動します。 停止 IRP は削除 IRP の前身ではありません。 参照してください[プラグ アンド プレイ](https://msdn.microsoft.com/library/windows/hardware/ff547125)どの PnP Irp の順序の詳細についてはデバイスに送信されます。

Windows 98 で/Me 停止 IRP のデバイスを無効にされていると失敗した開始後にも使用します。 これらのオペレーティング システム上で実行される WDM ドライバーは、デバイスを停止、任意の受信の I/O は失敗を無効にしておよび他のユーザー モード インターフェイスを登録解除する必要があります。

ドライバーでは、この IRP が失敗する必要があります。 ドライバーは、デバイスのハードウェア リソースを解放できない場合に、上記のクエリ停止 IRP が失敗する必要があります。

参照してください[デバイスを停止する](https://msdn.microsoft.com/library/windows/hardware/ff563868)処理の詳細については Irp を停止します。

**この IRP を送信します。**

システムの使用に予約されています。 ドライバーは、この IRP を送信する必要があります。

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
<td>Wdm.h (Wdm.h、Ntddk.h、Ntifs.h など)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**IRP\_MN\_クエリ\_停止\_デバイス**](irp-mn-query-stop-device.md)

[**IRP\_MN\_START\_DEVICE**](irp-mn-start-device.md)

[**IoSetDeviceInterfaceState**](https://msdn.microsoft.com/library/windows/hardware/ff549700)

[**IoRegisterDeviceInterface**](https://msdn.microsoft.com/library/windows/hardware/ff549506)

 

 




