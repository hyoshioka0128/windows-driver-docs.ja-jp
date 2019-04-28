---
title: GUID_DEVINTERFACE_NET
description: GUID_DEVINTERFACE_NET
ms.assetid: e1cdda95-1915-4bbc-86e9-dff99b7fcc7b
keywords:
- GUID_DEVINTERFACE_NET デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_NET
api_location:
- Ndisguid.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5970f5a734e17a9b59c3a4db9b163b89aa71c68e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363744"
---
# <a name="guiddevinterfacenet"></a>GUID_DEVINTERFACE_NET


GUID_DEVINTERFACE_NET[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)が定義されている[ネットワーク デバイス](https://msdn.microsoft.com/library/windows/hardware/ff568356)します。

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
<td align="left"><p>GUID_DEVINTERFACE_NET</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{CAC88484-7515-4C03-82E6-71A87ABAC361}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

ネットワーク デバイスのドライバーでは、他のネットワーク コンポーネントやネットワーク デバイスの存在をアプリケーションに通知するこのデバイスのインターフェイス クラスのインスタンスを登録します。

NDIS は、NDIS ミニポート ドライバーの場合は、このインターフェイス クラスのインスタンスを登録します。

ネットワーク デバイスとドライバーについては、次を参照してください。[ネットワーク設計ガイド](https://msdn.microsoft.com/library/windows/hardware/ff568356)します。

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
<td align="left"><p>Windows Vista、Windows Server 2003 スケーラブルな Networking Pack (SNP)、および以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ndisguid.h (Ndisguid.h を含む)</td>
</tr>
</tbody>
</table>

 

 





