---
ms.assetid: 2F30E68B-B643-4387-9430-793D08AAF0E7
description: 日付範囲やその他のオプション フィルターを指定して、Windows 7 や Windows 8.x のドライバーに関する集計エラー報告データを取得するには、Microsoft Store 分析 API の以下のメソッドを使います。 このメソッドは、IHV のみを対象としています。
title: Windows 7 や Windows 8.x のドライバーに関するエラー報告データを取得する
ms.topic: article
ms.date: 08/28/2018
keywords: Windows 10, UWP, Store サービス, Microsoft Store 分析 API, エラー
ms.localizationpriority: medium
ms.openlocfilehash: 28d6d19adc0de3d8f9627148213795820ddb8d43
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364434"
---
# <a name="get-error-reporting-data-for-windows-7-and-windows-8x-drivers"></a>Windows 7 や Windows 8.x のドライバーに関するエラー報告データを取得する

> [!IMPORTANT]
> このトピックには、サポートが終了した機能に関する内容が含まれています。 この記事では、ドライバー申請エラーに関するデータを収集するための、古いメソッドについて説明しています。 これはレガシー サポートのみを目的に提供されているものです。
>
> 代わりに、次の新しいトピックを使用してください。
>
> - [ドライバー エラー詳細のカスタム レポートをスケジュールする](schedule-custom-reports-for-driver-failure-details.md)
> - [レポート テンプレートの新規作成](create-a-new-report-template.md)
> - [新しいレポートをスケジュールする](schedule-a-new-report.md)
> - [レポート データの取得](get-report-data.md)
> - [エラー CAB のダウンロード](download-failure-cabs.md)

日付範囲やその他のオプション フィルターを指定して、Windows 7 や Windows 8.x のドライバー エラーに関する集計報告データを取得するには、Microsoft Store 分析 API の以下のメソッドを使います。 また、[Windows 7 や Windows 8.x のドライバー エラーに関する詳細を取得する](get-details-for-a-windows-7-or-windows-8.x-driver-error.md)メソッドを利用すれば、追加のエラー情報を取得することもできます。

