---
Description: Installing the WpdWudfSampleDriver Sample
title: WpdWudfSampleDriver サンプルのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00676b468d3211077e759f6364e8cabf8adccd4a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577723"
---
# <a name="installing-the-wpdwudfsampledriver-sample"></a>WpdWudfSampleDriver サンプルのインストール


WPD 他のサンプルと同様に、このドライバーのサンプルは、ルート列挙デバイスとしてインストールされます。 下に表示されます、**ポータブル デバイス**または**WPD**ノード**デバイス マネージャー**、デバイス ID のルートと\\WPD\\NNNN します。

### <a name="span-iddriverinstallationstepsspanspan-iddriverinstallationstepsspanspan-iddriverinstallationstepsspandriver-installation-steps"></a><span id="Driver_Installation_Steps"></span><span id="driver_installation_steps"></span><span id="DRIVER_INSTALLATION_STEPS"></span>ドライバーのインストール手順

サンプル ドライバーをインストールするには、次の手順を完了するには。

1.  目的のビルド環境を起動、**開始**メニュー。
2.  ("Build-、cZ") のサンプルをビルドします。
3.  コピー *WUDFUpdate\_0xxxx.dll*ドライバー DLL が含まれているディレクトリにします。 確認できます、 &lt;WDK をインストール パス&gt;\\redist\\wdf\\&lt;アーキテクチャ&gt;ディレクトリ
4.  ドライバーをインストールする ("devcon インストール wpdwudfsampledriver.inf WUDF\\基本的な")

Devcon コマンドの最後の引数が、ドライバーの INF ファイルに含まれる次のエントリに対応する注意。

```ManagedCPlusPlus
[Microsoft.NTx86]
%BasicDeviceName%=Basic_Install,WUDF\Basic
```

### <a name="span-iddriverremovalstepsspanspan-iddriverremovalstepsspanspan-iddriverremovalstepsspandriver-removal-steps"></a><span id="Driver_Removal_Steps"></span><span id="driver_removal_steps"></span><span id="DRIVER_REMOVAL_STEPS"></span>ドライバーの削除手順

サンプル ドライバーを削除するには、次の手順を完了するには。

1.  開いている**デバイス マネージャー**します。
2.  下、**ポータブル デバイス**ノード、ドライバーを削除する をクリックします。
3.  **[アンインストール]** をクリックします。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


****
[WpdWudfSampleDriverSample](the-wpdwudfsampledriver-sample.md)

[WPD ドライバーのサンプル](the-wpd-driver-samples.md)

 

 





