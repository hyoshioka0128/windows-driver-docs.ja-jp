---
title: クライアント オブジェクト
description: クライアント オブジェクト
ms.assetid: 173a67f1-093e-4462-8e2c-41d0f10106d0
keywords:
- デバッガーエンジン、クライアントオブジェクト
- クライアントオブジェクト
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15b22ddb8039fe1c602be46b9e82e1dac10a644e
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242823"
---
# <a name="client-objects"></a>クライアント オブジェクト


## <span id="client-objects"></span><span id="CLIENT_OBJECTS"></span>


ほとんどの場合、[デバッガーエンジン](introduction.md#debugger-engine)とのやり取りは*クライアントオブジェクト*を介して行われ、多くの場合 *、クライアントと呼ばれます。* 各クライアントには、最上位レベルのエンジンインターフェイスの実装が用意されています。 各インターフェイスには、さまざまなメソッドが用意されています。これらのメソッドを使用して、エンジンや、エンジン (ターゲット) を操作できます。 エンジンのインスタンスは、それぞれが独自の状態を持つ多数のクライアントを持つことができます。

### <a name="span-idprimary-clientsspanspan-idprimary_clientsspanprimary-clients"></a><span id="primary-clients"></span><span id="PRIMARY_CLIENTS"></span>プライマリクライアント

*プライマリクライアント*は、現在のデバッグセッションに参加しているクライアントです。 初期状態では、新しいクライアントオブジェクトが作成されると、プライマリクライアントではなくなります。 クライアントがターゲットを取得するために使用される場合 (たとえば、 [**CreateProcess2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocess2)を呼び出すことによって)、または[**connectsession**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-connectsession)を使用してデバッグセッションに接続されている場合は、クライアントがプライマリクライアントになります。 デバッガーコマンド。クライアントには、プライマリクライアントのみが表示され[**ます。** ](-clients--list-debugging-clients-.md)

### <a name="span-idcallback-objectsspanspan-idcallback_objectsspancallback-objects"></a><span id="callback-objects"></span><span id="CALLBACK_OBJECTS"></span>コールバックオブジェクト

コールバックオブジェクトは、各クライアントに登録できます。 コールバックオブジェクトには、次の3種類があります。

1.  **入力コールバックオブジェクト**(または*入力コールバック*): エンジンは入力コールバックを呼び出して入力を要求します。 たとえば、コンソールウィンドウがあるデバッガーは、入力コールバックを登録してユーザーからの入力をエンジンに提供したり、デバッガーが入力コールバックを登録して、エンジンにファイルからの入力を提供したりする可能性があります。

2.  **出力コールバックオブジェクト**(または*出力コールバック*): エンジンは、出力を表示するための出力コールバックを呼び出します。 たとえば、コンソールウィンドウがあるデバッガーでは、出力コールバックを登録してユーザーにデバッガーの出力を表示することも、出力をログファイルに送信するための出力コールバックをデバッガーで登録することもできます。

3.  **イベントコールバックオブジェクト**(または*イベントコールバック*): エンジンは、ターゲットでイベントが発生するたびにイベントコールバックを呼び出します (またはエンジンの状態が変更されている場合)。 たとえば、デバッガー拡張ライブラリは、特定のイベントを監視したり、特定のイベントが発生したときに自動アクションを実行したりするために、イベントコールバックを登録できます。

### <a name="span-idremote-debuggingspanspan-idremote_debuggingspanremote-debugging"></a><span id="remote-debugging"></span><span id="REMOTE_DEBUGGING"></span>リモートデバッグ

クライアントオブジェクトは、ホストエンジンのリモートインスタンスへの通信を容易にします。 [**Debugconnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-debugconnect)関数は、リモートエンジンインスタンスに接続されているクライアントオブジェクトを作成します。このクライアントで呼び出されたメソッドはリモートエンジンによって実行され、クライアントとローカルに登録されたコールバックオブジェクトは、リモートエンジンがコールバック呼び出しを行うときに呼び出されます。

### <a name="span-idadditional-informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional-information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

クライアントオブジェクトの作成と使用の詳細については、「[コールバックオブジェクトの使用](using-callback-objects.md)」を参照してください。 コールバックオブジェクトの登録の詳細については、「コールバックオブジェクトの使用」を参照してください。

 

 





