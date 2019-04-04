---
title: .chain (リスト デバッガー拡張)
description: .Chain コマンドでは、すべての読み込まれたデバッガー拡張機能の既定の検索順序で一覧表示します。
ms.assetid: 73139b02-265a-424d-9de8-f4f3736e62db
keywords:
- .chain (リスト デバッガー拡張) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .chain (List Debugger Extensions)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bd87e6c1863a3ad9e1883c40fefc7f8e137e30a3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538054"
---
# <a name="chain-list-debugger-extensions"></a>.chain (リスト デバッガー拡張)


**.Chain**コマンドは、既定の検索順序ですべての読み込まれたデバッガー拡張機能を一覧表示します。

```dbgsyntax
.chain
.chain /D
```

## <a name="span-idddkmetaclosehandledbgspanspan-idddkmetaclosehandledbgspanparameters"></a><span id="ddk_meta_close_handle_dbg"></span><span id="DDK_META_CLOSE_HANDLE_DBG"></span>パラメーター


<span id="________D______"></span><span id="________d______"></span> **/D**   
使用して、出力が表示されます。[デバッガー Markup Language](debugger-markup-language-commands.md)します。 出力では、表示される各モジュールは、モジュールによって実装されている拡張機能に関する情報を取得するクリックできるリンクです。

## <span id="ddk_meta_list_debugger_extensions_dbg"></span><span id="DDK_META_LIST_DEBUGGER_EXTENSIONS_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>モード</p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="even">
<td align="left"><p>ターゲット</p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>プラットフォーム</p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

読み込みの詳細については、アンロード、および拡張機能を制御するを参照してください[デバッガー拡張 Dll の読み込み](loading-debugger-extension-dlls.md)します。 拡張機能コマンド、および既定の検索順序の説明を実行する方法の詳細については、[デバッガー拡張機能コマンドの使用](using-debugger-extension-commands.md)を参照してください。

 

 





