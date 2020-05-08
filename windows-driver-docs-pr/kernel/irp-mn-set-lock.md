---
title: IRP_MN_SET_LOCK
description: バスドライバーは、デバイスのロックをサポートする子デバイス (子 PDOs) に対して、この IRP を処理する必要があります。 関数ドライバーとフィルタードライバーは、この要求を処理しません。
ms.date: 08/12/2017
ms.assetid: d4e09527-f817-4eb5-b0f5-7584de8888b1
keywords:
- IRP_MN_SET_LOCK カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 0f9a31f2e4dcc0245e5b4877e71fb7f89337a95c
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922555"
---
# <a name="irp_mn_set_lock"></a>IRP\_の\_全\_セットのロック


バスドライバーは、デバイスのロックをサポートする子デバイス (子 PDOs) に対して、この IRP を処理する必要があります。 関数ドライバーとフィルタードライバーは、この要求を処理しません。

## <a name="value"></a>値

0x12

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>送信時
---------

PnP マネージャーはこの IRP を送信して、デバイスをロックし、デバイスの取り出しを防止したり、デバイスのロックを解除したりします。

PnP マネージャーは、任意のスレッドコンテキストで\_この IRP を IRQL パッシブレベルで送信します。

## <a name="input-parameters"></a>入力パラメーター


" [**IO\_\_スタックの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)" 構造のパラメーターである**setlock. lock**メンバーは、デバイスをロックする (TRUE) かロック解除する (FALSE) かを指定するブール値です。

## <a name="output-parameters"></a>出力パラメーター


None

## <a name="io-status-block"></a>I/O ステータス ブロック


バスドライバーは、 **Irp-&gt;iostatus**を、状態\_が SUCCESS または適切なエラー状態に設定します。

成功した場合、ドライバーは**Irp&gt;-Iostatus. 情報**をゼロに設定します。

バスドライバーがこの IRP を処理しない場合は、 **irp-&gt;iostatus**をそのままにして、irp を完了します。

関数ドライバーとフィルタードライバーは、この IRP を処理しません。 このようなドライバーでは、 [**Ioskipの場所**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を呼び出し、IRP を次のドライバーに渡します。 関数ドライバーとフィルタードライバーは[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定せず、 **irp&gt;** を変更しないようにします。 irp を完了することはできません。

<a name="operation"></a>Operation
---------

ドライバーがこの IRP の成功を返した場合、IRP を完了する前に、デバイスがロックまたはロック解除されていることを確認します。

[プラグアンドプレイの小さな irp](plug-and-play-minor-irps.md)を処理するための一般的な規則については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。

**この IRP を送信しています**

システムで使用するために予約されています。 ドライバーは、この IRP を送信することはできません。

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

 

 




