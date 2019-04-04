---
title: 複数のプラットフォームやオペレーティング システムの INF ファイルの作成
description: 複数のプラットフォームやオペレーティング システムの INF ファイルの作成
ms.assetid: 61996c72-c5a7-4ff0-aeb3-6e77b77542c8
keywords:
- INF ファイル WDK デバイス インストールでは、複数のプラットフォームやオペレーティング システム
- 複数のオペレーティング システムの WDK、INF ファイル
- クロス プラットフォームの INF ファイル WDK
- WDK、クロスプラット フォーム システム INF ファイルのオペレーティング システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2e1eea87b4be2374b764981dcc7288e94ae469a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560870"
---
# <a name="creating-inf-files-for-multiple-platforms-and-operating-systems"></a>複数のプラットフォームやオペレーティング システムの INF ファイルの作成





システム定義のプラットフォームの拡張機能を使用して[INF ファイルのセクションとディレクティブ](inf-file-sections-and-directives.md)、クロスプラット フォームのインストールの 1 つの INF ファイルを作成することができます。 拡張機能は、作成する*装飾*セクション名で、各ターゲット プラットフォームとオペレーティング システムに関連するどのセクションとディレクティブを指定します。 たとえば、x64 ベース システムでのみ、Itanium ベース システムでのみ、x86 ベースのシステムでのみ、または Windows 2000 および Windows の以降のバージョンでサポートされているすべてのシステムでは、デバイスをインストールする INF ファイルを作成することができます。

次の表では、拡張機能をサポートするセクションの名前を追加できるプラットフォームのシステムでサポートされている拡張機能をまとめたものです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">プラットフォームの拡張機能</th>
<th align="left">使用</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>.ntamd64</strong></p></td>
<td align="left"><p>セクションでは、Windows XP 以降でサポートされている x64 ベースのシステムにデバイスまたはデバイスと互換性のあるモデルのセットをインストールするための手順を説明します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>.ntia64</strong></p></td>
<td align="left"><p>セクションでは、Itanium ベース システム Windows XP 以降でサポートされているデバイスまたはデバイスと互換性のあるモデルのセットをインストールするための手順を説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>.ntx86</strong></p></td>
<td align="left"><p>セクションでは、Windows XP 以降でサポートされている x86 ベースのシステムにデバイスまたはデバイスと互換性のあるモデルのセットをインストールするための手順を説明します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>.ntarm</strong></p></td>
<td align="left"><p>セクションでは、Windows 8 以降でサポートされている ARM ベースのシステムにデバイスまたはデバイスと互換性のあるモデルのセットをインストールするための手順を説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>.ntarm64</strong></p></td>
<td align="left"><p>セクションでは、Windows 10 バージョン 1709 以降でサポートされている ARM64 ベースのシステムにデバイスまたはデバイスと互換性のあるモデルのセットをインストールするための手順を説明します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>.nt</strong></p></td>
<td align="left"><p>Windows Server 2003 SP1 より前のバージョンの Windows では、セクションは、デバイスまたはデバイスと互換性のあるモデルのセットをオペレーティング システムでサポートされているすべてのシステムをインストールするための手順を説明します。</p>
<p>Windows Server 2003 SP1 以降、セクションは、デバイスまたはデバイスと互換性のあるモデルのセットをオペレーティング システムでサポートされている x86 ベースのシステムをインストールするための手順を説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>(プラットフォーム拡張子なし)</p></td>
<td align="left"><p>Windows Server 2003 SP1 より前のバージョンの Windows では、セクションは、デバイスまたはデバイスと互換性のあるモデルのセットをオペレーティング システムでサポートされているすべてのシステムをインストールするための手順を説明します。</p>
<p>Windows Server 2003 SP1 以降、セクションは、デバイスまたはデバイスと互換性のあるモデルのセットをオペレーティング システムでサポートされている x86 ベースのシステムをインストールするための手順を説明します。</p></td>
</tr>
</tbody>
</table>

 

**重要な**  以降 Windows Server 2003 SP1 では、INF ファイルは内のエントリを装飾する必要があります、 [ **INF モデル セクション**](inf-models-section.md)と **。ntia64**、.**ntarm**、.**ntarm64**または **。ntamd64** x86 以外を指定するプラットフォームの拡張機能は、オペレーティング システムのバージョンを対象します。 X86 ベースのターゲット オペレーティング システムのバージョンの INF ファイルまたは (x64 ベースのアーキテクチャのファイル システム ドライバー INF ファイル) などの非 PnP ドライバーの INF ファイルでは、これらのプラットフォーム拡張機能は必要はありません。

 

**ヒント:** 内のエントリを常に修飾することを強くお勧め、 [ **INF モデル セクション**](inf-models-section.md)プラットフォーム拡張機能は、Windows XP のターゲットのオペレーティング システム以降のバージョンの Windows を含むです。 X86 ベースのハードウェア プラットフォームでの使用を避ける必要があります、 **.nt**プラットフォーム拡張機能と使用 **.ntx86**代わりにします。

 

## <a name="in-this-section"></a>このセクションの内容


-   [INF ファイル プラットフォーム拡張機能と x64 ベース システム](inf-file-platform-extensions-and-x64-based-systems.md)
-   [INF ファイル プラットフォーム拡張機能とシステムの x86 ベース](inf-file-platform-extensions-and-x86-based-systems.md)
-   [クロス プラットフォームの INF ファイル](cross-platform-inf-files.md)
-   [その他のセクション名の拡張子を持つプラットフォーム拡張機能を組み合わせること](combining-platform-extensions-with-other-section-name-extensions.md)

INF ファイル プラットフォーム拡張機能を使用して、クロス プラットフォームのインストールをサポートする方法の例は、[クロスプラット フォーム対応の INF ファイル](cross-platform-inf-files.md)を参照してください。

セクション名の拡張機能と組み合わせてプラットフォーム拡張機能を使用する方法については、[結合プラットフォーム拡張機能とその他のセクション名の拡張機能](combining-platform-extensions-with-other-section-name-extensions.md)を参照してください。

プラットフォームの拡張機能を通じてターゲットのオペレーティング システムを指定する方法については、[プラットフォーム拡張機能バージョンのオペレーティング システムと組み合わせて](combining-platform-extensions-with-operating-system-versions.md)を参照してください。

複数のオペレーティング システム バージョンでドライバーをインストールするのに使用できるサンプルの INF ファイルについては、[複数バージョンの Windows デバイスのインストール用のサンプル INF ファイル](sample-inf-file-for-device-installation-on-multiple-versions-of-windows.md)を参照してください。

 

 





