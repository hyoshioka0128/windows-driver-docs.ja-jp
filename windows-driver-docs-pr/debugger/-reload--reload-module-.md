---
title: .reload (モジュールの再読み込み)
description: .Reload コマンドでは、指定したモジュールのすべてのシンボル情報を削除し、必要に応じて、これらのシンボルを再読み込みします。 場合によっては、このコマンドも再読み込みまたはモジュール自体がアンロードされます。
ms.assetid: 750eb1a2-7af9-4f2d-81ca-9ea0fb157961
keywords:
- モジュール (.reload) コマンドを再読み込み
- シンボル、モジュールの再読み込み (.reload) コマンド
- .reload (モジュールの再読み込み) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .reload (Reload Module)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 36c3aba41ef95f9880ba5e1835c1b6a1392c069b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335738"
---
# <a name="reload-reload-module"></a>.reload (モジュールの再読み込み)


**.Reload**コマンドは、指定したモジュールのすべてのシンボル情報を削除し、必要に応じて、これらのシンボルを再読み込みします。 場合によっては、このコマンドも再読み込みまたはモジュール自体がアンロードされます。

```dbgcmd
.reload [Options] [Module[=Address[,Size[,Timestamp]]]] 
.reload -?
```

## <a name="span-idddkmetareloadmoduledbgspanspan-idddkmetareloadmoduledbgspanparameters"></a><span id="ddk_meta_reload_module_dbg"></span><span id="DDK_META_RELOAD_MODULE_DBG"></span>パラメーター


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
次のオプションのいずれか:

<span id="_d"></span><span id="_D"></span>**/d**  
デバッガーのモジュールの一覧のすべてのモジュールを再読み込みします。 (すべてのパラメーターを省略するとこのような状況は、既定のユーザー モードのデバッグ中に) です。

<span id="_f"></span><span id="_F"></span>**/f**  
デバッガーをすぐに、シンボルの読み込みを強制します。 このパラメーターはオーバーライド*シンボルの遅延読み込み*します。 詳細については、「解説」を参照してください。

<span id="_i"></span><span id="_I"></span>**/i**  
.Pdb ファイルのバージョンの不一致を無視します。 (このパラメーターを含めない場合、デバッガーは読み込みません不一致シンボル ファイル。)使用すると **/i**、 **/f**場合でも、明示的に指定しないことも、使用します。

<span id="_l"></span><span id="_L"></span>**/l**  
モジュールの一覧が、そのシンボルを再読み込みされません。 (カーネル モードでは、このパラメーターにより、同じ出力として、 [ **! ドライバー** ](-drivers.md)拡張機能です)。

<span id="_n"></span><span id="_N"></span>**/n**  
カーネルのシンボルのみを再読み込みします。 このパラメーターは、すべてのユーザーのシンボルを再読み込みされません。 (カーネル モードのデバッグ時にのみこのオプションを使用することができます)。

<span id="_o"></span><span id="_O"></span>**/o**  
上書きをシンボル サーバーのダウン ストリームのストア内のキャッシュ ファイルを強制します。 このフラグを使用する場合も含めます **/f**します。 既定では、ダウン ストリームのストアのファイルは上書きことはありません。

シンボル サーバーは、すべてのバイナリの別のビルドのシンボルの個別のファイル名を使用するため、ダウン ストリームのストアが破損すると思われる場合を除き、このオプションを使用することはありません。

<span id="_s"></span><span id="_S"></span>**/s**  
システムのモジュール イメージ リストのすべてのモジュールを再読み込みします。 (すべてのパラメーターを省略するとこのような状況は、既定のカーネル モードのデバッグ中に) です。

ユーザー モードのデバッグの実行中に名前で、個々 のシステム モジュールを読み込むの場合は、 **/s**します。

<span id="_u"></span><span id="_U"></span>**/u**  
指定したモジュールとそのすべてのシンボルをアンロードします。 デバッガーは、名前に一致するすべての読み込まれたモジュールをアンロード*モジュール*の完全なパスに関係なく、します。 イメージの名前も検索されます。 詳細については、次の「解説」セクションの注を参照してください。

<span id="_unl"></span><span id="_UNL"></span>**/unl**  
アンロードされたモジュールの一覧でイメージの情報に基づくシンボルを再読み込みします。

<span id="_user"></span><span id="_USER"></span>**/user**  
ユーザーのシンボルのみを再読み込みします。 (カーネル モードのデバッグ時にのみこのオプションを使用することができます)。

<span id="_v"></span><span id="_V"></span>**/v**  
詳細モードをオンにします。

<span id="_w"></span><span id="_W"></span>**/w**  
扱います*モジュール*としてリテラル文字列。 この処理は、デバッガーがワイルドカード文字を展開することを防ぎます。

