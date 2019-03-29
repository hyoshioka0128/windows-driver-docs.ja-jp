---
title: バグ チェック 0x135 REGISTRY_FILTER_DRIVER_EXCEPTION
description: REGISTRY_FILTER_DRIVER_EXCEPTION のバグ チェックでは、0x00000135 の値を持ちます。 このバグチェックはレジストリ フィルタ リング ドライバーで未処理の例外によって発生します。
ms.assetid: 99E171F4-5629-405F-993C-51287AD7D2C8
keywords:
- バグ チェック 0x135 REGISTRY_FILTER_DRIVER_EXCEPTION
- REGISTRY_FILTER_DRIVER_EXCEPTION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- REGISTRY_FILTER_DRIVER_EXCEPTION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: af398289213475aafea20cda58c526865f6b81ec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572460"
---
# <a name="bug-check-0x135-registryfilterdriverexception"></a>バグ チェック 0x135:レジストリ\_フィルター\_ドライバー\_例外


レジストリ\_フィルター\_ドライバー\_例外のバグ チェックが 0x00000135 の値を持ちます。 このバグチェックはレジストリ フィルタ リング ドライバーで未処理の例外によって発生します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="registryfilterdriverexception-parameters"></a>レジストリ\_フィルター\_ドライバー\_例外パラメーター


| パラメーター | 説明                                                              |
|-----------|--------------------------------------------------------------------------|
| 1         | 例外コード                                                           |
| 2         | バグチェックの原因となった例外のコンテキスト レコードのアドレス |
| 3         | ドライバーのコールバック ルーチンのアドレス                                    |
| 4         | 予約済み                                                                 |

 

<a name="cause"></a>原因
-----

このバグチェックでは、ドライバーをフィルタ リング レジストリがその通知ルーチン内で例外を処理していないことを示します。

<a name="resolution"></a>解決方法
----------

3 番目のパラメーターを使用して、問題のあるドライバーを特定します。

 

 




