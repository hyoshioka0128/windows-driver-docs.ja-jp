---
title: KDbgCtrl のコマンドライン オプション
description: KDbgCtrl コマンドラインでは、次の構文を使用します。
ms.assetid: 0367a09d-c475-4aeb-8f88-47d51ec7e9d5
keywords:
- KDbgCtrl コマンドラインオプション Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- KDbgCtrl Command-Line Options
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3d07c39fb30b3abecac0a2792be4d0c67d228f55
ms.sourcegitcommit: 99997c9eb94b1f58f5e881a17f7bdb7b5d005019
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2020
ms.locfileid: "82255485"
---
# <a name="kdbgctrl-command-line-options"></a>KDbgCtrl のコマンドライン オプション


KDbgCtrl コマンドラインでは、次の構文を使用します。

```dbgcmd
kdbgctrl [-e|-d|-c] [-ea|-da|-ca] [-eu|-du|-cu] [-eb|-db|-cb] [-sdb Size | -cdb] 

kdbgctrl -cx 

kdbgctrl -td ProcessID File 

kdbgctrl -sd {active|automatic|full|kernel|mini}

kdbgctrl -? 
```

## <a name="span-idddk_kdbgctrl_command_line_options_dbgspanspan-idddk_kdbgctrl_command_line_options_dbgspanparameters"></a><span id="ddk_kdbgctrl_command_line_options_dbg"></span><span id="DDK_KDBGCTRL_COMMAND_LINE_OPTIONS_DBG"></span>パラメータ


<span id="_______-e______"></span><span id="_______-E______"></span>**-e**   
カーネルの完全デバッグを有効にします。

<span id="_______-d______"></span><span id="_______-D______"></span>**-d**   
完全なカーネルデバッグを無効にします。

<span id="_______-c______"></span><span id="_______-C______"></span>**-c**   
完全なカーネルデバッグが有効になっているかどうかを確認します。 完全なカーネル Deubugging が有効になっている場合は true、完全なカーネルデバッグが無効になっている場合は false が表示されます。

<span id="_______-ea______"></span><span id="_______-EA______"></span>**-ea**   
カーネルの自動デバッグを有効にします。

<span id="_______-da______"></span><span id="_______-DA______"></span>**-da**   
カーネルの自動デバッグを無効にします。

<span id="_______-ca______"></span><span id="_______-CA______"></span>**-ca**   
カーネルの自動デバッグが有効になっているかどうかを確認します。 自動カーネル Deubugging が有効になっている場合は true、自動カーネルデバッグが無効になっている場合は false が表示されます。

<span id="_______-eu______"></span><span id="_______-EU______"></span>**-eu**   
ユーザーモードのエラー処理を有効にします。

<span id="_______-du______"></span><span id="_______-DU______"></span>**-du**   
ユーザーモードのエラー処理を無効にします。

<span id="_______-cu______"></span><span id="_______-CU______"></span>**-cu**   
ユーザーモードのエラー処理が有効になっているかどうかを確認します。 ユーザーモードのエラー処理が有効になっている場合は true が表示され、ユーザーモードのエラー処理が無効になっている場合は false が表示されます。

<span id="-eb"></span><span id="-EB"></span>**-eb**  
カーネルデバッグのブロックを有効にします。

<span id="-db"></span><span id="-DB"></span>**-db**  
カーネルデバッグのブロックを無効にします

<span id="-cb"></span><span id="-CB"></span>**-cb**  
カーネルデバッグがブロックされているかどうかを確認します。 カーネルデバッグがブロックされている場合は true が表示され、カーネルデバッグがブロックされていない場合は false が表示されます。

<span id="_______-sdb_______Size______"></span><span id="_______-sdb_______size______"></span><span id="_______-SDB_______SIZE______"></span>**-sdb** *サイズ*   
DbgPrint バッファーのサイズを設定します。 *Size*が**0x**で始まる場合は、16進数として解釈されます。 プレフィックスが**0** (ゼロ) の場合は、8進数として解釈されます。 それ以外の場合、decimal として解釈されます。

<span id="_______-cdb______"></span><span id="_______-CDB______"></span>**-cdb**   
DbgPrint バッファーの現在のサイズをバイト単位で表示します。

<span id="_______-cx______"></span><span id="_______-CX______"></span>**-cx**   
現在の完全なカーネルデバッグ設定を確認し、適切な値を返します。 このオプションを他のオプションと組み合わせることはできません。また、出力は表示されません。 これは、KDbgCtrl プログラムの戻り値をテストできるバッチファイルで使用するように設計されています。 返される戻り値は次のとおりです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>0x10001</strong></p></td>
<td align="left"><p>完全なカーネルデバッグが有効になっています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>0x10002</strong></p></td>
<td align="left"><p>完全なカーネルデバッグが無効になっています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>その他の値</p></td>
<td align="left"><p>エラーが発生しました。 KDbgCtrl は、カーネルの完全デバッグの現在の状態を特定できませんでした。</p></td>
</tr>
</tbody>
</table>

 

<span id="-td_ProcessID_File"></span><span id="-td_processid_file"></span><span id="-TD_PROCESSID_FILE"></span>**-td** *ProcessID* *ファイル*  
カーネルトリアージダンプファイルを取得します。 ダンプファイルのプロセス ID と名前を入力します。

<span id="-sd_Type"></span>**-sd {アクティブ | 自動 | 完全 | カーネル | ミニ}**   
システムクラッシュが発生した場合に収集されるダンプの種類を設定し、クラッシュダンプスタックを再読み込みします。 ダンプの種類の詳細については、「[カーネルモードのダンプファイルの](varieties-of-kernel-mode-dump-files.md)種類」を参照してください。

<span id="_______-_______"></span> **-?**   
KDbgCtrl のコマンドラインヘルプを表示します。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

KDbgCtrl のすべての設定の詳細については、「 [KDbgCtrl の使用](using-kdbgctrl.md)」を参照してください。

 

 





