---
title: サンプル レポート テンプレート
description: Windows ドライバー申請エラーのサンプル レポート テンプレートを示します。 コードの形式は、REST API と JSON です。
ms.topic: article
ms.author: shganesh
ms.date: 09/01/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3ee53663a4c58346043d79d386aea5162eed268b
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "63334919"
---
# <a name="sample-report-templates"></a>サンプル レポート テンプレート

この記事では、一般的なビジネス ニーズにおいてよく発生する申請エラーを対象に、いくつかのレポート テンプレートを示します。 これらのテンプレートは、そのまま再利用することもできますし、ビジネス ニーズに基づいてカスタマイズすることもできます。

## <a name="request-syntax"></a>要求の構文

|メソッド|要求 URI|
|----|----|
|POST|`https://manage.devcenter.microsoft.com/analytics/driver/reporttemplate`|

## <a name="request-headers"></a>要求ヘッダー

|Header|種類|説明|
|----|----|----|
|Authorization|string|必須。 **Bearer** *\<トークン\>* という形式の Azure AD アクセス トークン|
|Content-Type|string|Application/JSON|

## <a name="sample-1--show-all-available-columns-for-ihv-failure-details-for-the-last-7-days"></a>サンプル 1:過去 7 日間の *IHV エラー*詳細に使用可能なすべての列を表示する

次の API 要求ペイロードでは、IHV エラー レポートで使用できるすべての列を一覧表示し、reportPeriod を過去 7 日間に設定しています。

```json
{
   "view":"IHVDriver",
   "projection":[
      "ReportId",
      "FailureDate",
      "FailureDateTime",
      "ApplicationId",
      "SubmissionId",
      "FailureName",
      "FailureHash",
      "Symbol",
      "OSVersion",
      "OSName",
      "EventType",
      "Market",
      "DeviceType",
      "DriverName",
      "DriverVersion",
      "Architecture",
      "OEMName",
      "OEMModel",
      "FlightRing",
      "Mode",
      "CPUName",
      "OSSKUType",
      "ReleaseName",
      "CabType",
      "CabIdHash",
      "CabExpirationTime",
      "DeviceId",
      "HardwareId",
      "CabCollectionTime",
      "EventCount"
   ],
   "dateRange":{
      "reportPeriod":"Last7Days"
   }
}
```

## <a name="sample-2-show-all-available-columns-for-oem-failure-details-for-the-last-7-days"></a>サンプル 2:過去 7 日間の *OEM エラー*詳細に使用可能なすべての列を表示する

次の API 要求ペイロードでは、*OEM エラー* レポートで使用できるすべての列を一覧表示し、reportPeriod を過去 7 日間に設定しています。

```json
{
   "view":"OEMDriver",
   "projection":
  [
      "ReportId",
      "FailureDate",
      "FailureDateTime",
      "FailureName",
      "FailureHash",
      "Symbol",
      "OSVersion",
      "EventType",
      "Market",
      "DeviceType",
      "DriverName",
      "DriverVersion",
      "Architecture",
      "Model",
      "Baseboard",
      "ModelFamily",
      "FlightRing",
      "Mode",
      "CPUName",
      "OSSKUType",
      "ReleaseName",
      "CabType",
      "CabIdHash",
      "CabExpirationTime",
      "DeviceId",
      "HardwareId",
      "CabCollectionTime",
      "EventCount"
   ],
   "dateRange":{
      "reportPeriod":"Last7Days"
   }
}
```

## <a name="sample-3--show-the-number-of-ihv-failures-the-unique-devices-impacted-for-each-driver-over-the-last-30-days-and-sort-by-devices-impacted"></a>サンプル 3:過去 30 日間の IHV エラーの数と、各ドライバーの影響を受ける一意のデバイスを表示し、影響を受けるデバイスごとに並べ替える

この API 要求ペイロードでは、過去 30 日間に報告されたドライバー エラーの合計数と、各ドライバーの影響を受けた一意のデバイスを一覧表示する IHV エラー レポートを呼び出しています。 レポートは、影響を受けたデバイスを基準に並べ替えられます。

```json
{
   "view":"IHVDriver",
   "projection":
  [
      "DriverName",
      "DriverVersion",
      "FailureName",
      "FailureHash"
   ],
   "dateRange":{
      "reportPeriod":"Last30Days"
   },
   "aggregation":{
      "aggregatedColumns":[
         "SUM(EventCount)",
         "DCOUNT(DeviceId)"
      ]
   },
   "orderby":[
      {
         "attribute":"DCOUNT(DeviceId)",
         "sort":"desc"
      }
   ]
}
```

## <a name="sample-4-list-the-number-of-oem-failure-details-over-the-past-seven-days-for-which-the-number-of-kernel-crashes-is-greater-than-1000"></a>サンプル 4:過去 7 日間の OEM エラー詳細のうち、カーネル クラッシュの数が 1000 を超えているものの数を一覧表示する

この API 要求ペイロードでは、過去 7 日間に報告されたすべてのエラーのうち、その期間中のカーネル クラッシュが 1000 を超えているエラーだけを一覧表示する OEM エラー レポートを呼び出しています。

```json
{
   "view":"OEMDriver",
   "projection":[
      "FailureName",
      "FailureHash"
   ],
   "dateRange":{
      "reportPeriod":"Last7Days"
   },
   "condition":{
      "and":[
         {
            "attribute":"EventType",
            "operator":"eq",
            "value":"Kernel"
         }
      ]
   },
   "aggregation":{
      "aggregatedColumns":[
         "SUM(EventCount)"
      ],
      "condition":{
         "or":[
            {
               "attribute":"SUM(EventCount)",
               "operator":"gt",
               "value":"1000"
            }
         ]
      }
   }
}
```

## <a name="sample-5-list-the-top-10-drivers-that-impact-the-maximum-number-of-unique-devices-in-the-last-90-days"></a>サンプル 5:過去 90 日間に最も多くの一意デバイスに影響を与えた上位 10 個のドライバーを一覧表示する

この API 要求ペイロードでは、すべてのドライバーを対象に IHV エラー レポートを呼び出しています。 その後、エラーの影響を受けたデバイスの数を基準に一覧を集計して並べ替え、デバイスに影響を与えた上位 10 個のドライバーを表示しています。

```json
{
  "view": "IHVDriver",
  "projection": [
    "DriverName"
  ],
  "dateRange": {
    "reportPeriod": "Last90Days"
  },
  
  "aggregation": {
    "aggregatedColumns": [
      "DCOUNT(DeviceId)"
    ]
  },
  "orderby": [
      {
        "attribute": "DCOUNT(DeviceId)",
        "sort": "desc"
      }
    ],
    "limit": 10  
}
```

## <a name="see-also"></a>関連項目

- [レポート テンプレートの新規作成](create-a-new-report-template.md)

- [分析レポート API (Swagger)](https://apidocs.microsoft.com/services/analyticsreportingapis)

- [ハードウェア ダッシュボード API のサンプル (GitHub)](https://aka.ms/hpc_async_api_samples)
