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
ms.openlocfilehash: 749a9c147b48a9200f53526a1709b2cd5904ea05
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369009"
---
# <a name="upgrading-network-components"></a>ネットワーク コンポーネントのアップグレード





ネットワーク コンポーネントは、ネットワーク構成のサブシステムによってアップグレードされます。

**ネットワーク コンポーネントをアップグレードするには**

1.  ネットワーク構成のサブシステムが通知オブジェクトのインスタンスを作成し、オブジェクトを呼び出して[ **INetCfgComponentControl::Initialize** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547729(v=vs.85))メソッド。 このメソッドは、オブジェクトを初期化し、コンポーネントとネットワークの構成のすべての側面へのアクセスを提供します。

2.  ネットワーク構成のサブシステムが通知オブジェクトを呼び出すときに、オペレーティング システムがインストールされているか、別のバージョンにアップグレード、 [ **INetCfgComponentSetup::Upgrade** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547783(v=vs.85))メソッド。

3.  サブシステムの呼び出し、通知オブジェクトの[ **INetCfgComponentControl::ApplyRegistryChanges** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547727(v=vs.85))メソッドは、レジストリ内のネットワーク コンポーネントに関する情報を変更し、通知を呼び出しますオブジェクトの[ **INetCfgComponentControl::ApplyPnpChanges** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547726(v=vs.85))メソッドを呼び出し、 [ **INetCfgPnpReconfigCallback** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547935(v=vs.85))アップグレード後の情報を使用して、コンポーネントのドライバーを構成するためのインターフェイス。

 

 





