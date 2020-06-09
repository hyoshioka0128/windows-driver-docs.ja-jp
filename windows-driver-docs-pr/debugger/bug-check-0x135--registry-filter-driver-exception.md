---
title: バグチェック 0x135 REGISTRY_FILTER_DRIVER_EXCEPTION
description: REGISTRY_FILTER_DRIVER_EXCEPTION のバグチェックの値は0x00000135 です。 このバグチェックは、レジストリフィルタリングドライバーのハンドルされない例外が原因で発生します。
ms.assetid: 99E171F4-5629-405F-993C-51287AD7D2C8
keywords:
- バグチェック 0x135 REGISTRY_FILTER_DRIVER_EXCEPTION
- REGISTRY_FILTER_DRIVER_EXCEPTION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- REGISTRY_FILTER_DRIVER_EXCEPTION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 600cc492d8bfe619d20a80bf9b1ae81b371b7d90
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534661"
---
# <a name="bug-check-0x135-registry_filter_driver_exception"></a>バグチェック 0x135: レジストリ \_ フィルター \_ ドライバーの \_ 例外


レジストリ \_ フィルタードライバーの例外のバグチェックには、 \_ \_ 0x00000135 の値が含まれています。 このバグチェックは、レジストリフィルタリングドライバーのハンドルされない例外が原因で発生します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="registry_filter_driver_exception-parameters"></a>レジストリ \_ フィルター \_ ドライバーの \_ 例外パラメーター


| パラメーター | 説明                                                              |
|-----------|--------------------------------------------------------------------------|
| 1         | 例外コード                                                           |
| 2         | バグチェックの原因となった例外のコンテキストレコードのアドレス |
| 3         | ドライバーのコールバックルーチンアドレス                                    |
| 4         | 予約済み                                                                 |

 

<a name="cause"></a>原因
-----

このバグチェックは、レジストリフィルタリングドライバーが通知ルーチン内の例外を処理しなかったことを示します。

<a name="resolution"></a>解像度
----------

! [デバッグ拡張機能の[**分析**](-analyze.md)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。 3番目のパラメーターを使用して、問題のあるドライバーを特定します。

 

 




