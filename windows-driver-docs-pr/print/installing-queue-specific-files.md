---
title: キュー固有ファイルのインストール
description: キュー固有ファイルのインストール
ms.assetid: 86cb16d5-6035-4a4d-a6b7-f27ebd3e9f5c
keywords:
- ポイント アンド プリントの WDK、キューに固有のファイル
- WDK のプリンターをキューに固有のファイル
- 印刷キューの WDK、ポイント アンド プリント
- キューの WDK プリンター、ポイント アンド プリント
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e022281cfbdc68ff209919f5de75c978f9a20bf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345516"
---
# <a name="installing-queue-specific-files"></a>キュー固有ファイルのインストール





プリンターのインストール時にインストールのベンダーから提供されたアプリケーションは、ファイル、特定の印刷キューに関連付けるには、任意の型のセットを指定できます。 ファイルは、プリント サーバーに接続する各クライアントにダウンロードされます。 インストール アプリケーションでは、次の表に示すように、レジストリで、値を配置することで、ファイルを指定します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>［値の名前］</th>
<th>値の種類</th>
<th>値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ディレクトリ</strong></p></td>
<td><p>REG_SZ</p></td>
<td><p>指定されたファイルへのディレクトリ パス<strong>ファイル</strong>します。 サーバー上のソース パスと、クライアントの移行先パスの両方として使用されます。 このパスでは、環境変数の PRINT$ 関連します。</p></td>
</tr>
<tr class="even">
<td><p><strong>ファイル</strong></p></td>
<td><p>REG_MULTI_SZ</p></td>
<td><p>ファイルのクライアントがプリント サーバーに接続するときに、クライアントにコピーするファイルの名前。 ファイルは、Dll、データ ファイル、または他の種類のファイルにあります。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Module</strong></p></td>
<td><p>REG_SZ</p></td>
<td><p>ファイル名の省略可能な<a href="point-and-print-dlls.md" data-raw-source="[Point and Print DLL](point-and-print-dlls.md)">ポイントと印刷 DLL</a>します。</p></td>
</tr>
</tbody>
</table>

 

アプリケーションは、印刷スプーラーを呼び出すことによってこれらの値を作成する必要があります**SetPrinterDataEx**関数。 この呼び出しで指定されたレジストリ キーは、として書式設定する必要があります。

**CopyFiles\\**<em>ComponentName</em>

場所*ComponentName*ファイルが関連付けられているソフトウェア コンポーネントの名前を指定します。 Image Color Management (ICM) と関連付けられているファイルを指定するなど、 **CopyFiles\\ICM**キー。 レジストリ キーの名前を引数として指定する、 **SetPrinterDataEx**関数、および関数は、プリント サーバー上の印刷キューのキーのサブキーとしてキーを作成します。

### <a href="" id="ddk-installation-example-gg"></a>インストール例

例については、HP 色 LaserJet プリンターがプリント サーバーがインストールされているし、"HpColor"の印刷キューの名前が割り当てられているとします。 また Microsoft ICM が印刷キューに関連する次の 2 つのファイルが必要であるとします。

-   PRINT$ hpclrlsr.icm、という名前のカラー プロファイルにある\\サーバー上の色。

-   PRINT$ Mscms.dll、という名前の DLL にある\\サーバー上の色。

インストール アプリケーションで ICM API 関数を呼び出します**AssociateColorProfileWithDevice**、この**SetPrinterDataEx**次のサーバーのレジストリ エントリを作成します。

```cpp
CopyFiles\ICM\Directory: Color
CopyFiles\ICM\Files: hpclrsr.icm
CopyFiles\ICM\Module: mscms.dll
```

Mscms.dll モジュールは、[ポイントと印刷 DLL](point-and-print-dlls.md)をエクスポートする**GenerateCopyFilePaths**と**SpoolerCopyFileEvent**関数。

 

 




