---
title: バグ チェック 0x162 KERNEL_AUTO_BOOST_INVALID_LOCK_RELEASE
description: KERNEL_AUTO_BOOST_INVALID_LOCK_RELEASE のバグ チェックでは、0x00000162 の値を持ちます。 これは、スレッドがロックを所有せず AutoBoost によって追跡されるロックが離されたことを示します。
ms.assetid: 8430B461-892C-4517-B5E1-94DCDB413B21
keywords:
- バグ チェック 0x162 KERNEL_AUTO_BOOST_INVALID_LOCK_RELEASE
- KERNEL_AUTO_BOOST_INVALID_LOCK_RELEASE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- KERNEL_AUTO_BOOST_INVALID_LOCK_RELEASE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d8f9ba7484fdece53d6d01b6ab78e7f826a4c34c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559727"
---
# <a name="bug-check-0x162-kernelautoboostinvalidlockrelease"></a>バグ チェック 0x162 の。カーネル\_自動\_BOOST\_無効な\_ロック\_リリース


カーネル\_自動\_BOOST\_無効な\_ロック\_リリースのバグ チェックが 0x00000162 の値を持ちます。 これは、スレッドがロックを所有せず AutoBoost によって追跡されるロックが離されたことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="kernelautoboostinvalidlockrelease-parameters"></a>カーネル\_自動\_BOOST\_無効な\_ロック\_リリース パラメーター


| パラメーター | 説明                  |
|-----------|------------------------------|
| 1         | スレッドのアドレス    |
| 2         | ロックのアドレス             |
| 3         | スレッドのセッション ID |
| 4         | 予約済み                     |

 

<a name="cause"></a>原因
-----

これにより、一部のスレッド (これは有効な AutoBoost 追跡を有効に) 別のスレッドの代わりのロックを解放するとき、または不要になった所有しているロックを解除しようとする一部のスレッドが通常発生します。

 

 




