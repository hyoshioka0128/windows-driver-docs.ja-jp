---
title: ate
description: 拡張機能の表示を指定したアドレスを代替のページ テーブル エントリ (食事) ate します。
ms.assetid: 8ec98fa5-4939-49cb-8678-e412b9cbe7e3
keywords:
- Windows デバッグ ate
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- ate
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9fca51ae0b2ab19ccbb09ba1ea3d680508adccac
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527866"
---
# <a name="ate"></a>! ate


**! Ate**拡張機能には、指定されたアドレスの代替のページ テーブル エントリ (食事) が表示されます。

```dbgcmd
    !ate Address
```    

**重要な**  このコマンドが 10.0.14257 Windows デバッガーのバージョンでは非推奨以降されてし、は現在利用できません。

 

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
表示する食事を指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>利用不可</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ページのテーブルとページのディレクトリについては、*Microsoft Windows internals 』*、Mark Russinovich と David Solomon を参照してください。 (この本できない場合がありますのいくつかの言語および国。)

<a name="remarks"></a>注釈
-------

この拡張機能は、Itanium ベースのコンピューターにできるだけです。

次の表に、食事のステータスのフラグが表示されます。 **! Ate**表示大文字またはダッシュでこれらのビットを示すし、も情報を追加します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ときに表示される設定</th>
<th align="left">オフにすると表示</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>V</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>コミットします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>G</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>アクセスはできません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>E</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>実行します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>W</p></td>
<td align="left"><p>R</p></td>
<td align="left"><p>書き込み可能または読み取り専用です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>L</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>[ロック] をオンにします。 食事がロックされている、現在の障害が満たされるまでの食事を含むページの障害の再試行そのため、します。 これは、マルチプロセッサ システムで発生することができます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Z</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>0 を入力します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>N</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>アクセスがありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>C</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>書き込み時にコピーします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>私</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>間接 PTE します。 この食事が別の物理ページを直接参照します。 競合する 2 つの食事属性、食事を含むページがあります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>P</p></td>
<td align="left"></td>
<td align="left"><p>予約済み。</p></td>
</tr>
</tbody>
</table>

 

 

 





