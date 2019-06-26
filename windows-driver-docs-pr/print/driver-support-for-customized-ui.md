---
title: カスタマイズされた UI のドライバー サポート
description: V4 印刷ドライバー モデルは、印刷用のプリンター拡張または UWP デバイス アプリを使用して UI カスタマイズの組み込みサポートを備えた開発されました。
ms.assetid: 91B0E824-1EE3-40B0-A24E-5A66C158972E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbd073c0eb01bbe5141d4452521795eec169525b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356079"
---
# <a name="driver-support-for-customized-ui"></a>カスタマイズされた UI のドライバー サポート


V4 印刷ドライバー モデルは、印刷用のプリンター拡張または UWP デバイス アプリを使用して UI カスタマイズの組み込みサポートを備えた開発されました。

次のセクションでは、追加の UI カスタマイズの設計考慮事項を説明します。

**印刷設定**

印刷設定がすべて v4 印刷ドライバーが、すべてのシナリオにおいて最大の一貫性を確保するために、構成と UI 層間の境界を維持するために重要です。 できませんのプリンター拡張または UWP デバイス アプリがインストールされている (または、それらが自動的にインストールされます)、ために、v4 印刷ドライバーは印刷ドライバーが、エクスペリエンスをカスタマイズしたプリンター設定なしで機能であることを確認する必要があります。 具体的には、完全かつ GPD/PPD + ドライバーでの JavaScript の制約の実装で包括的な PrintTicket と PrintCapabilities サポートがあることこれを意味します。

プリンターの拡張機能または UWP デバイス アプリでいくつかの制約検証に関して最も効果的な対話型エクスペリエンスを提供する役に立ちますが、権限を持つと見なされます、ドライバーの検証を置き換える必要がありますされません。

プリンターの拡張機能と UWP デバイス アプリを使用する必要があります、 [ **IPrinterQueue::SendBidiQuery** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nf-printerextension-iprinterqueue-sendbidiquery)ネットワーク リソースへの直接のネットワークではなく、メソッドを呼び出します。 ネットワーク リソースに接続する必要がある場合は、別のスレッドで、または分岐から UI を防ぐために非同期的に実行する必要があります。 今後の呼び出しを速く取得した後、データをキャッシュする必要があります。

**プリンターの通知**

プリンターの通知は DriverEvent XML ファイルと Bidi によって駆動されます。 バッテリの寿命を管理しやすくするためと中断を最小限に抑えるには、ただし、通知のみを表示するユーザーが印刷されます。

印刷設定は、印刷しているアプリのコンテキストは、プリンターの通知はありません。 次のフロー チャートでは、Windows を使用してプリンターの通知の動作を決定するデシジョン ツリーについて説明します。 場合、使用可能な UWP デバイス アプリはプリンターの拡張機能より優先されます。

![プリンターの通知動作のフローチャート](images/notificationbhvr.png)

**注**  という事実を意識することが重要するには、Windows 8 環境で呼び出すことによって、通知を表示するカスタム UI を使用しようとする場合[GetForegroundWindow](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-getforegroundwindow)、通知ウィンドウにすることはできません表示されます。 これは、オペレーティング システムが GetForegroundWindow を使用して、フォア グラウンド ウィンドウを作成するスレッドに優先順位の高いを割り当てようとしているため、これは許可されていませんダイアログで、Windows 8 環境。 Windows 8 環境で通知を表示するカスタム UI を使用する場合を行う必要がありますを呼び出して[GetDesktopWindow します。](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-getdesktopwindow)

 

**ドライバーのイベントを作成する**します。 V4 印刷ドライバーでは、DriverEvent XML ファイルを使用して、双方向のクエリとトリガーが発生します。 ドライバーのイベントが発生することを説明します。 ドライバーのイベントでは標準の文字列のみをサポートすることが重要です。 標準の文字列の詳細については、次を参照してください。 [AsyncUI 既定のリソース ファイルの文字列リソース](https://docs.microsoft.com/openspecs/windows_protocols/ms-pan/cbd34ab3-5a2a-4292-b7ce-e584020d14d7)します。 これにより、現在の実装では、 [AsyncUIBalloon](https://docs.microsoft.com/openspecs/windows_protocols/ms-pan/9ec494fd-eea8-4545-8e38-5992fa7f6a4a)メッセージを作成および発行を使用して、 [MS パン プロトコル](https://docs.microsoft.com/openspecs/windows_protocols/ms-pan/e44d984c-07d3-414c-8ffc-f8c8ad8512a8)します。 この実装は、パフォーマンスを向上させるために、後で変わる可能性があります、基になるプロトコルに依存関係を受け取らないように、v4 プリンター ドライバーを開発することが重要であるためです。

次の図は、プロトコルの使用率を示します。

![ドライバーのイベントとプロトコルの使用率](images/drivereventprotutil.png)

**ドライバーのイベントの XML サンプル**します。 次の XML コード スニペットでは、1 つのドライバーのイベントを指定します。 黄色のインクを Bidi によって報告された合計容量の 21% 未満のイベントを確認します。 このような場合は、resourceID 132 によって参照される文字列で、AsyncUIBalloon メッセージが作成されます。 つまり、メッセージが言い"'%1' があるトナー/インクが不足します" %1 の場所リソース 2002 ("Yellow") が置き換えられます。

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

**ドライバーのイベント スキーマ**します。 DriverEvent スキーマとして Windows Driver Kit \\Include\\um\\PrinterDriverEvents.xsd します。

**ドライバーのイベントの XML 検証**です。 ドライバー マニフェストで適切に DriverEvent XML を記述する場合に限り、XML ファイルは INFGate ツールによって自動的に検証します。

## <a name="related-topics"></a>関連トピック
[AsyncUIBalloon](https://docs.microsoft.com/openspecs/windows_protocols/ms-pan/9ec494fd-eea8-4545-8e38-5992fa7f6a4a)  
[AsyncUI 既定リソース ファイルの文字列リソース](https://docs.microsoft.com/openspecs/windows_protocols/ms-pan/cbd34ab3-5a2a-4292-b7ce-e584020d14d7)  
[**IPrinterQueue::SendBidiQuery**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nf-printerextension-iprinterqueue-sendbidiquery)  
[MS パン プロトコル](https://docs.microsoft.com/openspecs/windows_protocols/ms-pan/e44d984c-07d3-414c-8ffc-f8c8ad8512a8)  



