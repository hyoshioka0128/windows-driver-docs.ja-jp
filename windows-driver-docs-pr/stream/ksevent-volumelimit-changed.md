---
title: KSEVENT \_ volumelimit の \_ 変更 (ストリーム)
description: KSEVENT \_ volumelimit \_ CHANGED イベントは、ボリューム変更アクションをカーネルモードドライバーからユーザーモードに伝達します。
ms.assetid: C4CB9E8A-A0B6-48E1-B020-EA6A0768AE05
keywords:
- ストリーミングメディアデバイスの KSEVENT_VOLUMELIMIT_CHANGED
topic_type:
- apiref
api_name:
- KSEVENT_VOLUMELIMIT_CHANGED
api_type:
- NA
ms.date: 07/07/2020
ms.localizationpriority: medium
ms.openlocfilehash: 8d792c2f06183294822ee351f71f562233b54961
ms.sourcegitcommit: ff2f72fe98f6ba559c1c01b17d25c773df7337c1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2020
ms.locfileid: "86060845"
---
# <a name="ksevent_volumelimit_changed-stream"></a>KSEVENT \_ volumelimit の \_ 変更 (ストリーム)

**KSEVENT \_ volumelimit \_ CHANGED**イベントは、ボリューム変更アクションをカーネルモードドライバーからユーザーモードに伝達します。

## <a name="usage-summary-table"></a>使用状況の概要テーブル

| 取得 | オン | Target | イベント記述子の種類 | イベント値の種類 |
|--|--|--|--|--|
| いいえ | はい | Pin | [**KSE_NODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kse_node) | [**KSEVENTDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata) |
