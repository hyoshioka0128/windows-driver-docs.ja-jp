---
title: センサードライバーの作成
description: センサードライバーの作成
ms.assetid: 7a1cea3c-d542-47e9-90f9-18bae4969b9f
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8da141f0a9ccd5603212cb8c2b81ef648910e510
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837623"
---
# <a name="creating-a-sensor-driver"></a>センサードライバーの作成


センサーで HID が使用されている場合は、ドライバーを作成するのではなく、受信トレイ HID クラスドライバーを使用することをお勧めします。 センサーが HID 以外のトランスポートを使用する場合は、[センサーの地理位置情報のドライバーサンプル](https://docs.microsoft.com/windows-hardware/drivers/gnss/sensors-geolocation-driver-sample)または SpbAccelerometer サンプルから始める必要があります。

これらのサンプルは、センサードライバーが必要とするクラスおよび COM インターフェイスの基本的な動作実装を提供します。 次の手順は、サンプルからドライバーを作成するために従う必要がある手順を示しています。

1.  「[永続的な一意の識別子の作成](creating-a-persistent-unique-identifier.md)」に記載されている手順に従って、ドライバーが一意であることを確認します。 サンプルドライバーソースを使用する場合は、常に新しい**GUID**とその他の識別子を指定します。

2.  デバイスハードウェアとの通信を処理するクラス、またはセンサーが論理センサーの場合はソフトウェアデータプロバイダーとの通信を処理するクラスを追加します。

3.  必要に応じて、イベントのサポートを追加します。 特定の時間間隔でイベントを発生させるスレッドを作成するコードを記述する必要があります。 また、SensorDdi の[**ISensorDriver:: OnGetSupportedEvents**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetsupportedevents)の実装を更新して、ドライバーが生成できるイベントの一覧を報告する必要があります。

4.  不要なすべてのコードを削除します。

## <a name="build-the-driver"></a>ドライバーをビルドする

ドライバーをビルドするには、次の手順を実行します。

1.  Microsoft Visual Studio 2012 を開始します。
2.  ビルド構成 (たとえば、デバッグ) とアーキテクチャ (Win32 など) を選択します。
3.  ドライバーのソリューションまたはプロジェクトファイルを開きます。
4.  [ビルド]、[ソリューションのビルド] の順に選択します。

## <a name="install-the-sensors-geolocation-driver-sample-for-testing"></a>テスト用のセンサーの地理位置情報ドライバーのサンプルをインストールする

テスト用のドライバーをインストールするには、次の手順を実行します。

1.  ドライバーがエラーなしでビルドされていることを確認します。

2.  ドライバーの DLL ファイルと INF ファイルを別のフォルダーにコピーします。

3.  WDK がインストールされている redist/wdf/*processor\_type*フォルダーから、2つの共同インストーラー DLL ファイル (checked または free) を見つけます。 これらのファイルを、手順 3. で作成したフォルダーにコピーします。 たとえば、ドライブ C に WDK をインストールした場合、C:\\WinDDK\\*ビルド\#* \\redist\\wdf\\X86 から WUDFUpdate\_01009 をコピーすることができます。

4.  Devcon を実行します。 このプログラムは、WDK がインストールされている [ツール]\\[devcon] フォルダーにあります。 たとえば、WDKExample という名前のセンサーの場合は、次のように入力します。

    **devcon install WDKExample "センサー\\WDKExample"**

    リリースされたドライバーをインストールするために、Devcon を使用しない  に**注意**してください。 この推奨事項は、テストのみを目的としています。

     

ドライバーをインストールできない場合は、手順 2. のいずれかの方法でエラーコードが返された可能性があります。 この問題をデバッグするには、インストール中にデバッガーをアタッチする必要があります。 読み込み中に UMDF ドライバーをデバッグする方法の詳細については、「 [Umdf ドライバーの読み込みに失敗した原因の特定」または「Umdf デバイスの起動失敗](https://docs.microsoft.com/windows-hardware/drivers/wdf/determining-why-the-umdf-driver-fails-to-load-or-the-umdf-device-fails)」を参照してください。

また、INF ファイルに指定したクラス ID が、ドライバーのコクラスの IDL ファイルで使用した**GUID**と一致していることを確認する必要があります。

## <a name="uninstalling-the-driver"></a>ドライバーのアンインストール

テスト中にドライバーのアンインストールが必要になる場合があります。たとえば、コードに変更を加えた後にドライバーのインストールを更新する場合などです。 ドライバーをアンインストールするには、次の手順を実行します。

1.  **デバイスマネージャー**を開きます。 たとえば、 **[スタート]** をクリックし、 **[検索の開始]** ボックスに次のように入力します。

    ``` syntax
    Device Manager
    ```

    その後、CTRL + ENTER キーを押します。

2.  [センサー] ノードを展開します。

3.  ドライバーの名前を右クリックし、 **[アンインストール]** をクリックします。

4.  [**このデバイスのドライバーソフトウェアを削除**する] を選択します。

5.  **[OK]** をクリックします。

## <a name="related-topics"></a>関連トピック
[センサーの地理位置情報ドライバーのサンプル](https://docs.microsoft.com/windows-hardware/drivers/gnss/sensors-geolocation-driver-sample)



