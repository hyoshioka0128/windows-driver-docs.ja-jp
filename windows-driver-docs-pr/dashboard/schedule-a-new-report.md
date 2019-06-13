---
title: 新しいレポートをスケジュールする
description: Microsoft ハードウェア デベロッパー センターのレポート テンプレートに基づいてカスタム エラー レポートをスケジュールする方法について説明します。
ms.topic: article
ms.author: shganesh
ms.date: 09/01/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5d7aa593bee432cb9a3732c8e0298af06e2f9ca0
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "63337113"
---
# <a name="schedule-a-new-report"></a>新しいレポートをスケジュールする

レポート テンプレートを正常に作成し、*templateID* を受信したら、次のメソッドを使用して頻度を設定し、レポートを定期的に配信するようにスケジュールします。

## <a name="request-syntax"></a>要求の構文

|メソッド|要求 URI|
|----|----|
|POST|`https://manage.devcenter.microsoft.com/analytics/driver/report`|

## <a name="request-header"></a>要求ヘッダー

|Header|種類|説明|
|----|----|----|
|Authorization|string|必須。 **Bearer** *\<トークン\>* という形式の Azure AD アクセス トークン|
|Content-Type|string|Application/JSON|

## <a name="sample-request-payload"></a>要求ペイロードのサンプル

次の形式を使用して、カスタム レポートを実行するためのスケジュールを定義します。

```json
{
  "templateId": 15, // sample report template id
  "schedule":
    {
      "startTime": "2018-07-24T00:00:00Z",//Date Time in UTC
      "recurrenceInterval": 12, // in hours
      "recurrence": 10    // number of times you want the report to run
    }
  
}
```

## <a name="parameters"></a>パラメーター

次の表に示すのは、レポート スケジュール JSON 内のパラメーターの説明です。

<table>
    <thead>
        <tr>
            <th>パラメーター</th>
            <th>必須</th>
           <th>説明</th>
        </tr>
    </thead>
    <tbody>
       <tr>
          <td>templateId</td>
          <td>〇</td>
          <td>Create Report Template API への応答として受信した templateId 値</td>
        </tr>
        <tr>
            <td>startTime</td>
            <td>〇</td>
            <td>レポートの初回実行予定日時。形式は次のとおりです。<pre>yyyy-MM-ddTHH:mm:ssZ</pre></td>
        </tr>
        <tr>
           <td>recurrenceInterval</td>
           <td>〇</td>
           <td>レポートが再度実行されるまでの時間間隔。時間単位で指定します。 指定できる最短の間隔は 12 時間です。</td>
        </tr>
        <tr>
            <td>recurrence</td>
            <td>〇</td>
            <td>このレポートを実行する回数。</td>
        </tr>
        <tr>
           <td>CallbackURL</td>
           <td>X</td>
           <td>レポート データの準備ができた際にそのことを通知する URL</td>
        </tr>

</tbody>
</table>

## <a name="response"></a>応答

応答ペイロードは、JSON 形式で次のように構成されます。

<table>
<thead>
    <tr>
      <th>項目</th>
      <th>説明</th>
    </tr>
</thead>
    <tr>
      <td>応答コード</td>
      <td>201/500/400</td>
    </tr>
    <tr>
      <td>応答ペイロード</td>
      <td><pre>{
    "data": {
        "reportId": reportId
    },
    "errors": []
}
</pre>
      </td>
    </tr>
<tr></tr>
  </tbody>
</table>

## <a name="response-parameters"></a>応答パラメーター

次の表に示すのは、応答内のパラメーターです。  

|パラメーター|説明|
|----|----|
|reportId|スケジュールされたレポートの ID を表します|

レポート データの準備ができた時に通知を受けるためのコールバック URL を設定した場合は、[レポート データの取得](get-report-data.md)メソッドを呼び出すことで、ダウンロードの準備が整い次第、レポート データをフェッチすることができます。

## <a name="see-also"></a>関連項目

- [分析レポート API (Swagger)](https://apidocs.microsoft.com/services/analyticsreportingapis)

- [レポート データの取得](get-report-data.md)

- [レポート テンプレートの管理](manage-report-templates-and-scheduled-reports.md)

- [サンプル レポート テンプレート](sample-report-templates.md)

- [ハードウェア ダッシュボード API のサンプル (GitHub)](https://aka.ms/hpc_async_api_samples)
