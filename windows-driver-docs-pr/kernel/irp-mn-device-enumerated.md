---
title: IRP_MN_DEVICE_ENUMERATED
description: PnP マネージャーは、この i/o 要求パケット (IRP) を使用して、デバイスオブジェクトが存在することと、プラグアンドプレイマネージャーによって完全に列挙されたことをバスドライバーに通知します。
ms.date: 08/12/2017
ms.assetid: 50ECF6E1-4FC6-4EEA-BACF-EBAD0329DA2E
keywords:
- IRP_MN_DEVICE_ENUMERATED カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 51de059536e25608d0c2b3746ab04ba56d27492f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828072"
---
# <a name="irp_mn_device_enumerated"></a>IRP\_\_デバイス\_列挙されています


PnP マネージャーは、この i/o 要求パケット (IRP) を使用して、デバイスオブジェクトが存在することと、プラグアンドプレイマネージャーによって完全に列挙されたことをバスドライバーに通知します。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)送信時
---------

PnP マネージャーは、GUID\_デバイス\_列挙された状態でユーザーモードに通知する直前に、この IRP を送信します。 この IRP を使用すると、ドライバーは、追加のデバイスプロパティの入力など、列挙された IRP\_\_デバイス\_の前処理ルーチンを提供できます。 この IRP は、主に[**Iosetdevicepropertydata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdevicepropertydata)を使用して、ドライバーが物理デバイスオブジェクト (PDO) のデバイスプロパティを設定できるようにします。

## <a name="input-parameters"></a>入力パラメーター


なし

## <a name="output-parameters"></a>出力パラメーター


なし

## <a name="io-status-block"></a>I/O ステータス ブロック


この IRP を処理するドライバーは、 [irp&gt;iostatus](https://docs.microsoft.com/windows-hardware/drivers/kernel/i-o-status-blocks)を、STATUS\_SUCCESS または適切なエラー状態に設定します。

<a name="operation"></a>操作
---------

**Irp\_\_デバイス\_列挙**型の irp をバスドライバーの pdo に送信して、バスドライバーの pdo が存在することを示します。

## <a name="sending-the-irp"></a>IRP の送信


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
<td><p>バージョン</p></td>
<td><p>Windows 7 以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wdm</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[プラグアンドプレイの小さな Irp](plug-and-play-minor-irps.md)

 

 




