---
title: プロパティを表示するコンテキストの設定
description: プロパティを表示するコンテキストの設定
ms.assetid: 9a5835b2-19a2-47fb-aa5b-87c3a9b955de
keywords:
- WDK のオブジェクトへの通知、ネットワー キングのコンテキスト
- ネットワークの通知、WDK のオブジェクト コンテキスト
- コンテキストの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2cd7231e7b457b1a03ed514e31ca20415d4d645e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570709"
---
# <a name="setting-context-to-display-properties"></a>プロパティを表示するコンテキストの設定





通知オブジェクトには、オブジェクトを所有しているネットワーク コンポーネントのプロパティを表示するためのコンテキストを設定できます。 通知オブジェクトは、ネットワーク構成のサブシステムの呼び出し、オブジェクトの後にディスプレイ コンテキストを設定[ **INetCfgComponentPropertyUi::SetContext** ](https://msdn.microsoft.com/library/windows/hardware/ff547752)メソッドを呼び出し、サブシステムの前に、オブジェクトの[ **INetCfgComponentPropertyUi::MergePropPages** ](https://msdn.microsoft.com/library/windows/hardware/ff547746)メソッド。

ネットワーク構成のサブシステムを呼び出すと**SetContext**、合格、 **IUnknown**インターフェイス。 **SetContext**呼び出し、 **QueryInterface**メソッドをこの**IUnknown**サブシステムが提供される特定のオブジェクトのインターフェイスを決定するインターフェイス。

たとえば、ネットワーク構成のサブシステムを指定できます、 [ **INetLanConnectionUiInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff548005)インターフェイスを呼び出すときに**SetContext**します。 **SetContext**使用できる、 [ **GetDeviceGuid** ](https://msdn.microsoft.com/library/windows/hardware/ff548012)メソッドの**INetLanConnectionUiInfo** LAN デバイスの GUID を取得します。 通知オブジェクトは、この LAN デバイスのコンテキストでそのネットワーク コンポーネントのプロパティをその後表示できます。 たとえば、TCP/IP プロトコルの通知オブジェクトは、そのアダプターのコンテキストで特定の LAN アダプターに関連付けられている IP アドレスを表示できます。 これにより、ユーザーがそのアダプターの IP アドレスを指定できます。

 

 





