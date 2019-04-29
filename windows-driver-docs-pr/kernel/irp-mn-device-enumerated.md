---
title: IRP_MN_DEVICE_ENUMERATED
description: PnP マネージャーでは、この I/O 要求パケット (IRP) を使用して、デバイス オブジェクトが存在して、プラグ アンド プレイ マネージャによって完全に列挙されていますが、バス ドライバーに通知します。
ms.date: 08/12/2017
ms.assetid: 50ECF6E1-4FC6-4EEA-BACF-EBAD0329DA2E
keywords:
- IRP_MN_DEVICE_ENUMERATED Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: 3bbc6f730d711860a950e02ca25a34044d260c15
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391977"
---
# <a name="irpmndeviceenumerated"></a>IRP\_MN\_デバイス\_列挙


PnP マネージャーでは、この I/O 要求パケット (IRP) を使用して、デバイス オブジェクトが存在して、プラグ アンド プレイ マネージャによって完全に列挙されていますが、バス ドライバーに通知します。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP** ](irp-mj-pnp.md)送信されるときに
---------

PnP マネージャーがユーザー モードには GUID で通知する前に、この IRP を送信\_デバイス\_列挙します。 IRP の前処理ルーチンを提供するドライバーにより、この IRP\_MN\_デバイス\_列挙など、追加のデバイス プロパティを入力します。 主に、この IRP により、ドライバーを使用して物理デバイス オブジェクト (PDO) のデバイスのプロパティを設定する[ **IoSetDevicePropertyData**](https://msdn.microsoft.com/library/windows/hardware/ff549704)します。

## <a name="input-parameters"></a>入力パラメーター


なし

## <a name="output-parameters"></a>出力パラメーター


なし

## <a name="io-status-block"></a>I/O ステータス ブロック


この IRP を処理するドライバーの設定[Irp -&gt;IoStatus.Status](https://msdn.microsoft.com/library/windows/hardware/ff551825)ステータス\_成功またはエラーを適切な状態です。

<a name="operation"></a>操作
---------

**IRP\_MN\_デバイス\_列挙**をバス ドライバーの PDO が存在することを示すために、バス ドライバーの PDO に IRP が送信されます。

## <a name="sending-the-irp"></a>IRP の送信


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
<td><p>バージョン</p></td>
<td><p>Windows 7 および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wdm.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[プラグ アンド プレイのマイナー Irp](plug-and-play-minor-irps.md)

 

 




