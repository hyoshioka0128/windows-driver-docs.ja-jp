---
title: JobHistory 要素 (必須)
description: 必須の JobHistory 要素には、スキャンデバイスで最後に完了したジョブを説明する Jobhistory 要素の一覧が含まれています。
ms.assetid: d1439e56-b2fe-4db8-b063-56537a3346c6
keywords:
- JobHistory 要素イメージングデバイス
topic_type:
- apiref
api_name:
- wscn JobHistory
api_type:
- Schema
ms.date: 07/06/2020
ms.localizationpriority: medium
ms.openlocfilehash: 4f16fcbeec046dbeabc8af1d81ce4f83fb749a90
ms.sourcegitcommit: 40d7d538756767d26bbda636589f614f85a6fab3
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86020049"
---
# <a name="jobhistory-element-required"></a>JobHistory 要素 (必須)

必須の**Jobhistory**要素には、スキャンデバイスで最後に完了したジョブを説明する[**jobhistory**](jobsummary.md)要素の一覧が含まれています。

## <a name="usage"></a>使用

```xml
<wscn:JobHistory>
  child elements
</wscn:JobHistory>
```

## <a name="attributes"></a>属性

属性はありません。

## <a name="child-elements"></a>子要素

| 要素 |
|--|
| [**JobSummary**](jobsummary.md) |

## <a name="parent-elements"></a>親要素

| 要素 |
|--|
| [**GetJobHistoryResponse**](getjobhistoryresponse.md) |

## <a name="remarks"></a>注釈

**Jobhistory**要素には、スキャナーが最近完了したすべてのジョブの[**jobhistory**](jobsummary.md)要素が含まれています。 WSD スキャンサービスに最近完了したジョブのレコードが存在しない場合、 **Jobhistory**は空になります。 スキャンサービスは、この一覧を[**Getjobhistory 応答**](getjobhistoryresponse.md)から返します。

WSD Scan サービスが格納して返すジョブ履歴の量は、実装固有です。

## <a name="see-also"></a>こちらもご覧ください

[**GetJobHistoryResponse**](getjobhistoryresponse.md)

[**JobSummary**](jobsummary.md)
