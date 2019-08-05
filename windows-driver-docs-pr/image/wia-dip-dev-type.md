---
title: WIA\_DIP\_DEV\_型
description: WIA\_DIP\_DEV\_型のプロパティには、デバイスの種類とデバイスのサブタイプが含まれています。
ms.assetid: 685c1cfa-cc3b-42e6-aef3-359ae7220715
keywords:
- WIA_DIP_DEV_TYPE イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DIP_DEV_TYPE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1fdd7876517039b0b13dde957e36c4f5aa0c6427
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375362"
---
# <a name="wia_dip_dev_type"></a>WIA\_DIP\_DEV\_型


WIA\_DIP\_DEV\_型のプロパティには、デバイスの種類とデバイスのサブタイプが含まれています。 WIA サービスを作成してこのプロパティの保持

## <span id="ddk_wia_dip_dev_type_si"></span><span id="DDK_WIA_DIP_DEV_TYPE_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

デバイスの種類とサブタイプは、デバイスのファイル、ドライバーの INF ファイルから取得されます。 アプリケーションの読み取り、WIA\_DIP\_DEV\_スキャナー、カメラ、またはビデオ デバイスを使用しているかどうかが決定する型のプロパティ。

次の表では、デバイスの種類の有効な値について説明します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>デバイスの種類</th>
<th>Value</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>StiDeviceTypeDefault</strong></p></td>
<td><p>0x0000</p></td>
<td><p>既定のデバイス</p></td>
</tr>
<tr class="even">
<td><p><strong>StiDeviceTypeScanner</strong></p></td>
<td><p>0x0001</p></td>
<td><p>スキャナーのデバイス</p></td>
</tr>
<tr class="odd">
<td><p><strong>StiDeviceTypeDigitalCamera</strong></p></td>
<td><p>0x0002</p></td>
<td><p>デバイスのカメラ</p></td>
</tr>
<tr class="even">
<td><p><strong>StiDeviceTypeStreamingVideo</strong></p></td>
<td><p>0x0003</p></td>
<td><p>ビデオ デバイス</p></td>
</tr>
</tbody>
</table>

 

INF ファイルの詳細については、次を参照してください。 [WIA デバイスの INF ファイル](https://docs.microsoft.com/windows-hardware/drivers/image/inf-files-for-wia-devices)します。 **StiDeviceType * * * Xxx*定数で定義されて*Sti.h*します。

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
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

 

 





