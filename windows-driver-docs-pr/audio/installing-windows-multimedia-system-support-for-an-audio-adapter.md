---
title: オーディオ アダプター用の Windows マルチ メディア システム サポートのインストール
description: オーディオ アダプター用の Windows マルチ メディア システム サポートのインストール
ms.assetid: 5846404f-3a6a-4e55-ba83-18404ea7cace
keywords:
- WDK のマルチ メディア オーディオのアダプターをサポートします。
- アダプターのドライバー WDK のオーディオ、マルチ メディア サポート
- ポート クラス オーディオ アダプター WDK、マルチ メディア サポートします。
- WDK のマルチ メディア オーディオ
- Windows のマルチ メディア サポート WDK オーディオ
ms.date: 10/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: a94a890ba4b6c6ee43787fd880e16caa3940b331
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359867"
---
# <a name="installing-windows-multimedia-system-support-for-an-audio-adapter"></a>オーディオ アダプター用の Windows マルチ メディア システム サポートのインストール


## <span id="ddk_installing_windows_multimedia_system_support_for_an_audio_adapter_"></span><span id="DDK_INSTALLING_WINDOWS_MULTIMEDIA_SYSTEM_SUPPORT_FOR_AN_AUDIO_ADAPTER_"></span>


INF の追加レジストリ セクションを作成または、システム レジストリのドライバー固有の情報を変更します。 PortCls オーディオ アダプターの追加レジストリ セクションには、アダプターを Windows のマルチ メディアのシステム コンポーネントにアクセスできるようにする情報が含まれています。

次の例は、追加のレジストリ セクションで、XYZ-オーディオ-Device.AddReg に示されている、 [ **INF AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)前の例 (を参照してください[ポート クラスのオーディオをインストールします。アダプター](installing-a-port-class-audio-adapter.md))。

```cpp
  [XYZ-Audio-Device.AddReg]
  HKR,,AssociatedFilters,,"wdmaud,swmidi,redbook"
  HKR,,Driver,,xyzaud.sys 
  HKR,Drivers,SubClasses,,"wave,midi,mixer,aux"

  HKR,Drivers\wave\Wdmaud.drv,Driver,,Wdmaud.drv
  HKR,Drivers\midi\Wdmaud.drv,Driver,,Wdmaud.drv
  HKR,Drivers\mixer\Wdmaud.drv,Driver,,Wdmaud.drv
  HKR,Drivers\aux\Wdmaud.drv,Driver,,Wdmaud.drv

  HKR,Drivers\wave\Wdmaud.drv,Description,,%XYZ-Audio-Device-Description%
  HKR,Drivers\midi\Wdmaud.drv,Description,,%XYZ-Audio-Device-Description%
  HKR,Drivers\mixer\Wdmaud.drv,Description,,%XYZ-Audio-Device-Description%
  HKR,Drivers\aux\Wdmaud.drv,Description,,%XYZ-Audio-Device-Description%
```

追加レジストリ セクションでは、システムは、Windows のマルチ メディア システム オーディオのアダプターを使用できるようにを読み込む必要があるコンポーネントを指定するレジストリ エントリを追加します。 これらのコンポーネントには、アダプター ドライバー、Xyzaud.sys、および WDMAud、SWMidi、および Redbook システム ドライバーの両方が含まれます (を参照してください[カーネル モード WDM オーディオ コンポーネント](kernel-mode-wdm-audio-components.md))。

**AssociatedFilters**キーワードの例の追加レジストリ セクションでは、ディレクティブには読み込みがアダプター ドライバーが必要になるまで遅延するには 1 つまたは複数の補助ドライバー ファイルの名前が含まれていることを示します。 代わりに、同時に、デバイス ドライバーが読み込まれる補助ファイルを読み込むことです。

 

 




