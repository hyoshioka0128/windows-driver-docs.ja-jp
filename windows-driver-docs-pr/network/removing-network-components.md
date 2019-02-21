---
title: ネットワーク コンポーネントを削除します。
description: ネットワーク コンポーネントを削除します。
ms.assetid: db1928ff-7570-411c-b770-274428a0d432
keywords:
- オブジェクトの WDK ネットワーク、ネットワーク コンポーネントの削除の通知します。
- ネットワーク通知オブジェクト WDK、ネットワーク コンポーネントを削除します。
- ネットワーク コンポーネントの削除を WDK
- ネットワーク コンポーネントを削除します。
- 通知の WDK ネットワーク、ネットワーク コンポーネントを削除します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c41c95fcf2fa73e00c534cbc793adc70573c2fb3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528607"
---
# <a name="removing-network-components"></a>ネットワーク コンポーネントを削除します。





ネットワーク コンポーネントは、ネットワーク構成のサブシステムによって削除されます。

**ネットワーク コンポーネントを削除するには**

1.  ネットワーク構成のサブシステムが通知オブジェクトのインスタンスを作成し、オブジェクトを呼び出して[ **INetCfgComponentControl::Initialize** ](https://msdn.microsoft.com/library/windows/hardware/ff547729)メソッド。 このメソッドは、オブジェクトを初期化し、コンポーネントとネットワークの構成のすべての側面へのアクセスを提供します。

2.  サブシステムの呼び出し、通知オブジェクトの[ **INetCfgComponentSetup::Removing** ](https://msdn.microsoft.com/library/windows/hardware/ff547769)コンポーネントを削除するために必要な操作を実行するメソッド。 **Removing**メソッドは、コンポーネントの削除の準備のクリーンアップ操作を実行します。

3.  サブシステムの呼び出し、通知オブジェクトの[ **INetCfgComponentControl::ApplyRegistryChanges** ](https://msdn.microsoft.com/library/windows/hardware/ff547727)ネットワーク コンポーネントに関する情報をレジストリから削除する方法。

 

 





