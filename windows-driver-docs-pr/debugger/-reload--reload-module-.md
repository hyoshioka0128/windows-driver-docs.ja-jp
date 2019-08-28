---
title: .reload (モジュールの再読み込み)
description: Reload コマンドは、指定されたモジュールのすべてのシンボル情報を削除し、必要に応じてこれらのシンボルを再度読み込みます。 場合によっては、このコマンドによってモジュール自体が再読み込みまたはアンロードされることもあります。
ms.assetid: 750eb1a2-7af9-4f2d-81ca-9ea0fb157961
keywords:
- リロード (モジュールの再読み込み) コマンド
- シンボル、再読み込みモジュール (. リロード) コマンド
- 。再読み込み (モジュールの再読み込み) Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .reload (Reload Module)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 610f495e4b7e77307a9a01f796608e272f64e0fc
ms.sourcegitcommit: 238308264c1ee2c74ec0c8c303258dc00c79b902
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2019
ms.locfileid: "70063892"
---
# <a name="reload-reload-module"></a>.reload (モジュールの再読み込み)


Reload コマンドは、指定されたモジュールのすべてのシンボル情報を削除し、必要に応じてこれらのシンボルを再度読み込み**ます。** 場合によっては、このコマンドによってモジュール自体が再読み込みまたはアンロードされることもあります。

```dbgcmd
.reload [Options] [Module[=Address[,Size[,Timestamp]]]] 
.reload -?
```

## <a name="span-idddk_meta_reload_module_dbgspanspan-idddk_meta_reload_module_dbgspanparameters"></a><span id="ddk_meta_reload_module_dbg"></span><span id="DDK_META_RELOAD_MODULE_DBG"></span>パラメータ


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*オプション*   
次のオプションのいずれかを選択します。

<span id="_d"></span><span id="_D"></span>**d**  
デバッガーのモジュール一覧にあるすべてのモジュールを再読み込みします。 (すべてのパラメーターを省略した場合、この状況はユーザーモードのデバッグ時の既定値になります)。

<span id="_f"></span><span id="_F"></span> **/f**  
デバッガーが強制的にシンボルを読み込むようにします。 このパラメーターは、*遅延シンボルの読み込み*をオーバーライドします。 詳細については、「解説」を参照してください。

<span id="_i"></span><span id="_I"></span> **/i**  
.Pdb ファイルバージョンの不一致を無視します。 (このパラメーターを含めない場合、デバッガーは一致しないシンボルファイルを読み込みません。) **/I**を使用する場合は、明示的に指定しない場合でも、 **/f**が使用されます。

<span id="_l"></span><span id="_L"></span> **/l**  
モジュールを一覧表示しますが、シンボルを再読み込みしません。 (カーネルモードでは、このパラメーターは、 [**lm**](lm--list-loaded-modules-.md)コマンドに似た出力を提供します)。

<span id="_n"></span><span id="_N"></span>**ms-dos**  
カーネルシンボルのみを再読み込みします。 このパラメーターでは、ユーザーシンボルは再読み込みされません。 (このオプションは、カーネルモードのデバッグ中にのみ使用できます)。

<span id="_o"></span><span id="_O"></span> **/o**  
シンボルサーバーのダウンストリームストア内のキャッシュされたファイルを強制的に上書きします。 このフラグを使用する場合は、 **/f**も含める必要があります。 既定では、ダウンストリームストアファイルは上書きされません。

シンボルサーバーでは、バイナリの各ビルドのシンボルに対して個別のファイル名が使用されるため、ダウンストリームストアが破損していると思われる場合を除き、このオプションを使用する必要はありません。

<span id="_s"></span><span id="_S"></span> **/s**  
システムのモジュールイメージリスト内のすべてのモジュールを再読み込みします。 (すべてのパラメーターを省略した場合、カーネルモードのデバッグ中は、この状況が既定値になります)。

ユーザーモードのデバッグを実行しているときに、名前を指定して個々のシステムモジュールを読み込む場合は、 **/s**を含める必要があります。

<span id="_u"></span><span id="_U"></span> **/u**  
指定したモジュールとそのすべてのシンボルをアンロードします。 デバッガーは、完全パスに関係なく、*モジュール*に一致する名前を持つ読み込み済みモジュールをアンロードします。 イメージ名も検索されます。 詳細については、次の「解説」のメモを参照してください。

<span id="_unl"></span><span id="_UNL"></span> **/unl**  
アンロードされたモジュールの一覧のイメージ情報に基づいてシンボルを再読み込みします。

<span id="_user"></span><span id="_USER"></span> **/user**  
ユーザーシンボルのみを再読み込みします。 (このオプションは、カーネルモードのデバッグ中にのみ使用できます)。

<span id="_v"></span><span id="_V"></span> **/v**  
詳細モードをオンにします。

