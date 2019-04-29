---
title: デバイスのロック解除
description: デバイスのロック解除
ms.assetid: 4e6ed725-2384-429b-be1e-027b7784e95b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 452fe864df1f7dd7d2fa1f72e89025f1f39ac36a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383763"
---
# <a name="unlock-a-device"></a>デバイスのロック解除


モバイル ブロード バンド API のサブセットには、PIN の管理 API が含まれています。 デバイスのロックを解除するには、次の操作を行います。

1.  アカウント デバイスのネットワーク アダプターの ID を取得します。

    ``` syntax
    account.currentNetwork.networkAdapter. networkAdapterId
    ```

2.  作成、 [ **IMbnInterfaceManager** ](https://msdn.microsoft.com/library/windows/desktop/dd430416)インスタンス。

3.  通知を[ **IMbnPinManagerEvents** ](https://msdn.microsoft.com/library/windows/desktop/dd323118)と[ **IMbnPinEvents** ](https://msdn.microsoft.com/library/windows/desktop/dd323110)接続ポイント (これらのピンの状態を取得するために使用およびブロック解除/結果のロックを解除) します。 詳細については、の「解説」を参照してください。 [ **IMbnInterfaceManager**](https://msdn.microsoft.com/library/windows/desktop/dd430416)します。

4.  ネットワーク アダプター ID を渡す[ **IMbnInterfaceManager::GetInterface** ](https://msdn.microsoft.com/library/windows/desktop/dd430420)を取得する、 [ **IMbnInterface** ](https://msdn.microsoft.com/library/windows/desktop/dd430406)デバイスのインターフェイス。

5.  取得、 [ **IMbnPinManager** ](https://msdn.microsoft.com/library/windows/desktop/dd323117)インターフェイスを呼び出すことによって、デバイスの[ **IMbnInterface::QueryInterface**](https://msdn.microsoft.com/library/windows/desktop/dd430406)します。

6.  呼び出す[ **IMbnPinManager::GetPinState** ](https://msdn.microsoft.com/library/windows/desktop/dd323123)デバイス (手順 3 で登録された接続ポイントを使用して返された状態) の暗証番号 (pin) の状態を取得します。

7.  デバイスがロックされているかを使用してブロックする方法の決定、 [ **MBN\_PIN\_INFO::pinState** ](https://msdn.microsoft.com/library/windows/desktop/dd323226)イベントに渡されるパラメーター。

8.  IMbnPin インターフェイスを適切な暗証番号 (pin) を呼び出すことによって取得[ **IMbnPinManager::GetPin**](https://msdn.microsoft.com/library/windows/desktop/dd323121)します。

9.  いずれかを呼び出す[ **IMbnPin::Enter** ](https://msdn.microsoft.com/library/windows/desktop/dd323127)または[ **IMbnPin::Unblock**](https://msdn.microsoft.com/library/windows/desktop/dd323134)を基にする方法、デバイスがロックされる (手順 7 を参照してください)。

10. リッスン**Unlock**または**ブロックを解除する**を使用して結果[ **IMbnPinEvents** ](https://msdn.microsoft.com/library/windows/desktop/dd323110)登録操作が成功したかどうかを把握します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[モバイル ブロード バンドの Windows ランタイム Api の一般的なタスク](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 






