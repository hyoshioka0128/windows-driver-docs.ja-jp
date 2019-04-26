---
title: ネットワーク プロファイル拡張機能の作成
description: ネットワーク プロファイル拡張機能の作成
ms.assetid: b5f7a057-28bc-4df9-99da-58d39b81fb60
keywords:
- ネットワーク プロファイル WDK ネイティブ 802.11 IHV 拡張機能の DLL、拡張機能の作成
- WDK ネイティブ 802.11 のスキャン操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7bc1f7f5e30e379989a65a118946c6dc609000f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357274"
---
# <a name="creating-network-profile-extensions"></a>ネットワーク プロファイル拡張機能の作成




 

基になるワイヤレス LAN (WLAN) アダプターには、スキャン操作が完了すると、オペレーティング システムに検出された基本的なサービスのセット (BSS) ネットワークの一覧を返します。 オペレーティング システムの呼び出し、 [ *Dot11ExtIhvCreateDiscoveryProfiles* ](https://msdn.microsoft.com/library/windows/hardware/ff547445)関数をユーザーがいない作成ネットワーク プロファイルをすべて BSS ネットワーク。 この関数が呼び出されると、IHV 拡張機能の DLL は一時的な接続と BSS ネットワークへの接続に使用できるセキュリティ プロファイルのフラグメントを返すことができます。

スキャン操作の詳細については、次を参照してください。[ネイティブ 802.11 スキャン操作](native-802-11-scan-operations.md)します。

ときに[ *Dot11ExtIhvCreateDiscoveryProfiles* ](https://msdn.microsoft.com/library/windows/hardware/ff547445)が呼び出されると、IHV 拡張機能の DLL は次のガイドラインを従う必要があります。

-   オペレーティング システムに渡します、 *pConnectableBssid* IEEE 802.11 ビーコンおよびプローブ応答のフレームの一覧は、最後のスキャン操作中に受信するパラメーター。 この一覧は、DOT11 として書式設定\_BSS\_エントリの構造体。 リスト内で各ビーコンまたはプローブの応答は、同じサービス セット識別子 (SSID) とアクセス ポイント (AP) によって送信されました。

    **注**  Windows Vista の IHV 拡張機能の DLL は、基本的なサービスのインフラストラクチャ (BSS) ネットワークの設定のみをサポートします。

     

    IHV 拡張機能の DLL は、適切なプロファイルのフラグメントを作成するには、固定長フィールドと可変長情報要素 (IEs) の各を解析する必要があります。

-   接続とセキュリティ プロファイルのフラグメントがある BSS 識別子 (Bssid) は、によって参照されます、アクセス ポイントの各への接続に使用できる有効な設定を含める必要があります、 *pConnectableBssid*パラメーター。

-   各接続とセキュリティ プロファイルのフラグメントには、IHV によって定義されたプロファイルの拡張機能用の XML データが含まれています。 プロファイルのフラグメント内の XML データを区切る&lt;IHV&gt;と&lt;/IHV&gt;タグ。

 

 





