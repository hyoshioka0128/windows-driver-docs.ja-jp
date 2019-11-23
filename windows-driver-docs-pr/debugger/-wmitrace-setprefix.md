---
title: wmitrace
description: Wmitrace 拡張機能は、このセッションからトレースメッセージの前に付加されるトレースメッセージのプレフィックスを指定します。
ms.assetid: 8712af44-f231-48f6-97ac-56a1d737cd6b
keywords:
- wmitrace Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.setprefix
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b93c586578e5e20efd498f0ac301c4a721e76975
ms.sourcegitcommit: ee1fc949d1ae5eb14df4530758f767702a886e36
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2019
ms.locfileid: "71164784"
---
# <a name="wmitracesetprefix"></a>!wmitrace.setprefix


**! Wmitrace**拡張機能は、このセッションからトレースメッセージの前に付加されるトレースメッセージのプレフィックスを指定します。 この拡張機能を使用すると、デバッグセッション中にプレフィックスを変更できます。

```dbgcmd
!wmitrace.setprefix [+] PrefixVariables 
!wmitrace.setprefix 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="______________"></span> **+**    
*PrefixVariables*をトレースメッセージのプレフィックスに追加します。 **+** トークンが使用されていない場合、 *PrefixVariables*は既存のトレースメッセージのプレフィックスを置き換えます。

<span id="_______PrefixVariables______"></span><span id="_______prefixvariables______"></span><span id="_______PREFIXVARIABLES______"></span>*PrefixVariables*   
トレースメッセージプレフィックスの形式とデータを指定する変数のセット。

変数の形式は% n! x! です。% n はデータフィールドを表し、! x! です。 データ型を表します。 また、コロン (:)、セミコロン (;)、かっこ (())、中かっこ ({})、および角かっこ (\[ \]) などの区切り文字を使用して、フィールドを区切ることもできます。

各% n 変数は、次の表で説明されているパラメーターを表します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">プレフィックス変数識別子</th>
<th align="left">変数の型</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>%1</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>トレースメッセージのメッセージ GUID のフレンドリ名。 既定では、メッセージ GUID のフレンドリ名は、トレースプロバイダーがビルドされたディレクトリの名前です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%2</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>ソースファイルと行番号。</p>
<p>この変数は、トレースメッセージのフレンドリ名を表します。 既定では、トレースメッセージの表示名は、ソースファイルの名前と、トレースメッセージを生成したコードの行番号です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%3</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>スレッド ID。</p>
<p>トレースメッセージを生成したスレッドを識別します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%4</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>トレースメッセージが生成された時刻のタイムスタンプ。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%5</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>カーネル時間。</p>
<p>トレースメッセージが生成された時点でのカーネルモード命令の経過実行時間 (CPU ティック) を表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%6</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>ユーザー時間。</p>
<p>トレースメッセージが生成された時点のユーザーモード命令 (CPU ティック) の経過実行時間を表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%7</p></td>
<td align="left"><p>LONG</p></td>
<td align="left"><p>シーケンス番号。</p>
<p>トレースメッセージのローカルまたはグローバルシーケンス番号を表示します。 既定では、このトレースセッションだけに固有のローカルシーケンス番号が使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%8</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>プロセス ID。</p>
<p>トレースメッセージを生成したプロセスを識別します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%9</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>CPU 数。</p>
<p>トレースメッセージが生成された CPU を識別します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%!FUNC!</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>関数名。</p>
<p>トレースメッセージを生成した関数の名前が表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%!示す</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>トレースメッセージを有効にするトレースフラグの名前を表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%!平準!</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>トレースメッセージを有効にするトレースレベルの値を表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%!COMPNAME!</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>コンポーネント名。</p>
<p>トレースメッセージを生成したプロバイダーのコンポーネントの名前を表示します。 コンポーネント名は、トレースコードに指定されている場合にのみ表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%!SUBCOMP!</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>サブコンポーネント名。</p>
<p>トレースメッセージを生成したプロバイダーのサブコンポーネントの名前を表示します。 サブコンポーネント名は、トレースコードに指定されている場合にのみ表示されます。</p></td>
</tr>
</tbody>
</table>

 

感嘆符内の記号は、変数の形式と有効桁数を指定する変換文字です。 たとえば、%8! 04X! 4桁の符号なしの16進数値として書式設定されたプロセス ID を指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

この拡張機能は、Wmitrace によってエクスポートされます。

この拡張機能は、Windows 2000 以降のバージョンの Windows で使用できます。 Windows 2000 でこの拡張機能を使用する場合は、まず、Windows 用デバッグツールのインストールディレクトリの winxp サブディレクトリの Wmitrace ファイルを w2kfre サブディレクトリにコピーする必要があります。

### <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>よう

次のコマンドは、デバッガーの出力のトレースメッセージのプレフィックスを次の形式に変更します。

**! wmitrace %2! s!:%!FUNC!: %8! 04x!。%3! 04x!: %4! s!:**

この拡張コマンドは、トレースメッセージのプレフィックスを次の形式に設定します。

*SourceFile\_LineNumber: FunctionName: ProcessID: SystemTime:*

その結果、指定された形式でトレースメッセージの先頭に指定された情報が付加されます。 次のコード例は、WDK の Tracedrv サンプルドライバーのトレースから取得されます。

```dbgcmd
tracedrv_c258: TracedrvDispatchDeviceControl: 0af4.0c64: 07/25/2003-13:55:39.998:  IOCTL = 1
```

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

イベントトレースの概念の概要については、Microsoft Windows SDK のドキュメントを参照してください。 トレースメッセージのフォーマットファイルの詳細については、WDK ドキュメントの「トレースメッセージのプレフィックス」を参照してください。

<a name="remarks"></a>注釈
-------

パラメーターを指定せずに使用した場合、 **! wmitrace**によって、トレースメッセージのプレフィックスの現在の値が表示されます。

*トレースメッセージのプレフィックス*は、Windows software trace プリプロセッサ (WPP) ソフトウェアトレース中に各トレースメッセージの前に付加されるトレースメッセージに関するデータで構成されます。 このデータの生成元は、トレースログ (.etl) ファイルとトレースメッセージ形式 (tmf) ファイルです。 トレースメッセージプレフィックスの形式とデータをカスタマイズできます。

既定のトレースメッセージのプレフィックスは次のとおりです。

```dbgcmd
[%9!d!]%8!04X!.%3!04X!::%4!s! [%1!s!]
```

とは、次のプレフィックスを生成します。

```dbgcmd
[CPUNumber]ProcessID.ThreadID::SystemTime [ProviderDirectory] 
```

トレースメッセージのプレフィックスの形式とデータをデバッガーの外部で変更するには、% TRACE\_FORMAT\_PREFIX% environment 変数を設定します。 デバッガーの外部でトレースメッセージのプレフィックスを設定する方法を示す例については、Windows Driver Kit (WDK) のドキュメントの「例 7: トレースメッセージのプレフィックスをカスタマイズする」を参照してください。 メッセージのトレースメッセージのプレフィックスが既定値と異なる場合は、この環境変数がコンピューターで設定されている可能性があります。

この拡張コマンドを使用して設定したプレフィックスは、デバッガーの出力のみに影響します。 トレースログに表示されるトレースメッセージのプレフィックスは、既定値と% TRACE\_FORMAT\_PREFIX% environment 変数の値によって決まります。

この拡張機能は、WPP ソフトウェアのトレース、および Windows イベントトレーシングの以前の (レガシ) 方法でのみ役立ちます。 他のプロバイダーによって生成されるトレースイベントでは、トレースメッセージ形式 (TMF) ファイルが使用されないため、この拡張機能は影響を受けません。

 

 





