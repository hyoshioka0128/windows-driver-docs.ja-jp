---
title: 印刷ドライバーのサンプル
description: このディレクトリのドライバーサンプルは、デバイスのカスタム印刷ドライバーを作成するための開始点となります。
ms.assetid: B4485626-9062-4892-B317-8FFA8B68C0D0
ms.date: 12/02/2019
ms.localizationpriority: medium
ms.openlocfilehash: 175a2b0ae55999998fcacb0d0770e56f2fca9a47
ms.sourcegitcommit: 30fa63ad13fd5e2e883b76a44f0703e01049ffa1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74735225"
---
# <a name="print-driver-samples"></a>印刷ドライバーのサンプル

このディレクトリのドライバーサンプルは、デバイスのカスタム印刷ドライバーを作成するための開始点となります。

| サンプル | 説明 |
| --- | --- |
| [印刷の自動構成](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/print-auto-configuration-sample) | Unidrv ベースおよび PScript5 ベースのドライバーを実装して、自動構成の受信トレイサポートを利用する方法を示します。 このサンプルは、標準の TCP/IP ポートモニタまたはネットワーク接続デバイス (NCD) ポートモニタで使用されている場合にのみ機能します。 |
| [共通プロパティシートの UI](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/common-property-sheet-ui-sample) | 共通プロパティシートのユーザーインターフェイス (CPSUI) が Windows 印刷スプーラを呼び出して、システムの既定のプリンターのプロパティシートページを作成するアプリケーション。 |
| [OEM プリンターカスタマイズプラグインのサンプル](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/oem-printer-customization-plug-in-samples) | OEMDLL サンプルは、OEM カスタマイズプラグインの図です。ビットマップ、OEMPS、OEMPS、OEMPS、OEMPREAN、CUSTHLP、SyncSet、Set Eui、PSUIRep、および透かしサンプルは、プリンターの出力には影響しません。 これらは、さまざまな種類の OEM カスタマイズ Dll を構築する方法の例にすぎません。|
| [OpenXPS ドキュメント](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/openxps-documents-print-sample) | さまざまなソースから生成された一連のドキュメントが含まれています。これには、.NET Framework および Microsoft XPS ドキュメントライター (MXDW) の Windows Presentation Foundation から生成されたドキュメントが含まれます。 これらは、XML Paper Specification のさまざまな機能を実行するいくつかのドキュメントを提供するために用意されています。 |
| [XPS ドキュメント](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/xps-documents-print-sample) | さまざまなソースから生成された一連のドキュメントが含まれています。これには、.NET Framework および Microsoft XPS ドキュメントライター (MXDW) の Windows Presentation Foundation から生成されたドキュメントが含まれます。 これらは、XML Paper Specification のさまざまな機能を実行するいくつかのドキュメントを提供するために用意されています。 |
| [印刷パイプラインの単純なフィルター](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/print-pipeline-simple-filter) | 印刷パイプラインのフィルターインターフェイスを使用する方法について説明します。 |
| [プリンターの拡張機能](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/printer-extension-sample) | .NET を使用して、v4 印刷ドライバー用のカスタマイズされたデスクトップ UI を構築する方法を示します。 この .NET アプリケーションは、印刷システムと通信するために PrintTicket、PrintCapabilities、および Bidi を使用します。これは、v4 印刷ドライバーに含めるのに適しています。 |
| [印刷ドライバーの制約](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/print-driver-constraints-sample) | 高度な制約の処理、および JavaScript を使用した PrintTicket/PrintCapabilities 処理を実装する方法を示します。  |
| [USB ホストベースの印刷ドライバー](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/usb-host-based-print-driver-sample) | V4 印刷ドライバーモデルを使用し、USB 経由で接続されているホストベースのデバイスをサポートする方法を示します。 |
| [USB モニターと BiDi の印刷](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/print-driver-usb-monitor-and-bidi-sample)  | JavaScript と XML を使用して、USB バス経由で双方向 (Bidi) 通信をサポートする方法を示します。 このサンプルでは、印刷を行わずに双方向の状態をサポートし、印刷中はプリンターからの要請されていない状態をサポートします。 |
| [WSDMon Bidi 拡張](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/wsdmon-bidi-extension-sample)  | XML 拡張ファイルを使用して、WSD に接続されたプリンターとの双方向 (Bidi) 通信をサポートする方法を示します。 |
| [XPSDrv ドライバーとフィルター](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/xpsdrv-driver-and-filter-sample) | このサンプルは、XPSDrv プリンタードライバーを開発するための出発点として使用することを目的としており、XPSDrv 印刷ドライバーの機能と可能性を示しています。 この目標を達成するには、カスタム UI コンテンツと PrintTicket の処理をサポートする構成プラグインを使用して構成された一連の XPS 印刷パイプラインフィルター内に、いくつかの実際の機能を実装します。 |
| [XPS ラスタライズフィルターサービス](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/xps-rasterization-filter-service-sample) | XPS ドキュメント内の固定ページをラスタライズする XPSDrv フィルター。 ハードウェアベンダーは、このサンプルを変更して、プリンターまたはその他のディスプレイデバイスのビットマップイメージを生成する XPSDrv フィルターを作成できます。 |
