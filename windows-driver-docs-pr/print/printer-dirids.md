---
title: プリンター Dirids
description: プリンター Dirids
ms.assetid: 104af180-c739-4733-b21b-448cfe15ab71
keywords:
- INF ファイル WDK print、dirids
- dirids WDK
- ディレクトリ識別子 WDK プリンター
- プリンター dirids WDK
- id WDK プリンター
ms.date: 06/12/2020
ms.localizationpriority: medium
ms.openlocfilehash: 4ffc08cdf7f6adcd40052e178b6b93561b72e4d6
ms.sourcegitcommit: 8a3cb2a87ce9751059bca8145a55b8cc39c34de9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2020
ms.locfileid: "84756178"
---
# <a name="printer-dirids"></a>プリンター Dirids

INF ファイル内でターゲットディレクトリを指定する場合は、ディレクトリ識別子 ( `dirids` ) を使用する必要があります。 詳細については、「 [Dirids の使用](https://docs.microsoft.com/windows-hardware/drivers/install/using-dirids)」を参照してください。

次の表は、プリンター固有の一覧とその目的を示して `dirids` います。

| Dirid | 目的 | ディレクトリの内容 |
|--|--|--|
| 66000 | [Getprinterdriverdirectory](https://docs.microsoft.com/windows/win32/printdocs/getprinterdriverdirectory)関数によって返されるディレクトリパスを表します。 | ドライバーファイルと[依存ファイル](printer-inf-file-entries.md#ddk-dependent-files-gg)依存ファイル |
| 66001 | [Getprintprocessordirectory](https://docs.microsoft.com/windows/win32/printdocs/getprintprocessordirectory)関数によって返されるディレクトリパスを表します。 | [プリントプロセッサ](https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-print-processor)ファイル。 |
| 66002 | ローカルシステムの System32 にコピーする追加ファイルへのディレクトリパスを表します。 この表の次の段落を参照してください。 | [モニター](https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-print-monitor)ファイルを印刷します。 |
| 66003 | [Getcolordirectory](https://docs.microsoft.com/previous-versions/windows/desktop/wcs/getcolordirectory)関数によって返されるディレクトリパスを表します。 | ICM のカラープロファイルファイル。 |
| 66004 | プリンターの種類に固有の ASP ファイルのコピー先のディレクトリパスを表します。 | ASP ファイルと関連ファイル。 |

66002に割り当てられているディレクトリ内のファイルは、x86 `dirid` ドライバーが x86 システムにローカルにインストールされている場合など、ネイティブアーキテクチャのプリンタードライバーがローカルシステムにインストールされている場合に、System32 サブディレクトリにコピーされます。 ドライバーがリモートシステムにインストールされている場合、このディレクトリ内のファイルは無視されます。

プリンタクラスインストーラがスプーラの[Addprinter Driverex](https://docs.microsoft.com/windows/win32/printdocs/addprinterdriverex)関数を呼び出すと、プリンタドライバがインストールされます。 この関数では、すべてのドライバーファイルが**Getprinterdriverdirectory**関数によって返されるディレクトリに配置されている必要があります。
