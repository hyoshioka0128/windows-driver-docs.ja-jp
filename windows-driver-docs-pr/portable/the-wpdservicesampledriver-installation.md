---
Description: WpdServiceSampleDriver サンプルのインストール
title: WpdServiceSampleDriver サンプルのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da1b6877bb4a78941a117f5e089baf37c08cb203
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370491"
---
# <a name="installing-the-wpdservicesampledriver-sample"></a>WpdServiceSampleDriver サンプルのインストール


このサンプル ドライバー インストール ルート列挙デバイスとして WPD 他のサンプルと同様に、します。 下に表示されます、**ポータブル デバイス**または**WPD**ノード デバイス マネージャーで、デバイス ID のルートと\\WPD\\NNNN します。

### <a name="span-iddriverinstallationstepsspanspan-iddriverinstallationstepsspanspan-iddriverinstallationstepsspandriver-installation-steps"></a><span id="Driver_Installation_Steps"></span><span id="driver_installation_steps"></span><span id="DRIVER_INSTALLATION_STEPS"></span>ドライバーのインストール手順

サンプル ドライバーをインストールするには、次の手順を完了するには。

1.  目的のビルド環境を起動、**開始**メニュー。
2.  ("Build-、cZ") のサンプルをビルドします。
3.  コピー *WUDFUpdate\_0xxxx.dll*から、 &lt;WDK\_インストール\_場所&gt;\\redist\\wdf\\ &lt;アーキテクチャ&gt;ドライバー DLL が含まれているディレクトリにディレクトリ。
4.  ドライバーをインストールする ("devcon インストール wpdservicesampledriver.inf WUDF\\WpdService")

Devcon コマンドの最後の引数が、ドライバーの INF ファイルに配置されている次のエントリに対応するを認識します。

```ManagedCPlusPlus
[Microsoft.NTx86]
%BasicDeviceName%=Basic_Install,WUDF\WpdService
```

### <a name="span-iddriverremovalstepsspanspan-iddriverremovalstepsspanspan-iddriverremovalstepsspandriver-removal-steps"></a><span id="Driver_Removal_Steps"></span><span id="driver_removal_steps"></span><span id="DRIVER_REMOVAL_STEPS"></span>ドライバーの削除手順

サンプル ドライバーを削除するには、次の手順を完了するには。

1.  開いている**Windows デバイス マネージャ**します。
2.  下、**ポータブル デバイス**ノード、ドライバーを削除する をクリックします。
3.  **[アンインストール]** をクリックします。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


****
[WpdServiceSampleDriverSample](the-wpdservicesampledriver-sample.md)

[WPD ドライバーのサンプル](the-wpd-driver-samples.md)

 

 





