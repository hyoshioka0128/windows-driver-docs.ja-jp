---
title: RequestedElements 要素の名前
description: これには、Name 要素が、クライアントでは、呼び出し時に GetScannerElementsRequest または GetJobElementsRequest のデータが必要 WSD スキャン サービス スキーマのセクションを識別が必要です。
ms.assetid: 1b2bc3b4-24de-4957-a72a-6788425dc3b9
keywords:
- RequestedElements 要素イメージング デバイスの名前
topic_type:
- apiref
api_name:
- wscn Name
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4b37e6430ebba91062f593a6fc048a6d4f42264
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379673"
---
# <a name="name-for-requestedelements-element"></a>RequestedElements 要素の名前


この必須**名前**要素は、クライアントの呼び出し時にデータを要求する WSD スキャン サービス スキーマのセクションを識別します[ **GetScannerElementsRequest** ](getscannerelementsrequest.md)または。[**GetJobElementsRequest**](getjobelementsrequest.md)します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:Name>
  text
</wscn:Name>
```

<a name="attributes"></a>属性
----------

属性はありません。

<a name="text-value"></a>テキスト値
----------

必須。

[ **GetScannerElementsRequest**](getscannerelementsrequest.md)QName 値は次のいずれか。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>QName</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><span id="wscn_ScannerDescription"></span><span id="wscn_scannerdescription"></span><span id="WSCN_SCANNERDESCRIPTION"></span>wscn:ScannerDescription</p></td>
<td><p>すべてのデバイスのスキャンのわかりやすい情報を取得します。</p></td>
</tr>
<tr class="even">
<td><p><span id="wscn_ScannerConfiguration"></span><span id="wscn_scannerconfiguration"></span><span id="WSCN_SCANNERCONFIGURATION"></span>wscn:ScannerConfiguration</p></td>
<td><p>すべてのスキャン デバイスの構成情報を取得します。</p></td>
</tr>
<tr class="odd">
<td><p><span id="wscn_ScannerStatus"></span><span id="wscn_scannerstatus"></span><span id="WSCN_SCANNERSTATUS"></span>wscn:ScannerStatus</p></td>
<td><p>全体の状態 セクションで取得を含む<a href="activeconditions.md" data-raw-source="[&lt;strong&gt;ActiveConditions&lt;/strong&gt;](activeconditions.md)"> <strong>ActiveConditions</strong> </a>と<a href="conditionhistory.md" data-raw-source="[&lt;strong&gt;ConditionHistory&lt;/strong&gt;](conditionhistory.md)"> <strong>ConditionHistory</strong></a>します。</p></td>
</tr>
<tr class="even">
<td><p><span id="xmlns_VendorSection"></span><span id="xmlns_vendorsection"></span><span id="XMLNS_VENDORSECTION"></span>xmlns:VendorSection</p></td>
<td><p>WSD スキャン サービスにベンダー定義の拡張機能の特定のセクションを取得します。</p></td>
</tr>
</tbody>
</table>

 

[ **GetJobElementsRequest**](getjobelementsrequest.md)QName 値は次のいずれか。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>QName</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><span id="wscn_JobStatus"></span><span id="wscn_jobstatus"></span><span id="WSCN_JOBSTATUS"></span>wscn:JobStatus</p></td>
<td><p>現在の取得<a href="jobstatus.md" data-raw-source="[&lt;strong&gt;JobStatus&lt;/strong&gt;](jobstatus.md)"> <strong>JobStatus</strong> </a>指定したジョブの要素のデータ。</p></td>
</tr>
<tr class="even">
<td><p><span id="wscn_ScanTicket"></span><span id="wscn_scanticket"></span><span id="WSCN_SCANTICKET"></span>wscn:ScanTicket</p></td>
<td><p>取得、 <a href="scanticket.md" data-raw-source="[&lt;strong&gt;ScanTicket&lt;/strong&gt;](scanticket.md)"> <strong>ScanTicket</strong> </a>指定したジョブの要素のデータ。</p></td>
</tr>
<tr class="odd">
<td><p><span id="wscn_Documents"></span><span id="wscn_documents"></span><span id="WSCN_DOCUMENTS"></span>wscn:Documents</p></td>
<td><p>取得、 <a href="documents.md" data-raw-source="[&lt;strong&gt;Documents&lt;/strong&gt;](documents.md)"><strong>ドキュメント</strong></a>指定したジョブの要素のデータ。</p></td>
</tr>
<tr class="even">
<td><p><span id="xmlns_VendorSection"></span><span id="xmlns_vendorsection"></span><span id="XMLNS_VENDORSECTION"></span>xmlns:VendorSection</p></td>
<td><p>WSD スキャン サービスにベンダー定義の拡張機能の特定のセクションを取得します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="child-elements"></a>子要素


子要素はありません。

## <a name="parent-elements"></a>親要素


<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th>要素</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="requestedelements.md" data-raw-source="[&lt;strong&gt;RequestedElements&lt;/strong&gt;](requestedelements.md)"><strong>RequestedElements</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

Qname は、クライアントの情報を必要がある WSD スキャン サービス スキーマ内で最上位の要素を識別する必要があります。 クライアントは、スキーマ名前空間と要素名の両方を指定する必要があります。

## <a name="see-also"></a>関連項目


[**GetJobElementsRequest**](getjobelementsrequest.md)

[**ActiveConditions**](activeconditions.md)

[**ConditionHistory**](conditionhistory.md)

[**ドキュメント**](documents.md)

**GetJobElementsRequest**
[**GetScannerElementsRequest**](getscannerelementsrequest.md)

[**JobStatus**](jobstatus.md)

[**RequestedElements**](requestedelements.md)

[**ScanTicket**](scanticket.md)

 

 






