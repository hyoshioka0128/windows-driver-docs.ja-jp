---
title: デバイス制御のシナリオ
description: デバイス制御のシナリオ
ms.assetid: 9effc192-77ef-40fd-9ab6-564637019576
keywords:
- WSDBIT ツール WDK、テスト シナリオ
- WSDAPI 基本的な相互運用性ツール WDK、テスト シナリオ
- WDK WSDBIT のシナリオ
- WDK WSDBIT のシナリオをテストします。
- デバイス管理シナリオ WDK WSDBIT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7b65200abae6c0a230bc3333e8d37b8105aa7bf
ms.sourcegitcommit: 289b5f97aff1b9ea1fefc9a8731e0fc16533073b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2019
ms.locfileid: "67492518"
---
# <a name="device-control-scenarios"></a>デバイス制御のシナリオ


デバイスの制御のシナリオでは、単純な SOAP メッセージの交換をテストします。

このシナリオでの目標は、ホストされるサービス エンドポイントの検出ではありません。 このシナリオでは、これらのエンドポイントの検出またはこのシナリオの前に指定された前提としています。 このシナリオでは、これらのエンドポイントがある物理ネットワークのアドレス指定可能な必要。 詳細についてでの初期テスト デバイス設定のダイアグラムを参照してください。[テスト環境の WSDBIT](wsdbit-testing-environment.md)します。

クライアント アクション サーバー アクションの不合格条件の場合**2.1**

**OneWay メソッド**

2.1.1

呼び出し、 **OneWay**で SimpleService のメソッド。

-   **wsa:Action == http:\//schemas.example.org/SimpleService/OneWay**

-   Http:\//testdevice.interop/SimpleService1 サービスが使用されます。

-   整数の入力が提供されます。

受信した整数を表示、 **OneWay**メソッド。

送信された、整数は、表示された整数です。

**2.2**

**TwoWay メソッド**

2.2.1

呼び出し、 **TwoWay**で SimpleService のメソッド。

-   **wsa:Action == http:\//schemas.example.org/SimpleService/TwoWayRequest**

-   Http:\//testdevice.interop/SimpleService1 サービスが使用されます。

-   2 つの整数の入力を指定します。

使用して、クライアントに応答、 **TwoWayResponse**メソッド。

-   **wsa:Action == http:\//schemas.example.org/SimpleService/TwoWayResponse**

-   合計パラメーターは、2 つの入力パラメーターの合計から計算されます。

クライアントが受信した合計パラメーターがで送信された整数値の合計では実際、 **TwoWay**メソッド。

**2.3**

**入力メソッド**

2.3.1

呼び出し、**入力**で SimpleService のメソッド。

-   **wsa:Action == http:\//schemas.example.org/SimpleService/TypeCheckRequest**

-   Http:\//testdevice.interop/SimpleService1 サービスが使用されます。

-   ブール値、decimal、float、および一覧の**xs:anyURI**パラメーターを指定します。

使用して、クライアントに応答、 **TypeCheckResponse**メソッド。

-   **wsa:Action == http:\//schemas.example.org/SimpleService/TypeCheckResponse**

-   ブール値、decimal、float、および一覧の**xs:anyURI**パラメーターが返され、クライアントにエコー バックします。

ブール値、decimal、float、および一覧の**xs:anyURI**パラメーターに正しく表示される、デバイス クライアントにエコー出力する前にします。 パラメーターが再度表示クライアントで受信されているようです。

**2.4**

**AnyCheck メソッド**

2.4.1

呼び出し、 **AnyCheck**で SimpleService のメソッド。

-   **wsa:Action == http:\//schemas.example.org/SimpleService/AnyCheckRequest**

-   Http:\//testdevice.interop/SimpleService1 サービスが使用されます

-   任意の XML フラグメントは、パラメーターとして使用されます。

使用して、クライアントに応答、 **TypeCheckResponse**メソッド。

-   **wsa:Action == http:\//schemas.example.org/SimpleService/AnyCheckResponse**

-   任意の XML フラグメントが返され、クライアントにエコー バックします。

クライアントから送信された XML フラグメントは、クライアントにエコーされますが、前にも、デバイスに正しく表示されます。 クライアントで受信されると、XML フラグメントが正しく表示もう一度です。

 

 

 





