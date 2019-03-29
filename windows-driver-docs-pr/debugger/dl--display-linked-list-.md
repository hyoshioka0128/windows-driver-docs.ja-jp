---
title: dl (リンク リストの表示)
description: Dl コマンドでは、LIST_ENTRY または SINGLE_LIST_ENTRY リンク リストが表示されます。
ms.assetid: fbf03e78-d4b3-4dd9-904b-3f44a1a86cff
keywords:
- dl (リンクされたリストを表示) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dl (Display Linked List)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9998c5567a4e5ce43cc069e84487b065541450e6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573751"
---
# <a name="dl-display-linked-list"></a>dl (リンク リストの表示)


**Dl**コマンド一覧を表示\_エントリまたは SINGLE\_一覧\_エントリのリンクされたリスト。

```dbgcmd
dl[b] Address MaxCount Size
```

## <a name="span-idddkcmddisplaylinkedlistdbgspanspan-idddkcmddisplaylinkedlistdbgspanparameters"></a><span id="ddk_cmd_display_linked_list_dbg"></span><span id="DDK_CMD_DISPLAY_LINKED_LIST_DBG"></span>パラメーター


<span id="_______b______"></span><span id="_______B______"></span> **b**   
これが含まれている場合は、逆の順序でリストがダンプされます。 (つまり、デバッガーに依存、**点滅**s の代わりに、 **Flink**s)。これは、1 つで使用できない\_一覧\_エントリ。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
リストの開始アドレス。 構文の詳細については、次を参照してください。[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)します。

<span id="_______MaxCount______"></span><span id="_______maxcount______"></span><span id="_______MAXCOUNT______"></span> *MaxCount*   
ダンプする要素の最大数。

<span id="_______Size______"></span><span id="_______size______"></span><span id="_______SIZE______"></span> *サイズ*   
各要素のサイズ。 これは、連続する ULONG 数\_PTRs 一覧の各要素に対して表示されます。

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
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

その他のメモリに関連するコマンドの説明とメモリの操作の概要については、次を参照してください。[読み取りと書き込みメモリ](reading-and-writing-memory.md)します。

<a name="remarks"></a>コメント
-------

このリストはリストである必要があります\_エントリまたは SINGLE\_一覧\_エントリの構造体。 これより大きな構造体に埋め込まれている場合ことを確認します*アドレス*ポイント リンク リストの構造、外側の構造体の先頭にありません。

表示が始まります*アドレス*します。 そのため、リストの先頭を指すポインターのアドレスを指定している場合は、印刷された最初の要素を無視する必要があります。

*アドレス*、 *MaxCount*、および*サイズ*パラメーターは、現在の既定の基数。 使用することができます、 [ **n (設定数の基本)** ](n--set-number-base-.md)コマンドまたは**0 x**基数を変更するプレフィックス。

一覧をループ自体に戻り、ダンプが停止します。 Null ポインターが発生した場合、ダンプは停止します。

一覧の各要素のいくつかのコマンドを実行する場合を使用して、 [ **! 一覧**](-list.md)拡張機能。

 

 





