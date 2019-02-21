---
title: セッション
description: セッションの拡張機能は、セッションのコンテキストを制御します。 すべてのユーザー セッションの一覧を表示することもできます。
ms.assetid: c5f32bf0-59b5-4274-9271-1ad4913ffa1a
keywords:
- Windows のデバッグ セッション
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- session
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c51bf0bc2461d62f62e7ad2fc2a639b2e4e02eea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553028"
---
# <a name="session"></a>! セッション


**! セッション**拡張機能は、セッションのコンテキストを制御します。 すべてのユーザー セッションの一覧を表示することもできます。

構文

```dbgcmd
!session 
!session -s DefaultSession 
!session -?
```

## <a name="span-idddksessiondbgspanspan-idddksessiondbgspanparameters"></a><span id="ddk__session_dbg"></span><span id="DDK__SESSION_DBG"></span>パラメーター


<span id="_______-s_______DefaultSession______"></span><span id="_______-s_______defaultsession______"></span><span id="_______-S_______DEFAULTSESSION______"></span> **-s** **** *DefaultSession*   
セット、[セッション コンテキスト](changing-contexts.md#session-context)指定された値。 場合*DefaultSession* -1 の場合は、コンテキストが現在のセッションに設定されているセッションです。

<span id="_______-_______"></span> **-?**   
この拡張機能のデバッガー コマンド ウィンドウでヘルプを表示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ユーザー セッションとセッション マネージャ (smss.exe) については、次を参照してください。 *Microsoft Windows internals 』*、Mark Russinovich と David Solomon します。

<a name="remarks"></a>注釈
-------

**! セッション**セッション コンテキストを制御する拡張機能を使用します。 使用して **! セッション**パラメーターなしのリストが表示されます、アクティブなセッションのターゲット コンピューターにします。 使用して **! セッション/s** *DefaultSession*セッションのコンテキストを新しい既定値に変更されます。

そのセッションのプロセスのコンテキストが自動的に変更、アクティブなプロセスにセッションのコンテキストを設定すると、 [ **.cache forcedecodeptes** ](-cache--set-cache-size-.md)セッション アドレスが実行されるため、オプションが有効になっています。正しく変換します。

詳細については、セッションのコンテキストの影響を受けるすべてのセッション関連の拡張機能の一覧を参照してください。[変更コンテキスト](changing-contexts.md)します。

 

 





