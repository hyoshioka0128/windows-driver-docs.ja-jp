---
Description: Installing the Sample Driver
title: サンプル ドライバーをインストールします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b941ddd5d1ee3bc51b8b9e5a3b4fa69184725b0a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527962"
---
# <a name="installing-the-sample-driver"></a>サンプル ドライバーをインストールします。


このサンプル ドライバー インストール ルート列挙デバイスとして Windows ポータブル デバイス (WPD) 他のサンプルと同様に、します。 ポータブル デバイスまたは WPD のノードの下に表示**デバイス マネージャー**、デバイス ID のルートであり\\WPD\\NNNN します。

ルートで列挙されるデバイスをインストールするときに、常に接続されているデバイスを取得します。 その結果、rs-232 ポートからセンサー デバイスを接続することはありません、場合でも、[デバイス] ノード (devnode) は削除されません。 Devnode 到着 (または削除) をサポートするために rs-232 接続が接続されている (または電源が入っていない) 場合は、プラグ アンド プレイ (PnP) バス列挙子を指定する必要があります。 サンプル bus 列挙子は、トースターの WDK サンプルで提供されます。

サンプル ドライバーのインストールの INF ファイルを WpdHelloWorldDriver の INF ファイルに基づきます。 ほとんど変更にはには、WpdHelloWorldDriver WpdBasicHardwareDriver での文字列の置換が含まれます。 次のセクションより重要な変更をまとめたものです。

### <a name="span-idenablingfile-handletargetsspanspan-idenablingfile-handletargetsspanspan-idenablingfile-handletargetsspanenabling-file-handle-targets"></a><span id="Enabling_File-Handle_Targets"></span><span id="enabling_file-handle_targets"></span><span id="ENABLING_FILE-HANDLE_TARGETS"></span>ファイル ハンドルのターゲットを有効にします。

下に次のエントリが追加\[*基本的な\_Install.Wdf* \]ファイル ハンドル ベース UMDF I/O ターゲットを有効にします。 これらの I/O ターゲットは、rs-232 ポートを使用して、デバイスとのデータの交換に使用されます。 I/O のターゲットの詳細については、[をサポートしている I/O](the-wpdbasichardwaredriver-supporting-io.md)を参照してください。

```cpp
UmdfDispatcher = FileHandle
```

### <a name="span-iddisablinglegacywiasupportspanspan-iddisablinglegacywiasupportspanspan-iddisablinglegacywiasupportspandisabling-legacy-wia-support"></a><span id="Disabling_Legacy_WIA_Support"></span><span id="disabling_legacy_wia_support"></span><span id="DISABLING_LEGACY_WIA_SUPPORT"></span>WIA のレガシ サポートを無効にします。

サンプル ドライバーがイメージのコンテンツをサポートしていないためこのドライバーへのアクセスをレガシ アプリケーションを Windows Image Acquisition (WIA) を無効にする、次の行はコメント アウトします。

```cpp
;HKR,,”EnableLegacySupport”,0x10001,1
```

### <a name="span-idinstallingthedriverspanspan-idinstallingthedriverspanspan-idinstallingthedriverspaninstalling-the-driver"></a><span id="Installing_the_Driver"></span><span id="installing_the_driver"></span><span id="INSTALLING_THE_DRIVER"></span>ドライバーをインストールします。

サンプル ドライバーをインストールするには、次の手順を完了します。

1.  **開始**メニューで、目的のビルド環境を開きます。
2.  ("Build-、cZ") のサンプルをビルドします。
3.  コピー *WUDFUpdate\_0xxxx.dll*から、 &lt;WDK をインストール場所&gt;\\redist\\wdf\\&lt;アーキテクチャ&gt;ドライバーの DLL を含むディレクトリのディレクトリ。
4.  ドライバーをインストールする ("devcon インストール*Wpdbasichardwaredriver.inf* WUDF\\WpdBasicHardware")

**注**  devcon コマンドの最後の引数は、ドライバーの INF ファイルからの抜粋を次に対応します。

 

```ManagedCPlusPlus
[Microsoft.NTx86]
%BasicDeviceName%=Basic_Install,WUDF\WpdBasicHardware
```

### <a name="span-idremovingthedriverspanspan-idremovingthedriverspanspan-idremovingthedriverspanremoving-the-driver"></a><span id="Removing_the_Driver"></span><span id="removing_the_driver"></span><span id="REMOVING_THE_DRIVER"></span>ドライバーの削除

ドライバーのサンプルを削除するには、次の手順を完了します。

1.  Windows デバイス マネージャを開きます。
2.  ドライバーを右クリックし、**ポータブル デバイス**ノードをクリックします**アンインストール**します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD ドライバーのサンプル](the-wpd-driver-samples.md)

 

 





