---
title: デバイスのロック解除
description: デバイスのロック解除
ms.assetid: 4e6ed725-2384-429b-be1e-027b7784e95b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53025a63733775b0a05406248527680ceb6073d2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357857"
---
# <a name="unlock-a-device"></a>デバイスのロック解除


モバイル ブロード バンド API のサブセットには、PIN の管理 API が含まれています。 デバイスのロックを解除するには、次の操作を行います。

1.  アカウント デバイスのネットワーク アダプターの ID を取得します。

    ``` syntax
    account.currentNetwork.networkAdapter. networkAdapterId
    ```

2.  作成、 [ **IMbnInterfaceManager** ](https://docs.microsoft.com/windows/desktop/api/mbnapi/nn-mbnapi-imbninterfacemanager)インスタンス。

3.  通知を[ **IMbnPinManagerEvents** ](https://docs.microsoft.com/windows/desktop/api/mbnapi/nn-mbnapi-imbnpinmanagerevents)と[ **IMbnPinEvents** ](https://docs.microsoft.com/windows/desktop/api/mbnapi/nn-mbnapi-imbnpinevents)接続ポイント (これらのピンの状態を取得するために使用およびブロック解除/結果のロックを解除) します。 詳細については、の「解説」を参照してください。 [ **IMbnInterfaceManager**](https://docs.microsoft.com/windows/desktop/api/mbnapi/nn-mbnapi-imbninterfacemanager)します。

4.  ネットワーク アダプター ID を渡す[ **IMbnInterfaceManager::GetInterface** ](https://docs.microsoft.com/windows/desktop/api/mbnapi/nf-mbnapi-imbninterfacemanager-getinterface)を取得する、 [ **IMbnInterface** ](https://docs.microsoft.com/windows/desktop/api/mbnapi/nn-mbnapi-imbninterface)デバイスのインターフェイス。

5.  取得、 [ **IMbnPinManager** ](https://docs.microsoft.com/windows/desktop/api/mbnapi/nn-mbnapi-imbnpinmanager)インターフェイスを呼び出すことによって、デバイスの[ **IMbnInterface::QueryInterface**](https://docs.microsoft.com/windows/desktop/api/mbnapi/nn-mbnapi-imbninterface)します。

6.  呼び出す[ **IMbnPinManager::GetPinState** ](https://docs.microsoft.com/windows/desktop/api/mbnapi/nf-mbnapi-imbnpinmanager-getpinstate)デバイス (手順 3 で登録された接続ポイントを使用して返された状態) の暗証番号 (pin) の状態を取得します。

7.  デバイスがロックされているかを使用してブロックする方法の決定、 [ **MBN\_PIN\_INFO::pinState** ](https://docs.microsoft.com/windows/desktop/api/mbnapi/ns-mbnapi-mbn_pin_info)イベントに渡されるパラメーター。

8.  IMbnPin インターフェイスを適切な暗証番号 (pin) を呼び出すことによって取得[ **IMbnPinManager::GetPin**](https://docs.microsoft.com/windows/desktop/api/mbnapi/nf-mbnapi-imbnpinmanager-getpin)します。

9.  いずれかを呼び出す[ **IMbnPin::Enter** ](https://docs.microsoft.com/windows/desktop/api/mbnapi/nf-mbnapi-imbnpin-enter)または[ **IMbnPin::Unblock**](https://docs.microsoft.com/windows/desktop/api/mbnapi/nf-mbnapi-imbnpin-unblock)を基にする方法、デバイスがロックされる (手順 7 を参照してください)。

10. リッスン**Unlock**または**ブロックを解除する**を使用して結果[ **IMbnPinEvents** ](https://docs.microsoft.com/windows/desktop/api/mbnapi/nn-mbnapi-imbnpinevents)登録操作が成功したかどうかを把握します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[モバイル ブロード バンドの Windows ランタイム Api の一般的なタスク](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 






