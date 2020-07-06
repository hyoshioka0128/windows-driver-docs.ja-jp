---
Description: プラグ アンド プレイおよび電源管理イベントの処理
title: プラグ アンド プレイおよび電源管理イベントの処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbf0bb8787f271f3618d9e919822569e6b52b8ac
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85967875"
---
# <a name="handling-plug-and-play-and-power-management-events"></a>プラグ アンド プレイおよび電源管理イベントの処理


プラグアンドプレイ (PnP) または電源管理 (PM) イベントが発生した場合、ユーザーモードドライバーフレームワーク (UMDF) は、イベントを処理するために CDevice クラスの1つ以上のメソッドを呼び出します。 (CDevice クラスは、ファイル*デバイス .cpp*に定義されています)。イベントハンドラーは、 **IPnpCallback**、 **IPnpCallbackHardware**、および**IPnpCallbackSelfManagedIo**の3つのインターフェイスにあります。

WpdHelloWorldDriver サンプルでは、ほとんどの PnP および PM イベントハンドラーが値を返さないか、または OK を返し \_ ます。 例外が2つあります。 **IPnpCallbackHardware:: On hardware**と**IPnpCallbackHardware:: onpreparehardware**です。 次の表では、各方法について説明します。

IPnpCallbackHardware:: On Hardware * * * *: **Wpdbasedriver:: Initialize**メソッドを呼び出します。 WPD クラス拡張を初期化し、デバイスのフレンドリ名を更新します。

IPnPCallbackHardware:: OnReleaseHardware * * * *: **Wpdbasedriver:: 初期化**解除メソッドを呼び出し、WPD クラス拡張を初期化前します。


 

各インターフェイスとそのメソッドの説明については、「」の[UMDF ドキュメント](https://go.microsoft.com/fwlink/p/?linkid=153678)を参照してください。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


****
[WPD ドライバーのサンプル](the-wpd-driver-samples.md)

 

 





