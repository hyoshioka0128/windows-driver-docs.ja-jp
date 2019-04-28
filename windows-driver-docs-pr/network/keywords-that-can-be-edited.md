---
title: 編集可能なキーワード
description: 編集可能なキーワード
ms.assetid: 88c3a285-941a-4c91-9e61-25c445d07344
keywords:
- インストール キーワード WDK ネットワー キング、編集
- インストールのキーワードの編集
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa0be1bd273a620d252be35c452fa946550b99f7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361049"
---
# <a name="keywords-that-can-be-edited"></a>編集可能なキーワード





NDIS 6.0 および以降のバージョンの NDIS ミニポート ドライバーのネットワーク デバイスの編集可能な標準化されたキーワードを提供します。 これらの標準的なキーワードは、ユーザー インターフェイスで編集可能な数値またはテキストの値に関連付けられます。

次の例では、編集可能なキーワードの INF ファイルの定義を示します。

```INF
HKR, Ndi\params\<SubkeyName>,ParamDesc, 0, "<ParamDesc>"
HKR, Ndi\params\<SubkeyName>,Type, 0, "int"
HKR, Ndi\params\<SubkeyName>,Default, 0, "<IHV defined>"
HKR, Ndi\params\<SubkeyName>,Optional, 0, "0"
HKR, Ndi\params\<SubkeyName>,Min, 0, "0"
HKR, Ndi\params\<SubkeyName>,Max, 0, "<IHV defined>"
```

編集可能な標準のキーワードは次のとおりです。

<a href="" id="---------jumbopacket"></a> \*JumboPacket  
サイズ、最大のバイト単位としてのジャンボ パケット (1514 バイトよりも大きいイーサネット フレーム) サポートされて、ハードウェアをサポートできます。 ジャンボ フレームでとも呼ばれます。 *\*JumboPacket*の値と最大値の範囲は IHV が定義されます。 一部のベンダーは、サポートされている値の列挙体を定義する他のユーザー定義の最小値と最大値、間の任意の値を許可します。 詳細については、IHV を確認してください。

<a href="" id="---------receivebuffers"></a> \*ReceiveBuffers  
ミニポート アダプターによって使用される記述子を受信する数。 ミニポート ドライバーが適切な任意の既定値を選択のパフォーマンス チューニングします。 値が小さすぎる場合は、ミニポート アダプターが過負荷の受信バッファーから実行可能性がありますに注意してください。 値が大きすぎる場合は、システム リソースが無駄になります。

<a href="" id="---------transmitbuffers"></a> \*TransmitBuffers  
ハードウェアをサポートできる送信バッファーのバイト単位のサイズ。 このサイズは、ハードウェアに依存して、データ バッファー、バッファーの記述子を含めることができます。 ハードウェア ベンダーは、それぞれの目的に適した任意の値を割り当てることができます。

<a href="" id="--------networkaddress"></a> networkAddress  
デバイスのネットワーク アドレス。 MAC アドレスの形式です。XX-XX-XX-XX-XX-XX します。 ハイフン (-) は省略可能です。

このトピックの最後にテーブルの列には、編集可能なキーワードは次の属性について説明します。

<a href="" id="subkeyname"></a>SubkeyName  
レジストリ内の INF ファイルに指定する必要があります、キーワードの名前が表示されます。

<a href="" id="paramdesc"></a>ParamDesc  
SubkeyName に関連付けられているテキスト。

<a href="" id="type"></a>型  
編集可能な値の型。 値を指定できますいずれかの数値 (**Int**) またはテキストを編集できます (**編集**)。

<a href="" id="default-value"></a>既定値  
整数またはテキストの既定値。 &lt;定義されている IHV&gt;値が特定の独立系ハードウェア ベンダー (IHV) の要件に関連付けられていることを示します。

<a href="" id="min"></a>最小値  
整数値が許容される最小値。 &lt;定義されている IHV&gt;最小値が特定の IHV 要件に関連付けられていることを示します。

<a href="" id="max"></a>最大  
整数値で許可される最大値。 &lt;定義されている IHV&gt;最小値が特定の IHV 要件に関連付けられていることを示します。

次の表は、すべてのキーワードの一覧し、ドライバーは、上記の属性に使用する必要があります値を示します。 キーワードの詳細については、WDK ドキュメントでのキーワードを検索してください。

<table style="width:100%;">
<colgroup>
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SubkeyName</th>
<th align="left">ParamDesc</th>
<th align="left">型</th>
<th align="left">既定値</th>
<th align="left">最小</th>
<th align="left">最大</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>JumboPacket</p></td>
<td align="left"><p>ジャンボ パケット</p></td>
<td align="left"><p>整数</p></td>
<td align="left"><p>1514</p></td>
<td align="left"><p>1514</p></td>
<td align="left"><p>&lt;IHV が定義されています。&gt;</p></td>
</tr>
<tr class="even">
<td align="left"><p></em>ReceiveBuffers</p></td>
<td align="left"><p>受信バッファー</p></td>
<td align="left"><p>整数</p></td>
<td align="left"><p>&lt;IHV が定義されています。&gt;</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>&lt;IHV が定義されています。&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>* TransmitBuffers</p></td>
<td align="left"><p>バッファーを送信します。</p></td>
<td align="left"><p>整数</p></td>
<td align="left"><p>&lt;IHV が定義されています。&gt;</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>&lt;IHV が定義されています。&gt;</p></td>
</tr>
<tr class="even">
<td align="left"><p>networkAddress</p></td>
<td align="left"><p>[ネットワーク アドレス]</p></td>
<td align="left"><p>編集</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>なし</p></td>
</tr>
</tbody>
</table>

 

 

 





