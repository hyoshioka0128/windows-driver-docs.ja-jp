---
title: ネットワークの構成
description: ネットワークの構成
ms.assetid: 9529467b-353d-41c3-9d4e-bb5df5c43665
keywords:
- 通知オブジェクトの WDK ネットワーク、ネットワークの構成
- ネットワーク通知オブジェクト WDK、ネットワークの構成
- 通知の WDK ネットワーク、ネットワークの構成
- ネットワーク構成 WDK ofbject を通知します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9fb147b81d48700b57c6f437ba7dca79c6eb60fe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374959"
---
# <a name="configuring-the-network"></a>ネットワークの構成





通知オブジェクトは、ネットワークの構成をプログラムで制御を所有するネットワーク コンポーネントに提供できます。

コントロール パネルの ネットワーク アプリケーションからは、ネットワーク コンポーネントのプロパティを構成できます。 クリックすると、**ネットワーク**アイコン、通知オブジェクトのインスタンスを作成し、オブジェクトの呼び出しが、ネットワーク構成サブシステムを起動する[ **INetCfgComponentControl::Initialize**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547729(v=vs.85))メソッド。 このメソッドは、オブジェクトを初期化し、コンポーネントとネットワークの構成のすべての側面へのアクセスを提供します。

サブシステムに通知オブジェクトの呼び出し後、ネットワーク構成のサブシステムでは、インスタンスを作成し、通知オブジェクトを初期化します、 [ **INetCfgComponentNotifyGlobal::GetSupportedNotifications** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547734(v=vs.85))オブジェクトで必要な通知の種類を取得します。 この情報では、サブシステムは、オブジェクトに必要な通知を送信できます。 オブジェクトは、これらの通知を使用して、ネットワークのセットアップと構成オブジェクトを所有するコンポーネントに影響を与える可能性がありますの側面を制御できます。 たとえば、サブシステムの呼び出し、通知オブジェクトの[ **INetCfgComponentNotifyGlobal::SysQueryBindingPath** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547737(v=vs.85))サブシステムはバインド パスを追加するオブジェクトに通知するメソッドその他のネットワーク コンポーネントが属しているが、オブジェクトがサブシステムに、そのバインディング パスが無効にすることを要求すること。 さらに、通知オブジェクトのメソッドのいずれかの呼び出し、サブシステム[INetCfgComponentNotifyBinding](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547730(v=vs.85))インターフェイス。 これらのメソッドに通知方法、サブシステムへの変更に関するオブジェクトは、通知オブジェクトを所有するコンポーネントを他のネットワーク コンポーネントをバインドします。

 

 





