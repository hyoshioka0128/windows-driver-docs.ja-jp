---
title: PNP-X 対応デバイス用のコンテナー Id
description: PNP-X 対応デバイス用のコンテナー Id
ms.assetid: 6a1ea4e9-e672-4f37-ab26-932591fe4da4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1250b34309df64f25321c0e6154bdc0bb0032574
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528064"
---
# <a name="container-ids-for-pnp-x-devices"></a>PNP-X 対応デバイス用のコンテナー Id


PnP 拡張機能 (PNP-X) は、IP ベースのネットワークを介してコンピューターに接続されているデバイスをサポートするには、Windows のプラグ アンド プレイ (PnP) を拡張します。 PNP-X 対応の詳細についてを参照してください、 [PnP-x:Windows の仕様のプラグ アンド プレイ拡張機能。](https://go.microsoft.com/fwlink/p/?linkid=142398                  )

PNP-X 対応デバイスでは、そのデバイスのメタデータ内の XML 要素として、コンテナー ID を指定できます。 2 つのプロトコルがサポートされています。

-   Web サービス (DPWS) 用のデバイス プロファイル。

    DPWS の詳細についてを参照してください、 [DPWS 仕様。](https://go.microsoft.com/fwlink/p/?linkid=142400)

    DPWS を通じてコンテナー Id のサポートに関する詳細については、[DPWS デバイス用のコンテナー Id](container-ids-for-dpws-devices.md)を参照してください。

-   ユニバーサル PnP (UPnP)。

    詳細についてを参照してください、 [UPnP デバイスのアーキテクチャの仕様。](https://go.microsoft.com/fwlink/p/?linkid=142402)

    UPnP を通じてコンテナー Id のサポートに関する詳細については、[UPnP デバイス用のコンテナー Id](container-ids-for-upnp-devices.md)を参照してください。

PNP-X 対応デバイスがデバイスの DPWS メタデータまたは UPnP デバイスの説明ドキュメントでコンテナー ID を指定しない場合、PnP マネージャーには、デバイスがサポートされるプロトコルに固有のアルゴリズムを使用して、デバイスのコンテナー ID が生成されます。

-   DPWS デバイスの場合は、生成されたコンテナー ID は、アドレス (EPR) を参照か、デバイスのエンドポイントで GUID から作成されたか、デバイスの EPR (ない場合は、GUID) の sha-1 ハッシュです。

-   UPnP デバイスの場合は、生成されたコンテナー ID は、デバイスの一意なデバイス名 (UDN) です。

    **注**  Windows 10 では、PnP マネージャーは常に生成 DPWS デバイス用のコンテナー ID を上記のアルゴリズムを使用してコンテナー ID は、デバイスのメタデータで指定されている場合でもです。

     

1 つのバスまたは PNP-X 対応のプロトコルで動作するデバイスの場合、生成された PNP-X コンテナー ID で十分です。

マルチ プロトコルのデバイスがコンテナー ID を指定することがあります。 マルチ プロトコルのデバイスでは、Windows コンテナーの 1 つのデバイスにデバイスのすべてのインスタンスをグループ化を許可するには、各プロトコルに同じコンテナー ID を共有するは。 この方法で、DPWS と UPnP の両方でデバイスのコンテナー ID を指定できます。

 

 





