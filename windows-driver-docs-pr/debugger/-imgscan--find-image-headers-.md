---
title: .imgscan (イメージ ヘッダーの検索)
description: .Imgscan コマンドでは、イメージ ヘッダーの仮想メモリをスキャンします。
ms.assetid: 8b524665-0471-4634-aa31-1c82d6cc8569
keywords:
- イメージ ヘッダー (.imgscan) コマンドを見つける
- .imgscan (イメージ ヘッダーを検索) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .imgscan (Find Image Headers)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 92a77a5c6c481736380f411e2c8659941746b41d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574732"
---
# <a name="imgscan-find-image-headers"></a>.imgscan (イメージ ヘッダーの検索)


**.Imgscan**コマンドはイメージ ヘッダーの仮想メモリをスキャンします。

```dbgcmd
.imgscan [Options] 
```

## <a name="span-idddkmetafindimageheadersdbgspanspan-idddkmetafindimageheadersdbgspanparameters"></a><span id="ddk_meta_find_image_headers_dbg"></span><span id="DDK_META_FIND_IMAGE_HEADERS_DBG"></span>パラメーター


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
次のオプションのいずれか:

<span id="_r_Range"></span><span id="_r_range"></span><span id="_R_RANGE"></span>**/r** **** *範囲*  
検索範囲を指定します。 構文の詳細については、次を参照してください。[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)します。 1 つだけのアドレスを指定する場合、デバッガーはそのアドレスで開始し、0x10000 (バイト) を拡張する範囲を検索します。

<span id="_l"></span><span id="_L"></span>**/l**  
見つかったすべてのイメージ ヘッダーのモジュール情報を読み込みます。

<span id="_v"></span><span id="_V"></span>**/v**  
詳細な情報を表示します。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

使用しない場合、 **/r**パラメーター、デバッガーは、すべての仮想メモリ領域を検索します。

**.Imgscan**コマンドは、検出されたすべてのイメージ ヘッダーとヘッダーの種類が表示されます。 ヘッダーの種類には、ポータブル実行可能ファイル (PE) のヘッダーと Microsoft MS-DOS MZ ヘッダーが含まれます。

次の例は、 **.imgscan**コマンド。

```dbgcmd
0:000> .imgscan
MZ at 00400000, prot 00000002, type 01000000 - size 2d000
MZ at 77f80000, prot 00000002, type 01000000 - size 7d000
  Name: ntdll.dll
MZ at 7c570000, prot 00000002, type 01000000 - size b8000
  Name: KERNEL32.dll
```

 

 





