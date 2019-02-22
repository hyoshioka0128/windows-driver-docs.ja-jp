---
title: IRP_MN_QUERY_PNP_DEVICE_STATE
description: 関数、フィルター、およびバス ドライバーには、この要求を処理できます。
ms.date: 08/12/2017
ms.assetid: 24362a20-9e9d-4566-bc95-ce52b91056af
keywords:
- IRP_MN_QUERY_PNP_DEVICE_STATE カーネル モード ドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 945a7056bc30bc9455a569dcd586044c0ad19443
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531116"
---
# <a name="irpmnquerypnpdevicestate"></a>IRP\_MN\_クエリ\_PNP\_デバイス\_状態


関数、フィルター、およびバス ドライバーには、この要求を処理できます。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP** ](irp-mj-pnp.md)送信されるときに
---------

PnP マネージャーは、デバイスのドライバーからの成功の return の後にこの IRP を送信、 [ **IRP\_MN\_開始\_デバイス**](irp-mn-start-device.md)デバイスが最初に送信された要求開始します。 この IRP は、開始時の負荷を分散リソースの停止後に送信されません。 PnP マネージャーでは、この IRP の呼び出しにデバイス ドライバーの場合にも送信します[ **IoInvalidateDeviceState**](https://msdn.microsoft.com/library/windows/hardware/ff549361)します。

PnP マネージャーでは、この IRP を送信 IRQL パッシブで\_任意のスレッドのコンテキストでレベル。

## <a name="input-parameters"></a>入力パラメーター


なし

## <a name="output-parameters"></a>出力パラメーター


状態の I/O ブロックで返されます。

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーの設定**Irp -&gt;IoStatus.Status**ステータス\_成功や状態などの適切なエラー状態に\_失敗しました。

成功した場合、ドライバーの設定**Irp -&gt;IoStatus.Information**を[ **PNP\_デバイス\_状態**](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-an-irp-mn-surprise-removal-request#about-pnpdevicestate)ビットマスク。


呼び出す関数またはフィルター ドライバーがこの IRP を処理しない場合[ **IoSkipCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff550355)、設定されていない、 [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)ルーチンと次のドライバーに IRP のパス。 このようなドライバーを変更する必要がありますいない**Irp -&gt;IoStatus** IRP を完了する必要があります。

バス ドライバーがこの IRP を処理しない場合の外に出て**Irp -&gt;IoStatus.Status** IRP の完了であり。

<a name="operation"></a>操作
---------

デバイス スタックの上部にある、ドライバー、続いて各 [次へ] の下位のドライバー スタックでこの IRP が最初に処理されます。

ドライバーは、PnP デバイスの状態に関する情報がある場合、この IRP を処理します。 ドライバーを設定したり、PNP でフラグをクリア\_デバイス\_状態のビットマスク。 別のドライバー、PNP を設定した場合\_デバイス\_で状態**Irp -&gt;IoStatus.Information**、構造全体を上書きするのではなく、そのビットマスク内のフラグを変更するドライバーを処理する必要があります。

参照してください[プラグ アンド プレイ](https://msdn.microsoft.com/library/windows/hardware/ff547125)処理のための一般的な規則[プラグ アンド プレイ マイナー Irp](plug-and-play-minor-irps.md)します。

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


[**IoInvalidateDeviceState**](https://msdn.microsoft.com/library/windows/hardware/ff549361)

[**PNP\_デバイス\_状態**](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-an-irp-mn-surprise-removal-request#about-pnpdevicestate)
