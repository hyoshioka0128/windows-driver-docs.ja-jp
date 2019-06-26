---
title: クライアント オブジェクト
description: クライアント オブジェクト
ms.assetid: 173a67f1-093e-4462-8e2c-41d0f10106d0
keywords:
- デバッガー エンジンでは、クライアント オブジェクト
- クライアント オブジェクト
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2c0482dc75eafefc504966c53fb753aa349f27c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367018"
---
# <a name="client-objects"></a>クライアント オブジェクト


## <span id="client-objects"></span><span id="CLIENT_OBJECTS"></span>


ほぼすべての対話、[デバッガー エンジン](introduction.md#debugger-engine)は*クライアント オブジェクト*、多くの場合、単に呼ば*クライアント*。 各クライアントは、最上位のエンジンのインターフェイスの実装を提供します。 各インターフェイスでは、エンジンと、ターゲット、エンジンを操作するために使用するには、メソッドの別のセットを提供します。 エンジンのインスタンスには、多くのクライアントがそれぞれ独自の状態を持つことができます。

### <a name="span-idprimary-clientsspanspan-idprimaryclientsspanprimary-clients"></a><span id="primary-clients"></span><span id="PRIMARY_CLIENTS"></span>主なクライアント

A*プライマリ クライアント*は現在参加して、クライアントではデバッグ セッション。 最初に、新しいクライアント オブジェクトが作成されると、そのクライアントではないプライマリです。 クライアントは、ターゲットを取得する際にプライマリのクライアントになります (呼び出すことによって、たとえば、 [ **CreateProcess2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-createprocess2)) を使用してデバッグ セッションに接続されているまたは[ **ConnectSession**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-connectsession)します。 デバッガー コマンド[ **.clients** ](-clients--list-debugging-clients-.md)主なクライアントのみを一覧表示されます。

### <a name="span-idcallback-objectsspanspan-idcallbackobjectsspancallback-objects"></a><span id="callback-objects"></span><span id="CALLBACK_OBJECTS"></span>コールバック オブジェクト

コールバック オブジェクトは、各クライアントを登録することができます。 コールバック オブジェクトの 3 つの種類があります。

1.  **コールバック オブジェクトを入力**(または*入力コールバック*): エンジンは入力を要求する入力のコールバックを呼び出します。 たとえば、コンソール ウィンドウで、デバッガーは、ユーザーからの入力に、エンジンを提供する入力のコールバックを登録でしたまたはデバッガーがファイルからの入力に、エンジンを提供する入力のコールバックを登録します。

2.  **コールバック オブジェクトを出力**(または*コールバックを出力*): エンジンは出力を表示する出力のコールバックを呼び出します。 たとえば、コンソール ウィンドウで、デバッガーが登録する、ユーザーに、デバッガーの出力を表示する出力のコールバックをやデバッガーは、出力ログ ファイルを送信する出力のコールバックを登録可能性があります。

3.  **イベントのコールバック オブジェクト**(または*イベント コールバック*): ターゲットのイベントが発生した (または、エンジンの状態の変更がある) されるたびに、エンジンはイベント コールバックを呼び出します。 たとえば、デバッガー拡張機能ライブラリは、イベント コールバックを特定のイベントを監視したり、特定のイベントが発生したときに、自動化されたアクションを実行したりを登録するでした。

### <a name="span-idremote-debuggingspanspan-idremotedebuggingspanremote-debugging"></a><span id="remote-debugging"></span><span id="REMOTE_DEBUGGING"></span>リモート デバッグ

クライアント オブジェクトには、ホストのエンジンのリモート インスタンスへの通信が容易になります。 [ **DebugConnect** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-debugconnect)関数は、リモート エンジンのインスタンスに接続されているクライアント オブジェクトを作成しますこのクライアントで呼び出されたメソッドが登録されているリモート エンジンとコールバック オブジェクトによって実行されます。ローカル クライアントのときに呼び出されますリモート エンジンはコールバックの呼び出しを行います。

### <a name="span-idadditional-informationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional-information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

作成して、クライアント オブジェクトの使用に関する詳細については、次を参照してください。[コールバック オブジェクトを使用する](using-callback-objects.md)します。 コールバック オブジェクトの登録方法の詳細については、コールバック オブジェクトを使用するを参照してください。

 

 





