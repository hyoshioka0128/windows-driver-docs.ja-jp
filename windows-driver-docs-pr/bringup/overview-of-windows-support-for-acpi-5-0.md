---
title: ACPI 5.0 に対する Windows サポートの概要
description: ACPI 5.0 仕様では、8 以降、Windows を実行する SoC ベースのモバイル プラットフォームのサポートを有効には、Windows の以前のバージョンで導入された多くの便利な機能をサポートするために続行されます。
ms.assetid: BAFBA051-FEDA-469B-9B67-C74D252C84F9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c44a09ba3320c491de3ac345a3899dd1e769283d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549821"
---
# <a name="overview-of-windows-support-for-acpi-50"></a>ACPI 5.0 に対する Windows サポートの概要


[ACPI 5.0 仕様](https://www.uefi.org/specifications)で導入された多くの便利な機能をサポートするために引き続き有効以降を実行する Windows 8、SoC ベースのモバイル プラットフォームをサポートによって、Windows Server 2016 の以降のサポート以前のバージョンの Windows。 この設計のガイドは、具体的には、Windows Server 2016 用に設計されたシステムの場合ともプラットフォーム SoC ベースに適用される ACPI 5.0 の部分に実装を指揮してで Windows を実行する ACPI の SoC 固有の機能を実装するためのベスト プラクティスについて説明しますこれらのプラットフォームです。

## <a name="scope"></a>Scope


この設計ガイドの対象とは、ファームウェアの開発者およびファームウェアのサポートと実装のガイダンスを必要とするシステム設計者です。 監視と次のガイドラインに準拠しているにより、SoC プラットフォームおよび Windows Server 2016 のシステムで Windows の適切な機能は役立ちます。

具体的には、この設計のガイダンスには、アイドル状態の省電力 S0 をサポートするハードウェアに削減 ACPI プラットフォームが対象とします。 ただし、このガイドのほとんどは、ACPI 5.0 および Windows 8 を実行しているに準拠した以降である任意のプラットフォームまたは Windows Server 2012 またはそれ以降にも適用されます。 さらに、このトピックでは、クラムシェル フォーム ファクターまたはワイヤレス、マルチ touch 専用のモバイル プラットフォームのいずれかを想定しています。 そのため、自体を予想されるこのようなプラットフォームで広く使用されるテクノロジに制限されます。 このドキュメントで取り上げられていないテクノロジのリーダーは実装については、ACPI 仕様自体に呼ばれます。

## <a name="firmware-revision-support"></a>ファームウェアのリビジョンのサポート


Windows がファームウェアのリビジョンに基づくをサポートしている、 [ACPI 5.0 仕様](https://www.uefi.org/specifications)します。

**注**  Windows は、ACPI 5.0 仕様で定義されている機能のサブセットをサポートします。 Windows では、ファームウェアのリビジョンをより高いを比較する明示的なチェックはありません。 Windows では、この設計ガイド」の説明に従ってこのファームウェアには、必要なサポートが含まれている場合、ACPI 仕様の上位のリビジョンに準拠したファームウェアをサポートします。

 

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>トピック</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="summary-of-acpi-support-in-windows.md" data-raw-source="[Summary of ACPI support in Windows](summary-of-acpi-support-in-windows.md)">Windows での ACPI のサポートの概要</a></p></td>
<td><p>このトピックでは、Advanced Configuration and Power Interface (ACPI) 5.0 機能 SoC ベースのプラットフォームで Windows をサポートするために必要なのサブセットをまとめたものです。</p></td>
</tr>
<tr class="even">
<td><p><a href="hardware-requirements-for-soc-based-platforms.md" data-raw-source="[Hardware requirements for SoC-based platforms](hardware-requirements-for-soc-based-platforms.md)">SoC ベースのプラットフォームのハードウェア要件</a></p></td>
<td><p><a href="https://www.uefi.org/specifications" data-raw-source="[ACPI 5.0 specification](https://www.uefi.org/specifications)">ACPI 5.0 仕様</a>Windows を実行している SoC ベースのプラットフォームをサポートするためのハードウェア要件の新しいセットが導入されています。 ACPI 5.0 は、コストを削減するシステムのハードウェア制限の設計をサポートしていますが、長いバッテリ寿命を有効にするコネクテッド スタンバイ電源モデルをサポートしています。</p></td>
</tr>
<tr class="odd">
<td><p><a href="acpi-namespace-hierarchy.md" data-raw-source="[ACPI namespace hierarchy](acpi-namespace-hierarchy.md)">ACPI 名前空間の階層</a></p></td>
<td><p>ACPI 名前空間の階層は、プラットフォームを正確に反映する必要があります&#39;以降、プロセッサでは、s ハードウェア トポロジ&#39;s システム バス (&quot;_SB&quot;)。 一般に、バスまたはコント ローラーに接続するデバイスは、名前空間にそのバスまたはコント ローラーのデバイスの子として表示されます。</p></td>
</tr>
<tr class="even">
<td><p><a href="microsoft-asl-compiler.md" data-raw-source="[Microsoft ASL compiler](microsoft-asl-compiler.md)">Microsoft ASL コンパイラ</a></p></td>
<td><p>Microsoft ACPI のソース言語 (ASL) コンパイラ サポートでは、Advanced Configuration and Power Interface Specification、バージョン 5.0 の機能のバージョン 5.0 (<a href="https://www.uefi.org/specifications" data-raw-source="[ACPI 5.0 specification](https://www.uefi.org/specifications)">ACPI 5.0 仕様</a>)。 ASL コンパイラで、Windows Driver Kit (WDK) 8.1 に分散されます。</p></td>
</tr>
</tbody>
</table>

 

 

 




