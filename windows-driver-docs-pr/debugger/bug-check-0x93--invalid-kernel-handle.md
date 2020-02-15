---
title: バグチェック 0x93 INVALID_KERNEL_HANDLE
description: INVALID_KERNEL_HANDLE バグチェックの値は0x00000093 です。 このバグチェックは、無効または保護されたハンドルが NtClose に渡されたことを示します。
ms.assetid: c8564da7-cdbf-40f5-94f4-b1fac23b8b42
keywords:
- バグチェック 0x93 INVALID_KERNEL_HANDLE
- INVALID_KERNEL_HANDLE
ms.date: 10/10/2019
topic_type:
- apiref
api_name:
- INVALID_KERNEL_HANDLE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 09fef2b03617e44de3f335d158b955a667f3d088
ms.sourcegitcommit: c2a96138fe8d619c2d2591cd849ae2dd4bb6c37b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/15/2020
ms.locfileid: "77260502"
---
# <a name="bug-check-0x93-invalid_kernel_handle"></a>バグチェック 0x93: 無効な\_カーネル\_ハンドル

無効な\_カーネル\_ハンドルのバグチェックには、0x00000093 という値が指定されています。 このバグチェックは、無効または保護されたハンドルが**Ntclose**に渡されたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。

## <a name="invalid_kernel_handle-parameters"></a>\_カーネル\_ハンドルパラメーターが無効です

|パラメーター1|パラメータ 2|パラメーター3|パラメーター4|エラーの原因|
|--- |--- |--- |--- |--- |
|NtClose が呼び出されたハンドル |0                |0   | 0  | プロテクトハンドルが閉じられました。|
|NtClose が呼び出されたハンドル |1                |0   | 0  | 無効なハンドルが閉じられたか、参照されました。|
|参照されたハンドル          |Handle テーブル |0   | 1  | 無効なカーネルハンドルを参照しているときにエラーが発生しました。無効なハンドル検出が有効になりました。|

## <a name="cause"></a>原因

INVALID_KERNEL_HANDLE のバグチェックは、一部のカーネルコード (サーバー、リダイレクター、その他のドライバーなど) が無効なハンドルまたは保護ハンドルを閉じようとしたことを示します。

パラメーター4の値が1の場合は、無効なカーネルハンドルの参照中にエラーが発生し、無効なハンドル検出が有効になったことを示します。

このメッセージは、カーネルコードが有効なハンドルではないハンドルを閉じるか参照しようとした場合に発生します。 無効なハンドル検出が有効になっていない限り、NtClose に渡される無効なハンドルまたは保護されたハンドルのみがこのバグチェックを実行します。
