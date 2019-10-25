---
title: カスタマイズされた UI のドライバー サポート
description: V4 印刷ドライバーモデルは、印刷用のプリンター拡張機能または UWP デバイスアプリを使用した UI カスタマイズの組み込みサポートを使用して開発されました。
ms.assetid: 91B0E824-1EE3-40B0-A24E-5A66C158972E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f84396268e051b0fcadd7748df95070f965b8ac7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845053"
---
# <a name="driver-support-for-customized-ui"></a>カスタマイズされた UI のドライバー サポート


V4 印刷ドライバーモデルは、印刷用のプリンター拡張機能または UWP デバイスアプリを使用した UI カスタマイズの組み込みサポートを使用して開発されました。

次のセクションでは、追加の UI カスタマイズの設計に関する考慮事項について説明します。

**印刷設定**

すべての v4 印刷ドライバーは印刷設定で動作しますが、すべてのシナリオで最大の一貫性を確保するために、構成層と UI 層の境界を維持することが重要です。 プリンターの拡張機能や UWP デバイスアプリがインストールされていない可能性があるため (または自動的にインストールされている場合もあります)、v4 印刷ドライバーは、プリンターの設定をカスタマイズしなくても印刷ドライバーが機能していることを確認する必要があります。 特に、これは、ドライバーの GPD/PPD + JavaScript 制約の実装で、PrintTicket と PrintCapabilities のサポートが完全で包括的である必要があることを意味します。

プリンター拡張機能や UWP デバイスアプリにおける制約の検証には、非常に有益で対話的なエクスペリエンスを提供するという観点で役立つ場合がありますが、信頼できると見なされるドライバーの検証を置き換えることはできません。

プリンター拡張機能と UWP デバイスアプリでは、ネットワークリソースに対して直接ネットワーク呼び出しを行うのではなく、 [**Iprinter queue:: SendBidiQuery**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nf-printerextension-iprinterqueue-sendbidiquery)メソッドを使用する必要があります。 ネットワークリソースに接続する必要がある場合は、別のスレッドで実行するか、UI がハングするのを防ぐために非同期に実行する必要があります。 将来の呼び出しを高速化するためにデータを取得した後は、データをキャッシュする必要があります。

**プリンター通知**

プリンター通知は、Bidi および DriverEvent XML ファイルによって駆動されます。 ただし、バッテリの寿命を適切に管理し、中断を最小限に抑えるために、ユーザーが印刷しているときにのみ通知が表示されます。

印刷設定は、印刷するアプリにコンテキストがありますが、プリンター通知は実行されません。 次のフローチャートでは、Windows がプリンター通知の動作を決定するために使用するデシジョンツリーについて説明します。 使用可能な場合は、UWP デバイスアプリがプリンター拡張より優先されます。

![プリンター通知動作のフローチャート](images/notificationbhvr.png)

[GetForegroundWindow](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-getforegroundwindow)を呼び出すことによって Windows 8 環境でカスタム UI を使用して通知を表示しようとすると、通知ウィンドウが表示されないことに  **注意**してください。 これは、オペレーティングシステムが、GetForegroundWindow を使用してフォアグラウンドウィンドウを作成するスレッドに高い優先順位を割り当てようとするためです。これは、Windows 8 環境のダイアログでは許可されません。 カスタム UI を使用して Windows 8 環境に通知を表示する場合は、 [Getdesktopwindow](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-getdesktopwindow)を呼び出して、通知を表示する必要があります。

 

**ドライバーイベントを作成**しています。 V4 印刷ドライバーは、DriverEvent XML ファイルを使用して、Bidi クエリと、ドライバーイベントを発生させるトリガーを記述します。 また、ドライバーイベントは標準の文字列のみをサポートすることに注意してください。 標準文字列の詳細については、「 [AsyncUI Default Resource File String Resources](https://docs.microsoft.com/openspecs/windows_protocols/ms-pan/cbd34ab3-5a2a-4292-b7ce-e584020d14d7)」を参照してください。 現在の実装では、これにより、 [AsyncUIBalloon](https://docs.microsoft.com/openspecs/windows_protocols/ms-pan/9ec494fd-eea8-4545-8e38-5992fa7f6a4a)メッセージが作成され、 [MS PAN プロトコル](https://docs.microsoft.com/openspecs/windows_protocols/ms-pan/e44d984c-07d3-414c-8ffc-f8c8ad8512a8)を使用して公開されます。 この実装は、将来、パフォーマンスを向上させるために変更される可能性があるため、基になるプロトコルに依存しないように v4 印刷ドライバーを開発することが重要です。

次の図は、プロトコル使用率を示しています。

![ドライバーイベントを使用したプロトコル使用率](images/drivereventprotutil.png)

**ドライバーイベントの XML サンプル**。 次の XML コードスニペットでは、1つのドライバーイベントを指定しています。 イベントは、Bidi によって報告された合計容量の21% 未満の黄色いインクを確認します。 このような場合は、resourceID 132 によって参照される文字列を使用して AsyncUIBalloon メッセージが作成されます。 つまり、"' %1 ' はトナー/インクが不足しています" というメッセージが表示されます。 リソース 2002 ("黄") は %1 に置き換えられます。

```xml
<de:DriverEvents xmlns:de="http://schemas.microsoft.com/windows/2011/08/printing/driverevents" schemaVersion="4.0">
  <DriverEvent eventId="{A04CF0FC-1CEB-4C62-B967-6F0AE5C5F81E}">
    <Transport>USB</Transport>
    <Transport>WSD</Transport>
    <Query>\Printer.Consumables</Query>
    <Trigger result="\Printer.Consumables.Yellow:Level" comparison="LessThan" value="21">
      <StandardMessage resourceId="132">
        <StringParameter index="1" resourceId="2002" />
      </StandardMessage>
    </Trigger>
  </DriverEvent>
</de:DriverEvents>
```

**ドライバーイベントスキーマ**。 DriverEvent スキーマは、Windows Driver Kit で、\\um\\プリンター Driverevent. xsd \\インクルードされています。

**ドライバーイベントの XML 検証**。 ドライバーマニフェストで DriverEvent XML を正しく記述している限り、XML ファイルは INFGate ツールによって自動的に検証されます。

## <a name="related-topics"></a>関連トピック
[AsyncUIBalloon](https://docs.microsoft.com/openspecs/windows_protocols/ms-pan/9ec494fd-eea8-4545-8e38-5992fa7f6a4a)  
[AsyncUI 既定のリソースファイル文字列リソース](https://docs.microsoft.com/openspecs/windows_protocols/ms-pan/cbd34ab3-5a2a-4292-b7ce-e584020d14d7)  
[**Iプリンターキュー:: SendBidiQuery**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nf-printerextension-iprinterqueue-sendbidiquery)  
[MS PAN プロトコル](https://docs.microsoft.com/openspecs/windows_protocols/ms-pan/e44d984c-07d3-414c-8ffc-f8c8ad8512a8)  



