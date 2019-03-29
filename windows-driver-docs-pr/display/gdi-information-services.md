---
title: GDI 情報サービス
description: GDI 情報サービス
ms.assetid: f3575d68-1d90-4ccd-adb1-5d2a26099397
keywords:
- GDI WDK Windows 2000 の表示、情報サービス
- グラフィックス ドライバー WDK Windows 2000 の表示、情報サービス
- 描画 WDK GDI や情報サービス
- WDK GDI をタイムスタンプします。
- WDK GDI のカウンター
- パフォーマンス カウンターの WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7e54bfa34ec8013547431b81fb2851e99fcd7af
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579788"
---
# <a name="gdi-information-services"></a>GDI 情報サービス


## <span id="ddk_gdi_information_services_gg"></span><span id="DDK_GDI_INFORMATION_SERVICES_GG"></span>


GDI は、ドライバーを使用してデバイスおよびシステム属性、ファイルのタイムスタンプ、およびパフォーマンス カウンターに関するシステム クエリを実行するいくつかのサービスを提供します。 これらのサービスは、次の表に表示されます。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564986" data-raw-source="[&lt;strong&gt;EngQueryDeviceAttribute&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564986)"><strong>EngQueryDeviceAttribute</strong></a></p></td>
<td align="left"><p>デバイスの特定の属性について、システムを照会するドライバーをできます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564988" data-raw-source="[&lt;strong&gt;EngQueryFileTimeStamp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564988)"><strong>EngQueryFileTimeStamp</strong></a></p></td>
<td align="left"><p>ファイルのタイムスタンプを返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564990" data-raw-source="[&lt;strong&gt;EngQueryLocalTime&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564990)"><strong>EngQueryLocalTime</strong></a></p></td>
<td align="left"><p>ローカル時刻をクエリします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564994" data-raw-source="[&lt;strong&gt;EngQueryPerformanceCounter&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564994)"><strong>EngQueryPerformanceCounter</strong></a></p></td>
<td align="left"><p>パフォーマンス カウンターを照会します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564996" data-raw-source="[&lt;strong&gt;EngQueryPerformanceFrequency&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564996)"><strong>EngQueryPerformanceFrequency</strong></a></p></td>
<td align="left"><p>パフォーマンス カウンターの頻度を照会します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564997" data-raw-source="[&lt;strong&gt;EngQuerySystemAttribute&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564997)"><strong>EngQuerySystemAttribute</strong></a></p></td>
<td align="left"><p>クエリ プロセッサまたはシステム固有の機能です。</p></td>
</tr>
</tbody>
</table>

 

 

 





