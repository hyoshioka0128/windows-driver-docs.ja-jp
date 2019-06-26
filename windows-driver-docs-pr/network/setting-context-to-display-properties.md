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
ms.openlocfilehash: de7c059594a5ee6eaca97fa80500c889c07d61bc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375156"
---
# <a name="setting-context-to-display-properties"></a>プロパティを表示するコンテキストの設定





通知オブジェクトには、オブジェクトを所有しているネットワーク コンポーネントのプロパティを表示するためのコンテキストを設定できます。 通知オブジェクトは、ネットワーク構成のサブシステムの呼び出し、オブジェクトの後にディスプレイ コンテキストを設定[ **INetCfgComponentPropertyUi::SetContext** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547752(v=vs.85))メソッドを呼び出し、サブシステムの前に、オブジェクトの[ **INetCfgComponentPropertyUi::MergePropPages** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547746(v=vs.85))メソッド。

ネットワーク構成のサブシステムを呼び出すと**SetContext**、合格、 **IUnknown**インターフェイス。 **SetContext**呼び出し、 **QueryInterface**メソッドをこの**IUnknown**サブシステムが提供される特定のオブジェクトのインターフェイスを決定するインターフェイス。

たとえば、ネットワーク構成のサブシステムを指定できます、 [ **INetLanConnectionUiInfo** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff548005(v=vs.85))インターフェイスを呼び出すときに**SetContext**します。 **SetContext**使用できる、 [ **GetDeviceGuid** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff548012(v=vs.85))メソッドの**INetLanConnectionUiInfo** LAN デバイスの GUID を取得します。 通知オブジェクトは、この LAN デバイスのコンテキストでそのネットワーク コンポーネントのプロパティをその後表示できます。 たとえば、TCP/IP プロトコルの通知オブジェクトは、そのアダプターのコンテキストで特定の LAN アダプターに関連付けられている IP アドレスを表示できます。 これにより、ユーザーがそのアダプターの IP アドレスを指定できます。

 

 





