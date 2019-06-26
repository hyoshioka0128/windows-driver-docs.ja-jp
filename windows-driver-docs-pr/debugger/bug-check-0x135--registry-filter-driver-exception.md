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
ms.openlocfilehash: d5a76735a85ef71344ce186e8388a1627131510c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362253"
---
# <a name="bug-check-0x135-registryfilterdriverexception"></a>バグ チェック 0x135:レジストリ\_フィルター\_ドライバー\_例外


レジストリ\_フィルター\_ドライバー\_例外のバグ チェックが 0x00000135 の値を持ちます。 このバグチェックはレジストリ フィルタ リング ドライバーで未処理の例外によって発生します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


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

[ **! 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)バグ チェックに関する情報を表示拡張機能をデバッグおよび根本原因を突き止めるに役に立ちます。 3 番目のパラメーターを使用して、問題のあるドライバーを特定します。

 

 




