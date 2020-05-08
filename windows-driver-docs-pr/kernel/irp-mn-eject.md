---
title: IRP_MN_EJECT
description: 通常、バスドライバーは、デバイスの取り出しをサポートする子デバイス (子 PDOs) に対してこの要求を処理します。 関数ドライバーとフィルタードライバーは、この要求を受信しません。
ms.date: 08/12/2017
ms.assetid: 2807eeca-c614-469a-baeb-3d2d65416c57
keywords:
- IRP_MN_EJECT カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: f3d983bfe7094e6ccf952b7aec592a23cff3fa1a
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922468"
---
# <a name="irp_mn_eject"></a>IRP\_の\_全取り出し


通常、バスドライバーは、デバイスの取り出しをサポートする子デバイス (子 PDOs) に対してこの要求を処理します。 関数ドライバーとフィルタードライバーは、この要求を受信しません。

## <a name="value"></a>値

0x11

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>送信時
---------

PnP マネージャーは、この IRP を送信して適切なドライバーをダイレクトし、スロットからデバイスを取り出します。

PnP マネージャーは、任意のスレッドコンテキストで\_この IRP を IRQL パッシブレベルで送信します。

## <a name="input-parameters"></a>入力パラメーター


None

## <a name="output-parameters"></a>出力パラメーター


None

## <a name="io-status-block"></a>I/O ステータス ブロック


バスドライバーは、 **Irp-&gt;iostatus**を、状態\_が SUCCESS または適切なエラー状態に設定します。

成功した場合、バスドライバーは**Irp&gt;-Iostatus. 情報**をゼロに設定します。

バスドライバーがこの IRP を処理しない場合は、 **irp-&gt;iostatus**をそのままにして、irp を完了します。

<a name="operation"></a>Operation
---------

デバイスを取り出すには、デバイスが D3 デバイスの電源状態 (オフ) になっている必要があります。また、デバイスがロックをサポートしている場合は、ロックを解除する必要があります。

この IRP の成功を返すドライバーは、IRP を完了する前にデバイスが取り出されるまで待機する必要があります。

[プラグアンドプレイの小さな irp](plug-and-play-minor-irps.md)を処理するための一般的な規則については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。

**この IRP を送信しています**

システムで使用するために予約されています。 ドライバーは、この IRP を送信することはできません。

代わりに、 [**IoRequestDeviceEject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iorequestdeviceeject)ルーチンのリファレンスページを参照してください。

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


[**IoRequestDeviceEject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iorequestdeviceeject)

 

 




