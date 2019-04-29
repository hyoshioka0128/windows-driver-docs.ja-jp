---
title: ネットワーク コンポーネントのアップグレード
description: ネットワーク コンポーネントのアップグレード
ms.assetid: c183cd0a-53a7-4172-9cf8-70a93877c8a8
keywords:
- オブジェクトの WDK ネットワーク、ネットワーク コンポーネントのアップグレードの通知します。
- ネットワークがネットワーク コンポーネントのアップグレード、WDK をオブジェクトに通知します。
- ネットワークのコンポーネントのアップグレード WDK、オブジェクトに通知
- WDK のネットワーク コンポーネントをアップグレードするには、オブジェクトに通知します。
- 通知の WDK ネットワーク、ネットワーク コンポーネントのアップグレード
- WDK、手順のネットワーク コンポーネントをアップグレードします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96c4b89da09db5b095a48b3d664c80bc7caed257
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387144"
---
# <a name="upgrading-network-components"></a>ネットワーク コンポーネントのアップグレード





ネットワーク コンポーネントは、ネットワーク構成のサブシステムによってアップグレードされます。

**ネットワーク コンポーネントをアップグレードするには**

1.  ネットワーク構成のサブシステムが通知オブジェクトのインスタンスを作成し、オブジェクトを呼び出して[ **INetCfgComponentControl::Initialize** ](https://msdn.microsoft.com/library/windows/hardware/ff547729)メソッド。 このメソッドは、オブジェクトを初期化し、コンポーネントとネットワークの構成のすべての側面へのアクセスを提供します。

2.  ネットワーク構成のサブシステムが通知オブジェクトを呼び出すときに、オペレーティング システムがインストールされているか、別のバージョンにアップグレード、 [ **INetCfgComponentSetup::Upgrade** ](https://msdn.microsoft.com/library/windows/hardware/ff547783)メソッド。

3.  サブシステムの呼び出し、通知オブジェクトの[ **INetCfgComponentControl::ApplyRegistryChanges** ](https://msdn.microsoft.com/library/windows/hardware/ff547727)メソッドは、レジストリ内のネットワーク コンポーネントに関する情報を変更し、通知を呼び出しますオブジェクトの[ **INetCfgComponentControl::ApplyPnpChanges** ](https://msdn.microsoft.com/library/windows/hardware/ff547726)メソッドを呼び出し、 [ **INetCfgPnpReconfigCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff547935)アップグレード後の情報を使用して、コンポーネントのドライバーを構成するためのインターフェイス。

 

 





