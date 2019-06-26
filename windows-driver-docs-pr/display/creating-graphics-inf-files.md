---
title: グラフィックス INF ファイルの作成
description: グラフィックス INF ファイルの作成
ms.assetid: e56d4881-5ad2-41fc-a6fb-bc72c5106361
keywords:
- ドライバー モデル WDK Windows 2000 では、グラフィックスを表示します。
- Windows 2000 のディスプレイ ドライバー モデル WDK、グラフィック
- ビデオのミニポート ドライバー WDK Windows 2000 では、グラフィック
- ディスプレイ ドライバー WDK Windows 2000 では、グラフィック
- Windows 2000 の WDK の INF ファイルを表示します。
- グラフィックス WDK Windows 2000 の INF ファイルを表示します。
- geninf.exe
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 673e56e9911f39df38ccb27556f18eb07ec82fe2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370186"
---
# <a name="creating-graphics-inf-files"></a>グラフィックス INF ファイルの作成


## <span id="ddk_creating_graphics_inf_files_gg"></span><span id="DDK_CREATING_GRAPHICS_INF_FILES_GG"></span>


INF ファイルを使用して、NT ベースのオペレーティング システムの表示とビデオのミニポート ドライバーをインストールする必要があります。 ドライバー開発キット (DDK) と呼ばれるツールを提供する*geninf.exe*画面とビデオのミニポート ドライバーの INF ファイルを生成できます。

**注**   、 *geninf.exe*ツールはで、Windows Driver Kit (WDK)、DDK の代わりとして使用できません。

 

ときに*geninf.exe*はさまざまな会社名や、ディスプレイ ドライバーとビデオのミニポート ドライバーの名前などの情報を要求するダイアログが表示されますを実行します。 *Geninf.exe*情報から、INF ファイルを生成します。

**注**  によって生成されたファイル*geninf.exe* INF ファイルを完全に有効にできない場合があります。 *Geninf.exe* INF ファイルで説明されている各デバイスの追加、カスタムのレジストリ設定を必要があります INF ファイルを作成します。

 

ミニポート ドライバー 8 MB を超えるデバイスのメモリをマップする場合は、セクションを追加する INF ファイルを手動で編集する必要がありますで適切なエントリが説明されている[INF GeneralConfigData セクション](inf-generalconfigdata-section.md)します。

実行すると*geninf.exe*、「表示」デバイス クラスを選択するように求められたら を選択します。 としてマークされている、INF ファイル**クラスの表示を =** ドライバーのインストール中に、システム提供の表示のクラスのインストーラーによって解釈されます。 これにより、ビデオ ドライバーに関連付けられているすべてのレジストリ エントリを適切に初期化します。

クラスの INF ファイルを**表示**システムに次のファイルのみをインストールすることができます。

-   1 つのミニポート ドライバー

-   1 つのディスプレイ ドライバー

-   コントロール パネルの拡張 Dll

クラスの INF ファイルからの他の種類のドライバーまたはアプリケーションのファイルをインストールできません**表示**します。

### <a name="span-idlimitationsofgeninfexespanspan-idlimitationsofgeninfexespanspan-idlimitationsofgeninfexespanlimitations-of-geninfexe"></a><span id="Limitations_of_geninf.exe"></span><span id="limitations_of_geninf.exe"></span><span id="LIMITATIONS_OF_GENINF.EXE"></span>Geninf.exe の制限事項

使用することはできません*geninf.exe*を生成します。

-   1 つ以上のアーキテクチャをサポートする INF ファイルを指定します。

-   Windows 95/98/Me または Windows NT 4.0 または以前のバージョンをサポートする INF ファイルを指定します。

-   A*ミラー ドライバー* INF ファイル。 提供される INF ファイルを使用して、*ミラー*をテンプレートとしてサンプル ドライバー。 参照してください[ミラー ドライバーの INF ファイル](mirror-driver-inf-file.md)の詳細。

-   モニター INF ファイルです。 という名前の INF を使用して、 *monsamp.inf*をテンプレートとして。 参照してください[INF ファイルのセクションではモニター](monitor-inf-file-sections.md)の詳細。

これらのサンプル INF ファイル、Windows Driver Kit (WDK) ではどちらも付属しています。

参照してください[INF ファイルを作成する](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-inf-files)と[INF ファイルのセクションとディレクティブ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-file-sections-and-directives)詳細については、サンプルの INF ファイルを更新するときにします。

 

 





