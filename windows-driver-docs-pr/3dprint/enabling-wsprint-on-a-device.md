---
title: デバイスで WSPrint 2.0 を有効にする
description: デバイスで WSPrint 2.0 を有効にするには、これらの設定を使用します。
ms.date: 05/18/2020
ms.localizationpriority: medium
ms.openlocfilehash: 5d01b0d6fa3a69dffcaf46e50c3263fe8be38657
ms.sourcegitcommit: 32f42241991d57032e5d39ee9f2a3ab4a66ae396
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/18/2020
ms.locfileid: "83553333"
---
# <a name="enable-wsprint-20-on-a-device"></a>デバイスで WSPrint 2.0 を有効にする

このトピックでは、デバイスで WSPrint 2.0 を有効にするために必要な設定について説明します。

## <a name="broadcast-a-mdns-printer-service"></a>Mdn printer サービスをブロードキャストする

これは、PrintService のサービスの種類を使用して行う必要があります。 \_プリンター。 \_tcp. ローカル (ポート 80)。

## <a name="implement-a-http-endpoint"></a>HTTP エンドポイントを実装する

エンドポイントは、WSPrint 2.0 操作に応答できる必要があります。 SOAP の検証と処理を実行する必要はありません。 代わりに、文字列の検出と置換を使用できます。

WSPrint エンドポイントが機能したら、カスタムデバイス id を使用して、Getプリンター要素の呼び出しから返された XML をカスタマイズする必要があります。

```xml
<wprt:DeviceId>MFG:MS3D; CMD:XPS; MDL:Compat; CLS:Printer; DES:Compat; CID:MS3DWSD</wprt:DeviceId>
```

これは、公開されている INF の互換性のある ID と一致します。

```xml
WSDPRINT\MS3DCompatE2D2
```

## <a name="wsprint-interactions"></a>WSPrint の相互作用

次の図は、WSPrint 2.0 の相互作用を示しています。

![wsprint の相互作用](images/wsprint-interactions.png)

WSPrint 2.0 の相互作用の詳細については、次の手順を参照してください。

1. プローブ–ネットワーク探索のブートストラップ

2. 解決–ネットワーク探索のブートストラップ

3. Get –プリンターメタデータクエリ

4. Getprinter Elements –プリンターメタデータクエリ

5. サブスクライブ-イベントモデルの登録

6. サブスクリプション解除–イベントの登録解除

7. SetEventRate –イベントレート

8. 更新–更新

9. 表示/印刷–印刷の初期化

10. CreatePrintJob –印刷の送信

11. CreatePrintJob2 –印刷の送信

12. GetPrintDeviceResources – ResX (マルチパート発信応答) でローカライズされたリソースを取得できます。

13. GetPrintDeviceCapabilities-印刷デバイスの機能 (マルチパート発信応答) を取得できるようにします。

14. GetBidiSchemaExtensions-Bidi スキーマ拡張 (マルチパート発信応答) の取得を許可します。

15. CancelJob –ジョブの取り消し

16. GetActiveJobs –ジョブの進行状況

17. GetJobHistory –ジョブ履歴

18. AddDocument –現在の印刷にドキュメントを追加します

19. GetJobElements –ジョブの状態を取得します。

20. SendDocument –実際の印刷データ (マルチパート受信要求)

WSPrint 2.0 の詳細については、次のリソースを参照してください。

[印刷用デバイスでの Web サービスの実装](https://docs.microsoft.com/windows-hardware/design/whitepapers/implementing-web-services-on-devices-for-printing)

[WSPrint 2.0 仕様](https://docs.microsoft.com/windows-hardware/design/whitepapers/implementing-web-services-on-devices-for-printing#file-downloads)
