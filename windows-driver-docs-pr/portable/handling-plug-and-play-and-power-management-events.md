---
Description: Handling Plug and Play and Power Management Events
title: プラグ アンド プレイおよび電源管理イベントの処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a09183eaaf9abfbf74a838c93d17f440f1f43ca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530905"
---
# <a name="handling-plug-and-play-and-power-management-events"></a>プラグ アンド プレイおよび電源管理イベントの処理


プラグ アンド プレイ (PnP) または電源管理 (PM) のイベントが発生したときに、ユーザー モード ドライバー フレームワーク (UMDF) は、イベントを処理する CDevice クラスで 1 つまたは複数のメソッドを呼び出します。 (CDevice クラスがファイルで定義されている*Device.cpp*)。イベント ハンドラーは、3 つのインターフェイスにあります。**IPnpCallback**、 **IPnpCallbackHardware**、および**IPnpCallbackSelfManagedIo**します。

WpdHelloWorldDriver サンプルでは、ほとんどの PnP および PM のイベント ハンドラーを返さない値または S\_ok をクリックします。 2 つの例外があります。**IPnpCallbackHardware::OnPrepareHardware**と**IPnPCallbackHardware::OnReleaseHardware**します。 次の表では、各メソッドについて説明します。

|                                             |                                                                                                                           |
|---------------------------------------------|---------------------------------------------------------------------------------------------------------------------------|
| **IPnpCallbackHardware::OnPrepareHardware** | 呼び出し、 **WpdBaseDriver::Initialize**メソッド。 WPD クラスの拡張を初期化し、デバイスのわかりやすい名前を更新します。 |
| **IPnPCallbackHardware::OnReleaseHardware** | 呼び出し、 **WpdBaseDriver::Uninitialize**メソッドと WPD クラスの拡張機能の初期化を解除します。                               |

 

各インターフェイスとそのメソッドの説明は、次を参照してください、 [UMDF ドキュメント](https://go.microsoft.com/fwlink/p/?linkid=153678)。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


****
[WPD ドライバーのサンプル](the-wpd-driver-samples.md)

 

 





