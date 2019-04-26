---
title: バグ チェック 0x11F INVALID_DRIVER_HANDLE
description: INVALID_DRIVER_HANDLE のバグ チェックでは、0x0000011F の値を持ちます。 これは、ドライバー オブジェクトを挿入すると、ハンドルを参照してドライバーを初期のハンドルをだれかが閉じたことを示します。
ms.assetid: A669256B-737D-4215-8E0E-5500D7704F4E
keywords:
- バグ チェック 0x11F INVALID_DRIVER_HANDLE
- INVALID_DRIVER_HANDLE
ms.date: 01/30/2019
topic_type:
- apiref
api_name:
- INVALID_DRIVER_HANDLE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b6afd88545c1043e19c725337742b4b10f5dc5c7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358152"
---
# <a name="bug-check-0x11f-invaliddriverhandle"></a>バグ チェック 0x11F:無効な\_ドライバー\_処理


無効な\_ドライバー\_ハンドルのバグ チェックが 0x0000011F の値を持ちます。 これは、ドライバー オブジェクトを挿入すると、ハンドルを参照してドライバーを初期のハンドルをだれかが閉じたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="invaliddriverhandle-parameters"></a>無効な\_ドライバー\_ハンドル パラメーター


| パラメーター | 説明                                         |
|-----------|-----------------------------------------------------|
| 1         | ドライバー オブジェクトのハンドル値。             |
| 2         | オブジェクトを参照しようとしました。 状態が返されます。 |
| 3         | PDRIVER のアドレス\_オブジェクト。                 |
| 4         | 予約済み                                            |

 

 

 




