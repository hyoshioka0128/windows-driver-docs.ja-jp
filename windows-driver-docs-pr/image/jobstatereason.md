---
title: JobStateReason 要素
description: 省略可能な JobStateReason 要素には、ジョブが現在の状態である理由の 1 つを指定します。
ms.assetid: daaa288b-fa56-4d29-92f6-0283fbbd2fe8
keywords:
- JobStateReason 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn JobStateReason
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e311538ed80b498bcf2ab48c95e017e3e0c0972
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550305"
---
# <a name="jobstatereason-element"></a>JobStateReason 要素


省略可能な**JobStateReason**要素は、ジョブが現在の状態である理由の 1 つを指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:JobStateReason>
  text
</wscn:JobStateReason>
```

<a name="attributes"></a>属性
----------

属性はありません。

<a name="text-value"></a>テキスト値
----------

必須。 次のいずれかの値です。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>用語</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><span id="InvalidScanTicket"></span><span id="invalidscanticket"></span><span id="INVALIDSCANTICKET"></span>InvalidScanTicket</p></td>
<td><p>ジョブは、WSD スキャン サービスは、ScanTicket を処理できなかったために拒否されました。</p></td>
</tr>
<tr class="even">
<td><p><span id="DocumentFormatError"></span><span id="documentformaterror"></span><span id="DOCUMENTFORMATERROR"></span>DocumentFormatError</p></td>
<td><p>WSD スキャン サービスは、要求されたドキュメントの形式をサポートしていません。</p></td>
</tr>
<tr class="odd">
<td><p><span id="ImageTransferError"></span><span id="imagetransfererror"></span><span id="IMAGETRANSFERERROR"></span>ImageTransferError</p></td>
<td><p>ジョブ内のイメージのデータ転送に失敗しました。 このエラーが発生した場合、WSD スキャン サービスは、ジョブを中止する必要があります。</p></td>
</tr>
<tr class="even">
<td><p><span id="JobCanceledAtDevice"></span><span id="jobcanceledatdevice"></span><span id="JOBCANCELEDATDEVICE"></span>JobCanceledAtDevice</p></td>
<td><p>デバイスのスキャンでスキャンの現在のジョブが取り消されました&#39;s フロント パネル。</p></td>
</tr>
<tr class="odd">
<td><p><span id="JobCompletedWithErrors"></span><span id="jobcompletedwitherrors"></span><span id="JOBCOMPLETEDWITHERRORS"></span>JobCompletedWithErrors</p></td>
<td><p>ジョブは 1 つ以上のエラーで完了しました。</p></td>
</tr>
<tr class="even">
<td><p><span id="JobCompletedWithWarnings"></span><span id="jobcompletedwithwarnings"></span><span id="JOBCOMPLETEDWITHWARNINGS"></span>JobCompletedWithWarnings</p></td>
<td><p>ジョブは少なくとも 1 つの警告がある完了しました。 ジョブのデータは、正常に転送が必要です。 この警告は、WSD スキャン サービスにジョブの処理にスキャン チケットへの変更が行われる可能性があります。</p></td>
</tr>
<tr class="odd">
<td><p><span id="JobScanning"></span><span id="jobscanning"></span><span id="JOBSCANNING"></span>JobScanning</p></td>
<td><p>スキャナーがジョブのデータをデジタル化します。</p></td>
</tr>
<tr class="even">
<td><p><span id="JobScanningAndTransferring"></span><span id="jobscanningandtransferring"></span><span id="JOBSCANNINGANDTRANSFERRING"></span>JobScanningAndTransferring</p></td>
<td><p>スキャナーがジョブのデータをデジタル化と、データのクライアントに転送します。</p></td>
</tr>
<tr class="odd">
<td><p><span id="JobTimedOut"></span><span id="jobtimedout"></span><span id="JOBTIMEDOUT"></span>JobTimedOut</p></td>
<td><p>WSD スキャン サービスでは、RetrieveImageRequest 操作の後にない適切なタイミングで CreateScanJobRequest 操作後に、ジョブが終了しました。</p></td>
</tr>
<tr class="even">
<td><p><span id="JobTransferring"></span><span id="jobtransferring"></span><span id="JOBTRANSFERRING"></span>JobTransferring</p></td>
<td><p>ジョブ データがクライアントに転送されます。</p></td>
</tr>
<tr class="odd">
<td><p><span id="None"></span><span id="none"></span><span id="NONE"></span>[なし]</p></td>
<td><p>ジョブには、ジョブの状態に関する追加情報がありません。</p></td>
</tr>
<tr class="even">
<td><p><span id="ScannerStopped"></span><span id="scannerstopped"></span><span id="SCANNERSTOPPED"></span>ScannerStopped</p></td>
<td><p>デバイスのスキャンがアクティブの状態のため停止し、条件が訂正されるまで、ジョブを続行できません。</p></td>
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
<td><p><a href="jobcompletedstatereasons.md" data-raw-source="[&lt;strong&gt;JobCompletedStateReasons&lt;/strong&gt;](jobcompletedstatereasons.md)"><strong>JobCompletedStateReasons</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobstatereasons.md" data-raw-source="[&lt;strong&gt;JobStateReasons&lt;/strong&gt;](jobstatereasons.md)"><strong>JobStateReasons</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

WSD スキャン サービスの実装を検出する条件を表す値をサポートする必要があります。 特定の場合に使用できる値のサブセットのみをサポートするそのため、 **JobStateReason**理由は、実装では検出されません。

許可の値を拡張できますが、クライアントに影響がこのリストを拡張します。 クライアントは通常ローカライズ、 **JobStateReason** (その他の文字列変数の値) と同様の値は、ユーザーの言語をします。 ただし、クライアントには、ベンダー拡張の値は認識しません。 クライアントは、値を表示できますつまり受信"と"が、この値は英語で表示されます、一部のユーザーを理解しないため値。

## <a name="see-also"></a>関連項目


[**CreateScanJobRequest**](createscanjobrequest.md)

[**JobCompletedStateReasons**](jobcompletedstatereasons.md)

[**JobStateReasons**](jobstatereasons.md)

[**RetrieveImageRequest**](retrieveimagerequest.md)

 

 






