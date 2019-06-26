---
title: IRP_MN_SET_LOCK
description: バス ドライバーには、その子デバイス (子 Pdo) デバイスのロックをサポートするには、この IRP を処理する必要があります。 関数とフィルター ドライバーでは、この要求は処理しません。
ms.date: 08/12/2017
ms.assetid: d4e09527-f817-4eb5-b0f5-7584de8888b1
keywords:
- IRP_MN_SET_LOCK カーネル モード ドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: c100b8c427067239d3b390fea035681cf8de6fb7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371852"
---
# <a name="irpmnsetlock"></a>IRP\_MN\_SET\_LOCK


バス ドライバーには、その子デバイス (子 Pdo) デバイスのロックをサポートするには、この IRP を処理する必要があります。 関数とフィルター ドライバーでは、この要求は処理しません。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP** ](irp-mj-pnp.md)送信されるときに
---------

PnP マネージャーでは、デバイスがロックされ、デバイスに直接ドライバーには、この IRP を取り出すと、送信しますまたは、デバイスのロックを解除します。

PnP マネージャーでは、この IRP を送信 IRQL パッシブで\_任意のスレッド コンテキストでします。

## <a name="input-parameters"></a>入力パラメーター


**Parameters.SetLock.Lock**のメンバー、 [ **IO\_スタック\_場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)構造体をロックするかどうかを指定するブール値 (TRUE は、) または (FALSE)、デバイスをロック解除します。

## <a name="output-parameters"></a>出力パラメーター


なし

## <a name="io-status-block"></a>I/O ステータス ブロック


バス ドライバーの設定**Irp -&gt;IoStatus.Status**ステータス\_成功または適切なエラーの状態にします。

成功した場合、ドライバーの設定**Irp -&gt;IoStatus.Information**をゼロにします。

バス ドライバーがこの IRP を処理しない場合の外に出て**Irp -&gt;IoStatus.Status** IRP の完了であり。

関数とフィルター ドライバーでは、この IRP は処理されません。 このようなドライバー呼び出し[ **IoSkipCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)し、[次へ] のドライバーに IRP を渡します。 関数とフィルター ドライバーを設定しないでください、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)ルーチンを変更しないでください**Irp -&gt;IoStatus**IRP を完了する必要があります。

<a name="operation"></a>操作
---------

ドライバーでは、この IRP の成功が返された場合、デバイスがロックされているまたは IRP を完了する前にロックが解除されたことになります。

参照してください[プラグ アンド プレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)処理のための一般的な規則[プラグ アンド プレイ マイナー Irp](plug-and-play-minor-irps.md)します。

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

 

 




