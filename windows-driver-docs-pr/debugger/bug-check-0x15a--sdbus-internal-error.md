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
ms.openlocfilehash: 57b520c8cfc1e71717c76bd98fc0eb08a7a73ea2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573809"
---
# <a name="bug-check-0x15a-sdbusinternalerror"></a>バグ チェック 0x15A:SDBUS\_内部\_エラー


SDBUS\_内部\_エラーのバグ チェックが 0x0000015A の値を持ちます。 これは、SD に接続されたデバイスで、回復不可能なハードウェア障害が発生したことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="sdbusinternalerror-parameters"></a>SDBUS\_内部\_エラー パラメーター


| パラメーター | 説明                                                    |
|-----------|----------------------------------------------------------------|
| 1         | エラーの原因となった内部 SD 作業パケットへのポインター |
| 2         | ポインター コント ローラーのソケット情報                      |
| 3         | バス ドライバーに送信 SD 要求パケットへのポインター   |
| 4         | 予約済み                                                       |

 

 

 




