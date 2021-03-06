---
title: センサー ドライバーを作成します。
description: センサー ドライバーを作成します。
ms.assetid: 7a1cea3c-d542-47e9-90f9-18bae4969b9f
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 138949e47b4b517d9aa1028a0f55649c704d5e74
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360690"
---
# <a name="creating-a-sensor-driver"></a>センサー ドライバーを作成します。


センサー HID 推奨を作成せずに、ドライバーを使用する場合は、受信トレイの HID クラス ドライバーを使用します。 センサー HID 以外のトランスポートを使用する場合は、いずれかで開始する必要があります、[センサー地理位置情報ドライバー サンプル](https://docs.microsoft.com/windows-hardware/drivers/gnss/sensors-geolocation-driver-sample)または SpbAccelerometer サンプル。

これらのサンプルでは、クラスとセンサー ドライバーで必要な COM インターフェイスの基本的な作業の実装を提供します。 次の手順では、サンプルからドライバーを作成する必要がありますに従うことの手順を示しています。

1.  用意されている手順に従って、[永続的な一意の識別子を作成する](creating-a-persistent-unique-identifier.md)トピックには、ドライバーが一意であるかどうかを確認します。 サンプル ドライバーのソースを使用するときに常に提供する新しい**GUID**s および他の識別子。

2.  センサーが論理センサーの場合と、デバイスのハードウェアまたはソフトウェアのデータ プロバイダー間の通信を処理するクラスを追加します。

3.  必要に応じて、イベントのサポートを追加します。 特定の時間間隔でイベントを発生させるスレッドを作成するコードを記述する必要があります。 実装を更新する必要も[ **ISensorDriver::OnGetSupportedEvents** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetsupportedevents)ドライバーを発生させるイベントの一覧を報告する SensorDdi.cpp でします。

4.  不要なコードを削除します。

## <a name="build-the-driver"></a>ドライバーをビルドします。

ドライバーをビルドするには、次の次の手順を実行します。

1.  Microsoft Visual Studio 2012 を起動します。
2.  (たとえば、デバッグ) ビルド構成と (たとえば、Win32) アーキテクチャを選択します。
3.  ドライバーのソリューションまたはプロジェクト ファイルを開きます。
4.  ソリューションのビルド/ビルドを選択します。

## <a name="install-the-sensors-geolocation-driver-sample-for-testing"></a>テスト用センサー地理位置情報ドライバー サンプルをインストールします。

テスト用にドライバーをインストールするには、次の手順を実行します。

1.  ドライバーがエラーなしでビルドされることを確認します。

2.  別のフォルダーに、ドライバーの DLL と INF ファイルをコピーします。

3.  再頒布可能パッケージ/wdf から 2 つの共同インストーラー DLL ファイル (checked または無料) を検索/*プロセッサ\_型*WDK をインストールしたフォルダーです。 手順 3 で作成したフォルダーには、これらのファイルをコピーします。 たとえば、ドライブ C に WDK をインストールする場合は、WUDFUpdate をコピー可能性があります\_c: から 01009.dll\\WinDDK\\*ビルド\#* \\redist\\wdf\\x86。

4.  Devcon.exe を実行します。 ツールでこのプログラムを見つけることができます\\WDK をインストールした devcon フォルダー。 たとえば、センサー WDKExample という名前では、入力します。

    **devcon.exe インストール WDKExample.inf"センサー\\WDKExample"**

    **注**  にリリースされたドライバーをインストールする Devcon.exe を使用しないでください。 この推奨事項はテストのみです。

     

場合は、ドライバーをインストールすることはできません、手順 2 のエラー コードが返されたメソッドの 1 つでは可能性があります。 この問題をデバッグするには、インストール中にデバッガーをアタッチする必要があります。 UMDF ドライバーを読み込み中にデバッグする方法については、次を参照してください。[を決定する、UMDF ドライバーが失敗した理由の読み込みまたは開始に失敗した UMDF デバイス](https://docs.microsoft.com/windows-hardware/drivers/wdf/determining-why-the-umdf-driver-fails-to-load-or-the-umdf-device-fails)します。

クラス ID を INF でファイルと一致する指定を確認する必要がありますも、 **GUID**コクラス 's ドライバー用の IDL ファイルで使用することです。

## <a name="uninstalling-the-driver"></a>ドライバーをアンインストールします。

コードに変更を行った後は、ドライバーのインストールを更新する場合などのテスト中にドライバーをアンインストールする必要があります。 ドライバーをアンインストールするには、次の手順を実行します。

1.  開いている**デバイス マネージャー**します。 たとえば、をクリックして**開始**、次に、**検索の開始**ボックスに、次を入力します。

    ``` syntax
    Device Manager
    ```

    その後、ctrl キーを押しながら ENTER キーを押します。

2.  センサーのノードを展開します。

3.  ドライバーの名前を右クリックし、**アンインストール**します。

4.  選択**このデバイスのドライバー ソフトウェアを削除する**します。

5.  **[OK]** をクリックします。

## <a name="related-topics"></a>関連トピック
[センサー地理位置情報ドライバー サンプル](https://docs.microsoft.com/windows-hardware/drivers/gnss/sensors-geolocation-driver-sample)



