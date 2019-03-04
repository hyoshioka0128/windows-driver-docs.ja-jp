---
title: レポート テンプレートとスケジュールされたレポートを管理する
description: これらの API を使用して、既存の Windows ドライバー申請レポート テンプレートを表示および変更し、スケジュールされたレポートを管理します
ms.topic: article
ms.author: shganesh
ms.date: 09/01/2018
ms.localizationpriority: medium
ms.openlocfilehash: e009b5ec0b4404172346cc9fdb64454a309c38f7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518754"
---
# <a name="manage-report-templates-and-scheduled-reports"></a>レポート テンプレートとスケジュールされたレポートを管理する

既存のレポート テンプレートを表示および変更し、スケジュールされたレポートを管理するには、これらのメソッドを使用します。

## <a name="request-headers"></a>要求ヘッダー

|Header|種類|説明|
|----|----|----|
|Authorization|string|必須。 **Bearer** *\<トークン\>* という形式の Azure AD アクセス トークン|
|Content-Type|string|Application/JSON|

## <a name="view-a-definition-of-a-report-template"></a>レポート テンプレートの定義を表示する

レポート テンプレートの定義を表示するには、このメソッドを使用します。

<table>
  <thead>
    <tr>
      <th>項目</th>
      <th>説明</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>GET</td>
      <td><pre>https://manage.devcenter.microsoft.com/analytics/driver/reporttemplate/{templateId}</pre></td>
    </tr>
    <tr>
      <td>応答コード</td>
      <td>200/500/400</td>
    </tr>
    <tr>
      <td>応答ペイロード</td>
      <td><pre>{
    "data": {
        "templateId": &lt;templateid&gt;
        " template": "{report template}”,
    "errors": []
}</pre></td>
    </tr>
  </tbody>
</table>

## <a name="view-all-available-report-templates"></a>使用可能なすべてのレポート テンプレートを表示する

自分のアカウント用に作成したすべてのレポート テンプレートを表示するには、このメソッドを使用します。

<table>
  <thead>
    <tr>
      <th>項目</th>
      <th>説明</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>GET</td>
      <td><pre>https://manage.devcenter.microsoft.com/analytics/driver/reporttemplate</pre></td>
    </tr>
    <tr>
      <td>応答コード</td>
      <td>200/500/400</td>
    </tr>
    <tr>
      <td>応答ペイロード</td>
      <td><pre>{
    "data": [
        {
            "templateId": &lt;templateid&gt;,
            "template": "{report template}",
            "createdDatetime": "2018-06-24T16:39:46.683",
            "modifiedDatetime": "2018-06-24T16:39:46.683"
        }
        {
            "templateId": &lt;templateid&gt;,
            "template": "{report template}",
            "createdDatetime": "2018-06-27T14:09:27.243",
            "modifiedDatetime": "2018-06-27T14:09:32.733"
        }
],
    "errors": []
}
</pre></td>
    </tr>
  </tbody>
</table>

## <a name="edit-a-report-template"></a>レポート テンプレートを編集する

既存のレポート テンプレートを編集するには、このメソッドを使用します。

<table>
  <thead>
    <tr>
      <th>項目</th>
      <th>説明</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>POST</td>
      <td><pre>https://manage.devcenter.microsoft.com/analytics/driver/reporttemplate/{templateId}</pre></td>
    </tr>
    <tr>
      <td>サンプル ペイロード</td>
      <td><pre>{<br/>   &quot;view&quot;:&quot;IHVDriver&quot;,
   &quot;projection&quot;:[<br/>      &quot;EventType&quot;,
      &quot;DriverName&quot;
   ],
   &quot;dateRange&quot;:{<br/>      &quot;reportPeriod&quot;:&quot;Yesterday&quot;
   },
   &quot;condition&quot;:{  

   },
   "aggregation":{  
      "aggregatedColumns":[  
         "sum(EventCount)"
      ]
   }
}</pre></td>
    </tr>
    <tr>
      <td>応答コード</td>
      <td>201/500/400</td>
    </tr>
    <tr>
      <td>応答ペイロード</td>
      <td><pre>{
    "data": {
        "templateId": “templateId”
    },
    "errors": []
}</pre></td>
    </tr>
  </tbody>
</table>

## <a name="view-the-scheduled-reports"></a>スケジュールされたレポートを表示する

スケジュールされたレポートの一覧を表示するには、このメソッドを使用します。

<table>
  <thead>
    <tr>
      <th>項目</th>
      <th>説明</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>取得</td>
      <td><pre>https://manage.devcenter.microsoft.com/analytics/driver/report</pre></td>
    </tr>
    <tr>
      <td>ペイロード</td>
      <td>なし</td>
    </tr>
    <tr>
      <td>応答コード</td>
      <td>201/500/400</td>
    </tr>
    <tr>
      <td>サンプル応答ペイロード</td>
      <td><pre>{
    &quot;data&quot;: [
        {
            &quot;reportId&quot;: 2,
            &quot;templateId&quot;: 7,
            &quot;schedule&quot;: &quot;{report details}&quot;,
            &quot;isActive&quot;: true,
            &quot;createdDatetime&quot;: &quot;2018-06-24T17:04:18.487&quot;,
            &quot;modifiedDatetime&quot;: &quot;2018-06-25T08:28:42.063&quot;
        },

                  {
            "reportId": 4,
            "templateId": 12,
            "schedule": "{report details}",
            "isActive": true,
            "createdDatetime": "2018-06-28T10:11:44.873",
            "modifiedDatetime": "2018-06-28T10:30:27.93"
        }
           ],
    "errors": []
}
</pre></td>
    </tr>
  </tbody>
</table>

## <a name="edit-a-scheduled-report"></a>スケジュールされたレポートを編集する

既存のスケジュールされたレポートを編集するには、このメソッドを使用します。

<table>
  <thead>
    <tr>
      <th>項目</th>
      <th>説明</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>POST</td>
      <td><pre>https://manage.devcenter.microsoft.com/analytics/driver/report/{reportId}</pre></td>
    </tr>
    <tr>
      <td>ペイロード</td>
      <td><pre>{
   "templateId":&lt;templateid&gt;,
   "Schedule":{
      "StartTime":"2018-07-24T00:00:00Z", //Datetime in UTC
      "RecurrenceInterval":12, // in hours
      "Recurrence":2
   }
}</pre></td>
    </tr>
    <tr>
      <td>応答コード</td>
      <td>201/500/400</td>
    </tr>
    <tr>
      <td>応答ペイロード</td>
      <td><pre>{
    "data": {
        "reportId": &lt;reportId&gt;
    },
    "errors": []
}</pre></td>
    </tr>
  </tbody>
</table>

## <a name="pause-a-report"></a>レポートを一時停止する

スケジュールされたレポートを一時停止するには、このメソッドを使用します。

<table>
  <tbody>
    <tr>
      <td>POST</td>
      <td><pre>https://manage.devcenter.microsoft.com/analytics/driver/report/pause/{reportId}</pre></td>
    </tr>
    <tr>
      <td>応答コード</td>
      <td>201/500/400</td>
    </tr>
    <tr>
      <td>応答ペイロード</td>
      <td><pre>{
    "data": {
        "reportId": &lt;reportId&gt;
    },
    "errors": []
}</pre></td>
    </tr>
  </tbody>
</table>

## <a name="resume-a-report"></a>レポートを再開する

スケジュールされたレポートを再開するには、このメソッドを使用します。

<table>
  <tbody>
    <tr>
      <td>POST</td>
      <td><pre>https://manage.devcenter.microsoft.com/analytics/driver/report/resume/{reportId}</pre></td>
    </tr>
    <tr>
      <td>応答コード</td>
      <td>201/500/400</td>
    </tr>
    <tr>
      <td>応答ペイロード</td>
      <td><pre>{
    "data": {
        "reportId": &lt;reportId&gt;
    },
    "errors": []
}</pre></td>
    </tr>
  </tbody>
</table>

## <a name="see-also"></a>関連項目

- [分析レポート API (Swagger)](https://apidocs.microsoft.com/services/analyticsreportingapis)

- [ハードウェア ダッシュボード API のサンプル (GitHub)](https://aka.ms/hpc_async_api_samples)
