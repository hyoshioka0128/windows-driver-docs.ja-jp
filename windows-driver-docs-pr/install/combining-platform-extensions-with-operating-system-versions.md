---
title: プラットフォーム拡張機能とオペレーティング システム バージョンを組み合わせる
description: プラットフォーム拡張機能とオペレーティング システム バージョンを組み合わせる
ms.assetid: ef3b7138-b68a-4dba-b011-fcb93e3072a3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 827d79100eae252ec08dca93ac455f8dc1371fd7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357026"
---
# <a name="combining-platform-extensions-with-operating-system-versions"></a>プラットフォーム拡張機能とオペレーティング システム バージョンを組み合わせる


内で、 [ **INF 製造元セクション**](inf-manufacturer-section.md)指定することができます、INF ファイルの[ **INF*モデル*セクション**](inf-models-section.md)さまざまなバージョンの Windows オペレーティング システムに固有です。 これらのバージョン固有*モデル*のセクションを使用して識別されます、 *TargetOSVersion*装飾します。

異なる同じ INF ファイル内で[ **INF*モデル*セクション**](inf-models-section.md)オペレーティング システムの異なるバージョンを指定できます。 指定されたバージョンをターゲット オペレーティング システムのバージョンを示すため、INF*モデル*セクションが使用されます。 Windows を使用してバージョンが指定されていない場合、*モデル*せずセクション、 *TargetOSVersion*の装飾をすべてのオペレーティング システムのすべてのバージョン。

### <a name="targetosversion-decoration-format"></a>*TargetOSVersion*装飾形式

次の例では、正しい形式の*TargetOSVersion* Windows XP、Windows 10 バージョン 1511 を装飾します。

**nt**\[*アーキテクチャ*\]\[**.**\[ *OSMajorVersion*\]\[**.**\[ *OSMinorVersion*\]\[**.**\[ *ProductType*\]\[**.**\[ *SuiteMask*\]\]\]\]\]

以降では、Windows 10 バージョン 1607 (ビルド 14310 およびそれ以降)、正しい形式の*TargetOSVersion*装飾が含まれています*BuildNumber*:

**nt**\[*アーキテクチャ*\]\[**.**\[ *OSMajorVersion*\]\[**.**\[ *OSMinorVersion*\]\[**.**\[ *ProductType*\]\[**.**\[ *SuiteMask*\]\]\[**.**\[ *BuildNumber*\]\]\]\]\]

各フィールドの定義は次のとおりです。

<a href="" id="nt"></a>**nt**  
対象のオペレーティング システムは、NT ベースを指定します。 Windows 2000 および以降のバージョンの Windows NT ベースのすべてが。

<a href="" id="architecture"></a>*アーキテクチャ*  
ハードウェア プラットフォームを識別します。 指定する場合、この必要がありますで**x86**、 **ia64**、または**amd64**します。 指定しない場合、関連付けられている INF*モデル*セクションは、任意のハードウェア プラットフォームで使用できます。

<a href="" id="osmajorversion"></a>*OSMajorVersion*  
オペレーティング システムのメジャー バージョン番号を表す数値。 次の表では、Windows オペレーティング システムのメジャー バージョンを定義します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Windows のバージョン</th>
<th align="left">メジャー バージョン</th>
</tr>
</thead>
<tbody>
<tr class="even">
<td align="left"><p>Windows 10</p></td>
<td align="left"><p>10</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Server 2012 R2</p></td>
<td align="left"><p>6</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 8.1</p></td>
<td align="left"><p>6</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Server 2012</p></td>
<td align="left"><p>6</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 8</p></td>
<td align="left"><p>6</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Server 2008 R2</p></td>
<td align="left"><p>6</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 7</p></td>
<td align="left"><p>6</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Server 2008</p></td>
<td align="left"><p>6</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows Vista</p></td>
<td align="left"><p>6</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Server 2003</p></td>
<td align="left"><p>5</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows XP</p></td>
<td align="left"><p>5</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="osminorversion"></a>*OSMinorVersion*  
オペレーティング システムのマイナー バージョン番号を表す数値。 次の表では、Windows オペレーティング システムのマイナー バージョンを定義します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Windows のバージョン</th>
<th align="left">［マイナー バージョン］</th>
</tr>
</thead>
<tbody>
<tr class="even">
<td align="left"><p>Windows 10</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Server 2012 R2</p></td>
<td align="left"><p>3</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 8.1</p></td>
<td align="left"><p>3</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Server 2012</p></td>
<td align="left"><p>2</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 8</p></td>
<td align="left"><p>2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Server 2008 R2</p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 7</p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Server 2008</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows Vista</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Server 2003</p></td>
<td align="left"><p>2</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows XP</p></td>
<td align="left"><p>1</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="producttype"></a>*ProductType*

表す数値*1 つ*、VER_NT_ の*xxxx*で定義されているフラグ*Winnt.h*次のようします。

**0x0000001** (VER_NT_WORKSTATION)

**0x0000002** (VER_NT_DOMAIN_CONTROLLER)

**0x0000003** (VER_NT_SERVER)

製品の種類が指定されている場合、INF ファイルは、オペレーティング システムが指定された製品の種類と一致する場合にのみ使用されます。 INF ファイルは、単一のオペレーティング システムのバージョンでは、複数の製品の種類をサポートしている場合複数*TargetOSVersion*エントリが必要です。

*SuiteMask*

表す数値*を組み合わせた*1 つ以上の VER_SUITE_*xxxx*で定義されているフラグ*Winnt.h*します。 これらのフラグを以下に示します。

