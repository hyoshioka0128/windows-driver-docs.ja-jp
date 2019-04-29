---
title: USB のデバイス固有のメソッド (_DSM)
description: USB サブシステムのデバイス固有クラスの構成をサポートするためには、Windows は、特定のデバイス メソッド (_DSM) この記事で説明されている関数を持つを定義します。
ms.assetid: 8F0EDE17-9895-4C24-B061-963DA0D7882B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6379d3b85d092e6867fc60436b1a7f5ebd6dc185
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337351"
---
# <a name="usb-device-specific-method-dsm"></a>USB デバイスに固有のメソッド (\_DSM)


Windows を USB サブシステムのデバイス クラス固有の構成をサポートするには、デバイス固有のメソッドを定義します (\_DSM) を持つ、この記事で説明されている関数。

## <a name="function-1-post-reset-processing-for-dual-role-controllers"></a>関数 1:デュアル ロール コント ローラーの処理後のリセット


\_DSM がデュアル ロール USB コント ローラーは、次のように、後のリセット処理関数のメソッド パラメーターを制御します。

### <a name="arguments"></a>引数

-   **Arg0:** UUID ce2ee385-00e6-48cb-9f05-2edb927c4899 を =
-   **Arg1:** リビジョン ID = 0
-   **Arg2:** 関数インデックス = 1
-   **Arg3:** 空のパッケージ (未使用)

### <a name="return"></a>戻り値

None、Windows のインボックス ドライバーは、USB コント ローラーをホスト モードでのみサポートします。 USB ドライバーが呼び出す各コント ローラーをリセットした後、 \_DSM 関数インデックス 1 にホスト モードで動作する USB コント ローラーの構成に必要なコント ローラーに固有の初期化を実行します。

この関数を使用する場合、 \_DSM メソッドは、USB コント ローラー デバイス下に表示する必要があります。

## <a name="function-2-port-type-identification"></a>関数 2:ポートの種類の識別


\_USB ポートの種類を識別するための DSM 制御メソッドのパラメーターは、次のようにします。

### <a name="arguments"></a>引数

-   **Arg0:** UUID ce2ee385-00e6-48cb-9f05-2edb927c4899 を =
-   **Arg1:** リビジョン ID = 0
-   **Arg2:** 関数インデックス = 2
-   **Arg3:** 空のパッケージ (未使用)

### <a name="return"></a>戻り値

次の値のいずれかを表す整数。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>要素</th>
<th>オブジェクトの種類</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>[ポートの種類]</td>
<td>整数 (バイト)</td>
<td><p>USB ポートの種類を指定します。</p>
<ul>
<li>0x00 – 正規 USB</li>
<li>0X01-HSIC</li>
<li>0X02-SSIC</li>
<li>0x03 – 0 xff に予約されています</li>
</ul></td>
</tr>
</tbody>
</table>

 

この関数を使用する場合、 \_DSM メソッドは、USB ポートのデバイスの 表示する必要があります。

**注**  関数インデックス 0 の各\_DSM がサポートされている関数のインデックスのセットを返しますは常に必要とするクエリ関数を示します。 詳細については、セクション 9.14.1 を参照してください。"\_DSM (デバイスの特定のメソッド)"で、 [ACPI 5.0 仕様](https://www.uefi.org/specifications)します。

 

 

 




