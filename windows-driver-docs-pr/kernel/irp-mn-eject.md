---
title: IRP_MN_EJECT
description: 通常、バスドライバーは、デバイスの取り出しをサポートする子デバイス (子 PDOs) に対してこの要求を処理します。 関数ドライバーとフィルタードライバーは、この要求を受信しません。
ms.date: 08/12/2017
ms.assetid: 2807eeca-c614-469a-baeb-3d2d65416c57
keywords:
- IRP_MN_EJECT カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: d5848375fc53b681ca5633d1ba8c16d5ee03ae2d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838585"
---
# <a name="irp_mn_eject"></a>IRP\_\_排出


通常、バスドライバーは、デバイスの取り出しをサポートする子デバイス (子 PDOs) に対してこの要求を処理します。 関数ドライバーとフィルタードライバーは、この要求を受信しません。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)送信時
---------

PnP マネージャーは、この IRP を送信して適切なドライバーをダイレクトし、スロットからデバイスを取り出します。

PnP マネージャーは、任意のスレッドコンテキストでこの IRP を IRQL パッシブ\_レベルで送信します。

## <a name="input-parameters"></a>入力パラメーター


なし

## <a name="output-parameters"></a>出力パラメーター


なし

## <a name="io-status-block"></a>I/O ステータス ブロック


バスドライバーは、 **Irp&gt;iostatus. status**を STATUS\_SUCCESS または適切なエラー状態に設定します。

成功した場合、バスドライバーは**Irp&gt;IoStatus. 情報**をゼロに設定します。

バスドライバーがこの IRP を処理しない場合は、 **irp&gt;iostatus**がそのままの状態になり、irp が完了します。

<a name="operation"></a>操作
---------

デバイスを取り出すには、デバイスが D3 デバイスの電源状態 (オフ) になっている必要があります。また、デバイスがロックをサポートしている場合は、ロックを解除する必要があります。

この IRP の成功を返すドライバーは、IRP を完了する前にデバイスが取り出されるまで待機する必要があります。

[プラグアンドプレイの小さな irp](plug-and-play-minor-irps.md)を処理するための一般的な規則については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。

**この IRP を送信しています**

システム用に予約されています。 ドライバーは、この IRP を送信することはできません。

代わりに、 [**IoRequestDeviceEject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iorequestdeviceeject)ルーチンのリファレンスページを参照してください。

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


[**IoRequestDeviceEject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iorequestdeviceeject)

 

 




