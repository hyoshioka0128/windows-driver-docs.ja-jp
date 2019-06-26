---
title: 印刷モニターのインストール
description: 印刷モニターのインストール
ms.assetid: 2ab993fd-647b-40aa-981c-1bc270ec79a4
keywords:
- 印刷モニター、WDK をインストールします。
- 印刷モニター WDK をインストールします。
- INF ファイル WDK の印刷、印刷のモニター
- 言語モニター WDK が印刷をインストールします。
- WDK のポート モニターが印刷をインストールします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8746157eb85bc5e3230ae4e4d5d1fb141d31d68d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385980"
---
# <a name="installing-a-print-monitor"></a>印刷モニターのインストール





このセクションでは、印刷のモニターをインストールするために使用する方法を説明します。 (使用するプリンターをインストールする INF ファイルと同じファイルで印刷のモニターをインストールできます。 INF ファイルの詳細については、次を参照してください[プラグ アンド プレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)と[電源管理](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-power-management)。)。

### <a href="" id="ddk-installing-a-language-monitor-gg"></a>言語モニターをインストールします。

言語モニターをインストールするには、LanguageMonitor エントリを追加、 [ **INF DDInstall セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)の INF ファイル。 LanguageMonitor エントリでは、言語モニターの表示名と INF の次の例のように、その DLL の名前の一覧を表示します。 LanguageMonitor エントリは、プリンター言語モニターを使用することを制御するすべてのプリンター ドライバーを含める必要があります。 詳細については、次を参照してください。[プリンター INF ファイル](printer-inf-files.md)します。

```cpp
[AcmeInst]
CopyFiles=@ACME.PPD,ACMEMON
DataSection=PSCRIPT_DATA
DataFile=ACME.PPD
LanguageMonitor="Acme Language Monitor,acmemon.dll"
Include=ntprint.inf
Needs=PSCRIPT.OEM

[ACMEMON]
acmemon.dll,,,0x00000020

[DestinationDirs]
DefaultDestDir=66000
ACMEMON=66002

[SourceDisksNames]
1= %Location%,,,

[SourceDisksFiles]
acme.ppd = 1,\i386
acmemon.dll = 1,\i386
```

ドライバーの追加ウィザードまたはプリンターの追加ウィザードは、この INF ファイルを読み取るし、プリンタ ドライバに関連付けられた言語モニターをインストールします。

カスタム インストール アプリケーションが、スプーラーを呼び出すことによって言語モニターをインストールする代わりに、 **AddMonitor**関数を明示的に特定のモニター DLL のみをインストールします。

(、 **AddMonitor**関数は、Microsoft Windows SDK ドキュメントに記載されています)。

### <a href="" id="ddk-installing-a-port-monitor-gg"></a>ポート モニターをインストールします。

ポート モニターをインストールするには、インストール メディアがプリンター INF ファイルを含める必要があります (どのクラスに対して、INF ファイルは、プリンターを =) PortMonitors セクションを格納しています。 このセクションでは 1 つのエントリが 2 つのエントリを含むインストール セクションを指す: [ **INF CopyFiles ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive)のすべてのポート モニター、および PortMonitorDll エントリを構成するファイルを一覧表示します。ポート モニター インターフェイスは、前の一覧の実装でいる DLL を指定します。 次のコード例は、これらの点を示しています。 PortMonitors セクションのという名前の SamplePortMon インストール セクションへのポインター。 ここでは、INF、 **CopyFiles**ディレクティブは、ポート モニターを構成する 3 つのファイルをコピーします。 次は、PortMonitorDll エントリは、ポート モニターのインターフェイスを実装する DLL を識別します。

```cpp
[PortMonitors]
"Sample Port Monitor" = SamplePortMon

[SamplePortMon]
CopyFiles = @file1.dll, @file2.dll, @file3.hlp
PortMonitorDll = file1.dll
```

ポート モニターをインストールするには、コントロール パネルの [プリンタ] フォルダを開きます。 プリンター フォルダーの**ファイル**メニューの **サーバー プロパティ**します。 **ファイル サーバーのプロパティ**ダイアログ ボックスで、をクリックして、**ポート**タブをクリックし、をクリックし、**ポートの追加.** ボタンをクリックします。 **プリンター ポート**ダイアログ ボックスで、をクリックして、**新しいポートの種類.** ボタンをクリックします。 テキスト入力ボックスでは、INF ファイルへのパスを入力し、クリックして**OK**します。

カスタム インストール アプリケーションがポートをインストールする代わりへの呼び出しで DLL を監視、 **AddMonitor**で説明されているとおりに機能[ポート モニター](https://docs.microsoft.com/windows/desktop/printdocs/port-monitors)します。

 

 




