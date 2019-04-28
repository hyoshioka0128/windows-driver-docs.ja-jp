---
title: KSCATEGORY_BDA_NETWORK_TUNER
description: KSCATEGORY_BDA_NETWORK_TUNER
ms.assetid: d3f9d393-c8a1-4280-8796-a1de755f9508
keywords:
- KSCATEGORY_BDA_NETWORK_TUNER デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_BDA_NETWORK_TUNER
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 45ce647f797c85d59c883e262cba75015bf38260
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377335"
---
# <a name="kscategorybdanetworktuner"></a>KSCATEGORY_BDA_NETWORK_TUNER


KSCATEGORY_BDA_NETWORK_TUNER[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)が定義されている、[カーネル ストリーミング](https://msdn.microsoft.com/library/windows/hardware/ff568277)でネットワーク チューナー (KS) 機能のカテゴリ、[ブロードキャストのドライバーのアーキテクチャ](https://msdn.microsoft.com/library/windows/hardware/ff556573) (性 BDA)。

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
<td align="left"><p>KSCATEGORY_BDA_NETWORK_TUNER</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{71985F48-1CA1-11d3-9CC8-00C04F7971E0}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

BDA デバイス用のドライバーでは、オペレーティング システムに、デバイスが BDA ネットワーク チューナー フィルターをサポートすることを示す KSCATEGORY_BDA_NETWORK_TUNER のインスタンスを登録します。

INF ファイルでこの機能のカテゴリを登録する方法の例は、INF ファイルを参照してください。 *BDASwTunerATSC.inf*します。 *BDASwTunerATSC.inf*で BDA サンプルの汎用的なチューナーに含まれている、 *src\\swtuner\\BDAtuner\\gentuner* WDK のサブディレクトリ。

ネットワークのチューナー フィルター KS 機能のカテゴリの詳細については、次を参照してください。[一般的なコントロールのノードとフィルター](https://msdn.microsoft.com/library/windows/hardware/ff557718)と[BDA フィルター カテゴリ Guid](https://msdn.microsoft.com/library/windows/hardware/ff556521)します。

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
<td align="left"><p>Windows XP、DirectX 9.0 a がインストールされている、Windows 2000 以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Bdamedia.h (Bdamedia.h を含む)</td>
</tr>
</tbody>
</table>

 

 





