---
title: .srcpath、.lsrcpath (ソース パスの設定)
description: .Srcpath と .lsrcpath コマンドを設定またはソース ファイルの検索パスを表示します。
ms.assetid: 416c062f-cbf9-4134-aa2c-306147a466b5
keywords:
- .srcpath、.lsrcpath (ソース パスの設定) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .srcpath, .lsrcpath (Set Source Path)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2e830d183bab930d2448ea57c265d0f65e16d84d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338797"
---
# <a name="srcpath-lsrcpath-set-source-path"></a>.srcpath、.lsrcpath (ソース パスの設定)


**.Srcpath**と **.lsrcpath**コマンドを設定またはソース ファイルの検索パスを表示します。

```dbgcmd
.srcpath[+] [Directory [; ...]] 
.lsrcpath[+] [Directory [; ...]] 
```

## <a name="span-idddkmetasetsourcepathdbgspanspan-idddkmetasetsourcepathdbgspanparameters"></a><span id="ddk_meta_set_source_path_dbg"></span><span id="DDK_META_SET_SOURCE_PATH_DBG"></span>パラメーター


<span id="______________"></span> **+**   
新しいディレクトリが (置換) ではなくに追加することを指定します。 前のソース ファイルの検索パス。

<span id="_______Directory______"></span><span id="_______directory______"></span><span id="_______DIRECTORY______"></span> *ディレクトリ*   
検索パスに配置する 1 つまたは複数のディレクトリを指定します。 場合*ディレクトリ*が指定されていない、現在のパスが表示されます。 複数のディレクトリをセミコロンで区切ります。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

**.Srcpath**コマンドはすべてのデバッガーで使用できます。 **.Lsrcpath**コマンドは、WinDbg でのみ使用でき、スクリプト ファイルでは使用できません。

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

詳細とこのパスを変更するには、他の方法では、次を参照してください。[ソース パス](source-path.md)します。 デバッガーからのリモート デバッグの実行中に使用できるコマンドの詳細については、次を参照してください。[リモート デバッグ セッションを制御する](controlling-a-remote-debugging-session.md)します。

<a name="remarks"></a>コメント
-------

含める場合`srv*`、デバッガーを使用して、ソース パスで[SrcSrv](srcsrv.md)対象モジュールのシンボル ファイルで指定された場所からソース ファイルを取得します。 Srv の使用の詳細については\*ソースのパスを参照してください。[移行元サーバーを使用して](using-a-source-server.md)と[ **.srcfix**](-srcfix---lsrcfix--use-source-server-.md)します。

このコマンドは、デバッグのクライアントから発行されたときに **.srcpath**デバッグのサーバー上のソース パスを設定中に **.lsrcpath**ローカル コンピューター上のソース パスを設定します。

 

 





