---
title: デバイスで WSPrint 2.0 を有効にする
description: これらの設定を使用して、デバイスで WSPrint 2.0 を有効にするには
ms.date: 01/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5942989ce749569d87966d3ea403aab5cca803c8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325459"
---
# <a name="enable-wsprint-20-on-a-device"></a>デバイスで WSPrint 2.0 を有効にする


このトピックでは、デバイスで WSPrint 2.0 を有効にするために必要な設定について説明します。

## <a name="broadcast-a-mdns-printer-service"></a>Mdn のプリンター サービスを配信します。


これは、作業は PrintService のサービスの種類を使用します。\_プリンターです。\_tcp.local ポート 80 でします。

## <a name="implement-a-http-endpoint"></a>HTTP エンドポイントを実装します。 


エンドポイントは、WSPrint 2.0 の操作に応答する必要があります。 SOAP の検証と処理を実行する必要はありません。 文字列の検出と置換を使用することができます。

WSPrint エンドポイントが機能している場合、カスタム デバイス id を持つ GetPrinterElements 呼び出しから返された XML をカスタマイズする必要があります。

```xml
<wprt:DeviceId>MFG:MS3D; CMD:XPS; MDL:Compat; CLS:Printer; DES:Compat; CID:MS3DWSD</wprt:DeviceId>
```
これは、パブリッシュされた INF で互換性のある ID と一致します。

```xml
WSDPRINT\MS3DCompatE2D2
```

## <a name="wsprint-interactions"></a>WSPrint 相互作用


次の図は、WSPrint 2.0 の相互作用を示しています。

![wsprint 相互作用](images/wsprint-interactions.png)

WSPrint 2.0 の相互作用の詳細な説明を次の手順には。

1.  プローブ: ネットワーク探索のブートス トラップ

2.  ネットワーク探索のブートス トラップを解決します。

3.  Get – プリンター メタデータ クエリ

4.  GetPrinterElements – プリンター メタデータ クエリ

5.  サブスクライブ-イベント モデルの登録

6.  サブスクライブ解除-イベントの登録解除します。

7.  SetEventRate – イベント レート

8.  更新-更新 

9.  PrepareToPrint – 印刷の初期化

10. CreatePrintJob – 印刷送信

11. CreatePrintJob2 – 印刷送信

12. GetPrintDeviceResources – ResX (マルチ一部の送信応答) のローカライズされたリソースの取得を許可

13. GetPrintDeviceCapabilities - 印刷デバイスの機能 (マルチ一部の送信応答) の取得が可能

14. GetBidiSchemaExtensions - により取得 Bidi スキーマの拡張機能 (マルチ一部の送信応答)

15. CancelJob – ジョブの取り消し

16. GetActiveJobs – ジョブの進行状況 

17. GetJobHistory – ジョブの履歴

18. AddDocument – 現在の印刷するドキュメントの追加

19. GetJobElements – Get ジョブの状態

20. SendDocument – 実際の印刷データ (マルチ一部受信要求)

WSPrint 2.0 の詳細については、次のリソースを参照してください。

[印刷用デバイスでの Web サービスの実装](https://go.microsoft.com/fwlink/p/?linkid=867155)

[WSPrint 2.0 仕様](https://go.microsoft.com/fwlink/p/?LinkId=534008) 



