---
title: PCL XL ミニドライバーをインストールする
description: PCL XL ミニドライバーをインストールする
ms.assetid: 88e4e1a0-8adb-4f40-abeb-a4da761ca4ee
keywords:
- PCL XL ベクター グラフィックス WDK Unidrv、ミニドライバーをインストールします。
- ミニドライバー WDK PCL XL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36202095f6d007dc86d2177a8dc6e7c43cd226b2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573291"
---
# <a name="installing-a-pcl-xl-minidriver"></a>PCL XL ミニドライバーをインストールする





Ntprint.inf が、次に、Windows XP 以降では、 \[PCLXL します。OEM\]セクション。

```cpp
[PCLXL.OEM]
CopyFiles=PCLXL,@PCL5ERES.DLL
```

[ **INF CopyFiles ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546346)すべてで示されているファイルのコピー、 \[PCLXL\]セクションと pcl5eres.dll、既定のインストール先ディレクトリにします。 \[PCLXL\]セクションも ntprint.inf に表示され、コピーするファイルを一覧表示されます。

```cpp
[PCLXL]
PCLXL.DLL
PCLXL.GPD
P6FONT.GPD
PJL.GPD
P6DISP.GPD
```

Pclxl.dll 含む PCL XL *UFMs*とさまざまなリソースの文字列。 このセクションで示すその他の GPDs は、PCL XL (PCL 6) のサポート ファイルです。

PCL XL プリンターのミニドライバーをインストールするには、OEM は、プリンターに固有の INF に、次のようなセクションを追加します。 この INF は、ntprint.inf が前に読み込まれます。

```cpp
[P6SAMPLE.GPD]
CopyFiles=@P6SAMPLE.GPD
DataSection=UNIDRV_DATA
DataFile=P6SAMPLE.GPD
Include=NTPRINT.INF
Needs=UNIDRV.OEM,TTFSUB.OEM,PCLXL.OEM
```

前のセクションで、 **CopyFiles**ディレクティブを 1 行目では、OEM の GPD ファイル (この例で呼び出された p6sample.gpd) をコピーします。 関連付けられているエントリ、 **DataSection** 2 行目でディレクティブ (を参照してください[INF ファイル データのセクションではプリンター](printer-inf-file-data-sections.md)と[プリンター INF ファイルのインストール セクション](printer-inf-file-install-sections.md)) を指す、\[UNIDRV\_データ\]ntprint.inf」セクション。 **DataFile** 3 行目のディレクティブは、その p6sample.gpd がこのプリンター ミニドライバーに関連付けられているデータ ファイルを指定します。 4 行目では、ntprint.inf にインクルードするとします。 次の 3 つのエントリ、**必要がある**5 行目のディレクティブは、ntprint.inf で同じ名前の付いたセクションを参照してください。 これにより、driver.cab で読み込まれるファイルにアクセスする INF ファイルです。

詳細についてを使用して、 **CopyFiles**プリンターのインストールのディレクティブを参照してください[プリンター INF ファイル CopyFiles セクション](printer-inf-file-copyfiles-sections.md)します。

 

 




