---
title: .cache (キャッシュ サイズの設定)
description: .Cache コマンドでは、ターゲットから取得したデータを保持するために使用される、キャッシュのサイズを設定します。 また多くのキャッシュとメモリのオプションを設定します。
ms.assetid: 638cb2e6-b333-4311-967c-d86c2e93b4ec
keywords:
- .cache (キャッシュ サイズの設定) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .cache (Set Cache Size)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7c7cac5f40151f3d11a1de2dbd04e7621863fc0d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571311"
---
# <a name="cache-set-cache-size"></a>.cache (キャッシュ サイズの設定)


**.Cache**コマンドは、ターゲットから取得したデータを保持するために使用される、キャッシュのサイズを設定します。 また多くのキャッシュとメモリのオプションを設定します。

```dbgsyntax
.cache Size 
.cache Option 
.cache 
```

## <a name="span-idddkmetasetcachesizedbgspanspan-idddkmetasetcachesizedbgspanparameters"></a><span id="ddk_meta_set_cache_size_dbg"></span><span id="DDK_META_SET_CACHE_SIZE_DBG"></span>パラメーター


<span id="_______Size______"></span><span id="_______size______"></span><span id="_______SIZE______"></span> *サイズ*   
カーネル デバッグ (キロバイト単位) のキャッシュのサイズ。 場合*サイズ*0 の場合は、キャッシュが無効になっています。 コマンドの出力では、キャッシュ サイズを表示します (バイト単位)。 (既定のサイズは 1,000 KB です)。

<span id="_______Option______"></span><span id="_______option______"></span><span id="_______OPTION______"></span> *オプション*   
次のオプションのいずれかを指定できます。

<span id="hold"></span><span id="HOLD"></span>**保留中**  
自動キャッシュのフラッシュが無効です。

<span id="unhold"></span><span id="UNHOLD"></span>**保持解除します。**  
オフ、**保持**オプション。 (これは、既定の設定です)。

<span id="decodeptes"></span><span id="DECODEPTES"></span>**decodeptes**  
すべての遷移のページ テーブル エントリ (Pte) は、暗黙的にデコードされたになります。 (これは、既定の設定です)。

<span id="nodecodeptes"></span><span id="NODECODEPTES"></span>**nodecodeptes**  
オフ、 **decodeptes**オプション。

<span id="forcedecodeptes"></span><span id="FORCEDECODEPTES"></span>**forcedecodeptes**  
すべての仮想アドレスは、アクセスする前に、物理アドレスに変換されます。 このオプションによって、キャッシュを無効にします。 使用する方が効率的ではカーネル モード メモリに懸念がある場合を除き、 **forcedecodeuser**代わりにします。

<span id="forcedecodeuser"></span><span id="FORCEDECODEUSER"></span>**forcedecodeuser**  
すべてのユーザー モード仮想アドレスは、アクセスする前に、物理アドレスに変換されます。 このオプションによって、キャッシュを無効にします。

**注**  アクティブ化する必要があります**forcedecodeuser** (または**forcedecodeptes**) を使用する前に[ **.thread (登録コンテキストの設定)** ](-thread--set-register-context-.md)、 [ **.context (ユーザー モード アドレス コンテキストの設定)**](-context--set-user-mode-address-context-.md)、 [ **.process (プロセス コンテキストの設定)**](-process--set-process-context-.md)、または[ **! セッション**](-session.md)ライブ デバッグ中にします。 使用する場合、 **/p**オプションと **.thread**と **.process**、 **forcedecodeuser**オプションが自動的に設定します。 それ以外の場合に使用する必要があります、 **.cache forcedecodeuser**コマンドが明示的にします。

 

<span id="noforcedecodeptes"></span><span id="NOFORCEDECODEPTES"></span>**noforcedecodeptes**  
オフ、 **forcedecodeptes**と**forcedecodeuser**オプション。 (これは、既定の設定です)。

<span id="flushall"></span><span id="FLUSHALL"></span>**flushall**  
全体の仮想メモリ キャッシュを削除します。

<span id="flushu"></span><span id="FLUSHU"></span>**flushu**  
ユーザー モードのすべてのエントリと同様に、キャッシュからのエラーのある範囲のすべてのエントリを削除します。

<span id="flush_Address"></span><span id="flush_address"></span><span id="FLUSH_ADDRESS"></span>**フラッシュ***アドレス*  
以降、キャッシュの 4096 バイトのブロックを削除します。*アドレス*します。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>カーネル モードのみ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ デバッグのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

場合 **.cache**引数なしでは、現在のキャッシュ サイズ、状態、と共に使用し、オプションが表示されます。

**.Cache forcedecodeuser**または **.cache forcedecodeptes**オプションのみデバッガーが機能しなくなります先のコンピューターにします。 ステップまたはターゲットの実行が実行する場合、 **noforcedecodeptes**状態は再度有効になります。 これは、デバッガーが非生産的な方法で実行または再起動に干渉することを防ぎます。

 

 





