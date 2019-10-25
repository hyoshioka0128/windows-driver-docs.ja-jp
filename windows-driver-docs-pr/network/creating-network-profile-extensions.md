---
title: ネットワーク プロファイル拡張機能の作成
description: ネットワーク プロファイル拡張機能の作成
ms.assetid: b5f7a057-28bc-4df9-99da-58d39b81fb60
keywords:
- ネットワークプロファイル WDK ネイティブ 802.11 IHV 拡張 DLL、拡張機能の作成
- スキャン操作 WDK ネイティブ802.11
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8724c6b65f900662b47863b2288c2da1276c9dde
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835017"
---
# <a name="creating-network-profile-extensions"></a>ネットワーク プロファイル拡張機能の作成




 

基になるワイヤレス LAN (WLAN) アダプターがスキャン操作を完了すると、検出された基本サービスセット (BSS) ネットワークの一覧がオペレーティングシステムに返されます。 オペレーティングシステムは、ユーザーがネットワークプロファイルを作成していないすべての BSS ネットワークに対して[*Dot11ExtIhvCreateDiscoveryProfiles*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_create_discovery_profiles)関数を呼び出します。 この関数が呼び出されると、IHV 拡張 DLL は、BSS ネットワークに接続するために使用できる一時的な接続とセキュリティプロファイルフラグメントを返すことができます。

スキャン操作の詳細については、「[ネイティブ802.11 のスキャン操作](native-802-11-scan-operations.md)」を参照してください。

[*Dot11ExtIhvCreateDiscoveryProfiles*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_create_discovery_profiles)が呼び出された場合、IHV 拡張 DLL は次のガイドラインに従う必要があります。

-   オペレーティングシステムは、最後のスキャン操作中に受信した IEEE 802.11 ビーコンフレームとプローブ応答フレームの一覧を、 *P/Tablebssid*パラメーターに渡します。 この一覧は、DOT11\_BSS\_ENTRY 構造体として書式設定されます。 リスト内の各ビーコンまたはプローブ応答は、同じサービスセット識別子 (SSID) を持つアクセスポイント (AP) によって送信されています。

    **注**  Windows Vista では、IHV 拡張 DLL は、インフラストラクチャの基本サービスセット (BSS) ネットワークのみをサポートしています。

     

    IHV 拡張 DLL は、適切なプロファイルフラグメントを作成するために、各固定長フィールドと可変長情報要素を解析する必要があります。

-   接続とセキュリティプロファイルのフラグメントには、各 APs に接続するために使用できる有効な設定が含まれている必要があります。この設定は、BSS 識別子 (BSSIDs) が*p Tablebssid*パラメーターを通じて参照されます。

-   各接続とセキュリティプロファイルフラグメントには、IHV によって定義されたプロファイル拡張の XML データが含まれています。 プロファイルフラグメント内の XML データは &lt;IHV&gt; と &lt;/ihv&gt; タグで区切る必要があります。

 

 





