---
title: V4 ドライバーの INF
description: V4 印刷ドライバーのセットアップのモデルでは、引き続き INF ファイルを使用するもプリンターの特定のセットアップのディレクティブをキャプチャする場合は、新しいマニフェスト ファイルを採用しています。
ms.assetid: 48F19796-43F9-4A69-B042-1305245C9CB9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c641762929e4619a4c15762878bd730d2e8e2f3b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550226"
---
# <a name="v4-driver-inf"></a>V4 ドライバーの INF


V4 印刷ドライバーのセットアップのモデルでは、引き続き INF ファイルを使用するもプリンターの特定のセットアップのディレクティブをキャプチャする場合は、新しいマニフェスト ファイルを採用しています。

## <a name="sample-inf"></a>サンプル INF


注意してくださいサンプル v4 印刷ドライバーの INF ファイルがこのトピックでは含まれていないこと、プリンターに固有のディレクティブ。 終わる名前は常に v4 のマニフェスト ファイルでプリンター固有の手順が含まれている"– manifest.ini"。 各ドライバーのドライバー パッケージ内では、独自の v4 マニフェスト ファイルを指定できます。

次のサンプルの INF ファイルでは、架空の会社 Fabrikam が v4 印刷ドライバーを実行するインストールされる印刷デバイスを製造されたことを前提としています。

```INF
[Version]
Signature="$Windows NT$"
Provider="Fabrikam"
ClassGUID={4D36E979-E325-11CE-BFC1-08002BE10318}
Class=Printer
CatalogFile=prnfa999.CAT
DriverVer=09/12/2010,6.2.8060.4
ClassVer=4.0 ;This causes v4 setup to take place

[Manufacturer]
"Fabrikam"=Fabrikam,NTamd64

[Fabrikam.NTamd64] ;Add your models here
"Fabrikam Laser 9000" =        Laser9000,Fabrik9000_sdfjkals                     ;HWID example
"Fabrikam Laser 9100" =        Laser9000,Fabrik9100_sjkasj                       ;HWID example
"Fabrikam Laser 9000 series" = Laser9000,{E0691E8C-F7CC-456E-A7B5-D1FC19BA2279}  ;PrinterDriverID

[Laser9000]
CopyFiles=Laser9000_FILES

[Laser9000_FILES]
faPDL.gpd
faPDL-pipelineconfig.xml
faPDL-manifest.ini
faPDL.dll

[SourceDisksNames.amd64]
1 = %Location%,,,
2 = %Location%,,,amd64

[SourceDisksNames.x86]
1 = %Location%,,,
2 = %Location%,,,x86

[DestinationDirs]
DefaultDestDir=66000

[SourceDisksFiles]
faPDL.gpd=1
faPDL-pipelineconfig.xml=1
faPDL-manifest.ini = 1
faPDL.dll =2

[Strings]
Location="Fabrikam DVD"
```

## <a name="inf-directives"></a>INF ディレクティブ


次の表では、v4 印刷ドライバーと印刷クラス ドライバーでは許可されているプリンター固有のディレクティブの一覧を示します。

| ディレクティブ | 説明                                         | 制限                                                                                                                                           | 使用方法        |
|-----------|-----------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|
| ClassVer  | プリンター クラス ドライバーが v4 であることを示すために使用します。 | V4 印刷ドライバーが ClassVer を指定する必要があります 4.0 を = です。 V3 プリンター ドライバーは ClassVer を指定できます = 3.0 では、これは省略可能ですが。 この時点でその他の値がサポートされていません。 | ClassVer 4.0 を = |

## <a name="the-destinationdirs-keyword"></a>DestinationDirs キーワード


V4 ドライバーの INF では、する必要があります**DestinationDir**パッケージ内のすべてのファイルが指定されています。 サポートされている**DestinationDir**値が次の表に一覧表示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>DestinationDir ID</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>66000</td>
<td><p>[この宛先 ID がオーバー ロードされて v4 ドライバーの]</p>
<p>V4:これは、v4 印刷ドライバーの DefaultDestDir として設定する必要があります。 ドライバー ストアからファイルを実行することを指定します。</p>
<p>V3:これは、\3 ディレクトリにファイルをインストールすることを指定します。</p></td>
</tr>
<tr class="even">
<td>23</td>
<td><p>V4:これは、として設定する必要があります、 <strong>DestinationDir</strong>のカラー プロファイル。</p>
<p>V3:カラー プロファイルは、プリンター固有 DirID 66003 を使用してインストールする必要があります。</p></td>
</tr>
</tbody>
</table>

 

## <a name="inf-restrictions"></a>INF の制限


V4 印刷ドライバーでは、他のプリンター固有のディレクティブまたは、次の一覧が呼び出されたキーワードは定義する必要があります。

| INF ファイル キーワード            | 使用法の種類         |
|-----------------------------|--------------------|
| AddInterface                | ディレクティブ          |
| AddReg                      | ディレクティブ          |
| AddService                  | ディレクティブ          |
| BitReg                      | ディレクティブ          |
| ClassInstall32              | セクションの種類       |
| ClassInstall32.Service      | セクションの種類       |
| ConfigFile                  | v3 印刷ディレクティブ |
| CoreDriverDependencies      | v3 印刷ディレクティブ |
| CoreDriverSections          | v3 印刷ディレクティブ |
| データ ファイル                    | v3 印刷ディレクティブ |
| DDInstall.CoInstallers      | セクションの種類       |
| DDInstall.FactDef           | セクションの種類       |
| DDInstall.HW                | セクションの種類       |
| DDInstall.Interfaces        | セクションの種類       |
| DDInstall.LogConfigOverride | セクションの種類       |
| DDInstall.Services          | セクションの種類       |
| DDInstall.WMI               | セクションの種類       |
| DefaultInstall              | セクションの種類       |
| DefaultInstall.Services     | セクションの種類       |
| DelFiles                    | ディレクティブ          |
| DelReg                      | ディレクティブ          |
| DelService                  | ディレクティブ          |
| DontReflectOffline          | ディレクティブ          |
| DriverFile                  | v3 印刷ディレクティブ |
| DriverIsolation             | v3 印刷ディレクティブ |
| FeatureScore                | ディレクティブ          |
| HelpFile                    | v3 印刷ディレクティブ |
| Include                     | ディレクティブ          |
| Ini2Reg                     | ディレクティブ          |
| InterfaceInstall32          | セクションの種類       |
| LayoutFile                  | ディレクティブ          |
| LogConfig                   | ディレクティブ          |
| 必要があります。                       | ディレクティブ          |
| PackageAware                | v3 印刷ディレクティブ |
| RenFiles                    | ディレクティブ          |
| UpdateIniFields             | ディレクティブ          |
| UpdateInis                  | ディレクティブ          |

 

**NTPrint 参照**します。 NTPrint 参照は、マニフェスト ファイルで行われます。 INF ファイルでは、その DDInstall、CopyFiles、または SourceDisksFiles のセクションで NTPrint 参照に関する情報は必要ありません。

**構成のモジュール参照**します。 すべての印刷ドライバーを使用して、同じの構成モジュールをバイナリ (PrintConfig.dll)。構成モジュールを選択するためのドライバーのメカニズムはありません。

基本的な v4 プリンター ドライバーの INF ファイルを作成する方法については、[構築の基本的な v4 プリンター ドライバー](building-a-basic-v4-printer-driver.md)を参照してください。

 

 




