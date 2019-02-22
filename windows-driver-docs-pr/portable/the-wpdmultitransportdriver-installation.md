---
Description: Installing the WpdMultiTransportDriver Sample
title: WpdMultiTransportDriver サンプルをインストールします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cba6081ea0ed411e29a35ed005ecda39c5a0d2f6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529997"
---
# <a name="installing-the-wpdmultitransportdriver-sample"></a>WpdMultiTransportDriver サンプルをインストールします。


WPD 他のサンプルと同様に、このドライバーのサンプルは、ルート列挙デバイスとしてインストールされます。 下に表示されます、**ポータブル デバイス**または**WPD**ノード**デバイス マネージャー**、デバイス ID のルートと\\WPD\\NNNN します。

### <a name="span-iddriverinstallationstepsspanspan-iddriverinstallationstepsspanspan-iddriverinstallationstepsspandriver-installation-steps"></a><span id="Driver_Installation_Steps"></span><span id="driver_installation_steps"></span><span id="DRIVER_INSTALLATION_STEPS"></span>ドライバーのインストール手順

サンプル ドライバーをインストールするには、次の手順を完了するには。

1.  目的のビルド環境を起動、**開始**メニュー。
2.  ("Build-、cZ") のサンプルをビルドします。
3.  コピー *WUDFUpdate\_0xxxx.dll*ドライバー DLL が含まれているディレクトリにします。 確認できます、 &lt;WDK をインストール パス&gt;\\redist\\wdf\\&lt;アーキテクチャ&gt;ディレクトリ。
4.  ドライバーをインストールする ("devcon インストール wpdmultitransportdriver.inf WUDF\\MultiTransport")。

Devcon コマンドの最後の引数が、ドライバーの INF ファイルから、次のエントリに対応するを認識します。

```ManagedCPlusPlus
[Microsoft.NTx86]
%BasicDeviceName%=Basic_Install,WUDF\MultiTransport
```

### <a name="span-iddriverremovalstepsspanspan-iddriverremovalstepsspanspan-iddriverremovalstepsspandriver-removal-steps"></a><span id="Driver_Removal_Steps"></span><span id="driver_removal_steps"></span><span id="DRIVER_REMOVAL_STEPS"></span>ドライバーの削除手順

サンプル ドライバーを削除するには、次の手順を完了するには。

1.  開いている**デバイス マネージャー**します。
2.  で、**ポータブル デバイス**ノード、ドライバーをアンインストールする をクリックします。
3.  **[アンインストール]** をクリックします。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


****
[WpdMultiTransportDriverSample](the-wpdmultitransportdriver-sample.md)

[WPD ドライバーのサンプル](the-wpd-driver-samples.md)

 

 





