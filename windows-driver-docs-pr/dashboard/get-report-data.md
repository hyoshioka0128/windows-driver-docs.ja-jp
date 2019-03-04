---
title: レポート データの取得
description: Windows ドライバー申請のエラー レポートの状態を照会し、エラー詳細レポートを取得します。
ms.author: shganesh
ms.topic: article
ms.date: 09/01/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3b3398095214950fe214ac72229330e1c575e980
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518996"
---
# <a name="get-report-data"></a>レポート データの取得

このメソッドを使用すると、reportId を使用してレポートの状態を照会し、エラー詳細レポートをフェッチすることができます。 このメソッドでは、ダウンロードの準備ができている場合、レポートのダウンロード リンクが返され、それ以外の場合は状態が返されます。

## <a name="request-syntax"></a>要求の構文

|メソッド|要求 URI|
|----|----|
|GET|`https://manage.devcenter.microsoft.com/analytics/driver/reportdata/{reportId}?startDate={yyyy-mm-dd}&endDate={yyyy-mm-dd}`|

## <a name="request-header"></a>要求ヘッダー

|Header|種類|説明|
|----|----|----|
|Authorization|string|必須。 **Bearer** *\<トークン\>* という形式の Azure AD アクセス トークン|
|Content-Type|String|Application/JSON|

## <a name="parameters"></a>パラメーター

次の表は、Get Failure Details API のパラメーターを説明したものです。

|パラメーター|説明|
|----|----|
|reportId|[Schedule Report API](schedule-a-new-report.md) の呼び出し時に受信したレポートのレポート ID|
|startDate|生成されたレポートがいつから要求されるのかを示す開始日。形式は `yyyy-mm-dd` です|
|endDate|生成されたレポートがいつまで要求されるのかを示す終了日。形式は `yyyy-mm-dd` です|

## <a name="response"></a>応答

応答ペイロードは、次の表に示すように、値の配列として構成されます。

<table>
  <thead>
    <tr>
      <th>項目</th>
      <th>説明</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>応答コード</td>
      <td>200/500/400</td>
    </tr>
    <tr>
      <td>応答ペイロード</td>
      <td><pre>{
    "data": [
        {
            "ReportDatetime": "2018-01-20T05:35:32",
            "ReportStatus": "Completed",
            "ReportLocation": "https://hardwareanalyticsint.blob.core.windows.net/drivers/Reports/2.txt?sv=2017 .... "
        },
        {
            "ReportDatetime": "2018-01-23T05:35:32",
            "ReportStatus": "Failed",
            "ReportLocation": ""
        }
    ],
    "errors": []
}</pre></td>
    </tr>
  </tbody>
</table>

## <a name="response-parameters"></a>応答パラメーター

次の表は、応答内のパラメーターについて説明したものです。

|パラメーター|説明|
|----|----|
|ReportDatetime|レポートが実行された日付|
|ReportStatus|ReportDateTime の時点でのレポートのステータスです。 値は "Completed (完了)"、"Pending (保留中)"、"In Progress (進行中)"、"Failed (失敗)" です。|
|ReportLocation|ReportStatus で "Completed" が返された場合の、レポートのダウンロード リンクです|

> [!NOTE]
> ReportLocation リンクは、12 時間で期限が切れます。 12 時間の期限内にデータをダウンロードしない場合は、Get Report Data API を使用して新しいレポート リンクを取得する必要があります。

レポート テンプレートは、「[Manage report templates and scheduled reports (レポート テンプレートとスケジュールされたレポートを管理する)](manage-report-templates-and-scheduled-reports.md)」で説明されているメソッドを使って管理できます。

## <a name="see-also"></a>関連項目

- [分析レポート API (Swagger)](https://apidocs.microsoft.com/services/analyticsreportingapis)

- [ハードウェア ダッシュボード API のサンプル (GitHub)](https://aka.ms/hpc_async_api_samples)
