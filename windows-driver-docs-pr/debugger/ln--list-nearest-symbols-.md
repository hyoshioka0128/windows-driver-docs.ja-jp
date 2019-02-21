---
title: ln (一番近いシンボルを)
description: Ln コマンドでは、指定されたアドレスに近い、シンボルが表示されます。
ms.assetid: ff01ace7-398a-4e32-9d58-00873eca3201
keywords:
- ln (一番近いシンボル リスト) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ln (List Nearest Symbols)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ded9b73fb0ab3adcddd7f754eb367fe2f8dc0ec2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527859"
---
# <a name="ln-list-nearest-symbols"></a>ln (一番近いシンボルを)


**Ln**コマンド、指定されたアドレスに近いシンボルを表示します。

```dbgcmd
ln Address
ln /D Address 
```

## <a name="span-idddkcmdlistnearestsymbolsdbgspanspan-idddkcmdlistnearestsymbolsdbgspanparameters"></a><span id="ddk_cmd_list_nearest_symbols_dbg"></span><span id="DDK_CMD_LIST_NEAREST_SYMBOLS_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
デバッガーがシンボルの検索を開始する位置のアドレスを指定します。 前に、または後は、最も近いシンボル*アドレス*が表示されます。 構文の詳細については、次を参照してください。[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)します。

<span id="_D"></span><span id="_d"></span>**/D**  
使用して、出力が表示されることを指定します。[デバッガー マークアップ言語 (DML)](debugger-markup-language-commands.md)します。 DML の出力には、最も近いシンボルを含むモジュールを探索に使用できるリンクが含まれています。 ブレークポイントを設定するために使用できるリンクも含まれています。

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
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

使用することができます、 **ln**を指すポインターが判断するためのコマンド。 このコマンドはことが破損したスタックの呼び出しを実行する手順を検討しているときに便利なできます。

ソース行情報がある場合、 **ln**表示には、ソース ファイル名と行番号の情報も含まれています。

使用する場合、[移行元サーバー](using-a-source-server.md)、 **ln**コマンドが移行元サーバーに関連する情報を表示します。

 

 