<span id="_w"></span><span id="_W"></span> **/w**  
*モジュール*をリテラル文字列として扱います。 この処理により、デバッガーはワイルドカード文字を展開できなくなります。

<span id="_______Module______"></span><span id="_______module______"></span><span id="_______MODULE______"></span>*モジュール*   
ホストコンピューター上のシンボルを再読み込みするターゲットシステム上のイメージの名前を指定します。 *モジュール*には、ファイルの名前とファイル名拡張子を含める必要があります。 **/W**オプションを使用しない限り、*モジュール*にはさまざまなワイルドカード文字と指定子が含まれている可能性があります。 構文の詳細については、「[文字列ワイルドカード構文](string-wildcard-syntax.md)」を参照してください。 *Module*を省略した場合、使用する*オプション*によって、reload コマンドの動作が異なり**ます。**

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*アドレス*   
モジュールのベースアドレスを指定します。 通常、このアドレスは、イメージヘッダーが破損しているか、ページアウトされている場合にのみ必要です。

<span id="_______Size______"></span><span id="_______size______"></span><span id="_______SIZE______"></span>*サイズ*   
モジュールイメージのサイズを指定します。 多くの場合、デバッガーはモジュールの正しいサイズを認識しています。 デバッガーが正しいサイズを把握していない場合は、*サイズ*を指定する必要があります。 このサイズは、実際のモジュールサイズまたはそれより大きい数値にすることができますが、サイズを小さくすることはできません。 通常、このサイズは、イメージヘッダーが破損しているか、ページアウトされている場合にのみ必要です。

<span id="_______Timestamp______"></span><span id="_______timestamp______"></span><span id="_______TIMESTAMP______"></span>*タイムスタンプ*   
モジュールイメージのタイムスタンプを指定します。 多くの場合、デバッガーはモジュールの正しいタイムスタンプを認識します。 デバッガーがタイムスタンプを認識しない場合は、*タイムスタンプ*を指定する必要があります。 通常、このタイムスタンプは、イメージヘッダーが破損しているか、ページアウトされている場合にのみ必要です。

**注** Address、Size、および Timestamp パラメーターの間に空白を入れることはできません。  

 

<span id="_______-_______"></span> **-?**    
このコマンドの短いヘルプテキストを表示します。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>Environment

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザーモード、カーネルモード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>・</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

遅延 (レイジー) シンボルの読み込みの詳細については、「[遅延シンボルの読み込み](deferred-symbol-loading.md)」を参照してください。 その他のシンボルオプションの詳細については、「[シンボルオプションの設定](symbol-options.md)」を参照してください。

<a name="remarks"></a>コメント
-------

**Reload**コマンドを実行しても、シンボル情報は読み込まれません。 代わりに、このコマンドを使用すると、シンボルファイルが変更された可能性があること、または新しいモジュールをモジュールリストに追加する必要があることがデバッガーに通知されます。 このコマンドを実行すると、デバッガーはモジュールリストを修正し、指定されたモジュールのシンボル情報を削除します。 実際のシンボル情報は、情報が必要になるまで個々の .pdb ファイルからは読み取られません。 (この読み込みの種類は、*遅延シンボルの読み込み*または*遅延シンボルの読み込み*と呼ばれます)。

**/F**オプションを使用するか、 [**Ld (読み込みシンボル)** ](ld--load-symbols-.md)コマンドを発行することにより、シンボルの読み込みを強制的に実行できます。

Reload コマンドは、システムが応答しなくなった場合 (つまりクラッシュ)、デバッグ中の対象コンピューターのシンボルが失われる可能性がある場合に便利です **。** このコマンドは、シンボルツリーを更新した場合にも役立ちます。

何らかの理由でイメージヘッダーが正しくない場合 (アンロードされているモジュールやページアウトされている場合など)、 **/unl**引数を使用するか、*アドレス*と*サイズ*の両方を指定することで、シンボルを正しく読み込むことができます。

**. Reload/u**コマンドは、広範な検索を実行します。 デバッガーは、パスに関係なく、最初に*モジュール*と完全に一致するモジュール名を照合しようとします。 デバッガーがこの一致を見つけることができない場合、*モジュール*は読み込まれたイメージの名前として扱われます。 たとえば、メモリに格納されている HAL のモジュール名が halacpi の場合、次のコマンドの両方でシンボルがアンロードされます。

```dbgcmd
kd> .reload /u halacpi.dll

kd> .reload /u hal
```

ユーザーモードのデバッグを実行していて、ターゲットアプリケーションのモジュール一覧に含まれていないモジュールを読み込む場合は、次の例に示すように、 **/s**オプションを含める必要があります。

```dbgcmd
0:000> .reload /u ntdll.dll
Unloaded ntdll.dll

0:000> .reload /s /f ntdll.dll
```

 

 