**0x00000001** (VER_SUITE_SMALLBUSINESS)  
**0x00000002** (VER_SUITE_ENTERPRISE)  
**0x00000004** (VER_SUITE_BACKOFFICE)  
**0x00000008** (VER_SUITE_COMMUNICATIONS)  
**0x00000010** (VER_SUITE_TERMINAL)  
**0x00000020** (VER_SUITE_SMALLBUSINESS_RESTRICTED)  
**0x00000040** (VER_SUITE_EMBEDDEDNT)  
**0x00000080** (VER_SUITE_DATACENTER)  
**0x00000100** (VER_SUITE_SINGLEUSERTS)  
**0x00000200** (VER_SUITE_PERSONAL)  
**0x00000400** (VER_SUITE_SERVERAPPLIANCE)  

1 つまたは複数のスイート マスク値を指定する場合は、オペレーティング システムには、すべての指定された製品スイートが一致する場合にのみ INF ファイルが使用されます。 INF ファイルは、単一のオペレーティング システムのバージョンでは、複数の製品スイートの組み合わせをサポートしている場合複数*TargetOSVersion*エントリが必要です。

*BuildNumber*

OS ビルド番号セクションを適用するビルド 14310 以降またはそれ以降、Windows 10 のリリースの最小値を指定します。

ビルド番号では、いくつか特定の OS メジャー/マイナー バージョンのみを基準としたと見なされます、将来の OS メジャー/マイナー バージョンをリセットすることがあります。

任意で指定された数のビルド、 *TargetOSVersion*装飾が OS のメジャー/マイナー バージョンの場合にのみ評価される、 *TargetOSVersion*現在の OS (または AltPlatformInfo) のバージョンを正確に一致します。  現在の OS バージョンがで指定された OS バージョンよりも大きい場合、 *TargetOSVersion*装飾 (OSMajorVersion、OSMinorVersion) セクションが指定されたビルド番号に関係なく適用できると見なされます。 同様に、現在の OS バージョンが TargetOSVersion 装飾で指定された OS バージョンよりも小さい場合は、セクションは適用されません。

ビルド番号は、指定した場合、OS のバージョンとの BuildNumber、 *TargetOSVersion*装飾する必要があります OS バージョンよりも大きくして、Windows 10 ビルドこの装飾が初めて導入された 14310 のビルド番号。  ターゲットのビルド前の試行が実際に妨げるその OS 検討、装飾のすべての有効なこれらの変更 (Windows 10 ビルド 10240 など) することがなく、オペレーティング システムの以前のバージョンは、不明な装飾を解析できません。

### <a href="" id="how-setup-processes-targetosversion-decorations"></a>Windows でどのように処理*TargetOSVersion*装飾

Windows ホストのオペレーティング システムで、デバイスまたはドライバーをインストールするときに、以下の手順を処理する、 [ **INF*モデル*セクション**](inf-models-section.md) INF ファイル内で。

1.  1 つまたは複数[ **INF*モデル*のセクションでは**](inf-models-section.md)が、 *TargetOS*の装飾は、Windows の選択、INF*モデル*セクションは、ホスト オペレーティング システムの属性に最も近い。

    場合、INF など*モデル*セクションには、 *TargetOS*の装飾**ntx86.5.1**、ホスト オペレーティング システムが Windows XP を実行している場合、Windows はそのセクションを選択しますまたは。Windows の x86 ベースのシステムでの以降のバージョン。

    同様に場合、 [ **INF*モデル*セクション**](inf-models-section.md)が、 *TargetOS*の装飾**nt.6.0**、Windowsホスト オペレーティング システムが Windows Vista または Windows の任意のサポートされているハードウェア プラットフォームでの以降のバージョンの場合は、そのセクションを選択します。

    場合、INF*モデル*セクションには、 *TargetOS*の装飾**nt.10.0.14393**、ホスト オペレーティング システムが実行されている場合、Windows 10 ビルド 14393 以上任意のサポートされているハードウェア プラットフォームで、Windows がそのセクションを選択します。

2.  None の場合、 [ **INF*モデル*セクション**](inf-models-section.md)が、 *TargetOS*装飾、ホスト オペレーティング システムに一致する場合は、Windows の選択、*モデル*に一致するプラットフォームの拡張機能またはないプラットフォーム拡張機能セクション。

    たとえば、INF、*モデル*セクションのプラットフォームの拡張機能には**ntx86**、Windows ホストのオペレーティング システムが Microsoft Windows 2000 または Windows の x86 ベースでの以降のバージョンの場合は、そのセクションを選択しますシステム。

    同様に場合、 [ **INF*モデル*セクション**](inf-models-section.md)プラットフォーム拡張機能、セクションの場合は、ホスト オペレーティング システムが Windows 2000 またはそれ以降のバージョンの Windows 選択がありませんいずれかの Windows には、ハードウェア プラットフォームがサポートされています。

3.  Windows は、一致するを見つけられない場合[ **INF*モデル*セクション**](inf-models-section.md)、デバイスまたはドライバーをインストールする INF ファイルは使用されません。

### <a name="sample-inf-models-sections-withtargetosversion-decorations"></a>サンプル INF*モデル*でセクション*TargetOSVersion*装飾

次のトピック内のターゲットのオペレーティング システムのプラットフォームの拡張機能を装飾する方法のサンプルを提供する、 [ **INF*モデル*セクション**](inf-models-section.md):

[サンプル INF*モデル*セクションでは、1 つまたは複数の対象オペレーティング システム](sample-inf-models-sections-for-one-or-more-target-operating-system.md)

[サンプル INF*モデル*セクションでは、1 つだけの対象オペレーティング システム](sample-inf-models-sections-for-only-one-target-operating-system.md)

[Windows の複数のバージョンでデバイスのインストール用のサンプルの INF ファイル](sample-inf-file-for-device-installation-on-multiple-versions-of-windows.md)

 

 





