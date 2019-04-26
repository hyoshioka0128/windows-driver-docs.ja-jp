---
title: ks.findlive
description: Ks.findlive 拡張機能は、指定した型のライブ オブジェクトを検索しようとする内部 Ks.sys デバッグ ログを検索します。
ms.assetid: 71372144-3f39-460b-859c-ac4cba0c766d
keywords:
- デバッグ ks.findlive Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.findlive
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c9470725ce1c6ba25c18f20241457857ba9bf6ed
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336249"
---
# <a name="ksfindlive"></a>!ks.findlive


**! Ks.findlive**拡張機能は、指定した型のライブ オブジェクトを検索しようとする内部 Ks.sys デバッグ ログを検索します。

```dbgcmd
!ks.findlive Type [Entries] [Level] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Type______"></span><span id="_______type______"></span><span id="_______TYPE______"></span> *型*   
検索対象のオブジェクトの種類を指定します。 リテラル値として、次のいずれかを入力します。**キュー**、**リクエスター**、 **Pin**、**フィルター**、または**Irp**します。

<span id="Entries"></span><span id="entries"></span><span id="ENTRIES"></span>エントリ  
このパラメーターがゼロまたは省略すると、ログ全体が検索されます。

<span id="_______Level______"></span><span id="_______level______"></span><span id="_______LEVEL______"></span> *レベル*   
(省略可能)。 0 ~ 7 で表示する詳細のレベルを指定の値を大きく表示徐々 に詳細なスケールします。 使用可能なすべての詳細を表示するには、7 の値を指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>winxp\Ks.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Ks.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。[ストリーミングのカーネル デバッグ](kernel-streaming-debugging.md)します。

<a name="remarks"></a>注釈
-------

**! Ks.findlive**コマンドが場合がありますすべての可能なライブ オブジェクトの指定に見つかりません。

この拡張機能では、対象のコンピュータがある必要があります Ks.sys のチェック (デバッグ) バージョンを実行します。

 

 





