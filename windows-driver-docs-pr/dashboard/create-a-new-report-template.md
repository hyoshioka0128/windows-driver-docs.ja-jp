---
title: 新しいレポート テンプレートを作成する
description: ドライバー エラー レポートの新しいレポート テンプレートを作成する方法について説明します。 REST API の情報が含まれます。
ms.author: shganesh
ms.topic: article
ms.date: 09/01/2018
ms.localizationpriority: medium
ms.openlocfilehash: 853efe8c8d2282c7cec0d95f043401b2f96b9fc8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518741"
---
# <a name="create-a-new-report-template"></a>新しいレポート テンプレートを作成する

ビジネス ニーズに基づいて新しいレポート テンプレートを作成するには、このメソッドを使用します。 既存のレポート テンプレートは、「[レポート テンプレートとスケジュールされたレポートを管理する](manage-report-templates-and-scheduled-reports.md)」で説明されているメソッドを使って管理できます

## <a name="request-syntax"></a>要求の構文

|メソッド|要求 URI|
|----|----|
|POST|`https://manage.devcenter.microsoft.com/analytics/driver/reporttemplate`|

## <a name="request-header"></a>要求ヘッダー

|Header|種類|説明|
|----|----|----|
|Authorization|string|必須。 **Bearer** *\<トークン\>* という形式の Azure AD アクセス トークン|
|Content-Type|string|Application/JSON|

## <a name="request-payload"></a>要求のペイロード

以下のように、JSON 形式でレポート テンプレートを定義します。

```json
{
  "view": " IHVDriver", // select “OEMDriver” for OEM Hardware Error data

  "projection": [
    "column1",
    "column2",
    "column3"
  ],

  "dateRange":
    {
      "reportPeriod": "Yesterday" // select date range
    }
  ,

  "condition": {
    "and": [
      {
        "attribute": "column1",
        "operator": "eq",
        "value": "1" // value that you desire to compare
      },
      {
        "condition": {
          "or": [
            {
              "attribute": "column2",
              "operator": "eq",
              "value": "2" //value that you desire to compare
            },
            {
              "attribute": "column3",
              "operator": "eq",
              "value": "3" //value that you desire to compare
            }
          ]
        }
      }
    ],

    "or": []
  },

  "aggregation": {
    "aggregatedColumns": [
      "SUM(column1)",
      "DCOUNT(column2)"
    ],

    "condition": {
      "or": [
        {
          "attribute": "column5",
          "operator": "gt",
          "value": "100" //value that you desire to compare
        }
      ]
    }
  },

  "orderby": [
    {
      "attribute": "column4",
      "sort": "desc"
    }
  ],

  "limit": 100
}
```

## <a name="parameters"></a>パラメーター

このテーブルでは、レポート テンプレート作成 JSON でのパラメーターについて説明します。

<table>
    <thead>
      <tr>
            <th>パラメーター</th>
            <th>必須</th>
            <th>説明</th>
            <th>指定可能な値</th>
        </tr>
    </thead>
    <tbody>
    <tr>
        <td>表示</td>
        <td>〇</td>
        <td>ドライバー エラー レポートを探している IHV/ISV の場合は、<b>IHVDriver</b> を選択します。<br/>ハードウェア エラー レポートを探している OEM パートナーの場合は、<b>OEMDriver</b> を選択します。</td>
        <td><b>IHVDriver</b> <br/><b>OEMDriver</b></td>
    <tr/>
    <tr>
        <td>プロジェクション</td>
        <td>〇</td>
        <td>レポートで必要な列のリスト。 これは、ビューが <b>IHVDriver</b> か <b>OEMDriver<b>  かによって異なります</td>
        <td>利用できる列の一覧は後で示します</td>
    </tr>
    <tr>
        <td>reportPeriod</td>
        <td>〇</td>
        <td>エラー データを要求する対象の日付範囲</td>
        <td>昨日<br/>Last3Days<br/>Last7Days<br/>Last10Days<br/>Last15Days<br/>Last30Days<br/>Last60Days<br/>Last90Days</td>
    </tr>
    <tr>
        <td>オペレーター</td>
        <td>X</td>
        <td>フィルター条件に対してサポートされる演算子のセット</td>
        <td>IN<br/>EQ<br/>NEQ<br/>LT<br/><br/>GT<br/>LTE<br/>GTE<br/>LIKE</td>
    </tr>
    <tr>
        <td>aggregatedColumns</td>
        <td>X</td>
        <td>エラー データでサポートされる集計のセット</td>
        <td>SUM<br/>AVG<br/>COUNT<br/>DCOUNT<br/>MAX<br/>MIN</td>
    </tr>
    <tr>
        <td>orderby</td>
        <td>X</td>
        <td>結果セットの順序を定義します。asc (昇順) または desc (降順) の順に並べ替えることができます</td>
        <td>使用可能なすべての列でサポートされます </td>
    </tr>
    <tr>
        <td>limit</td>
        <td>X</td>
        <td>応答内の行数を制限します</td>
        <td>整数 &gt;= 0<br/>0 は全レコードを示します</td>
    </tr>
    </tbody>
