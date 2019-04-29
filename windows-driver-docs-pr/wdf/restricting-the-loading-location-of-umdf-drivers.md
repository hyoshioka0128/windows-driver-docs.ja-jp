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
ms.openlocfilehash: 4232d013b5cd416928241301aa7d1d4386f06aaa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325177"
---
# <a name="restricting-the-loading-location-of-umdf-drivers"></a>UMDF ドライバーの読み込み場所の制限


UMDF プラットフォームの %systemroot% 以外の任意の場所からのメインの UMDF ドライバー バイナリの読み込みに失敗\\System32\\ドライバー\\Umdf ディレクトリ。 そのため、UMDF INF ファイルは、そのディレクトリに UMDF ドライバーをインストールする場所を制限する必要があります。 UMDF ドライバーは、特権のないユーザーが改ざんされないことによりもこのディレクトリにインストールします。

%Systemroot% に UMDF ドライバー バイナリをインストールする\\System32\\ドライバー\\Umdf、UMDF ドライバーの INF ファイルを含める必要があります、 [ **INF DestinationDirs セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547383)次のコード例と同様です。

```cpp
[DestinationDirs]
UMDriverCopy=12,UMDF ; copies to drivers\umdf
```

"UMDriverCopy"は、次の例に示すようには、UMDF ドライバーのバイナリを一覧表示するセクションの INF ライター決定名を表します。

```cpp
[UMDriverCopy]
WUDFOsrUsbDriver.dll
```

[ **CopyFiles ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546346)も参照する必要があります、 **UMDriverCopy**セクションは、ソースからコピーするオペレーティング システム用の UMDF ドライバー バイナリの一覧を示します次の例に示すように、先にメディア。

```cpp
[OsrUsb_Install.NT]
CopyFiles=UMDriverCopy
```

 

 





