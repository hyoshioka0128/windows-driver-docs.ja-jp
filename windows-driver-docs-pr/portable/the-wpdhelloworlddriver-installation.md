---
Description: WpdHelloWorldDriver サンプルのインストール
title: WpdHelloWorldDriver サンプルのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f92b35ecd1881a67f9bd03bfd51bdfca6fd55a9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387279"
---
# <a name="installing-the-wpdhelloworlddriver-sample"></a>WpdHelloWorldDriver サンプルのインストール


このサンプル ドライバー インストール ルート列挙デバイスとして WPD 他のサンプルと同様に、します。 下に表示されます、**ポータブル デバイス**または**WPD**ノード**デバイス マネージャー**、デバイス ID のルートと\\WPD\\NNNN します。

### <a name="span-iddriverinstallationstepsspanspan-iddriverinstallationstepsspanspan-iddriverinstallationstepsspandriver-installation-steps"></a><span id="Driver_Installation_Steps"></span><span id="driver_installation_steps"></span><span id="DRIVER_INSTALLATION_STEPS"></span>ドライバーのインストール手順

サンプル ドライバーをインストールするために実行する手順を次に示します。

1.  目的のビルド環境を起動、**開始**メニュー。
2.  ("Build-、cZ") のサンプルをビルドします。
3.  UMDF の共同インストーラーをコピー *WUDFUpdate\_0xxxx.dll*、ドライバー DLL が含まれているディレクトリにします。 共同インストーラーが記載されて、 &lt;WDK をインストール パス&gt;\\redist\\wdf\\&lt;アーキテクチャ&gt;ディレクトリ。
4.  ドライバーをインストールする ("devcon インストール wpdhelloworlddriver.inf WUDF\\WpdHelloWorld")

Devcon コマンドの最後の引数が、ドライバーの INF ファイルに含まれる次のエントリに対応するを認識します。

```ManagedCPlusPlus
[Microsoft.NTx86]
%BasicDeviceName%=Basic_Install,WUDF\WpdHelloWorld
```

### <a name="span-iddriverremovalstepsspanspan-iddriverremovalstepsspanspan-iddriverremovalstepsspandriver-removal-steps"></a><span id="Driver_Removal_Steps"></span><span id="driver_removal_steps"></span><span id="DRIVER_REMOVAL_STEPS"></span>ドライバーの削除手順

サンプル ドライバーを削除することを実行する手順を次に示します。

1.  Windows デバイス マネージャーを開きます。
2.  [ドライバー] をクリックして、**ポータブル デバイス**ノード。
3.  **[アンインストール]** をクリックします。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


****
[WpdHelloWorldDriverSample](the-sample-driver-architecture.md)

[WPD ドライバーのサンプル](the-wpd-driver-samples.md)

 

 





