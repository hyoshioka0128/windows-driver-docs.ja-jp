---
title: WMI クラス修飾子
description: WMI クラス修飾子
ms.assetid: 62a00184-59b7-496d-b523-f4adb879d402
keywords:
- WDK の WMI クラスの修飾子
- MOF クラスの修飾子 WDK WMI
- 埋め込みクラス WDK WMI
- 動的 MOF 修飾子 WDK WMI
- 静的な MOF 修飾子 WDK WMI
- WDK の WMI クラス
- WMI の WDK カーネルでは、クラス
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9ec82b101a42259efd2e2b5e0bef200c5e68a2d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386387"
---
# <a name="wmi-class-qualifiers"></a>WMI クラス修飾子





次の表は、必須および省略可能な MOF クラス修飾子がドライバーの WMI データのブロックとイベント ブロックを記述するために使用できます。

*クラスの埋め込み*、これは、別のクラス内のデータ項目としてのみ使用し、WMI データ ブロックとして公開されているクラスだけが必要です、 **WMI**と**Guid**修飾子。 その他の修飾子は埋め込みクラスには関係ないため、無視されます。 埋め込まれたクラスの詳細については、次を参照してください。 [WMI データ項目のドライバー定義](driver-defined-wmi-data-items.md)します。

**動的**と**静的**は標準の MOF 修飾子。 その他の標準的な MOF 修飾子については、Microsoft Windows SDK を参照してください。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>修飾子</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>動的</strong></p></td>
<td><p>データ プロバイダーが MOF ファイル内の静的データのインスタンスを提供するのではなく、実行時に、データ ブロックのインスタンスを提供することを示します。 ドライバーは、WMI で登録されるすべてのデータおよびイベント ブロックを定義する必要があります、<strong>動的</strong>修飾子。</p></td>
</tr>
<tr class="even">
<td><p><strong>静的</strong></p></td>
<td><p>データ プロバイダーが実行時に、データ ブロックのインスタンスを提供するのではなく、MOF ファイルの静的データのインスタンスを提供することを示します。 静的なデータが WMI データベースに存在するため、ドライバーは WMI を使って、静的データ ブロックを登録できません。 マークされたクラス<strong>静的</strong>、MOF でファイルが登録されていないドライバーの<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo" data-raw-source="[&lt;strong&gt;IRP_MN_REGINFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo)"> <strong>IRP_MN_REGINFO</strong> </a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo-ex" data-raw-source="[&lt;strong&gt;IRP_MN_REGINFO_EX&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo-ex)"> <strong>IRP_MN_REGINFO_EX</strong> </a>ハンドラー。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Provider("WMIProv")</strong></p></td>
<td><p>(必須)クラスのプロバイダーが WMI プロバイダーであることを示します。</p></td>
</tr>
<tr class="even">
<td><p><strong>WMI</strong></p></td>
<td><p>(必須)クラスが WMI クラスであることを示します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>説明 ("</strong><em>説明文字列</em><strong>")</strong></p></td>
<td><p>(省略可能)ブロックで指定されたロケールの説明を指定します、<strong>ロケール</strong>修飾子。 で定義されている場合、WMI クライアントは、ユーザーに説明文字列を表示できます。 ドライバーのライターを使用できます<strong>説明</strong>クラスを文書化します。</p></td>
</tr>
<tr class="even">
<td><p><strong>Guid ("</strong><em>guid 文字列</em><strong>")</strong></p></td>
<td><p>(必須)WMI にブロックを一意に識別する文字列の形式で、GUID を指定します。 ドライバー開発者が各データ ブロックの GUID を内で生成、ドライバーの MOF ファイルでは、guidgen.exe または uuidgen.exe (これは、Windows sdk に含まれる) を使用しています。 ドライバーは、ドライバーのブロックを登録するときにこの値を GUID 形式で、WMI に渡します。 WMI は、この GUID を使用して、ドライバーの MOF リソースのブロックの定義を検索します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Locale("MS&lt;/strong&gt;<em>locale-identifier</em><strong>")</strong></p></td>
<td><p>(省略可能)指定された文字列のロケールと言語識別子を指定します<strong>説明</strong>します。 たとえば、<em>ロケール識別子</em>0x409 の米国英語を指定します。 1 つの MOF ファイルが別のロケールでのブロックを含めることができますが、通常、MOF ファイル内のブロックのすべて同じロケールであります。</p></td>
</tr>
<tr class="even">
<td><p><strong>WmiExpense(</strong><em>expense-value</em><strong>)</strong></p></td>
<td><p>(省略可能)データ ブロックのデータを収集するために必要な CPU サイクルの平均数を指定します。 たとえば、WMI クライアントはデータ ブロックの可能性がありますチェック<strong>WmiExpense</strong>そのデータを照会する頻度を決定する値。 場合<strong>WmiExpense</strong>を省略すると、<em>経費値</em>0 と見なされます。 <strong>WmiExpense</strong>として収集する負荷の高いデータ ブロックを登録するとは関係ありません。</p></td>
</tr>
</tbody>
</table>

 

 

 




