---
title: GUID_DEVINTERFACE_OPM
description: GUID_DEVINTERFACE_OPM
ms.assetid: bd999b09-d531-4b89-a306-83e1ca7cac64
keywords:
- GUID_DEVINTERFACE_OPM デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_OPM
api_location:
- Dispmprt.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 554943cb78fa3690d74e5dae11538f048dc42210
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363708"
---
# <a name="guiddevinterfaceopm"></a>GUID_DEVINTERFACE_OPM


GUID_DEVINTERFACE_OPM[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)のコンテキストで動作するディスプレイ アダプター ドライバーが定義されている、 [Windows Vista のディスプレイ ドライバー モデル](https://msdn.microsoft.com/library/windows/hardware/ff570593)出力の保護をサポート管理 (OPM) 子デバイスを監視します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">属性</th>
<th align="left">設定</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>識別子</p></td>
<td align="left"><p>GUID_DEVINTERFACE_OPM</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{BF4672DE-6B4E-4BE4-A325-68A91EA49C09}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

ドライバーは、オペレーティング システムと OPM デバイス インターフェイスの存在をアプリケーションに通知するこのデバイスのインターフェイス クラスのインスタンスを登録します。

ディスプレイのミニポート ドライバーがこの直接呼出し OPM インターフェイスをサポートするかどうかは[デバイス セットアップ クラス](https://msdn.microsoft.com/library/windows/hardware/ff541509)、カーネル モード コンポーネントを呼び出して、ミニポート ドライバーの直接呼び出しインターフェイスを取得できます[ **DxgkDdiQueryInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff559764)関数とインターフェイスの種類を指定する GUID_DEVINTERFACE_OPM を指定します。

OPM については、次を参照してください。[出力 Protection Manager をサポートしている](https://msdn.microsoft.com/library/windows/hardware/ff569879)します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows Vista および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Dispmprt.h (Dispmprt.h を含む)</td>
</tr>
</tbody>
</table>

 

 





