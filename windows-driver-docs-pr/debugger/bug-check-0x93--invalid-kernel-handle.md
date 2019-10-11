---
title: バグチェック 0x93 INVALID_KERNEL_HANDLE
description: INVALID_KERNEL_HANDLE のバグチェックの値は、0x00000093 です。 このバグチェックは、無効または保護されたハンドルが NtClose に渡されたことを示します。
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
ms.openlocfilehash: 8f287c0daeaa4026d85343f0276dfc66bdd003b2
ms.sourcegitcommit: c33b45c9e1e3121c52b6758f30865f4c14b0a350
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/10/2019
ms.locfileid: "72258414"
---
# <a name="bug-check-0x93-invalid_kernel_handle"></a>バグ チェック 0x93:@ NO__T-0KERNEL @ NO__T ハンドルが無効です。


無効な @ no__t-0KERNEL @ no__t ハンドルのバグチェックには、値0x00000093 が指定されています。 このバグチェックは、無効または保護されたハンドルが**Ntclose**に渡されたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。

## <a name="invalid_kernel_handle-parameters"></a>@ No__t-0KERNEL @ no__t ハンドルパラメーターが無効です。

|パラメーター1|パラメータ 2|パラメーター3|パラメーター4|エラーの原因|
|--- |--- |--- |--- |--- |
|NtClose が呼び出されたハンドル |0                |0   | 0  | プロテクトハンドルが閉じられました。|
|NtClose が呼び出されたハンドル |1                |0   | 0  | 無効なハンドルが閉じられたか、参照されました。|
|参照されたハンドル          |Handle テーブル |0   | 1  | 無効なカーネルハンドルを参照しているときにエラーが発生しました。無効なハンドル検出が有効になりました。|

## <a name="cause"></a>原因

INVALID_KERNEL_HANDLE のバグチェックは、一部のカーネルコード (サーバー、リダイレクター、または他のドライバーなど) が無効なハンドルまたは保護ハンドルを閉じようとしたことを示します。

パラメーター4の値が1の場合は、無効なカーネルハンドルの参照中にエラーが発生し、無効なハンドル検出が有効になったことを示します。

このメッセージは、カーネルコードが有効なハンドルではないハンドルを閉じるか参照しようとした場合に発生します。 無効なハンドル検出が有効になっていない限り、NtClose に渡される無効なハンドルまたは保護されたハンドルのみがこのバグチェックを実行します。
