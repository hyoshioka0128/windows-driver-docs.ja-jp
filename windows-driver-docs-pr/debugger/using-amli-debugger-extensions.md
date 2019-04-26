---
title: AMLI Debugger 拡張機能の使用
description: AMLI Debugger 拡張機能の使用
ms.assetid: 98b9cd6e-b2e1-44bd-aff6-376b9cf2daa2
keywords:
- AMLI デバッガー、AMLI デバッガー拡張機能
- amli 拡張機能
- acpikd.amli 拡張機能
ms.date: 11/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: e2405122012154c1a54133e0a5134942496c64fb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342010"
---
# <a name="using-amli-debugger-extensions"></a>AMLI Debugger 拡張機能の使用


## <span id="ddk_using_amli_debugger_extensions_dbg"></span><span id="DDK_USING_AMLI_DEBUGGER_EXTENSIONS_DBG"></span>


AMLI デバッガー拡張機能のコマンドは、拡張モジュール Kdexts.dll に含まれ、次の構文を使用します。

```dbgcmd
kd> !amli command [parameters] 
```


任意の拡張機能で読み込まれたした後、モジュールを省略できますよう、 **acpikd**プレフィックス。

AMLI デバッガー プロンプトである場合は、入力するだけで実行するこれらの拡張機能コマンドのいずれかのことができます、*コマンド*名前なし、 **! amli**プレフィックス。

```dbgcmd
AMLI(? for help)-> command [parameters] 
```

このプロンプトでしたら、 **! amli デバッガー**コマンドは使用できません (ため、無意味になります)。 また、ヘルプ コマンド (**でしょうか。** ) このプロンプトですべての AMLI デバッガー拡張機能と、コマンドを示しています。 中に、 **! amli でしょうか。** 拡張機能には、実際の拡張子のヘルプのみが表示されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">アクション</th>
<th align="left">拡張機能コマンド</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ヘルプを表示します。</p></td>
<td align="left"><p><strong><a href="-amli--.md" data-raw-source="[!amli ?](-amli--.md)">! amli でしょうか。</a></strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>AML ブレークポイントの設定</p></td>
<td align="left"><p><strong><a href="-amli-bp.md" data-raw-source="[!amli bp](-amli-bp.md)">! amli bp</a></strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>AML ブレークポイントの一覧表示</p></td>
<td align="left"><p><strong><a href="-amli-bl.md" data-raw-source="[!amli bl](-amli-bl.md)">! amli bl</a></strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>AML ブレークポイントを無効にします。</p></td>
<td align="left"><p><strong><a href="-amli-bd.md" data-raw-source="[!amli bd](-amli-bd.md)">! amli bd</a></strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>AML ブレークポイントを有効にします。</p></td>
<td align="left"><p><strong><a href="-amli-be.md" data-raw-source="[!amli be](-amli-be.md)">! amli します。</a></strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>AML ブレークポイントをクリアします。</p></td>
<td align="left"><p><strong><a href="-amli-bc.md" data-raw-source="[!amli bc](-amli-bc.md)">! amli bc</a></strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>AMLI デバッガーを入力します。</p></td>
<td align="left"><p><strong><a href="-amli-debugger.md" data-raw-source="[!amli debugger](-amli-debugger.md)">! amli デバッガー</a></strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>イベント ログの表示</p></td>
<td align="left"><p><strong><a href="-amli-dl.md" data-raw-source="[!amli dl](-amli-dl.md)">!amli dl</a></strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>イベント ログの消去</p></td>
<td align="left"><p><strong><a href="-amli-cl.md" data-raw-source="[!amli cl](-amli-cl.md)">! amli cl</a></strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>ヒープの表示</p></td>
<td align="left"><p><strong><a href="-amli-dh.md" data-raw-source="[!amli dh](-amli-dh.md)">! amli dh</a></strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>データ オブジェクトの表示</p></td>
<td align="left"><p><strong><a href="-amli-do.md" data-raw-source="[!amli do](-amli-do.md)">! amli の操作を行います</a></strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>履歴の表示</p></td>
<td align="left"><p><strong><a href="-amli-ds.md" data-raw-source="[!amli ds](-amli-ds.md)">! amli ds</a></strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Namespace オブジェクトの表示</p></td>
<td align="left"><p><strong><a href="-amli-dns.md" data-raw-source="[!amli dns](-amli-dns.md)">! amli dns</a></strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>Namespace オブジェクトを見つける</p></td>
<td align="left"><p><strong><a href="-amli-find.md" data-raw-source="[!amli find](-amli-find.md)">! amli の検索</a></strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>メソッドに最も近いディスプレイ</p></td>
<td align="left"><p><strong><a href="-amli-ln.md" data-raw-source="[!amli ln](-amli-ln.md)">! amli ln</a></strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>すべてのコンテキストを一覧表示します。</p></td>
<td align="left"><p><strong><a href="-amli-lc.md" data-raw-source="[!amli lc](-amli-lc.md)">!amli lc</a></strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>コンテキスト情報を表示します。</p></td>
<td align="left"><p><strong><a href="-amli-r.md" data-raw-source="[!amli r](-amli-r.md)">!amli r</a></strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>AML コードを逆アセンブルします。</p></td>
<td align="left"><p><strong><a href="-amli-u.md" data-raw-source="[!amli u](-amli-u.md)">! amli u</a></strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>AMLI デバッガー オプションの設定</p></td>
<td align="left"><p><strong><a href="-amli-set.md" data-raw-source="[!amli set](-amli-set.md)">!amli set</a></strong></p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目

[AMLI デバッガー](the-amli-debugger.md)
