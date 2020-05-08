---
title: IRP_MN_DEVICE_ENUMERATED
description: PnP マネージャーは、この i/o 要求パケット (IRP) を使用して、デバイスオブジェクトが存在することと、プラグアンドプレイマネージャーによって完全に列挙されたことをバスドライバーに通知します。
ms.date: 08/12/2017
ms.assetid: 50ECF6E1-4FC6-4EEA-BACF-EBAD0329DA2E
keywords:
- IRP_MN_DEVICE_ENUMERATED カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 24a4ff2d7707eca98779563cffa791d7c71f06b2
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922577"
---
# <a name="irp_mn_device_enumerated"></a>IRP\_全\_デバイス\_列挙型


PnP マネージャーは、この i/o 要求パケット (IRP) を使用して、デバイスオブジェクトが存在することと、プラグアンドプレイマネージャーによって完全に列挙されたことをバスドライバーに通知します。

## <a name="value"></a>値

0x19

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>送信時
---------

PnP マネージャーは、GUID\_デバイス\_で列挙されたユーザーモードに通知する直前に、この IRP を送信します。 この IRP を使用すると、ドライバーは、追加\_の\_デバイス\_プロパティの入力など、irp がいっぱいになったデバイスの前処理ルーチンを提供できます。 この IRP は、主に[**Iosetdevicepropertydata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdevicepropertydata)を使用して、ドライバーが物理デバイスオブジェクト (PDO) のデバイスプロパティを設定できるようにします。

## <a name="input-parameters"></a>入力パラメーター


None

## <a name="output-parameters"></a>出力パラメーター


None

## <a name="io-status-block"></a>I/O ステータス ブロック


この IRP を処理するドライバーは、 [irp&gt;-iostatus を設定します。](https://docs.microsoft.com/windows-hardware/drivers/kernel/i-o-status-blocks)状態は\_SUCCESS または適切なエラー状態に設定されます。

<a name="operation"></a>Operation
---------

バスドライバー PDO が存在することを示すために、 **irp\_\_\_** の全列挙型の irp がバスドライバーの pdo に送信されます。

## <a name="sending-the-irp"></a>IRP の送信


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
<td><p>バージョン</p></td>
<td><p>Windows 7 以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td><p>ヘッダー</p></td>
<td>Wdm.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[プラグ アンド プレイのマイナー IRP](plug-and-play-minor-irps.md)

 

 




