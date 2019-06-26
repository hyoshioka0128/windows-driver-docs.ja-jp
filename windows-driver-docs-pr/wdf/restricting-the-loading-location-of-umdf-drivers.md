---
title: UMDF ドライバーの読み込み場所の制限
description: UMDF ドライバーの読み込み場所の制限
ms.assetid: eac19fa8-2889-4cc3-9f4b-d11d7d3ed684
keywords:
- WDK UMDF の場所
- バイナリ WDK UMDF
- WDK UMDF ディレクトリ
- UMDriverCopy
- 読み込み場所 WDK UMDF
- INF ファイルの場所を読み込んで、WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac2debb2b190ef3a599c05643b576d6b4fb38b9c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376274"
---
# <a name="restricting-the-loading-location-of-umdf-drivers"></a>UMDF ドライバーの読み込み場所の制限


UMDF プラットフォームの %systemroot% 以外の任意の場所からのメインの UMDF ドライバー バイナリの読み込みに失敗\\System32\\ドライバー\\Umdf ディレクトリ。 そのため、UMDF INF ファイルは、そのディレクトリに UMDF ドライバーをインストールする場所を制限する必要があります。 UMDF ドライバーは、特権のないユーザーが改ざんされないことによりもこのディレクトリにインストールします。

%Systemroot% に UMDF ドライバー バイナリをインストールする\\System32\\ドライバー\\Umdf、UMDF ドライバーの INF ファイルを含める必要があります、 [ **INF DestinationDirs セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-destinationdirs-section)次のコード例と同様です。

```cpp
[DestinationDirs]
UMDriverCopy=12,UMDF ; copies to drivers\umdf
```

"UMDriverCopy"は、次の例に示すようには、UMDF ドライバーのバイナリを一覧表示するセクションの INF ライター決定名を表します。

```cpp
[UMDriverCopy]
WUDFOsrUsbDriver.dll
```

[ **CopyFiles ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive)も参照する必要があります、 **UMDriverCopy**セクションは、ソースからコピーするオペレーティング システム用の UMDF ドライバー バイナリの一覧を示します次の例に示すように、先にメディア。

```cpp
[OsrUsb_Install.NT]
CopyFiles=UMDriverCopy
```

 

 





