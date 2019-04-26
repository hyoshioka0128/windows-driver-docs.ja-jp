---
title: IEEE EtherType 処理
description: IEEE EtherType 処理
ms.assetid: ddd7244b-05a0-4ee8-b9aa-300015fbe3bd
keywords:
- 送信操作 WDK ネイティブ 802.11 IHV 拡張 DLL
- 受信操作 WDK ネイティブ 802.11 IHV 拡張 DLL
- WDK の 802.11 IHV ・拡張機能のネイティブ DLL を処理する IEEE EtherType
- EtherType WDK ネイティブ 802.11 IHV 拡張 DLL の処理
- WDK ネイティブ 802.11 IHV 拡張 DLL のプライバシー例外
- WDK の 802.11 IHV ・拡張機能のネイティブ DLL を復号化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f05f3fb28c0465f509f360ba8d12913cd9dda0d4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349478"
---
# <a name="ieee-ethertype-handling"></a>IEEE EtherType 処理




 

IHV 拡張機能の DLL には、ワイヤレス LAN (WLAN) のアダプターで受信したパケットの特別な処理の IEEE EtherTypes の一覧を指定できます。 EtherType 処理の次の種類を指定することができます。

<a href="" id="privacy-exemptions"></a>**プライバシーの除外**  
IHV 拡張機能の DLL には、受信したパケットのパケットの復号化除外対象を指定できます。 たとえば、DLL では、一致する暗号化キーが WLAN アダプターで構成されている場合でも暗号化されていない受信パケットを指定した EtherType が許可されているを指定できます。

<a href="" id="ethertype-registration"></a>**EtherType 登録**  
IHV 拡張機能の DLL には、処理され使用される EtherTypes を登録できます。 オペレーティング システムの呼び出しを通じて DLL への登録済み EtherType に一致するパケットを転送する、 [ *Dot11ExtIhvReceivePacket* ](https://msdn.microsoft.com/library/windows/hardware/ff547513)関数。

IHV 拡張機能の DLL を呼び出すことによって処理 EtherType を指定します、 [ **Dot11ExtSetEtherTypeHandling** ](https://msdn.microsoft.com/library/windows/hardware/ff547587)関数。 この関数を呼び出すときに IHV 拡張機能の DLL は次のガイドラインに従う必要があります。

-   IHV 拡張機能の DLL を呼び出すことができますのみ[ **Dot11ExtSetEtherTypeHandling** ](https://msdn.microsoft.com/library/windows/hardware/ff547587)いつ関連付け前の操作を完了する前にします。 この操作の詳細については、次を参照してください。[関連付け前操作](pre-association-operations.md)します。

-   IHV 拡張機能の DLL は、0 個以上の配列のプライバシー例外の一覧を指定[ **DOT11\_プライバシー\_除外**](https://msdn.microsoft.com/library/windows/hardware/ff548756)構造体。 IHV 拡張機能の DLL が要求されていない場合[ **Dot11ExtSetEtherTypeHandling**](https://msdn.microsoft.com/library/windows/hardware/ff547587)、オペレーティング システムの既定値は空のアクセス ポイント (AP) と 802.11 の関連のプライバシーの除外対象のリスト。
    **注**  Windows Vista の IHV 拡張機能の DLL は、基本的なサービスのインフラストラクチャ (BSS) ネットワークの設定のみをサポートします。

     

-   IHV 拡張機能の DLL は、受信する 0 個以上の EtherTypes の一覧を登録します。 通常、DLL は、処理後の関連付け操作中にセキュリティ パケット EtherTypes を登録します。 この操作の詳細については、次を参照してください。[後関連付け操作](post-association-operations.md)します。

    IHV 拡張機能の DLL が要求されていない場合[ **Dot11ExtSetEtherTypeHandling**](https://msdn.microsoft.com/library/windows/hardware/ff547587)、オペレーティング システムの既定値は、AP と 802.11 関連付けの登録済み EtherTypes の空のリスト。

-   IHV 拡張機能の DLL が呼び出すことで関連付け前の操作を完了した後[ **Dot11ExtPreAssociateCompletion**](https://msdn.microsoft.com/library/windows/hardware/ff547538)プライバシーの除外と EtherType の登録を使用して指定の一覧を呼び出す[ **Dot11ExtSetEtherTypeHandling** ](https://msdn.microsoft.com/library/windows/hardware/ff547587)基本的なサービスのセット (BSS) ネットワークに接続されている、WLAN アダプターによって行われたすべての 802.11 アソシエーションに適用されます。

-   呼び出す前に、オペレーティング システムがプライバシーの除外と EtherType 登録の一覧を消去[ *Dot11ExtIhvAdapterReset*](https://msdn.microsoft.com/library/windows/hardware/ff547434)します。

 

 





