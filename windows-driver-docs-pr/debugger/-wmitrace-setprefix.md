---
title: wmitrace.setprefix
description: Wmitrace.setprefix 拡張機能では、このセッションからの前にメッセージをトレースにトレース メッセージのプレフィックスを指定します。
ms.assetid: 8712af44-f231-48f6-97ac-56a1d737cd6b
keywords:
- デバッグ wmitrace.setprefix Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.setprefix
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c04b8e2376d877c470ed651061a452e7fd5606ba
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531800"
---
# <a name="wmitracesetprefix"></a>!wmitrace.setprefix


**! Wmitrace.setprefix**拡張機能がこのセッションからの前にメッセージをトレースにトレース メッセージのプレフィックスを指定します。 この拡張機能を使用して、デバッグ セッション中に、プレフィックスを変更できます。

```dbgcmd
!wmitrace.setprefix [+] PrefixVariables 
!wmitrace.setprefix 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="______________"></span> **+**   
により*PrefixVariables* apended トレース メッセージのプレフィックスにします。 場合、 **+** トークンが使用されない*PrefixVariables*既存のトレース メッセージのプレフィックスが置き換えられます。

<span id="_______PrefixVariables______"></span><span id="_______prefixvariables______"></span><span id="_______PREFIXVARIABLES______"></span> *PrefixVariables*   
トレース メッセージのプレフィックスの形式とデータを指定する変数のセット。

変数がある %n がデータ フィールドを表す形式 %n! x!、! x! データ型を表します。 コロン (:)、セミコロン (;)、かっこ (())、中かっこ ({})、および角かっこなどの区切り文字を含めることもできます ( \[ \] ) フィールドを分割します。

%N の各変数は、次の表で説明されているパラメーターを表します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">変数の識別子をプレフィックスします。</th>
<th align="left">変数の型</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>%1</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>メッセージのトレース メッセージの GUID のフレンドリ名。 既定では、メッセージの GUID のフレンドリ名は、トレース プロバイダーが構築されたディレクトリの名前です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%2</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>ソース ファイルと行番号。</p>
<p>この変数は、トレース メッセージの表示名を表します。 既定では、トレース メッセージの表示名は、ソース ファイルとトレース メッセージを生成したコードの行番号の名前です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%3</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>スレッド id です。</p>
<p>トレース メッセージを生成したスレッドを識別します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%4</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>トレース メッセージが生成された時刻のタイムスタンプ。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%5</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>カーネル時間。</p>
<p>トレース メッセージが生成された時点で、CPU のティック単位で、カーネル モード命令の実行の経過時間を表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%6</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>ユーザーの時間です。</p>
<p>トレース メッセージが生成された時点で、CPU のティック単位でユーザー モードについては、実行の経過時間を表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%7</p></td>
<td align="left"><p>長い</p></td>
<td align="left"><p>シーケンス番号。</p>
<p>トレース メッセージのローカルまたはグローバルのシーケンス番号が表示されます。 このトレース セッションにのみ一意ではローカルのシーケンス番号は、既定値です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%8</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>プロセス id です。</p>
<p>トレース メッセージを生成したプロセスを識別します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%9</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>CPU の数。</p>
<p>トレース メッセージが生成された CPU を識別します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%!FUNC!</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>関数の名前。</p>
<p>トレース メッセージを生成した関数の名前が表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%!フラグの %</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>トレース メッセージを有効にするトレース フラグの名前を表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%!レベル。</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>トレース メッセージが可能なトレース レベルの値が表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%!COMPNAME!</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>コンポーネントの名前。</p>
<p>トレース メッセージを生成したプロバイダーのコンポーネントの名前が表示されます。 コンポーネント名では、トレース コードで指定されている場合にのみ表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%!SUBCOMP!</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>サブコンポーネントの名前。</p>
<p>トレース メッセージを生成したプロバイダーのサブコンポーネントの名前が表示されます。 サブコンポーネント名には、トレース コードで指定されている場合にのみが表示されます。</p></td>
</tr>
</tbody>
</table>

 

内の感嘆符シンボルは、形式と、変数の有効桁数を指定する変換の文字です。 たとえば、%8! 04 X! 4 桁、符号なし、16 進数として書式設定されたプロセス ID を指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

この拡張機能は、Wmitrace.dll によってエクスポートされます。

この拡張機能は、Windows 2000 以降のバージョンの Windows で使用できます。 Windows 2000 でこの拡張機能を使用する場合は、w2kfre サブディレクトリに Wmitrace.dll ファイルを Windows 内のデバッグ ツールのインストール ディレクトリの winxp サブディレクトリからまずコピーする必要があります。

### <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>例

次のコマンドは、次の形式にデバッガーの出力にトレース メッセージのプレフィックスを変更します。

**! wmitrace.setprefix %2!s!: % です。FUNC!: %8。 04 x です。%3! 04 x!: %4!s! です。**

この拡張機能コマンドでは、トレース メッセージのプレフィックスを次の形式に設定します。

*SourceFile\_LineNumber:関数名:ProcessID.ThreadID:SystemTime:*

その結果、トレース メッセージは指定された形式で指定した情報を前置します。 次のコード例は、WDK の Tracedrv サンプル ドライバーのトレースから取得されます。

```dbgcmd
tracedrv_c258: TracedrvDispatchDeviceControl: 0af4.0c64: 07/25/2003-13:55:39.998:  IOCTL = 1
```

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

イベントのトレースの概念的な概要については、Microsoft Windows SDK のドキュメントを参照してください。 トレース メッセージのフォーマット ファイルについては、WDK ドキュメントの「トレース メッセージのプレフィックス」のトピックを参照してください。

<a name="remarks"></a>注釈
-------

パラメーターなしで使用すると **! wmitrace.setprefix**トレース メッセージのプレフィックスの現在の値が表示されます。

*トレース メッセージのプレフィックス*Windows ソフトウェア トレース プリプロセッサ (WPP) ソフトウェア トレース中に、各トレース メッセージに付加されるトレース メッセージに関するデータで構成されます。 このデータは、トレース ログ (.etl) ファイルとトレース メッセージの形式 (.tmf) ファイルで発生します。 形式とトレース メッセージのプレフィックス内のデータをカスタマイズすることができます。

既定のトレース メッセージのプレフィックスは次のとおりです。

```dbgcmd
[%9!d!]%8!04X!.%3!04X!::%4!s! [%1!s!]
```

次のプレフィックスを生成します。

```dbgcmd
[CPUNumber]ProcessID.ThreadID::SystemTime [ProviderDirectory] 
```

形式と、デバッガーの外部でのトレース メッセージのプレフィックス内のデータを変更するには、% トレースを設定して\_形式\_%path% 環境変数のプレフィックス。 デバッガーの外でのトレース メッセージのプレフィックスを設定する方法を示す例を参照してください"例 7。カスタマイズするトレース メッセージのプレフィックス"、Windows Driver Kit (WDK) ドキュメント。 場合は、メッセージのトレース メッセージのプレフィックスは、既定値によって異なります、コンピューターにこの環境変数を設定する可能性があります。

この拡張機能のコマンドを使用して設定したプレフィックスでは、デバッガーの出力のみに影響します。 トレース ログに表示されるトレース メッセージのプレフィックスは、既定値とトレース % の値によって決まります\_形式\_%path% 環境変数のプレフィックス。

この拡張機能は、WPP ソフトウェア トレース、およびイベント トレースの Windows の以前の (レガシー) メソッドの中にのみ役立ちます。 Manifested 他のプロバイダーによって生成されるトレース イベントはトレース メッセージの形式 (TMF) ファイルを使用しないと、そのためこの拡張機能には影響しませんにします。

 

 





