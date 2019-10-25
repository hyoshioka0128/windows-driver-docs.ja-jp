---
title: IRP_MN_SET_LOCK
description: バスドライバーは、デバイスのロックをサポートする子デバイス (子 PDOs) に対して、この IRP を処理する必要があります。 関数ドライバーとフィルタードライバーは、この要求を処理しません。
ms.date: 08/12/2017
ms.assetid: d4e09527-f817-4eb5-b0f5-7584de8888b1
keywords:
- IRP_MN_SET_LOCK カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: fa948abd55a8531324ad30a2194100cf9e546a56
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827965"
---
# <a name="irp_mn_set_lock"></a>IRP\_\_設定\_ロック


バスドライバーは、デバイスのロックをサポートする子デバイス (子 PDOs) に対して、この IRP を処理する必要があります。 関数ドライバーとフィルタードライバーは、この要求を処理しません。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)送信時
---------

PnP マネージャーはこの IRP を送信して、デバイスをロックし、デバイスの取り出しを防止したり、デバイスのロックを解除したりします。

PnP マネージャーは、任意のスレッドコンテキストでこの IRP を IRQL パッシブ\_レベルで送信します。

## <a name="input-parameters"></a>入力パラメーター


[**IO\_STACK\_LOCATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)構造体の**Parameters. setlock. lock**メンバーは、デバイスをロックする (TRUE) かロック解除する (FALSE) かを指定するブール値です。

## <a name="output-parameters"></a>出力パラメーター


なし

## <a name="io-status-block"></a>I/O ステータス ブロック


バスドライバーは、 **Irp&gt;iostatus. status**を STATUS\_SUCCESS または適切なエラー状態に設定します。

成功した場合、ドライバーは**Irp&gt;IoStatus. 情報**をゼロに設定します。

バスドライバーがこの IRP を処理しない場合は、 **irp&gt;iostatus**がそのままの状態になり、irp が完了します。

関数ドライバーとフィルタードライバーは、この IRP を処理しません。 このようなドライバーでは、 [**Ioskipの場所**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を呼び出し、IRP を次のドライバーに渡します。 関数とフィルタードライバーは[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定しません。 **Irp&gt;iocompletion**を変更しないでください。 irp を完了できません。

<a name="operation"></a>操作
---------

ドライバーがこの IRP の成功を返した場合、IRP を完了する前に、デバイスがロックまたはロック解除されていることを確認します。

[プラグアンドプレイの小さな irp](plug-and-play-minor-irps.md)を処理するための一般的な規則については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。

**この IRP を送信しています**

システム用に予約されています。 ドライバーは、この IRP を送信することはできません。

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

 

 




