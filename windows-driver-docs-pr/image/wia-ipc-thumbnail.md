---
title: WIA\_IPC\_サムネイル
description: WIA\_IPC\_サムネイルのプロパティには、サムネイルのデータを 24 ビット/ピクセル ビットが含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: 748443a7-cc7f-4291-b987-21462af97c3c
keywords:
- WIA_IPC_THUMBNAIL イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPC_THUMBNAIL
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22e04d69180a1924b879a6ed87a0ba2958613274
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378396"
---
# <a name="wiaipcthumbnail"></a>WIA\_IPC\_サムネイル


WIA\_IPC\_サムネイルのプロパティには、サムネイルのデータを 24 ビット/ピクセル ビットが含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。

## <span id="ddk_wia_ipc_thumbnail_si"></span><span id="DDK_WIA_IPC_THUMBNAIL_SI"></span>


プロパティの種類:VT\_UI1 |VT\_ベクター

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

サムネイルのデータを WIA\_IPC\_サムネイルのプロパティには、する必要がありますが含まれています。 ビットマップの非圧縮データであり、32 ビットの境界にアラインされます。 アプリケーションがの値を読み取り、 [ **WIA\_IPC\_サムネイル\_幅**](wia-ipc-thumbnail-width.md)と[ **WIA\_IPC\_サムネイル\_高さ**](wia-ipc-thumbnail-height.md)プロパティ (これは、Microsoft Windows SDK ドキュメントで説明されている) BITMAPINFOHEADER 構造を作成します。 アプリケーションの WIA を読み取ることができるよう\_IPC\_サムネイル プロパティ (これは実際のサムネイル画像データを表します) と、このプロパティを使用して、新しく作成されたビットマップ サムネイル イメージを作成するには直接データを書き込みます。

WIA\_IPC\_サムネイルは、WIA ミニドライバーおよび Microsoft Windows XP、Windows Me、およびそれ以降のバージョンのオペレーティング システムで実行されているアプリケーションによって使用されます。

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
<td><p>Windows Vista 以降のオペレーティング システムで古いものであり使用できなくする必要があります。 ただし、アプリケーションやデバイス向けの Windows Server 2003、Windows XP、および Windows の以前のバージョンと互換性のこのプロパティが現在も Windows Vista で定義します。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WIA\_IPC\_サムネイル\_高さ**](wia-ipc-thumbnail-height.md)

[**WIA\_IPC\_サムネイル\_幅**](wia-ipc-thumbnail-width.md)

 

 






