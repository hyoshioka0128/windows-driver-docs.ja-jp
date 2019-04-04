---
title: 802.11 WLAN アダプターの接続
description: 802.11 WLAN アダプターの接続
ms.assetid: 4d533f32-0f98-4a65-ac1b-7a470e54ad29
keywords:
- WDK 802.11 WLAN、到着のアダプター
- WLAN アダプター WDK、到着
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77994d407a948bb81f1742260aa1e9e6a53d0045
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582382"
---
# <a name="80211-wlan-adapter-arrival"></a>802.11 WLAN アダプターの接続




 

オペレーティング システムでは、IHV の拡張 DLL がインストールされているワイヤレス LAN (WLAN) アダプターを検出すると、オペレーティング システムの呼び出し、 [ *Dot11ExtIhvInitAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff547469) IHV ハンドラー関数。 オペレーティング システム関数を呼び出しますこの WLAN アダプターになるたびに有効になっていますなど PCMCIA アダプターが挿入されると、使用するためです。

ときに、 [ *Dot11ExtIhvInitAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff547469)関数が呼び出されると、IHV 拡張機能の DLL は、次を実行します。

-   WLAN アダプターの DLL が必要なすべてのリソースと同様に、WLAN アダプター コンテキスト データの配列を割り当てます。

-   受信され、IHV 拡張機能の DLL によって使用されるセキュリティ パケットに IEEE EtherTypes の一覧を登録します。

-   独自の設定を IHV で定義されているとアダプターを構成します。

IHV 拡張機能の DLL が次のガイドラインに従う必要がありますと[ *Dot11ExtIhvInitAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff547469)が呼び出されます。

-   *HDot11SvcHandle*パラメーターには、WLAN アダプター用のオペレーティング システムによって割り当てられる一意のハンドル値が含まれています。 IHV 拡張機能の DLL は、このハンドルの値を保存する必要がありますに渡すと、 *hDot11SvcHandle* IHV 拡張関数のパラメーターなどのアダプター固有の処理に関連[ **Dot11ExtSetKeyMappingKey**](https://msdn.microsoft.com/library/windows/hardware/ff547597)します。

    通常、DLL は、その WLAN アダプター コンテキスト配列のメンバー内には、このハンドル値を保存します。

-   IHV 拡張機能の DLL を使って WLAN アダプターに固有のハンドル値を返す必要があります、 *phIhvExtAdapter*パラメーター。 オペレーティング システムへのハンドル値を渡します、 *hIhvExtAdapter* IHV ハンドラー関数のパラメーターなどのアダプター固有の処理に関連[ *Dot11ExtIhvReceiveIndication*](https://msdn.microsoft.com/library/windows/hardware/ff547512).

    通常、DLL は、ハンドル値として WLAN アダプター コンテキストの配列のアドレスを返します。

-   拡張 DLL の IHV 呼び出し[ **Dot11ExtSetEtherTypeHandling** ](https://msdn.microsoft.com/library/windows/hardware/ff547587) DLL を受信するセキュリティ パケットに IEEE EtherTypes の一覧を登録します。 IHV 拡張機能の DLL には、一連のペイロードの暗号化解除を除外 EtherTypes も指定できます。 EtherTypes の登録の詳細については、[IEEE EtherType 処理](ieee-ethertype-handling.md)を参照してください。

    EtherTypes が登録されると、オペレーティング システムの呼び出し、 [ *Dot11ExtIhvReceivePacket* ](https://msdn.microsoft.com/library/windows/hardware/ff547513)が EtherType には、リスト内のエントリが一致するすべてのパケットの IHV ハンドラー関数。

-   オペレーティング システムでは、ネイティブ 802.11 オブジェクト識別子 (Oid) のセット要求を通じた 802.11 標準のパラメーターに、アダプターを構成します。 これらの Oid の詳細については、[ネイティブ 802.11 ワイヤレス LAN の Oid](https://msdn.microsoft.com/library/windows/hardware/ff560691)を参照してください。

    ただし、DLL は、呼び出しを通じて独自のパラメーターを持つのアダプターを構成できます、 [ **Dot11ExtNicSpecificExtension** ](https://msdn.microsoft.com/library/windows/hardware/ff547526)関数。 この関数の呼び出しを通じて DLL は、WLAN アダプターとクエリの問題を管理するネイティブの 802.11 ミニポート ドライバーと直接通信または要求を IHV によって定義された独自の形式に基づくドライバーに設定します。

    DLL および WLAN のアダプターの通信インターフェイスの詳細については、[802.11 WLAN アダプターの通信チャネル](802-11-wlan-adapter-communication-channel.md)を参照してください。

 

 