<span id="_______Module______"></span><span id="_______module______"></span><span id="_______MODULE______"></span> *モジュール*   
ホスト コンピューター上のシンボルを再読み込みする対象のターゲット システム上の画像の名前を指定します。 *モジュール*ファイルの名前とファイル名拡張子を含める必要があります。 使用しない限り、 **/w**オプション、*モジュール*さまざまなワイルドカード文字と指定子を含めることができます。 構文の詳細については、次を参照してください。[文字列のワイルドカード構文](string-wildcard-syntax.md)します。 省略した場合*モジュール*の動作、 **.reload**コマンドによって異なりますが*オプション*を使用します。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
モジュールのベース アドレスを指定します。 通常がこのアドレスをイメージ ヘッダーが破損していますか、ページ アウトされた場合にのみ必要です。

<span id="_______Size______"></span><span id="_______size______"></span><span id="_______SIZE______"></span> *サイズ*   
モジュール イメージのサイズを指定します。 多くの状況では、デバッガーは、モジュールの適切なサイズを認識します。 デバッガーに適切なサイズを把握していないときに指定する必要があります*サイズ*します。 モジュールの実際のサイズまたはより多くの場合は、このサイズを指定できますが、サイズは小さい数をすることはできません。 通常がこのサイズをイメージ ヘッダーが破損していますか、ページ アウトされた場合にのみ必要です。

<span id="_______Timestamp______"></span><span id="_______timestamp______"></span><span id="_______TIMESTAMP______"></span> *タイムスタンプ*   
モジュール イメージのタイムスタンプを指定します。 多くの状況では、デバッガーは、モジュールの適切なタイムスタンプを認識します。 デバッガーにタイムスタンプを把握していないときに指定する必要があります*タイムスタンプ*します。 通常がこのタイムスタンプをイメージ ヘッダーが破損していますか、ページ アウトされた場合にのみ必要です。

**注**  間に空白が必要ない、*アドレス*、*サイズ*、および*タイムスタンプ*パラメーター。

 

<span id="_______-_______"></span> **-?**   
このコマンドの短いヘルプ テキストが表示されます。

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
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

遅延 (遅延) シンボルの読み込みの詳細については、次を参照してください。[シンボルの遅延読み込み](deferred-symbol-loading.md)します。 その他のシンボルのオプションの詳細については、次を参照してください。[シンボル オプションを設定](symbol-options.md)します。

<a name="remarks"></a>コメント
-------

**.Reload**コマンドでは、シンボル情報を読み取るは発生しません。 代わりに、このコマンドにより、デバッガーは、シンボル ファイルが変更された可能性があることや、モジュールの一覧に新しいモジュールを追加する必要があります。 このコマンドは、そのモジュールの一覧を修正して、指定されたモジュールのシンボル情報を削除するデバッガーを実行します。 情報が必要になるまで、実際のシンボル情報は、個々 の .pdb ファイルから読み取ることです。 (このタイプの読み込みと呼ばれる*シンボルの遅延読み込み*または*シンボルの読み込みの遅延*)。

使用して発生するシンボルの読み込みを強制することができます、 **/f**オプションまたは発行して、 [ **%ld (シンボルの読み込み)** ](ld--load-symbols-.md)コマンド。

**.Reload**コマンドは、システムが (つまり、クラッシュ) の応答を停止した場合に役立ちます。 シンボルは、デバッグ対象のコンピュータに対してが失われる原因となります。 コマンドは、シンボルのツリーを更新した場合に役立ちます。 ことができます。

使用してシンボルが正しく読み込むことができる場合、イメージ ヘッダーでは、アンロードされているモジュールなど、何らかの理由が正しくないか、ページ アウトされた、 **/unl**引数、または両方を指定する*アドレス*と*サイズ*します。

**.Reload/u**コマンドは、広範な検索を実行します。 デバッガーが最初に一致を試みます*モジュール*は正確なモジュール名、パスに関係なく。 デバッガーは、この一致を見つけられない場合*モジュール*は読み込まれたイメージの名前として扱われます。 たとえば、メモリ内にある HAL に halacpi.dll のモジュール名がある場合は、次のコマンドのどちらもそのシンボルをアンロードします。

```dbgcmd
kd> .reload /u halacpi.dll

kd> .reload /u hal
```

ターゲット アプリケーションのモジュールの一覧の一部でないユーザー モードのデバッグを実行してモジュールをロードする場合は、含める必要があります、 **/s**オプションを次の例を示します。

```dbgcmd
0:000> .reload /u ntdll.dll
Unloaded ntdll.dll

0:000> .reload /s /f ntdll.dll
```

 

 





