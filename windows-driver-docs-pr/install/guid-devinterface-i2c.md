---
title: GUID_DEVINTERFACE_I2C
description: GUID_DEVINTERFACE_I2C
ms.assetid: 765cecb7-b8ea-48ef-bdab-742da722e169
keywords:
- GUID_DEVINTERFACE_I2C デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_I2C
api_location:
- Dispmprt.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f6ea7eed9fcb6e4f59d2ffe99926a18968f31345
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578746"
---
# <a name="guiddevinterfacei2c"></a>GUID_DEVINTERFACE_I2C


GUID_DEVINTERFACE_I2C[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)のコンテキストで動作するディスプレイ アダプター ドライバーが定義されている、 [Windows Vista のディスプレイ ドライバー モデル](https://msdn.microsoft.com/library/windows/hardware/ff570593)による I2C トランザクションの実行と子のデバイスを監視します。

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
<td align="left"><p>GUID_DEVINTERFACE_I2C</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{2564AA4F-DDDB-4495-B497-6AD4A84163D7}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

ドライバーは、オペレーティング システムや子デバイスを監視でトランザクションを実行する I2C インターフェイスの存在をアプリケーションに通知するこのデバイスのインターフェイス クラスのインスタンスを登録します。

ディスプレイのミニポート ドライバーがこの直接呼出し I2C インターフェイスをサポートするかどうかは[デバイス セットアップ クラス](https://msdn.microsoft.com/library/windows/hardware/ff541509)、カーネル モード コンポーネントを呼び出して、ミニポート ドライバーの直接呼び出しインターフェイスを取得できます[ **DxgkDdiQueryInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff559764)関数とインターフェイスの種類を指定する GUID_DEVINTERFACE_I2C を指定します。

I2C バスについては、次を参照してください。 [I2C バスとディスプレイ アダプターの子デバイス](https://msdn.microsoft.com/library/windows/hardware/ff567381)します。

<a name="requirements"></a>必要条件
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

 

 





