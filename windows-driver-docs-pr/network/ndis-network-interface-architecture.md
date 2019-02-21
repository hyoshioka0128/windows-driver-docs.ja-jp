---
title: NDIS ネットワーク インターフェイスのアーキテクチャ
description: NDIS ネットワーク インターフェイスのアーキテクチャ
ms.assetid: ce51008e-678c-421c-b796-36baab3df6b3
keywords:
- NDIS ネットワーク インターフェイス、WDK のアーキテクチャ
- ネットワーク インターフェイスの WDK、アーキテクチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 715085aa9fe871dea542f8a385fe5f1e86a76076
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553411"
---
# <a name="ndis-network-interface-architecture"></a>NDIS ネットワーク インターフェイスのアーキテクチャ





NDIS は、一連のネットワーク インターフェイスとインターフェイスのスタックをサポートするためにサービスを提供します。 Wdk には、この一連のサービスと呼びます*NDIS ネットワーク インターフェイス (NDISIF)* サービス。

次の図は、NDIS 6.0 のネットワーク インターフェイスのアーキテクチャを示しています。

![ndis 6.0 のネットワーク インターフェイスのアーキテクチャを示す図](images/ifarch.png)

アーキテクチャの NDISIF コンポーネントは次のとおりです。

<a href="" id="ndis-if-services"></a>NDIS 場合サービス  
インターフェイスのプロバイダーとのインターフェイスの登録を処理する NDIS コンポーネントは、OID クエリ プロバイダーとサービスの設定を実装し、NDISIF 他のサービスを提供します。

<a href="" id="ndis-if-provider-interface"></a>NDIS 場合プロバイダー インターフェイス  
NDIS ドライバー インターフェイス プロバイダーを実装するために許可するように NDIS 場合サービス コンポーネントを提供するインターフェイスです。

<a href="" id="ndis-proxy-interface-provider"></a>NDIS プロキシ インターフェイス プロバイダー  
(各ミニポート アダプター) の NDIS ミニポート ドライバーと (の各フィルター モジュール) フィルター ドライバーに代わって NDISIF プロバイダー サービスを実装する NDIS コンポーネント。

<a href="" id="interface-provider"></a>プロバイダーのインターフェイス  
サービスを実行できません、NDIS プロキシ インターフェイス プロバイダー インターフェイスの NDISIF プロバイダー サービスを提供する NDIS ドライバー。 たとえば、MUX 中間ドライバーでは、仮想ミニポートと基になるアダプターの間の内部インターフェイスことができます。

NDIS プロキシ インターフェイス プロバイダーでは、標準の NDIS ミニポート ドライバーおよび NDIS フィルター ドライバー インターフェイスを使用して、ミニポート アダプター NDISIF サービスを提供し、モジュールをフィルター処理します。 そのため、ミニポート ドライバーとフィルター ドライバーは NDISIF の追加のサポートを提供する必要ありません。

 

 





