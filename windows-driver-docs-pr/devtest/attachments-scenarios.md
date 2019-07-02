---
title: 添付ファイルのシナリオ
description: 添付ファイルのシナリオ
ms.assetid: bd563919-961f-40eb-ad5c-26026fc1c0e6
keywords:
- WSDBIT ツール WDK、テスト シナリオ
- WSDAPI 基本的な相互運用性ツール WDK、テスト シナリオ
- WDK WSDBIT のシナリオ
- WDK WSDBIT のシナリオをテストします。
- 添付ファイル シナリオ WDK WSDBIT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 246240232095a3660908b4d338bda7bebd8f8b4b
ms.sourcegitcommit: 289b5f97aff1b9ea1fefc9a8731e0fc16533073b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2019
ms.locfileid: "67492522"
---
# <a name="attachments-scenarios"></a>添付ファイルのシナリオ


添付ファイルのシナリオでは、添付ファイルを送受信することをテストします。

このシナリオの目的は、ホストされるサービス エンドポイントの検出ではありません。 このシナリオは、これらのエンドポイントが検出されたか、このシナリオを開始する前に指定されたことを想定しています。

どのケースでも、TestDevice に送信される添付ファイルは Dpws1.jpg、TestDevice から受信した添付される Dpws2.jpg します。 添付ファイルは、予想される添付ファイルのコピーをメモリに読み込むと、受信した添付ファイルのメモリのバイト単位の比較を行ってして検証する必要があります。

詳細についてでの初期テスト デバイス設定のダイアグラムを参照してください。[テスト環境の WSDBIT](wsdbit-testing-environment.md)します。

クライアント アクション サーバー アクションの不合格条件の場合**3.1**

**一方向の添付ファイルのメソッドを呼び出す**

3.1.1

呼び出し、 **OneWay**で AttachmentService のメソッド

-   **wsa:Action == http://schemas.example.org/AttachmentService/OneWayAttachment**

-   Http:\//testdevice.interop/AttachmentService1 サービスが使用されます。

-   参照してください[AttachmentService WSDL](attachmentservice-wsdl.md)します。

-   デバイスに送信される添付ファイルのデータとして Dpws1.jpg を使用します。

添付ファイルのデータを検証します。

サーバーは正しく添付ファイルのデータを検証します。 サーバーは Dpws1.jpg を受信します。

**3.2**

**TwoWay の添付ファイルのメソッドを呼び出す**

3.2.1

呼び出し、 **TwoWay**で AttachmentService のメソッド。

-   **wsa:Action == http://schemas.example.org/AttachmentService/TwoWayAttachmentRequest**

-   Http:\//testdevice.interop/AttachmentService1 サービスが使用されます。

-   参照してください[AttachmentService WSDL](attachmentservice-wsdl.md)します。

-   デバイスに送信される添付ファイルのデータとして Dpws1.jpg を使用します。

<!-- -->

-   添付ファイルのデータを検証します。

-   送信**TwoWayAttachmentResponse**します。

-   **wsa:Action == http://schemas.example.org/AttachmentService/TwoWayAttachmentResponse**

-   参照してください[AttachmentService WSDL](attachmentservice-wsdl.md)します。

-   クライアントに返される添付ファイルのデータとして Dpws2.jpg を使用します。

サーバーが正しく添付ファイルのデータを検証し、クライアントは応答を受信します。 サーバーは Dpws1.jpg を受信します。

3.2.2

受信した添付ファイルのデータの検証、 **TwoWayAttachmentResponse**します。 クライアントは、Dpws2.jpg を受け取ります。

なし。

クライアントは正しく添付ファイルのデータを検証します。

 

 

 





