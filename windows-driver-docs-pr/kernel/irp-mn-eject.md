---
title: IRP_MN_EJECT
description: バス ドライバーは、通常は、デバイスの取り出しをサポートする子デバイス (子 Pdo) は、この要求を処理します。 関数とフィルター ドライバーは、この要求を受信しません。
ms.date: 08/12/2017
ms.assetid: 2807eeca-c614-469a-baeb-3d2d65416c57
keywords:
- IRP_MN_EJECT カーネル モード ドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 6fc9f3343ef77b93ee63aff6a29d69ee099ef1ef
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383727"
---
# <a name="irpmneject"></a>IRP\_MN\_EJECT


バス ドライバーは、通常は、デバイスの取り出しをサポートする子デバイス (子 Pdo) は、この要求を処理します。 関数とフィルター ドライバーは、この要求を受信しません。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP** ](irp-mj-pnp.md)送信されるときに
---------

PnP マネージャーでは、適切なドライバーまたはそのスロットからデバイスを取り出すようドライバーに出力するためには、この IRP を送信します。

PnP マネージャーでは、この IRP を送信 IRQL パッシブで\_任意のスレッド コンテキストでします。

## <a name="input-parameters"></a>入力パラメーター


なし

## <a name="output-parameters"></a>出力パラメーター


なし

## <a name="io-status-block"></a>I/O ステータス ブロック


バス ドライバーの設定**Irp -&gt;IoStatus.Status**ステータス\_成功または適切なエラーの状態にします。

成功した場合、バス ドライバーの設定**Irp -&gt;IoStatus.Information**をゼロにします。

バス ドライバーがこの IRP を処理しない場合の外に出て**Irp -&gt;IoStatus.Status** IRP の完了であり。

<a name="operation"></a>操作
---------

取り出すには、デバイスのデバイスが (オフ)、D3 デバイスの電源状態である必要がありする必要がありますロックを解除する (この場合、デバイスのロックをサポートしています)。

この IRP の成功を返す任意のドライバーは IRP を完了する前に、デバイスが排出されまで待つ必要があります。

参照してください[プラグ アンド プレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)処理のための一般的な規則[プラグ アンド プレイ マイナー Irp](plug-and-play-minor-irps.md)します。

**この IRP を送信します。**

システムの使用に予約されています。 ドライバーは、この IRP を送信する必要があります。

代わりのリファレンス ページを参照してください、 [ **IoRequestDeviceEject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iorequestdeviceeject)ルーチン。

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


[**IoRequestDeviceEject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iorequestdeviceeject)

 

 




