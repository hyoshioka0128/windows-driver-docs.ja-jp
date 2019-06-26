---
title: ユーザー インターフェイスに表示されないキーワード
description: ユーザー インターフェイスに表示されないキーワード
ms.assetid: 0d2aeaa3-4e47-413b-907f-5e70b34f0725
keywords:
- インストール キーワード WDK ネットワーク、非表示
- 非表示のキーワードの WDK DNIS ミニポート
- WDK DNIS ミニポートのキーワードを非表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f10ff63889c73f288064e35a59a66d8126aa09f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356243"
---
# <a name="keywords-not-displayed-in-the-user-interface"></a>ユーザー インターフェイスに表示されないキーワード





NDIS 6.0 および以降のバージョンの NDIS ミニポート ドライバーのネットワーク デバイスのいくつかの標準的なキーワードを提供します。 これらの標準的なキーワードは、ユーザー インターフェイスではなく INF ファイルに表示されます。

これらの一般的なキーワードは、次の一覧について説明します。 特定のキーワードの詳細については、WDK ドキュメントでのキーワードを検索してください。

<a href="" id="-iftype"></a> **\*IfType**  
デバイスの NDIS インターフェイスの型。 NDIS インターフェイスの種類の詳細については、次を参照してください。 [NDIS インターフェイス型](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-interface-types)します。

<a href="" id="-mediatype"></a> **\*メディアの種類**  
デバイスのメディアを種類します。 ミニポート アダプターのメディアの種類の詳細については、次を参照してください。 [OID\_GEN\_メディア\_サポートされている](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-media-supported)します。

<a href="" id="-physicalmediatype"></a> **\*PhysicalMediaType**  
デバイスの物理メディアを種類します。 ミニポート アダプタの物理メディアの種類の詳細については、次を参照してください。 [OID\_GEN\_物理\_MEDIUM](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-physical-medium)します。

<a href="" id="-ndisdevicetype-------"></a> **\*NdisDeviceType**   
デバイスの種類。 既定値は、0 で、標準的なネットワーク デバイスをネットワークに接続することを示します。 設定 **\*NdisDeviceType** NDIS に\_デバイス\_型\_エンドポイント (1) 場合、このデバイスは、エンドポイント デバイスとは、ネットワークに接続する場合は true。 ネットワーク インターフェイスではありません。 たとえば、NDIS を指定する必要があります\_デバイス\_型\_ネットワーク インフラストラクチャを使用して、ローカル コンピューターのシステムとの通信が外部への接続を提供しないスマート フォンなどのデバイス用のエンドポイントネットワーク。 ただし、必要があります **\*いない\*** 外部ネットワークへの接続を提供するために VPN インタ フェースなどの仮想アダプター NDIS_DEVICE_TYPE_ENDPOINT にこのキーワードを設定します。

**注**  Windows Vista は自動的に識別し、コンピューターに接続するネットワークを監視します。 場合は、NDIS\_デバイス\_型\_エンドポイント フラグが設定されて、デバイス エンドポイント デバイスしは true。 外部ネットワークへの接続ではありません。 その結果、Windows は、ネットワークを識別するときに、エンドポイント デバイスを無視します。 ネットワーク認識 Api は、デバイス、ネットワークに、コンピューターが接続しないことを示します。 このような状況でエンドユーザーのため、ネットワークと共有センターと、通知領域のネットワーク アイコンを表示しない NDIS エンドポイント デバイスが接続されています。 ただし、ネットワーク接続 フォルダーで、接続が表示されます。


 

 





