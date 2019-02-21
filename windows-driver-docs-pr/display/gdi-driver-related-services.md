---
title: GDI ドライバー関連のサービス
description: GDI ドライバー関連のサービス
ms.assetid: bb46ae7a-9ade-4e23-b9fe-489f83445ff3
keywords:
- GDI WDK Windows 2000 のディスプレイ ドライバー関連のサービス
- グラフィックス ドライバー WDK Windows 2000 の表示、ドライバーに関連するサービス
- 描画 WDK GDI やドライバー関連のサービス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ec6d3db4a151525592548529e32c4f365fe71bc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556439"
---
# <a name="gdi-driver-related-services"></a>GDI ドライバー関連のサービス


## <span id="ddk_gdi_driver_related_services_gg"></span><span id="DDK_GDI_DRIVER_RELATED_SERVICES_GG"></span>


ドライバーの作成者は、次の表に示す GDI ドライバーに関連するサービスを使用して、作成またはドライバー オブジェクトの削除、ドライバーの DLL の名前を取得し、ロックまたはドライバー オブジェクトのロックを解除できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564207" data-raw-source="[&lt;strong&gt;EngCreateDriverObj&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564207)"><strong>EngCreateDriverObj</strong></a></p></td>
<td align="left"><p>作成、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff556162" data-raw-source="[&lt;strong&gt;DRIVEROBJ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556162)"> <strong>DRIVEROBJ</strong> </a>構造体。 この構造体は、デバイス管理のリソースをクリーンアップすることがなく、リソース割り当てプロセスが終了した場合にリリースする必要がありますを追跡するために使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564792" data-raw-source="[&lt;strong&gt;EngDeleteDriverObj&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564792)"><strong>EngDeleteDriverObj</strong></a></p></td>
<td align="left"><p>デバイス管理のリソースを追跡するために使用されるハンドルを解放します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564927" data-raw-source="[&lt;strong&gt;EngGetDriverName&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564927)"><strong>EngGetDriverName</strong></a></p></td>
<td align="left"><p>ドライバーの名前を返します&#39;s DLL。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564967" data-raw-source="[&lt;strong&gt;EngLockDriverObj&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564967)"><strong>EngLockDriverObj</strong></a></p></td>
<td align="left"><p>呼び出し元のスレッドのドライバー オブジェクトに排他ロックを作成します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565044" data-raw-source="[&lt;strong&gt;EngUnlockDriverObj&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565044)"><strong>EngUnlockDriverObj</strong></a></p></td>
<td align="left"><p>ドライバー オブジェクトのロックを解除します。</p></td>
</tr>
</tbody>
</table>

 

 

 





