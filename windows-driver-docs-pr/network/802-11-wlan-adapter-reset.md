---
title: 802.11 WLAN アダプターのリセット
description: 802.11 WLAN アダプターのリセット
ms.assetid: 1f993977-b4a1-42ec-8de3-2f4855db93a7
keywords:
- WDK 802.11 の WLAN のアダプターをリセットします。
- WLAN アダプター、WDK をリセットします。
- WLAN のアダプターをリセットします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b2d432301a48e205aa7b662157fd54d8f722cba
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580715"
---
# <a name="80211-wlan-adapter-reset"></a>802.11 WLAN アダプターのリセット




 

オペレーティング システムの呼び出し[ *Dot11ExtIhvAdapterReset* ](https://msdn.microsoft.com/library/windows/hardware/ff547434)たびにする必要が生じたワイヤレス LAN (WLAN) アダプターを初期化済み状態に復元します。 オペレーティング システムは、次のイベントのいずれかが発生するたびに、この関数を呼び出します。

-   WLAN アダプターは、切断操作を実行します。 この操作の詳細については、次を参照してください。[切断操作](disconnection-operations.md)します。

-   オペレーティング システムのセットに要求を介して、アダプターを管理するネイティブの 802.11 ミニポート ドライバーをリセットする[OID\_DOT11\_リセット\_要求](https://msdn.microsoft.com/library/windows/hardware/ff569409)します。

ときに[ *Dot11ExtIhvAdapterReset* ](https://msdn.microsoft.com/library/windows/hardware/ff547434)が呼び出されると、IHV 拡張機能の DLL は次のガイドラインを従う必要があります。

-   IHV 拡張機能の DLL が同じ状態にした後にその状態を復元する必要があります、 [ *Dot11ExtIhvInitAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff547469)関数が呼び出されました。 後であった同じ状態にこれらの設定を復元する必要があります、DLL には、WLAN アダプターで独自の設定が構成されている場合、 *Dot11ExtIhvInitAdapter*が呼び出されました。

-   IHV 拡張機能の DLL を呼び出すことによって開始された保留中の関連付け前操作がある場合、 [ *Dot11ExtIhvPerformPreAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547499) IHV ハンドラー関数の場合は、DLL を呼び出す必要があります[**Dot11ExtPreAssociateCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff547538)操作をキャンセルします。 このような状況では、DLL、設定、 *dwWin32Error*パラメーターの**Dot11ExtPreAssociateCompletion**エラー\_キャンセルします。

    前の関連付け操作の詳細については、次を参照してください。[関連付け前操作](pre-association-operations.md)します。

-   DLL を呼び出すことによって開始された保留中の後の関連付け操作がある場合、 [ *Dot11ExtIhvPerformPostAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547492) IHV ハンドラー関数の場合は、DLL を呼び出す必要があります[ **Dot11ExtPostAssociateCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff547530)操作をキャンセルします。 このような状況では、DLL、設定、 *dwWin32Error*パラメーターの**Dot11ExtPostAssociateCompletion**エラー\_キャンセルします。

    詳細については、後の関連付け操作は、次を参照してください。[後関連付け操作](post-association-operations.md)します。

 

 





