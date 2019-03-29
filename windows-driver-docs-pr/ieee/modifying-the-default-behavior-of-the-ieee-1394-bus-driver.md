---
title: IEEE 1394 バス ドライバーの既定の動作の変更
description: Windows 7 には、1394ohci.sys、カーネル モード ドライバー フレームワーク (KMDF) を使用して実装されている新しい IEEE 1394 バス ドライバーが含まれています。
ms.assetid: B636943E-EE52-4D0D-A638-89C05AD41F1A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 305c180c8c9930b43a420d72395a4bdc2ffc9bf0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572296"
---
# <a name="modifying-the-default-behavior-of-the-ieee-1394-bus-driver"></a>IEEE 1394 バス ドライバーの既定の動作の変更


Windows 7 には、1394ohci.sys、カーネル モード ドライバー フレームワーク (KMDF) を使用して実装されている新しい IEEE 1394 バス ドライバーが含まれています。 1394ohci.sys バス ドライバーでは、従来の IEEE バス ドライバー ポート/ミニポート構成--1394bus.sys と ochi1394.sys に置き換えられます。

状況によっては、1394ohci.sys の既定の動作をオーバーライドする可能性があります。 サポートされている特定のレジストリ値を設定して、これを行うことができます。

## <a name="registry-value-locations"></a>レジストリ値の場所


設定できます 1394 関連のレジストリ値 1394 のすべてのコント ローラーに対してグローバルに、システムまたは個別に各 1394 コント ローラー。 1394ohci.sys、バス ドライバーでは、まずグローバル 1394 レジストリ値を照会し、1394 のコント ローラーの個々 のレジストリ値を照会します。

次のレジストリの場所には、グローバル 1394 レジストリ値が含まれています。

`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\1394ohci \Parameters`

次のレジストリの場所には、1394 コント ローラーの個々 のレジストリ値が含まれています。

`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class \{6BDD1FC1-810F-11D0-BEC7-08002BE2092F}\<NNNN>`

`<NNNN>` 1394 の各コント ローラーのインスタンスの id 番号を表します。

## <a name="registry-values"></a>レジストリ値


次の表では、新しい 1394 バス ドライバーがサポートするレジストリ値について説明します。 グローバルまたは特定の 1394 コント ローラーは、すべてのレジストリ値を指定できます。 特定の 1394 コント ローラーが指定されているすべてのレジストリ値は、対応するグローバルに指定されたレジストリ値をオーバーライドします。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>名前</th>
<th>型</th>
<th>値</th>
<th>既定</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>DisableGenerationCountCompare</td>
<td>DWORD</td>
<td>0 または 1</td>
<td>0</td>
<td>1394ohci.sys バス ドライバーの世代数の値を比較し、 <strong>self_id</strong>を非同期で受信した生成数の値がある 1394 コント ローラーの登録が処理するとき、DMA 要求コンテキスト バッファーを受信非同期要求を受信します。 この値を 0 に設定すると、生成数の比較が有効になります。 この値を 1 に設定すると、生成数の比較が無効にします。</td>
</tr>
<tr class="even">
<td>UseQuadletReadsForEnumeration</td>
<td>DWORD</td>
<td>0 または 1</td>
<td>0</td>
<td>ROM. 構成の内容を取得するための既定の方法により、この値を 0 に設定します。 この値を 1 に設定すると、ROM. 構成の内容を取得する非同期作成されます読み取りトランザクションを使用する新しい 1394 バス ドライバー</td>
</tr>
<tr class="odd">
<td>EnumerateIP1394</td>
<td>DWORD</td>
<td>0 または 1</td>
<td>0</td>
<td>この値を 0 に設定すると、1394 bus IP1394 のデバイスの列挙型が無効にします。 1394 bus IP1394 のデバイスの列挙を有効にこの値を 1 に設定します。</td>
</tr>
<tr class="even">
<td>EnableGapCountOptimization</td>
<td>DWORD</td>
<td>0 または 1</td>
<td>1394 a のトポロジのみの最適化します。</td>
<td>この値を 0 に設定すると、ギャップのカウントの最適化が無効にします。 間隔カウントの最適化を有効にこの値を 1 に設定します。
<div class="alert">
<strong>注</strong>  間隔カウントの最適化を有効にする 1394 b を含むすべての 1394 bus トポロジのギャップのカウントが向上します。 使用される間隔の数の値は、IEEE 1394 a 仕様で指定されている、テーブル メソッドに基づきます。 エンドユーザーが使用されるギャップ数が、1394 bus トポロジに対して有効であることを確認してください。
</div>
<div>
 
</div></td>
</tr>
<tr class="odd">
<td>EnablePersistentCycleStarts</td>
<td>DWORD</td>
<td>0 または 1</td>
<td>0</td>
<td>1394 バス アイソクロナス対応のノードが見つからない場合は、この値を 0 無効にします。 サイクルの開始パケットを設定します。 この値は、1394 バス上アイソクロナス対応のノードにあるかどうかに関係なく有効サイクル スタート パケットを 1 に設定します。
<div class="alert">
<strong>注</strong>  1394ohci.sys バス ドライバーを無効にし、ローカル ノードがバス manager 場合にのみ開始パケットのサイクルを有効にします。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[IEEE 1394 ドライバー スタック](https://msdn.microsoft.com/library/windows/hardware/ff538867)  
[Windows 7 での IEEE 1394 バス ドライバー](https://msdn.microsoft.com/library/windows/hardware/gg266402)  



