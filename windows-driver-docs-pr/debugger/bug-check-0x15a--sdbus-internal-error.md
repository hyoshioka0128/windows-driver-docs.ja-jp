---
title: バグ チェック 0x15A SDBUS_INTERNAL_ERROR
description: SDBUS_INTERNAL_ERROR のバグ チェックでは、0x0000015A の値を持ちます。 これは、SD に接続されたデバイスで、回復不可能なハードウェア障害が発生したことを示します。
ms.assetid: C5FBE617-DADD-452C-A1BC-A0DE228FF2DE
keywords:
- バグ チェック 0x15A SDBUS_INTERNAL_ERROR
- SDBUS_INTERNAL_ERROR
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- SDBUS_INTERNAL_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3f5ef8c28ad95e0afb9a38fc5d1d4fb507ee8543
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67520023"
---
# <a name="bug-check-0x15a-sdbusinternalerror"></a>バグ チェック 0x15A:SDBUS\_内部\_エラー


SDBUS\_内部\_エラーのバグ チェックが 0x0000015A の値を持ちます。 これは、SD に接続されたデバイスで、回復不可能なハードウェア障害が発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="sdbusinternalerror-parameters"></a>SDBUS\_内部\_エラー パラメーター


| パラメーター | 説明                                                    |
|-----------|----------------------------------------------------------------|
| 1         | エラーの原因となった内部 SD 作業パケットへのポインター |
| 2         | ポインター コント ローラーのソケット情報                      |
| 3         | バス ドライバーに送信 SD 要求パケットへのポインター   |
| 4         | 予約済み                                                       |

 

 

 




