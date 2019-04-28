---
title: DbEngPrx のコマンドライン オプション
description: DbEngPrx コマンドラインは、次の構文を使用します。
ms.assetid: 3c0675a4-93f0-4aaa-9f33-9a45c48c1ff4
keywords:
- DbEngPrx コマンド ライン オプションの Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DbEngPrx Command-Line Options
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1953578fa35e04c602c37dc70e07f8979ccd38aa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374946"
---
# <a name="dbengprx-command-line-options"></a>DbEngPrx のコマンドライン オプション


DbEngPrx コマンドラインは、次の構文を使用します。

```dbgcmd
dbengprx [-p] -c ClientTransport -s ServerTransport 

dbengprx -? 
```

## <a name="span-idddkdbengprxcommandlineoptionsdbgspanspan-idddkdbengprxcommandlineoptionsdbgspanparameters"></a><span id="ddk_dbengprx_command_line_options_dbg"></span><span id="DDK_DBENGPRX_COMMAND_LINE_OPTIONS_DBG"></span>パラメーター


<span id="_______-p______"></span><span id="_______-P______"></span> **-p**   
既存のすべての接続を削除した後も引き続き DbEngPrx をによりします。

<span id="_______-c_______ClientTransport______"></span><span id="_______-c_______clienttransport______"></span><span id="_______-C_______CLIENTTRANSPORT______"></span> **-c** *ClientTransport*   
サーバーへの接続に使用するプロトコル設定を指定します。 プロトコルは、サーバーの作成時に使用と一致する必要があります。 詳細については、次を参照してください。 [ **Repeater をアクティブ化する**](activating-a-repeater.md)します。

<span id="_______-s_______ServerTransport______"></span><span id="_______-s_______servertransport______"></span><span id="_______-S_______SERVERTRANSPORT______"></span> **-s** *サーバトランスポート*   
クライアントは、repeater に接続するときに使用されるプロトコルの設定を指定します。 詳細については、次を参照してください。 [ **Repeater をアクティブ化する**](activating-a-repeater.md)します。

<span id="_______-_______"></span> **-?**   
DbEngPrx コマンドラインのヘルプ テキストを含むメッセージ ボックスが表示されます。

DbEngPrx の使用方法の詳細については、次を参照してください。[リピータ](repeaters.md)します。

 

 





