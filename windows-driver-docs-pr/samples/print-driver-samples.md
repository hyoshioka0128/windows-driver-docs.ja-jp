---
title: 印刷ドライバーのサンプル
description: このディレクトリにドライバーのサンプルでは、デバイス用のカスタムのプリンター ドライバーを記述するための開始点を提供します。
ms.assetid: B4485626-9062-4892-B317-8FFA8B68C0D0
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 900bfc1806e5cbbfdb548af810062ba8dc29e4fe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366316"
---
# <a name="print-driver-samples"></a>印刷ドライバーのサンプル


このディレクトリにドライバーのサンプルでは、デバイス用のカスタムのプリンター ドライバーを記述するための開始点を提供します。

## <a name="print"></a>印刷


| サンプル名                      | ソリューション                                                                  | 説明  |
|----------------------------------|---------------------------------------------------------------------------|--------------|
| 印刷の自動構成         | [AutoConfig](https://go.microsoft.com/fwlink/p/?LinkId=617938)             | PScript5 ベースのドライバーの自動構成の受信トレイのサポートを利用して Unidrv ベースを実装する方法について説明します。 このサンプルでは、標準の TCP/IP ポート モニタまたは Network-Connected デバイス (NCD) ポート モニターで使用する場合にのみは機能します。                                                                                                                                                |
| 共通のプロパティ シートの UI         | [cpsuisam](https://go.microsoft.com/fwlink/p/?LinkId=617940)               | 一般的なプロパティ シートのユーザー インターフェイス (CPSUI) を Windows を呼び出すと、アプリケーションの印刷スプーラー システムの既定のプリンターのプロパティ シートのページを作成します。                                                                                                                                                                                                                       |
| OEM プリンタのカスタマイズのプラグイン サンプル | [OEM プリンタのカスタマイズのプラグイン サンプル](https://go.microsoft.com/fwlink/?linkid=862105) | OEMDLL サンプルは、OEM カスタマイズのプラグインを示しています。ビットマップ、OEMPS、OEMUI、OEMUNI、OEMPREAN、CUSTHLP、SyncSet、ThemeUI、PSUIRep、および透かしのサンプルは、プリンターの出力には影響しません。 これらは、さまざまな種類の OEM カスタマイズの Dll をビルドする方法の例のみです。               |
| OpenXPS ドキュメント                | [SampleOpenXps](https://go.microsoft.com/fwlink/p/?LinkId=617941)          | さまざまなソースから .NET Framework で Windows Presentation Foundation と Microsoft XPS ドキュメント ライター (MXDW) から生成されるなど、ソースから生成されたドキュメントのセットが含まれています。 これらはさまざまな XML Paper Specification の機能を実行するいくつかのドキュメントを提供するために含まれています。                                               |
| XPS ドキュメント                    | [SampleXPS](https://go.microsoft.com/fwlink/p/?LinkId=617942)              | さまざまなソースから .NET Framework で Windows Presentation Foundation と Microsoft XPS ドキュメント ライター (MXDW) から生成されるなど、ソースから生成されたドキュメントのセットが含まれています。 これらはさまざまな XML Paper Specification の機能を実行するいくつかのドキュメントを提供するために含まれています。                                               |
| 単純なフィルターのパイプラインを印刷します。     | [SimplePipelineFilter](https://go.microsoft.com/fwlink/p/?LinkId=617944)   | 印刷のパイプラインのフィルター インターフェイスを使用する方法を示します。                                                                                                                                                                                                                                                                                                                                             |
| プリンターの拡張機能                | [PrinterExtensionSample](https://go.microsoft.com/fwlink/p/?LinkId=617945) | .NET を使用して、v4 印刷ドライバー、カスタマイズされたデスクトップ UI を構築する方法を示します。 この .NET アプリケーションでは、PrintTicket と PrintCapabilities Bidi を印刷システムと通信するために使用し、v4 印刷ドライバーに含めることが適切です。                                                                                                                                           |
| 印刷ドライバーの制約         | [ConstraintScript](https://go.microsoft.com/fwlink/p/?LinkId=617946)       | 高度な制約の処理を実装する方法について説明し、また PrintTicket と PrintCapabilities JavaScript を使用して処理します。                                                                                                                                                                                                                                                                        |
| USB ホスト ベースの印刷ドライバー      | [HostBasedSampleDriver](https://go.microsoft.com/fwlink/p/?LinkId=617947)  | V4 印刷ドライバー モデルを使用して、USB 経由で接続されているホスト ベースのデバイスをサポートする方法を示します。                                                                                                                                                                                                                                                                                        |
| 印刷の USB モニターと BiDi       | [USBMon 双方向の拡張](https://go.microsoft.com/fwlink/p/?LinkId=617948)  | JavaScript and XML を使用して、USB バス経由で双方向 (Bidi) 通信をサポートする方法を示します。 このサンプルでは、印刷されていない、ときに双方向の状態と印刷中に、プリンターから要請されていない状態をサポートします。                                                                                                                                                                     |
| WSDMon 双方向の拡張機能            | [WSDMon 双方向の拡張](https://go.microsoft.com/fwlink/p/?LinkId=617949)  | XML 拡張ファイルを使用して、WSD プリンターとの双方向 (Bidi) 通信をサポートする方法を示します。                                                                                                                                                                                                                                                                            |
| XPSDrv ドライバーとフィルター         | [XPSDrvSmpl](https://go.microsoft.com/fwlink/p/?LinkId=617950)             | このサンプルでは、XPSDrv プリンター ドライバーを開発するための開始点を提供する機能と、XPSDrv プリンター ドライバーの可能性を示しています。 この目標は、さまざまな一連のカスタム UI のコンテンツと PrintTicket の処理をサポートする構成がプラグインで構成されている XPS 印刷のパイプライン フィルター内の実際の機能を実装することによって実現されます。 |
| XPS ラスタライズ フィルター サービス | [XpsRasFilter](https://go.microsoft.com/fwlink/p/?LinkId=617951)           | ラスタライズされますが、XPS ドキュメントのページを固定 XPSDrv フィルターです。 ハードウェア ベンダーは、このサンプルをビルドしてプリンターまたはその他のディスプレイ デバイスのビットマップ イメージを生成する XPSDrv フィルターを変更できます。                                                                                                                                                                                          |





