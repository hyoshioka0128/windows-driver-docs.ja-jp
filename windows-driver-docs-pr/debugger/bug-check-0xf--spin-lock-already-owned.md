---
title: バグ チェック 0 xf SPIN_LOCK_ALREADY_OWNED
description: SPIN_LOCK_ALREADY_OWNED のバグ チェックでは、0x0000000F の値を持ちます。 これは、スピン ロックが既に所有しているときに、スピン ロックの要求が開始されたことを示します。
ms.assetid: 8347a78a-528e-4767-a13d-ad2fd8f71818
keywords:
- バグ チェック 0 xf SPIN_LOCK_ALREADY_OWNED
- SPIN_LOCK_ALREADY_OWNED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- SPIN_LOCK_ALREADY_OWNED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: af2c767441d8ed49a0bafc2551f37ca8292c8a1b
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239435"
---
# <a name="bug-check-0xf-spinlockalreadyowned"></a>バグ チェック 0xF:スピン\_ロック\_ALREADY\_所有されています。


スピン\_ロック\_ALREADY\_所有されているバグ チェックが 0x0000000F の値を持ちます。 これは、スピン ロックが既に所有しているときに、スピン ロックの要求が開始されたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="spinlockalreadyowned-parameters"></a>スピン\_ロック\_ALREADY\_所有されているパラメーター


なし

<a name="cause"></a>原因
-----

通常、スピン ロックを再帰的な要求によってこのエラーが発生します。 ように、スピン ロックを再帰的な要求が開始されました - たとえば、スピン ロックがスレッドによって取得され、関数は、スピン ロックを取得しようとしてもその同じスレッドを呼び出している場合にも発生することができます。 これになるため、回復不可能なデッドロックが発生、スピン ロックの取得を 2 回目の試行はここではブロックされません。 1 つ以上のプロセッサ上の呼び出しが行われた場合、1 つのプロセッサがブロックされます他のプロセッサがロックを解放するまで。

このエラーときも発生、せず、明示的な再帰では、すべてのスレッドとすべてのスピン ロックによって、IRQL が割り当てられています。 スピン ロック Irql が、DPC レベル以上では常が、これはスレッドの場合は true ではありません。 ただし、スピン ロックの以上、スピン ロックが保持しているスレッドは IRQL を維持する必要があります。 スレッド、IRQL の下の IRQL を減少が保持して、スピン ロックのレベルには、プロセッサのようにスケジュールする別のスレッドが使用できます。 この新しいスレッドが同じスピン ロックの取得を試みますでした。

<a name="resolution"></a>解決方法
----------

ロックの獲得再帰的にあるしないことを確認します。 また、スピン ロックを保持するスレッドの場合は、IRQL が保持しているスピンロックの IRQL の下のレベルのスレッドを小さくしないことを確認してください。

 

 




