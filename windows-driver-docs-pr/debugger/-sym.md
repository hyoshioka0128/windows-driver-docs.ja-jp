---
title: sym
description: ノイズの多い sym 拡張機能コントロールはシンボルの読み込みとシンボルのプロンプトです。
ms.assetid: 84551b24-740c-4289-acc4-8a0053f80b41
keywords:
- シンボル、ノイズの多いシンボルの読み込み
- シンボル、画面の指示
- Windows デバッグ sym
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- sym
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8d83a66e563f5e3022f311c93d06593d51d929d2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338774"
---
# <a name="sym"></a>!sym


**! Sym**拡張コントロールのノイズの多いシンボルの読み込みとシンボルのプロンプト。

```dbgcmd
!sym 
!sym noisy 
!sym quiet 
!sym prompts 
!sym prompts off
```

## <a name="span-idddksymdbgspanspan-idddksymdbgspanparameters"></a><span id="ddk__sym_dbg"></span><span id="DDK__SYM_DBG"></span>パラメーター


<span id="_______noisy______"></span><span id="_______NOISY______"></span> **ノイズの多い**   
ノイズの多いシンボルの読み込みを有効にします。

<span id="_______quiet______"></span><span id="_______QUIET______"></span> **通知の停止**   
ノイズの多いシンボルの読み込みを無効になります。

<span id="_______prompts______"></span><span id="_______PROMPTS______"></span> **メッセージが表示されます。**   
SymSrv 認証要求を受信したときに表示されるダイアログ ボックスの認証を許可します。

<span id="_______prompts_off______"></span><span id="_______PROMPTS_OFF______"></span> **オフ メッセージが表示されます。**   
SymSrv 認証要求を受信したときに、すべての認証ダイアログ ボックスを抑制します。 これにより、インターネット経由でのシンボルをアクセスすることができません SymSrv 可能性があります。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Dbghelp.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Dbghelp.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

場合、 **! sym**引数なしで拡張機能が使用される、ノイズの多いシンボルの読み込みとシンボルのプロンプトの現在の状態が表示されます。

**! Sym ノイズの多い**と **! sym quiet**拡張機能は、ノイズの多いシンボルの読み込みを制御します。 詳細については、および、他のメソッドを表示して、このオプションを変更するのには、「 [SYMOPT\_デバッグ](symbol-options.md#symopt-debug)します。

**! Sym が求められます**と **! オフ sym が求められます**拡張機能は、SymSrv 認証要求を検出すると、認証ダイアログが表示されるかどうかを制御します。 これらのコマンドの後に[ **.reload (モジュールの再読み込み)** ](-reload--reload-module-.md)を有効にします。 プロキシ サーバー、インターネット ファイアウォール、スマート カード リーダー、およびセキュリティで保護された web サイトでは、認証要求を送信できます。 詳細については、および、このオプションを変更するには、他のメソッドには、「[ファイアウォールとプロキシ サーバー](firewalls-and-proxy-servers.md)します。

**注**  ノイズの多いシンボルの読み込みする必要がありますと混同しない--によって制御されるノイズの多いソースの読み込み、 [ **(ノイズの多いソースの読み込み) .srcnoisy** ](-srcnoisy--noisy-source-loading-.md)コマンド。

 

 

 





