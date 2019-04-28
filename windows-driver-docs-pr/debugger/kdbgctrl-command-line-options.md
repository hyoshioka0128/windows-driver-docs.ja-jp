---
title: KDbgCtrl のコマンドライン オプション
description: KDbgCtrl コマンドラインは次の構文を使用します。
ms.assetid: 0367a09d-c475-4aeb-8f88-47d51ec7e9d5
keywords:
- KDbgCtrl コマンド ライン オプションの Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- KDbgCtrl Command-Line Options
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 49569683160f426e7b2b3ad113ebd3528b2735ff
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367210"
---
# <a name="kdbgctrl-command-line-options"></a>KDbgCtrl のコマンドライン オプション


KDbgCtrl コマンドラインは、次の構文を使用します。

```dbgcmd
kdbgctrl [-e|-d|-c] [-ea|-da|-ca] [-eu|-du|-cu] [-eb|-db|-cb] [-sdb Size | -cdb] 

kdbgctrl -cx 

kdbgctrl -td ProcessID File 

kdbgctrl -? 
```

## <a name="span-idddkkdbgctrlcommandlineoptionsdbgspanspan-idddkkdbgctrlcommandlineoptionsdbgspanparameters"></a><span id="ddk_kdbgctrl_command_line_options_dbg"></span><span id="DDK_KDBGCTRL_COMMAND_LINE_OPTIONS_DBG"></span>パラメーター


<span id="_______-e______"></span><span id="_______-E______"></span> **-e**   
完全なカーネル デバッグを有効にします。

<span id="_______-d______"></span><span id="_______-D______"></span> **-d**   
完全なカーネルのデバッグを無効にします。

<span id="_______-c______"></span><span id="_______-C______"></span> **-c**   
完全なカーネルのデバッグが有効になっているかどうかを確認します。 完全なカーネル Deubugging が有効であり、完全なカーネルのデバッグが無効になっている場合、false を表示する場合は、true を表示します。

<span id="_______-ea______"></span><span id="_______-EA______"></span> **-ea**   
自動のカーネル デバッグを有効にします。

<span id="_______-da______"></span><span id="_______-DA______"></span> **-da**   
自動のカーネル デバッグを無効にします。

<span id="_______-ca______"></span><span id="_______-CA______"></span> **-ca**   
自動のカーネル デバッグが有効になっているかどうかを確認します。 自動のカーネル Deubugging が有効であり、自動カーネル デバッグが無効になっている場合は false を表示する場合は、true を表示します。

<span id="_______-eu______"></span><span id="_______-EU______"></span> **-eu**   
ユーザー モードのエラー処理を有効にします。

<span id="_______-du______"></span><span id="_______-DU______"></span> **-du**   
ユーザー モードのエラー処理を無効にします。

<span id="_______-cu______"></span><span id="_______-CU______"></span> **-cu**   
ユーザー モード エラーの処理が有効になっているかどうかを確認します。 ユーザー モード エラーの処理が有効であり、ユーザー モード エラーの処理が無効になっている場合は false を表示する場合、true が表示されます。

<span id="-eb"></span><span id="-EB"></span>**-eb**  
有効では、カーネルのデバッグのブロックしています。

<span id="-db"></span><span id="-DB"></span>**-db**  
カーネル デバッグをブロックして無効にします

<span id="-cb"></span><span id="-CB"></span>**-cb**  
カーネル デバッグがブロックされているかどうかを確認します。 カーネル デバッグがブロックされ、カーネルのデバッグがブロックされていない場合は false を表示する場合、true が表示されます。

<span id="_______-sdb_______Size______"></span><span id="_______-sdb_______size______"></span><span id="_______-SDB_______SIZE______"></span> **-sdb** *サイズ*   
による DbgPrint バッファーのサイズを設定します。 場合*サイズ*が付きます**0 x**は 16 進数として解釈されます。 付く場合**0** (ゼロ)、8 進数として、解釈されます。 それ以外の場合、10 進数として解釈されます。

<span id="_______-cdb______"></span><span id="_______-CDB______"></span> **-cdb**   
による DbgPrint バッファーのバイト単位では、現在のサイズを表示します。

<span id="_______-cx______"></span><span id="_______-CX______"></span> **-cx**   
現在の完全なカーネル デバッグ設定を決定し、適切な値を返します。 このオプションは、その他のオプションと組み合わせることはできませんし、出力は表示されません。 KDbgCtrl プログラムの戻り値をテストできるバッチ ファイルでの使用に適しています。 有効な戻り値は次のとおりです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">[値]</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>0x10001</strong></p></td>
<td align="left"><p>完全なカーネル デバッグを有効にするとします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>0x10002</strong></p></td>
<td align="left"><p>完全なカーネル デバッグを無効になっています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>その他の値</p></td>
<td align="left"><p>エラーが発生しました。 KDbgCtrl は完全なカーネル デバッグの現在の状態を確認できませんでした。</p></td>
</tr>
</tbody>
</table>

 

<span id="-td_ProcessID_File"></span><span id="-td_processid_file"></span><span id="-TD_PROCESSID_FILE"></span>**-td** *ProcessID* *File*  
カーネル トリアージのダンプ ファイルを取得します。 プロセス ID と、ダンプ ファイルの名前を入力します。

<span id="_______-_______"></span> **-?**   
コマンド ライン ヘルプを表示します KDbgCtrl します。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

すべての KDbgCtrl 設定については、次を参照してください。[を使用して KDbgCtrl](using-kdbgctrl.md)します。

 

 