> [!NOTE]
> このメソッドは、[Windows ハードウェア デベロッパー センター プログラム](https://docs.microsoft.com/windows-hardware/drivers/dashboard/get-started-with-the-hardware-dashboard)に参加している開発者アカウントでのみ使用できます。

## <a name="prerequisites"></a>前提条件

このメソッドを使うには、最初に次の作業を行う必要があります。

* Microsoft Store 分析 API に関するすべての[前提条件](https://docs.microsoft.com/windows/uwp/monetize/access-analytics-data-using-windows-store-services#prerequisites)を満たします (前提条件がまだ満たされていない場合)。
* このメソッドの要求ヘッダーで使う [Azure AD アクセス トークンを取得](https://docs.microsoft.com/windows/uwp/monetize/access-analytics-data-using-windows-store-services#obtain-an-azure-ad-access-token)します。 アクセス トークンを取得した後、アクセス トークンを使用できるのは、その有効期限が切れるまでの 60 分間です。 トークンの有効期限が切れたら新しいトークンを取得できます。

## <a name="request"></a>要求


### <a name="request-syntax"></a>要求の構文

| メソッド | 要求 URI                                                          |
|--------|----------------------------------------------------------------------|
| GET    | `https://manage.devcenter.microsoft.com/v1.0/my/analytics/ihvdriver/failurehits` |


### <a name="request-header"></a>要求ヘッダー

| Header        | 種類   | 説明                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| Authorization | string | 必須。 **Bearer** &lt;*トークン*&gt; という形式の Azure AD アクセス トークン。 |


### <a name="request-parameters"></a>要求パラメーター

| パラメーター        | 種類   |  説明      |  必須  
|---------------|--------|---------------|------|
| startDate | date | 取得するエラー報告データの日付範囲の開始日です。 既定値は現在の日付です。 |  X  |
| endDate | date | 取得するエラー報告データの日付範囲の終了日です。 既定値は現在の日付です。 |  X  |
| top | int | 要求で返すデータの行数です。 最大値および指定しない場合の既定値は 10000 です。 クエリにこれを上回る行がある場合は、応答本文に次リンクが含まれ、そのリンクを使ってデータの次のページを要求できます。 |  X  |
| skip | int | クエリでスキップする行数です。 大きなデータ セットを操作するには、このパラメーターを使用します。 たとえば、top=10000 と skip=0 を指定すると、データの最初の 10,000 行が取得され、top=10000 と skip=10000 を指定すると、データの次の 10,000 行が取得されます。 |  X  |
| filter | string  | 応答内の行をフィルター処理する 1 つまたは複数のステートメントです。 各ステートメントには、応答本文からのフィールド名、および **eq** 演算子または **ne** 演算子と関連付けられる値が含まれており、**and** や **or** を使用してステートメントを組み合わせることができます。 *filter* パラメーターでは、文字列値を単一引用符で囲む必要があります。 応答本文から次のフィールドを指定することができます。<p/><ul><li><strong>date</strong></li><li><strong>failureName</strong></li><li><strong>failureHash</strong></li><li><strong>symbol</strong></li><li><strong>osVersion</strong></li></li><li><strong>eventType</strong></li><li><strong>market</strong></li><li><strong>deviceType</strong></li><li><strong>driverName</strong></li><li><strong>driverVersion</strong></li><li><strong>oemName</strong></li><li><strong>oemModel</strong></li><li><strong>flightRing</strong></li><li><strong>architecture</strong></li></ul> | X   |
| aggregationLevel | string | 集計データを取得する時間範囲を指定します。 次のいずれかの文字列を指定できます。<strong>day</strong>、<strong>week</strong>、または <strong>month</strong>。 指定しない場合、既定値は <strong>day</strong> です。 <strong>week</strong> または <strong>month</strong> を指定した場合、<em>failureName</em> と <em>failureHash</em> の値は 1,000 バケットに制限されます。 | X |
| orderby | string | 結果データ値の順序を指定するステートメントです。 構文は <em>orderby=field [order],field [order],...</em> です。応答本文から次のフィールドを指定することができます。<p/><ul><li><strong>date</strong></li><li><strong>failureName</strong></li><li><strong>failureHash</strong></li><li><strong>symbol</strong></li><li><strong>osVersion</strong></li><li><strong>osName</strong></li><li><strong>eventType</strong></li><li><strong>market</strong></li><li><strong>deviceType</strong></li><li><strong>driverName</strong></li><li><strong>driverVersion</strong></li><li><strong>oemName</strong></li><li><strong>oemModel</strong></li><li><strong>flightRing</strong></li><li><strong>architecture</strong></li></ul><p><em>order</em> パラメーターは省略可能であり、<strong>asc</strong> または <strong>desc</strong> を指定して、各フィールドを昇順または降順にすることができます。 既定値は <strong>asc</strong> です。</p><p><em>orderby</em> 文字列の例: <em>orderby=date,market</em></p> |  X  |
| groupby | string | 指定したフィールドのみにデータ集計を適用するステートメントです。 応答本文から次のフィールドを指定することができます。<p/><ul><li><strong>failureName</strong></li><li><strong>failureHash</strong></li><li><strong>symbol</strong></li><li><strong>osVersion</strong></li><li><strong>eventType</strong></li><li><strong>market</strong></li><li><strong>deviceType</strong></li><li><strong>driverName</strong></li><li><strong>driverVersion</strong></li><li><strong>oemName</strong></li><li><strong>oemModel</strong></li><li><strong>flightRing</strong></li><li><strong>architecture</strong></li></ul><p>返されるデータ行には、<em>groupby</em> パラメーターに指定したフィールドと次の値が含まれます。</p><ul><li><strong>date</strong></li><li><strong>eventCount</strong></li></ul><p><em>groupby</em> パラメーターは、<em>aggregationLevel</em> パラメーターと同時に使用できます。 例: <em>&groupby=failureName,market&aggregationLevel=week</em></p></p> |  X  |


### <a name="request-example"></a>要求の例

OEM ハードウェア エラー報告データを取得するための要求の例をいくつか次に示します。

```syntax
GET https://manage.devcenter.microsoft.com/v1.0/my/analytics/ihvdriver/failurehits?startDate=1/1/2015&endDate=2/1/2015&top=10&skip=0 HTTP/1.1
Authorization: Bearer <your access token>

GET https://manage.devcenter.microsoft.com/v1.0/my/analytics/ihvdriver/failurehits?startDate=8/1/2015&endDate=8/31/2015&skip=0&filter=market eq 'US' and deviceType eq 'PC' HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>応答


### <a name="response-body"></a>応答本文

| Value      | 種類    | 説明     |
|------------|---------|--------------|
| Value      | array   | 集計エラー報告データが含まれるオブジェクトの配列です。 各オブジェクトのデータの詳細については、以下の表を参照してください。     |
| @nextLink  | string  | データの追加ページがある場合、この文字列には、データの次のページを要求するために使用できる URI が含まれます。 たとえば、要求の **top** パラメーターが 10000 に設定されたが、クエリの入手データに 10,000 を超えるエラー行が含まれている場合に、この値が返されます。 |
| TotalCount | 整数 | クエリの結果データ内の行の総数です。     |


*Value* 配列の要素には、次の値が含まれます。

| Value           | 種類    | 説明        |
|-----------------|---------|---------------------|
| date            | string  | エラー データの日付範囲の最初の日付です。 要求に日付を指定した場合、この値はその日付になります。 要求に週、月、またはその他の日付範囲を指定した場合、この値はその日付範囲の最初の日付になります。 |
| sellerId   | string  | 開発者アカウントに関連付けられている販売者 ID の値です (この値は、デベロッパー センター アカウントの設定にある **[販売者 ID]** の値と一致します)。 |
| failureName     | string  | 4 つの部分から成るエラーの名前です。問題が発生した 1 つ以上のクラス、例外/バグ チェック コード、障害が発生したドライバーの名前、関連する関数の名前で構成されます。  |
| failureHash     | string  | エラーの一意の識別子です。   |
| symbol          | string  | このエラーに割り当てられた記号です。 |
| osVersion       | string  | エラーが発生した OS のビルド バージョンです。4 つの部分から構成されます。  |
| osName       | string  | エラーが発生した OS の名前です。  |
| eventType       | string  | 発生したエラーの種類です。      |
| market          | string  | デバイス市場の ISO 3166 国コードです。   |
| deviceType      | string  | エラーが発生したデバイスの種類です。    |
| driverName     | string  | このエラーに関連付けられているドライバーの一意の名前です。      |
| driverVersion  | string  | このエラーに関連付けられているドライバーのバージョンです。   |
| architecture | string |  エラーが発生したデバイスのアーキテクチャです。  |
| oemName | string | エラーが発生したデバイスの OEM の名前です。 |
| oemModel | string | エラーが発生したデバイス モデルの名前です。 |
| flightRing | string | エラーが発生した OS フライトの名前です。 |
| eventCount      | 整数 | 指定した集計レベルでこのエラーに起因すると考えられるイベントの数です。      |


### <a name="response-example"></a>応答の例

この要求の JSON 返信の本文の例を次に示します。

```json
{
  "Value": [
    {
      "date": "2017-02-26",
      "sellerId":"14313740",
      "driverName": "fastboot.sys",
      "osVersion": "6.3.9600.9600",
      "osName": "Windows 8.1",
      "flightRing": "Unknown",
      "oemName": "Contoso",
      "oemModel": "C-122",
      "market": "US",
      "symbol": "fastboot",
      "failureName": "AV_fastboot!unknown_function",
      "failureHash": "f060c0b6-fbe6-463f-a9f1-b7ebc1cc722f",
      "architecture": "x64",
      "driverVersion": "2.1.1.0",
      "deviceType": "Unknown",
      "eventType": "System crash",
      "deviceCount": 1.0,
      "eventCount": 1.0
    }]
}
```

## <a name="related-topics"></a>関連トピック

- [Windows 7 や Windows 8.x のドライバー エラーに関する詳細を取得する](get-details-for-a-windows-7-or-windows-8.x-driver-error.md)

- [Windows 7 や Windows 8.x のドライバー エラーに関する CAB ファイルをダウンロードする](download-the-cab-file-for-a-windows-7-or-windows-8.x-driver-error.md)
