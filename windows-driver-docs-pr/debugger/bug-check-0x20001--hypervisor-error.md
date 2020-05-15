---
title: バグチェック 0x20001 HYPERVISOR_ERROR
description: HYPERVISOR_ERROR バグチェックの値は0x00020001 です。 これは、ハイパーバイザーで致命的なエラーが発生したことを示します。
ms.assetid: 5F62DEEA-D192-46ED-827C-021A749D7091
keywords:
- バグチェック 0x20001 HYPERVISOR_ERROR
- HYPERVISOR_ERROR
ms.date: 04/12/2019
topic_type:
- apiref
api_name:
- HYPERVISOR_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b3822317651aa3d6a1b0293f2561e70d371551f9
ms.sourcegitcommit: b35469bbcabee996af70bcbd8564184f547a8c57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83406246"
---
# <a name="bug-check-0x20001-hypervisor_error"></a>バグチェック 0x20001: ハイパーバイザー \_ エラー


ハイパーバイザー \_ エラーのバグチェックには、0x00020001 の値が含まれています。 これは、ハイパーバイザーで致命的なエラーが発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。

## <a name="hypervisor_error-parameters"></a>ハイパーバイザーの \_ エラーパラメーター


| パラメーター | 説明 |
|-----------|-------------|
| 1         | 予約されています。    |
| 2         | 予約されています。    |
| 3         | 予約されています。    |
| 4         | 予約されています。    |

## <a name="resolution"></a>解像度 

! [デバッグ拡張機能の[**分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)] には、バグチェックに関する情報が表示され、根本原因を特定するのに非常に役立ちます。
