---
title: DEP と PAE を構成するためのブート パラメーター
description: DEP と PAE を構成するためのブート パラメーター
ms.assetid: cb8b6298-e679-4ca3-8b94-4f0c6af23a3f
keywords:
- WDK のブート パラメーター
- ブート エントリ パラメーター WDK
- DEP の WDK のブート パラメーター
- データ実行防止 WDK のブート パラメーター
- 物理アドレス拡張機能の WDK のブート パラメーター
- PAE WDK のブート パラメーター
- ハードウェア ベースの DEP WDK ブート パラメーター
- ソフトウェア ベースの DEP WDK ブート パラメーター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac10907d10d41c66b677f8090e3c1251bde3f8d4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360411"
---
# <a name="boot-parameters-to-configure-dep-and-pae"></a>DEP と PAE を構成するためのブート パラメーター


このトピックでは、ブート パラメーターを使用して有効化、無効化、およびこれらの機能をサポートするオペレーティング システムでデータ実行防止 (DEP) と物理アドレス拡張 (PAE) を構成する方法について説明します。

DEP と PAE のブート パラメーターについては、次を参照してください。、 [ **BCDEdit/set** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--set)コマンドと**nx**と**pae**オプション。

**重要な**  DEP は、非常に効果的なセキュリティ機能の代替手段があるない場合、無効にしないことです。 DEP と PAE の既定の設定は、ほとんどのシステムに最適です。 重要な処理タスクに干渉しない限りは、既定の設定を変更しないでください。 このセクションでは、これらの機能を構成する方法について説明するが、既定の設定を変更する推奨事項として解釈されませんする必要があります。

 

### <a name="span-iddepandpaebootparametersspanspan-iddepandpaebootparametersspandep-and-pae-boot-parameters"></a><span id="dep_and_pae_boot_parameters"></span><span id="DEP_AND_PAE_BOOT_PARAMETERS"></span>DEP と PAE ブート パラメーター

ブート時に有効になっているし、値の設定で構成されます DEP と PAE、 **nx**と**pae**パラメーターを使用して、 [ **BCDEdit/set** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--set)コマンド。

これらのブート パラメーターには、競合する影響があります。 DEP と PAE を構成するには、各パラメーターのドキュメントで説明しをこのトピックで説明するパラメーターの組み合わせのみを使用します。 特に実稼働システムでの競合するパラメーターを持つ実験しない操作を行います。

### <a name="span-idtheinteractionofdepandpaebootparametersspanspan-idtheinteractionofdepandpaebootparametersspanthe-interaction-of-dep-and-pae-boot-parameters"></a><span id="the_interaction_of_dep_and_pae_boot_parameters"></span><span id="THE_INTERACTION_OF_DEP_AND_PAE_BOOT_PARAMETERS"></span>DEP と PAE ブート パラメーターの相互作用

DEP の 2 種類あります。

-   *ハードウェア - DEP で強制*カーネル モードとユーザー モードの両方のプロセスの DEP を有効にします。 これは、プロセッサとオペレーティング システムでサポートする必要があります。

<!-- -->

-   *ソフトウェア強制 DEP*ユーザー モード プロセスでのみ DEP を有効にします。 これは、オペレーティング システムでサポートする必要があります。

、Windows の 32 ビット バージョンで*ハードウェア - DEP で強制*PAE、DEP はサポートされているすべての Windows オペレーティング システムでサポートされている必要があります DEP は、ハードウェア DEP をサポートするプロセッサ コンピューターで有効な場合、Windows は自動的に PAE を有効にし、無効にするブート パラメーターの値を無視します。

次のセクションでは、各 Windows オペレーティング システムのパラメーターの組み合わせをまとめたものです。

### <a name="span-iddepandpaeparametercombinationsspanspan-iddepandpaeparametercombinationsspandep-and-pae-parameter-combinations"></a><span id="dep_and_pae_parameter_combinations"></span><span id="DEP_AND_PAE_PARAMETER_COMBINATIONS"></span>DEP と PAE パラメーターの組み合わせ

次の一覧には、DEP と PAE を構成するために使用するブート パラメーターの組み合わせについて説明します。

**注**省略可能な **{** <em>ID</em> **}** 特定 Windows ブート ローダー ブート エントリを構成するための GUID です。 指定しない場合、 **{** <em>ID</em> **}** のコマンドは、現在のオペレーティング システムのブート エントリを変更します。 詳細については、次を参照してください。、 [ **BCDEdit/set** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--set)コマンド。

 

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">アクション</th>
<th align="left"></th>
<th align="left">Windows Vista 以降</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>DEP を有効にするには</strong></p>
<p>(1 つのパラメーターの組み合わせを選択します)</p>
<p>DEP は、ハードウェア DEP をサポートするコンピューターで有効な場合は、PAE はこれらのパラメーターの組み合わせも有効にします。</p></td>
<td align="left"></td>
<td align="left"><p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>nx AlwaysOn</strong></p>
<p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>nx OptIn</strong></p>
<p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>nx OptOut</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>システム ソフトウェア DEP で DEP と PAE を有効にするには</strong></p>
<p>(1 つのパラメーターの組み合わせを選択します)</p>
<p>ハードウェア DEP をサポートしているコンピューターで、PAE は自動的に有効になっている DEP. を有効にすると</p></td>
<td align="left"></td>
<td align="left"><p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>nx AlwaysOn</strong></p>
<p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>pae default</strong></p>
<p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>nx OptIn</strong></p>
<p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>pae default</strong></p>
<p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>nx OptOut</strong></p>
<p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>pae default</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>DEP を無効にするには、PAE を有効にします。</strong></p></td>
<td align="left"></td>
<td align="left"><p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>nx AlwaysOff</strong></p>
<p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>pae ForceEnable</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>DEP を無効にするには、PAE を有効にします。</strong></p></td>
<td align="left"></td>
<td align="left"><p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>nx AlwaysOff</strong></p>
<p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>pae ForceEnable</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>DEP と PAE の両方を無効にするには</strong></p></td>
<td align="left"></td>
<td align="left"><p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>nx AlwaysOff</strong></p>
<p><strong>/set</strong> [<strong>{</strong><em>ID</em><strong>}</strong>] <strong>pae ForceDisable</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>DEP と PAE の両方を無効にするには</strong></p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

 

 





