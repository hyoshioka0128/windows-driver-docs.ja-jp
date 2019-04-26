---
title: EFI_USBFN_PORT_TYPE
description: EFI_USBFN_PORT_TYPE
ms.assetid: 2596dd4f-26bd-454b-9550-a89c7e1f790b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dea889b1b34bf22dcc97311dcb0693b54681e60f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337671"
---
# <a name="efiusbfnporttype"></a>EFI\_USBFN\_ポート\_型


この列挙体には、USB ポートの種類を指定します。

## <a name="syntax"></a>構文


```cpp
typedef enum _EFI_USBFN_PORT_TYPE 
{
    EfiUsbUnknownPort = 0,
    EfiUsbStandardDownstreamPort,
    EfiUsbChargingDownstreamPort,
    EfiUsbDedicatedChargingPort,
    EfiUsbInvalidDedicatedChargingPort
} EFI_USBFN_PORT_TYPE;
```

## <a name="constants"></a>定数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>値</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>EfiUsbUnknownPort</strong></p></td>
<td><p>不明なポート - ドライバー内部の既定のポートの種類。これは、ドライバー、成功状態コードでは返されません。</p></td>
</tr>
<tr class="even">
<td><p><strong>EfiUsbStandardDownstreamPort</strong></p></td>
<td><p>標準のダウン ストリームのポート - 標準の USB host.for 詳細についてを参照してください<strong>解説</strong>します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EfiUsbChargingDownstreamPort</strong></p></td>
<td><p>標準の USB ホスト - ダウン ストリームのポートを課金します。 詳細については、次を参照してください<strong>解説。</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>EfiUsbDedicatedChargingPort</strong></p></td>
<td><p>専用の充電中ポート – 壁充電器、USB ホストではありません。 詳細については、次を参照してください<strong>解説。</strong></p></td>
</tr>
<tr class="odd">
<td><p><strong>EfiUsbInvalidDedicatedChargingPort</strong></p></td>
<td><p>無効な専用充電中ポート – USB ホストまたは専用ポートを課金されません。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>注釈


「バッテリの充電リビジョン 1.1 の仕様」を参照、 [USB.org](https://go.microsoft.com/fwlink/p/?linkid=64124) web サイト。

## <a name="requirements"></a>要件


**ヘッダー:** ユーザーが生成しました。

 

 




