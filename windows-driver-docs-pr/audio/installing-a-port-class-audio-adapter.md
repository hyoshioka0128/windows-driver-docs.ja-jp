---
title: ポート クラス オーディオ アダプターをインストールします。
description: ポート クラス オーディオ アダプターをインストールします。
ms.assetid: 02cea7c1-cf9a-4f4b-9d35-d565fac731ec
keywords:
- ポート クラス オーディオ アダプター、WDK をインストールします。
- オーディオのミニポート ドライバー WDK、アダプターのドライバー
- ミニポート ドライバー WDK オーディオ、アダプターのドライバー
- アダプターのドライバー WDK オーディオをインストールします。
- アダプターのオーディオ ドライバー WDK をインストールします。
- ポート クラス オーディオ アダプター WDK
- レジストリの WDK オーディオ
- WDK オーディオの追加レジストリ セクション
- アダプターのオーディオ ドライバー WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e86466f11e950989d84c5de21cc3a032c44dfb5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551500"
---
# <a name="installing-a-port-class-audio-adapter"></a>ポート クラス オーディオ アダプターをインストールします。


## <span id="installing_a_port_class_audio_adapter"></span><span id="INSTALLING_A_PORT_CLASS_AUDIO_ADAPTER"></span>


このセクションでは、仕入先は、ポート クラス オーディオ アダプターをインストールする INF ファイルに含める必要がありますデバイス クラス固有の情報について説明します。 [全般] の INF ファイルの要件とのすべてのデバイス クラスに対するオプションについては、[デバイス インストールの概要](https://msdn.microsoft.com/library/windows/hardware/ff549455)を参照してください。

このセクションでは、必要なの INF ファイル エントリの説明は、XYZ のオーディオ デバイスを仮定に基づいています。 このデバイスのドライバーは、Xyzaudio.sys という名前のファイルに含まれます。 例**製造元**と**モデル**次のセクションでは、デバイスが表示されます。

```inf
  [VendorName]  ; Manufacturer section
  %XYZ-Audio-Device-Description%=XYZ-Audio-Device, <Plug and Play hardware ID>
  [XYZ-Audio-Device]  ; Models section
  AddReg=XYZ-Audio-Device.AddReg
```

詳細については、[ **INF AddReg ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546320)を参照してください。

その他の例は、SYVAD オーディオ サンプルに含まれる INF ファイルを参照してください。 詳細については、[サンプル オーディオ ドライバー](sample-audio-drivers.md)と[オーディオのユニバーサル Windows ドライバー](audio-universal-drivers.md)を参照してください。

次のトピックでは、デバイスをインストールする INF ファイルの主要なセクションの例を紹介します。

[オーディオのアダプターのバージョン情報を指定します。](specifying-version-information-for-an-audio-adapter.md)

[オーディオのアダプターのデバイスのインターフェイスのインストール](installing-device-interfaces-for-an-audio-adapter.md)

[オーディオのアダプターの主要なシステム コンポーネントをインストールします。](installing-core-system-components-for-an-audio-adapter.md)

[オーディオのアダプターの Windows のマルチ メディア システム サポートのインストール](installing-windows-multimedia-system-support-for-an-audio-adapter.md)

[Windows で、オーディオ アダプター サービスをインストールします。](installing-an-audio-adapter-service-in-windows.md)

[コントロール パネルのカスタマイズ](customizing-control-panel.md)

[オーディオのアダプターの他のインストールに関する問題](miscellaneous-installation-issues-for-an-audio-adapter.md)

 

 




