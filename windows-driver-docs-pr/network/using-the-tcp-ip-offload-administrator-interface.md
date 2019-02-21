---
title: TCP/IP のオフロード管理者インターフェイスを使用します。
description: TCP/IP のオフロード管理者インターフェイスを使用します。
ms.assetid: 2418e577-17cd-4db7-adb0-44b705e29d38
keywords:
- TCP/IP のオフロード WDK のネットワー キング、管理者インターフェイス
- WDK TCP/IP トランスポート、管理者インターフェイスの負荷を軽減します。
- タスクのオフロード WDK TCP/IP トランスポート、管理者インターフェイス
- 接続の負荷を軽減 WDK TCP/IP トランスポート、管理者インターフェイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19bb7382bce84973d681c02e3e6a5f1036517f94
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536389"
---
# <a name="using-the-tcpip-offload-administrator-interface"></a>TCP/IP のオフロード管理者インターフェイスを使用します。





NDIS 6.0 とそれ以降のバージョンでは、ユーザー モード アプリケーション (または上にあるドライバー) を有効にするしたり TCP/IP オフロード機能を無効にできます。 システム管理者は、Microsoft Windows Management Instrumentation (WMI) インターフェイスを介して設定にアクセスできます。 ハードウェアではサポートされている場合に有効にするレジストリ設定を無効になっている機能もあります。

応答、 [OID\_TCP\_オフロード\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569807)オブジェクト識別子 (OID) 要求の設定、ミニポート ドライバーの設定を使用して、 [ **NDIS\_オフロード\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff566706)ミニポート アダプターの現在オフロードまたは接続オフロードの構成を設定する構造体。

NDIS は、標準化されたオフロード キーワードでレジストリに要求された設定を保持します。 NDIS ミニポート アダプターを再起動すると、ミニポート ドライバーがオフロードが標準化されているキーワードを読み込みし、NIC の既定のオフロードの構成の設定にそれらを使用 ミニポート ドライバーでは、非標準のキーワードもサポートする場合は、タスクのオフロード設定を変更するときに、レジストリを更新するため、ミニポート ドライバーが担当します。 標準化されたキーワードの詳細については、次を参照してください。[ネットワーク デバイスの標準化された INF キーワード](standardized-inf-keywords-for-network-devices.md)します。

ミニポート ドライバーの内容を使用する必要があります、 [ **NDIS\_オフロード\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff566706)現在報告されたを更新する構造体は、構成をオフロードします。 ミニポート ドライバーが現在の構成とタスク オフロードを報告する必要があります[ **NDIS\_状態\_タスク\_オフロード\_現在\_CONFIG**](https://msdn.microsoft.com/library/windows/hardware/ff567424) NDIS 接続の負荷を軽減または\_状態\_オフロード\_再開状態を示す値。 (NDIS について\_状態\_オフロード\_再開を参照してください[NDIS 6.0 TCP chimney オフロード ドキュメント](full-tcp-offload.md))。状態の表示により、新しい機能の情報ですべての上位のプロトコルのドライバーが更新されるようになります。

ユーザー モード アプリケーション (または上にあるドライバー) を設定する前に[OID\_TCP\_オフロード\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569807)使用できる、 [OID\_TCP\_オフロード\_ハードウェア\_機能](https://msdn.microsoft.com/library/windows/hardware/ff569806)OID または[OID\_TCP\_接続\_オフロード\_ハードウェア\_機能](https://msdn.microsoft.com/library/windows/hardware/ff569803)OIDミニポート アダプターのハードウェアでサポートできるどのような機能を確認します。 OID を使用\_TCP\_オフロード\_パラメーター OID 機能を有効にする、 [OID\_TCP\_オフロード\_現在\_CONFIG](https://msdn.microsoft.com/library/windows/hardware/ff569805)OID または[OID\_TCP\_接続\_オフロード\_現在\_CONFIG](https://msdn.microsoft.com/library/windows/hardware/ff569802) OID レポートは現在有効になっています。

中間のドライバーがでオフロード ハードウェア機能のすべての変更を報告する必要があります (たとえば、MUX 中間ドライバーは、ミニポート アダプターを基になる相違に切り替える) ので、ハードウェア機能が変更する場合、 [ **NDIS\_状態\_タスク\_オフロード\_ハードウェア\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff567425)または[ **NDIS\_状態\_TCP\_接続\_オフロード\_ハードウェア\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff567828)状態を示す値。

NDIS および上にあるドライバーを使用できます、 [OID\_オフロード\_カプセル化](https://msdn.microsoft.com/library/windows/hardware/ff569762)設定またはタスクを照会する OID は、基になるミニポート アダプターの設定をカプセル化をオフロードします。 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造に含まれる、 [ **NDIS\_オフロード\_カプセル化**](https://msdn.microsoft.com/library/windows/hardware/ff566702)構造体。

 

 





