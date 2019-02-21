---
title: ネットワークを構成します。
description: ネットワークを構成します。
ms.assetid: 9529467b-353d-41c3-9d4e-bb5df5c43665
keywords:
- 通知オブジェクトの WDK ネットワーク、ネットワークの構成
- ネットワーク通知オブジェクト WDK、ネットワークの構成
- 通知の WDK ネットワーク、ネットワークの構成
- ネットワーク構成 WDK ofbject を通知します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f78f81f9bf90ee0f6076269363ce9cdea10b6adf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536535"
---
# <a name="configuring-the-network"></a>ネットワークを構成します。





通知オブジェクトは、ネットワークの構成をプログラムで制御を所有するネットワーク コンポーネントに提供できます。

コントロール パネルの ネットワーク アプリケーションからは、ネットワーク コンポーネントのプロパティを構成できます。 クリックすると、**ネットワーク**アイコン、通知オブジェクトのインスタンスを作成し、オブジェクトの呼び出しが、ネットワーク構成サブシステムを起動する[ **INetCfgComponentControl::Initialize**](https://msdn.microsoft.com/library/windows/hardware/ff547729)メソッド。 このメソッドは、オブジェクトを初期化し、コンポーネントとネットワークの構成のすべての側面へのアクセスを提供します。

サブシステムに通知オブジェクトの呼び出し後、ネットワーク構成のサブシステムでは、インスタンスを作成し、通知オブジェクトを初期化します、 [ **INetCfgComponentNotifyGlobal::GetSupportedNotifications** ](https://msdn.microsoft.com/library/windows/hardware/ff547734)オブジェクトで必要な通知の種類を取得します。 この情報では、サブシステムは、オブジェクトに必要な通知を送信できます。 オブジェクトは、これらの通知を使用して、ネットワークのセットアップと構成オブジェクトを所有するコンポーネントに影響を与える可能性がありますの側面を制御できます。 たとえば、サブシステムの呼び出し、通知オブジェクトの[ **INetCfgComponentNotifyGlobal::SysQueryBindingPath** ](https://msdn.microsoft.com/library/windows/hardware/ff547737)サブシステムはバインド パスを追加するオブジェクトに通知するメソッドその他のネットワーク コンポーネントが属しているが、オブジェクトがサブシステムに、そのバインディング パスが無効にすることを要求すること。 さらに、通知オブジェクトのメソッドのいずれかの呼び出し、サブシステム[INetCfgComponentNotifyBinding](https://msdn.microsoft.com/library/windows/hardware/ff547730)インターフェイス。 これらのメソッドに通知方法、サブシステムへの変更に関するオブジェクトは、通知オブジェクトを所有するコンポーネントを他のネットワーク コンポーネントをバインドします。

 

 





