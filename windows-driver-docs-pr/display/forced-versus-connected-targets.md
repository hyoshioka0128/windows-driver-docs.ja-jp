---
title: 強制されたターゲットと接続されたターゲット
description: 強制されたターゲットと接続されたターゲット
ms.assetid: 690e585b-3c90-4373-844d-42afe033b59b
keywords:
- WDK の Windows 7 の表示、CCD 概念、強制的に接続されているターゲットとの接続が表示されます。
- WDK の Windows Server 2008 R2 の表示、CCD 概念、強制的に接続されているターゲットとの接続が表示されます。
- WDK の Windows 7 の表示、CCD 概念、強制的に接続されているターゲットと構成が表示されます。
- WDK の Windows Server 2008 R2 の表示、CCD 概念、強制的に接続されているターゲットと構成が表示されます。
- CCD WDK Windows 7 の概念を表示し、接続されているターゲットと強制
- 接続されているターゲットと強制 CCD 概念 WDK Windows Server 2008 R2 表示
- 接続されているターゲット WDK Windows 7 の表示と強制
- 接続されているターゲット WDK Windows Server 2008 R2 の表示と強制
- 強制ターゲット WDK Windows 7 の表示と接続
- 強制ターゲット WDK Windows Server 2008 R2 の表示と接続
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ddc82180342a83e267e4d2583e6fe55e8667916
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325342"
---
# <a name="forced-versus-connected-targets"></a>強制されたターゲットと接続されたターゲット


このセクションでは、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Windows オペレーティング システムにのみ適用されます。

CCD Api では、接続されているモニタおよび forceable ターゲットの概念を紹介します。 モニターは、GPU は、モニターは、モニターとターゲットの物理属性の存在を検出できる場合、ターゲットに接続されます。 ターゲットとは forceable の場合は、GPU が接続されているモニターを検出できない場合でも、GPU がターゲットから表示シグナルを送信できます。 すべてのアナログのターゲット型は forceable と見なされ、すべてのデジタル ターゲットは forceable は考慮されません。 次の表では、パスがアクティブでアクティブでない場合、接続されていると強制の状態の組み合わせがについて説明します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パス アクティブ状態</th>
<th align="left">パスの強制状態</th>
<th align="left">接続モニターの状態</th>
<th align="left">結果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Active</p></td>
<td align="left"><p>強制</p></td>
<td align="left"><p>Connected</p></td>
<td align="left"><p>モニターが接続されているし、アクティブになっているために、ターゲットの出力が有効になります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Active</p></td>
<td align="left"><p>強制</p></td>
<td align="left"><p>接続されていません</p></td>
<td align="left"><p>ターゲットの出力は、パスが強制された、アクティブになっています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Active</p></td>
<td align="left"><p>強制されません。</p></td>
<td align="left"><p>Connected</p></td>
<td align="left"><p>モニターが接続されているし、アクティブになっているために、ターゲットの出力が有効になります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Active</p></td>
<td align="left"><p>強制されません。</p></td>
<td align="left"><p>接続されていません</p></td>
<td align="left"><p>強制されていないと、モニターが接続されていないために、パスを設定できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>アクティブではありません。</p></td>
<td align="left"><p>強制</p></td>
<td align="left"><p>Connected</p></td>
<td align="left"><p>強制されると、モニターが接続されているために、ターゲットの出力を有効にすることができます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>アクティブではありません。</p></td>
<td align="left"><p>強制</p></td>
<td align="left"><p>接続されていません</p></td>
<td align="left"><p>強制されているため、ターゲットの出力を有効にすることができます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>アクティブではありません。</p></td>
<td align="left"><p>強制されません。</p></td>
<td align="left"><p>Connected</p></td>
<td align="left"><p>モニターが接続されているために、ターゲットの出力を有効にすることができます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>アクティブではありません。</p></td>
<td align="left"><p>強制されません。</p></td>
<td align="left"><p>接続されていません</p></td>
<td align="left"><p>モニターが接続されていないと、パスが強制されませんので、ターゲットの出力を有効にすることはできません。</p></td>
</tr>
</tbody>
</table>

 

次の表では、複数の種類の各パスの強制状態について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">強制された状態</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>通常の強制</p></td>
<td align="left"><p>電源遷移、再起動の後にこの状態の強制が失われたか、強制された状態は無効になります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>パス-永続的です</p></td>
<td align="left"><p>この状態の強制は、再起動後に失われます。 Microsoft Win32 <strong>ChangeDisplaySettingsEx</strong>関数はパスに永続化されたすべてのモニターを常に破棄のパスでこれらのモニターの対象となっている場合でも、 <strong>ChangeDisplaySettingsEx</strong>呼び出します。 呼び出し元が呼び出す場合、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff569533" data-raw-source="[&lt;strong&gt;SetDisplayConfig&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff569533)"> <strong>SetDisplayConfig</strong> </a> CCD 関数で設定 SDC_USE_SUPPLIED_DISPLAY_CONFIG または SDC_TOPOLOGY_SUPPLIED フラグを使用して、<em>フラグ</em>パラメーター、 <strong>SetDisplayConfig</strong>新しいトポロジには、モニターされているパスが含まれていない場合は、パスに永続化されたモニターを削除します。 呼び出し元を指定するフラグを他のすべての SDC_TOPOLOGY_XXX の<em>フラグ</em>パラメーター、 <strong>SetDisplayConfig</strong>呼び出し元は、SDC_PATH_PERSIST_ も指定されていない限り、パスに永続化されたモニターを削除しますIF_REQUIRED フラグと、パスは新しいトポロジでアクティブです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>永続的なブート</p></td>
<td align="left"><p>ときに失わ強制状態これはのみ無効になっています。 この状態は、システムの再起動の間で永続的です。</p></td>
</tr>
</tbody>
</table>

 

 

 





