---
title: .pagein (メモリ内のページ)
description: メモリの指定した領域に .pagein コマンド ページ。
ms.assetid: 5fb8f9d2-d07a-49c3-b844-aade9bdba367
keywords:
- メモリ内のページ (.pagein) コマンド
- メモリ、メモリ内のページ (.pagein) コマンド
- .pagein (メモリ内のページ) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .pagein (Page In Memory)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5b9f6f6126d3d0ff439bbfe212c6c431ab1476a1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559916"
---
# <a name="pagein-page-in-memory"></a>.pagein (メモリ内のページ)


**.Pagein**メモリの指定した領域内のページをコマンドします。

```dbgcmd
.pagein [Options] Address
```

## <a name="span-idddkmetapageinmemorydbgspanspan-idddkmetapageinmemorydbgspanparameters"></a><span id="ddk_meta_page_in_memory_dbg"></span><span id="DDK_META_PAGE_IN_MEMORY_DBG"></span>パラメーター


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
次のオプションのいずれか:

<span id="_p_Process"></span><span id="_p_process"></span><span id="_P_PROCESS"></span>**/p** **** *プロセス*  
ページにするメモリを所有するプロセスのアドレスを指定します。 (正確には、このパラメーターは、プロセスの」プロセス ブロックのアドレスを指定します。)省略した場合*プロセス*または 0 の場合、デバッガーは使用して設定の現在のプロセスを指定します。 プロセスの設定の詳細については、次を参照してください[ **.process (プロセス コンテキストの設定)。**](-process--set-process-context-.md)

<span id="_f"></span><span id="_F"></span>**/f**  
カーネル メモリにアドレスがあり、Microsoft Windows オペレーティング システムのバージョンがこの操作をサポートしていない場合でも、ページング メモリを強制します。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
内のページにアドレスを指定します。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>カーネル モードのみ (ただしローカル カーネル デバッグ中ではなく)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ デバッグのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

実行した後、 **.pagein**コマンドを使用する必要があります、 [ **g (移動)** ](g--go-.md)プログラムの実行を再開するコマンド。 簡単な後は、ターゲット コンピューターに自動的にデバッガーを中断もう一度です。

この時点で指定したアドレスがページします。 使用する場合、 **/p**オプション、プロセスのコンテキストが設定も指定のプロセスに使用した場合とまったく同様、 [ **.process/i プロセス**](-process--set-process-context-.md)コマンド。

アドレスが、既にページングされた場合、 **.pagein**コマンドもであるか、アドレスでページングがデバッガーに中断されます。 アドレスが有効でない場合、このコマンドはデバッガーにのみ中断します。

使用して Windows Server 2003 および Windows XP では、ユーザー モード アドレスだけでページできます **.pagein**します。 この制限を使用してオーバーライドすることができます、 **/f**スイッチがこのスイッチを使用することがお勧めしません。 Windows Vista で安全にユーザー モードとカーネル モードのメモリ内ページことができます。

**警告**  を使用する場合 **.pagein** Windows Server 2003 または Windows XP でのカーネル スタック内のアドレス、バグ チェックが発生する可能性があります。

 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows XP および Windows の以降のバージョンでサポートされています。</p></td>
</tr>
</tbody>
</table>

 

 