</table>

## <a name="response"></a>応答

応答のペイロードは、JSON 形式で次のように構成されます。

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
        <td>201/500/400</td>
      </tr>
        <tr>
      <td>応答ペイロード</td>
          <td><pre>{
    &quot;data&quot;: {
        &quot;templateId&quot;: templateId
  },
  &quot;errors&quot;: null  }`</td>
      </tr>
     </tbody>
</table>

## 応答パラメーター

次のテーブルでは、応答のパラメーターについて説明します。

|パラメーター|説明| |----|----| |templateId|これは、作成されたレポート テンプレートのテンプレート ID です。 これは、Schedule Report API に対する入力として使用されます。 詳しくは、「[新しいレポートをスケジュールする](schedule-a-new-report.md)」をご覧ください。

既存のレポートは、「[レポート テンプレートとスケジュールされたレポートを管理する](manage-report-templates-and-scheduled-reports.md)」で説明されているメソッドを使って管理できます。 サンプル レポート テンプレートの一覧については、「[サンプル レポート テンプレート](sample-report-templates.md)」をご覧ください。

## プロジェクションに使用できる列 (IHV および OEM ビュー)

IHV または ISV 向けの Windows 10、Windows 8.x、Windows 7 のドライバー レポートでは、次の列から選択できます。

<table>
  <thead>
    <tr>
      <th>列名</th>
      <th>説明</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>ReportId</td>
      <td>このレコードが含まれるレポートのレポート ID</td>
    </tr>
    <tr>
      <td>FailureDate</td>
      <td>エラーが発生した日付 (mmddyy 形式)</td>
    </tr>
    <tr>
      <td>FailureDateTime</td>
      <td>エラーが発生したときのタイムスタンプ</td>
    </tr>
    <tr>
      <td>ApplicationId</td>
      <td>(<i>IHVDriver</i> ビューでのみ使用可能) エラーが発生したドライバー申請の ApplicationId または PrivateProductId</td>
    </tr>
    <tr>
      <td>SubmissionId</td>
      <td>(<i>IHVDriver</i> ビューでのみ使用可能) エラーが発生したドライバーの申請 ID</td>
    </tr>
    <tr>
      <td>FailureName</td>
      <td>エラー バケットの名前</td>
    </tr>
    <tr>
      <td>FailureHash</td>
      <td>エラー バケットのエラー ハッシュの値</td>
    </tr>
    <tr>
      <td>記号</td>
      <td>エラーのシンボル (存在する場合)</td>
    </tr>
    <tr>
      <td>OSVersion</td>
      <td>エラーが発生したオペレーティング システムのバージョン</td>
    </tr>
    <tr>
      <td>OSName</td>
      <td>(<i>IHVDriver</i> ビューでのみ使用可能) - エラーが発生したオペレーティング システムのフレンドリ名</td>
    </tr>
    <tr>
      <td>EventType</td>
      <td>エラー イベントがシステム エラー イベントかカーネル エラー イベントかを示します</td>
    </tr>
    <tr>
      <td>市場</td>
      <td>エラーが発生した市場</td>
    </tr>
    <tr>
      <td>DeviceType</td>
      <td>エラーが発生したデバイスの種類</td>
    </tr>
    <tr>
      <td>DriverName</td>
      <td>エラーの原因になったドライバーの名前</td>
    </tr>
    <tr>
      <td>DriverVersion</td>
      <td>エラーの原因になったドライバーのバージョン</td>
    </tr>
    <tr>
      <td>Architecture</td>
      <td>エラーが発生したアーキテクチャ</td>
    </tr>
    <tr>
      <td>OEMName</td>
      <td>(<i>IHVDriver</i> ビューでのみ使用可能) エラーが発生した OEM の名前</td>
    </tr>
    <tr>
      <td>OEMModel / Model</td>
      <td>エラーが発生した OEM モデルの名前<br/><i>IHVDriver</i> ビューでは <i>OEMModel</i> という名前です<br/><i>OEMDriver</i> ビューでは <i>Model</i> という名前です
</td>
    </tr>
    <tr>
      <td>FlightRing</td>
      <td>エラーが発生したフライト リング</td>
      </tr>
    <tr>
      <td>Mode</td>
      <td>カーネル モードまたはユーザー モードのどちらでエラーが発生したかを示します</td>
    </tr>
    <tr>
      <td>CPUName</td>
      <td>クラッシュが発生したデバイスの CPU 名</td>
    </tr>
    <tr>
      <td>OSSKUType</td>
      <td>エラーが発生した OS SKU の名前</td>
    </tr>
    <tr>
      <td>ReleaseName</td>
      <td>エラーが発生した OS の OS リリースの名前</td>
    </tr>
    <tr>
      <td>Baseboard</td>
      <td>(<i>OEMDriver</i> ビューでのみ使用可能) エラーが発生したベース ボードを示します</td>
    </tr>
    <tr>
      <td>ModelFamily</td>
      <td>(<i>OEMDriver</i> ビューでのみ使用可能) エラーが発生したモデル ファミリを示します</td>
    </tr>
    <tr>
      <td>CabType</td>
      <td>使用可能な CAB がカーネル CAB、ミニ CAB、フル CAB のいずれかを示します</td>
    </tr>
    <tr>
      <td>CabIdHash</td>
      <td><a href="https://manage.devcenter.microsoft.com/v1.0/my/analytics/driver/cabdownload" data-raw-source="[CabDownload](https://manage.devcenter.microsoft.com/v1.0/my/analytics/driver/cabdownload)">CabDownload</a> API を使用して CAB ファイルをダウンロードするために使用できる CabID のハッシュ</td>
    </tr>
    <tr>
      <td>DeviceId</td>
      <td>エラーが発生したデバイス ID</td>
    </tr>
    <tr>
      <td>HardwareId</td>
      <td>エラーが発生したデバイスのハードウェア ID</td>
    </tr>
    <tr>
      <td>CabCollectionTime</td>
      <td>Microsoft のサーバーによって CAB が収集されたときのタイムスタンプ</td>
    </tr>
    <tr>
      <td>CabExpirationTime</td>
      <td>CAB の有効期限が切れてダウンロードできなくなる時刻</td>
    </tr>
    <tr>
      <td>EventCount</td>
      <td>そのエラー ハッシュで発生したエラー イベントの数</td>
    </tr>
  </tbody>
</table>

既存のレポートは、「[レポート テンプレートとスケジュールされたレポートを管理する](manage-report-templates-and-scheduled-reports.md)」で説明されているメソッドを使って管理できます。 サンプル レポート テンプレートの一覧については、「[サンプル レポート テンプレート](sample-report-templates.md)」をご覧ください。

## 関連項目

- [分析レポート API (Swagger)](https://apidocs.microsoft.com/services/analyticsreportingapis)

- [新しいレポートをスケジュールする](schedule-a-new-report.md)

- [レポート テンプレートを管理する](manage-report-templates-and-scheduled-reports.md)

- [サンプル レポート テンプレート](sample-report-templates.md)

- [ハードウェア ダッシュボード API のサンプル (GitHub)](https://aka.ms/hpc_async_api_samples)
