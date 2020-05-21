---
title: バグチェック 0x20001 HYPERVISOR_ERROR
description: HYPERVISOR_ERROR バグチェックの値は0x00020001 です。 これは、ハイパーバイザーで致命的なエラーが発生したことを示します。
ms.assetid: 5F62DEEA-D192-46ED-827C-021A749D7091
keywords:
- バグチェック 0x20001 HYPERVISOR_ERROR
- HYPERVISOR_ERROR
ms.date: 05/15/2020
topic_type:
- apiref
api_name:
- HYPERVISOR_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 067d8df4d045e11eb96de2a78d10923333f4b6b1
ms.sourcegitcommit: 4d1ed685d198629f792d287619621a87ca42c26f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2020
ms.locfileid: "83435370"
---
# <a name="bug-check-0x20001-hypervisor_error"></a>バグチェック 0x20001: ハイパーバイザー \_ エラー

ハイパーバイザー \_ エラーのバグチェックには、0x00020001 の値が含まれています。 これは、ハイパーバイザーで致命的なエラーが発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。

## <a name="hypervisor_error-parameters"></a>ハイパーバイザーの \_ エラーパラメーター


| パラメーター | 説明 |
|-----------|-------------|
| 1         | 予約済み    |
| 2         | 予約済み    |
| 3         | 予約済み    |
| 4         | 予約済み    |

## <a name="resolution"></a>解決方法

! [デバッグ拡張機能の[**分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。
