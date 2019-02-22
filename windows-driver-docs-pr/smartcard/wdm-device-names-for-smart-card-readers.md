---
title: スマート カード リーダーの WDM デバイス名
description: スマート カード リーダーの WDM デバイス名
ms.assetid: 06f15b0d-d759-4cfe-a558-883f7f0d2581
keywords:
- スマート カードのドライバー WDK、デバイス名
- デバイス名 WDK のスマート カード
- WDK スマート カードの名前
- WDK スマート カードのシンボリック リンクの名前
- カーネル デバイス名の WDK スマート カード
- WDM デバイス名の WDK スマート カード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d6ceba9efb6422a631671bb2e65b7b7d6788fa5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548569"
---
# <a name="wdm-device-names-for-smart-card-readers"></a>スマート カード リーダーの WDM デバイス名


## <span id="_ntovr_wdm_device_names_for_smart_card_readers"></span><span id="_NTOVR_WDM_DEVICE_NAMES_FOR_SMART_CARD_READERS"></span>


WDM デバイス ドライバー、カーネルのデバイス名は、カーネルの名前空間でのみを認識する名前です。 シンボリック リンクの名前は、Microsoft Win32 アプリケーションは、ドライバーを使用した通信に使用する名前です。

カーネルの名前空間内でのみ、カーネル デバイス名がわかっているため、ドライバーの開発者は、名前を選択できますが、Windows オペレーティング システムでのデバイス名の名前付け規則を遵守する必要があります。 具体的には、デバイス名にする必要があります次のようになります。

*\\デバイス\\DeviceName\[単位\]*

場所*DeviceName*ドライバーの種類を反映した名前と*単位*ドライバーの 0 から始まる単位数です。 ユニット数は、システムにインストールされている型の 1 つ以上のデバイスがある場合に、別の 1 つのデバイスを区別するために使用されます。

すべてのドライバーは、スマート カード リソース マネージャーと通信する必要があります、ため、デバイスは Win32 名前空間にアクセスできる名前をいる必要があります。 このシンボリック リンクの名前は、次のように検索する必要があります。

*\\\Dosdevices\z\\SCReader\[単位\]*

Win32 名前空間内のデバイスのユニット数を同じカーネル デバイスの名前を形成するために使用する 1 つである必要はありません。 最初の使用可能なユニット数である必要があります。 使用[ **SmartcardCreateLink (WDM)** ](https://msdn.microsoft.com/library/windows/hardware/ff548935)を自動的にシンボリック リンクの名前を生成します。

 

 





