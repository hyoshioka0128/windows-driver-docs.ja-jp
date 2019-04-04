---
title: OidProcessing ルール セット (NDIS)
description: ドライバーが正しく OID 要求を処理することを確認するのにには、これらの規則を使用します。
ms.assetid: 0E12778B-BB86-4387-9B8A-19E3876D6F8C
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: e762c59c2d2dd2c5ad79108c028be473d3167e0f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559733"
---
# <a name="oidprocessing-rule-set-ndis"></a>OidProcessing ルール セット (NDIS)


ドライバーが正しく OID 要求を処理することを確認するのにには、これらの規則を使用します。

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="ndis-doublecomplete.md" data-raw-source="[&lt;strong&gt;DoubleComplete&lt;/strong&gt;](ndis-doublecomplete.md)"><strong>DoubleComplete</strong></a></p></td>
<td align="left"><p><a href="ndis-doublecomplete.md" data-raw-source="[DoubleComplete](ndis-doublecomplete.md)">DoubleComplete</a>ルールでは、NDIS ドライバーする必要があります完了しないこと、オブジェクト識別子 (OID) 要求を複数回を指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-doublecompleteworkitem.md" data-raw-source="[&lt;strong&gt;DoubleCompleteWorkItem&lt;/strong&gt;](ndis-doublecompleteworkitem.md)"><strong>DoubleCompleteWorkItem</strong></a></p></td>
<td align="left"><p>DoubleCompleteWorkItem ルールでは、NDIS ドライバーする必要がありますいない OID 要求を複数回ときに完了する作業項目の完了が遅延を指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndismnetpnpeventinoidrequest.md" data-raw-source="[&lt;strong&gt;NdisMNetPnPEventInOIDRequest&lt;/strong&gt;](ndis-ndismnetpnpeventinoidrequest.md)"><strong>NdisMNetPnPEventInOIDRequest</strong></a></p></td>
<td align="left"><p>このルールは、ことを確認<a href="https://msdn.microsoft.com/library/windows/hardware/ff563616" data-raw-source="[&lt;strong&gt;NdisMNetPnPEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563616)"> <strong>NdisMNetPnPEvent</strong> </a> OID 要求のコンテキストでは呼び出されません。</p></td>
</tr>
</tbody>
</table>

 

**OidProcessing ルールを選択するには、次のように設定します。**

1.  Microsoft Visual Studio で、ドライバーのプロジェクト (.vcxProj) を選択します。 **ドライバー**  メニューのをクリックして**Static Driver Verifier を起動しています**.

2.  をクリックして、**ルール**タブ。**規則セット**、 **OidProcessing**します。

    Visual Studio の開発者コマンド プロンプト ウィンドウから既定のルールを選択するには、次のように指定します。 **OidProcessing.sdv**で、 **/check**オプション。 次に、例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:OidProcessing.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、[ドライバーで障害を検出する Static Driver Verifier を使用して](https://msdn.microsoft.com/library/windows/hardware/hh454281)と[Static Driver Verifier のコマンド (MSBuild)](https://msdn.microsoft.com/library/windows/hardware/hh466459)を参照してください。

 

 





