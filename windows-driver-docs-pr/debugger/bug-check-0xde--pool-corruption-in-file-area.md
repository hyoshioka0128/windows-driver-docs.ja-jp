---
title: バグ チェック 0xDE POOL_CORRUPTION_IN_FILE_AREA
description: POOL_CORRUPTION_IN_FILE_AREA のバグ チェックでは、0x000000DE の値を持ちます。 これは、ドライバーによってページ宛てのディスクを保持するために使用されているプール メモリが破損していることを示します。
ms.assetid: 6394e0fa-76ee-4924-8aa3-d10a4d57c6e8
keywords:
- バグ チェック 0xDE POOL_CORRUPTION_IN_FILE_AREA
- POOL_CORRUPTION_IN_FILE_AREA
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- POOL_CORRUPTION_IN_FILE_AREA
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: afbd74a9760a9a835b14b9eaf25651c50cda255d
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67518836"
---
# <a name="bug-check-0xde-poolcorruptioninfilearea"></a>バグ チェック 0xDE:プール\_破損\_IN\_ファイル\_領域


プール\_破損\_IN\_ファイル\_領域のバグ チェックが 0x000000DE の値を持ちます。 これは、ドライバーによってページ宛てのディスクを保持するために使用されているプール メモリが破損していることを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="poolcorruptioninfilearea-parameters"></a>プール\_破損\_IN\_ファイル\_領域のパラメーター


なし

<a name="cause"></a>原因
-----

メモリ マネージャーは、ファイルを逆参照されたとき、に、このプールのメモリの破損を検出します。

 

 




