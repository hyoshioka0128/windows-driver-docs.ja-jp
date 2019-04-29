---
title: ドライバーによって定義される WMI データ項目
description: ドライバーによって定義される WMI データ項目
ms.assetid: 97b64571-95ff-4d61-9fa0-5690e9f29345
keywords:
- データ型の WDK WMI
- 埋め込みクラス WDK WMI
- WDK の WMI にデータ アイテムします。
- WMI の WDK カーネルでは、ドライバーの定義済みのデータ項目
- ドライバーの定義済みのデータ項目を WDK WMI
- WDK の WMI クラス
- WMI の WDK カーネルでは、クラス
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4f60b9b54329682edccfbc81fea01b995d3fa48
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387173"
---
# <a name="driver-defined-wmi-data-items"></a>ドライバーによって定義される WMI データ項目





WMI データまたはイベントのブロックのクラス定義内のデータ項目には、次のいずれかを指定できます。

-   文字列を符号なし整数などの基本的なデータ型。

-   埋め込みクラス。 埋め込みクラスは、別のクラス定義内のデータ項目としてのみ使用され、ブロックまたはブロックのイベント データとしては公開されません。

-   基本的なデータ型または埋め込みクラスの固定長または可変長の配列。

Wmi データ ブロックを送信するときに、ドライバーは 8 バイト境界でブロックの先頭に従う必要があります。 ブロック内のすべての後続のデータ項目は、データ型の対応する配置に合わせて調整する必要があります。 A**ブール**または**uint8**を 1 バイト境界に合わせて調整する必要があります。 A **sint16**、 **uint16**、または**文字列**項目は、2 バイト境界、という具合に合わせて調整する必要があります。 配列は、配列の基本型に基づいて配置する必要があります。 バイトの配列は、バイト境界に合わせて調整する必要があります、uint64 型の配列は、8 バイト境界、という具合に合わせて調整する必要があります。 埋め込みクラスは、埋め込みのクラス内で最大の要素に定義されている埋め込みのクラスの自然なアラインメントに基づいて配置する必要があります。 たとえば、埋め込みクラスに、 **uint64**クラスは、8 バイト境界に合わせて調整する必要があります。 WMI データ項目の配置と同じ規則に依存して、 **、/zp8 です**Microsoft C コンパイラをオンにします。

必要な項目以外のブロックでデータ項目を定義する必ずしも必要はありませんドライバー ライター **InstanceName**と**Active**します。 たとえば、空のイベント ブロックは、追加のデータのないイベントが発生したことを通知として使用できます。 またはデータ ブロックへの応答でインスタンス名を列挙だけですが、 [ **IRP\_MN\_クエリ\_すべて\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff551650)要求。

次の表では、WMI データまたはイベント ブロックで項目を定義するために使用する MOF データ型を示します。 MOF データの種類の詳細については、Microsoft Windows SDK を参照してください。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>データの種類</th>
<th>データ形式</th>
<th>バイト単位でアラインメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>string</strong></p></td>
<td><p>文字列の長さを指定する (バイト単位)、Unicode 文字列データが続きます USHORT します。 文字列データでは、埋め込み後に終端の 0 を含めることができます必要に応じて。 場合は、文字列の長さは終端の 0 とスペースを含める必要があります。 ドライバーを使用できる、 <strong>MaxLen</strong>文字列の文字の最大長を指定する修飾子。 文字列の最大長を指定するドライバーは、文字列を保持するのに固定サイズのバッファーを使用できます。 文字列がバッファーのサイズよりも厳密に小さい場合、ドライバーはゼロの文字列の残りの部分に埋め込むことができます。</p></td>
<td><p>2</p></td>
</tr>
<tr class="even">
<td><p><strong>boolean</strong></p></td>
<td><p>1 バイト値 0 は FALSE、0 以外の値は TRUE</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p><strong>sint8</strong></p></td>
<td><p>符号付き 8 ビット整数</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p><strong>uint8</strong></p></td>
<td><p>8 ビット符号なし整数</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p><strong>sint16</strong></p></td>
<td><p>符号付き 16 ビット整数</p></td>
<td><p>2</p></td>
</tr>
<tr class="even">
<td><p><strong>uint16</strong></p></td>
<td><p>16 ビット符号なし整数</p></td>
<td><p>2</p></td>
</tr>
<tr class="odd">
<td><p><strong>sint32</strong></p></td>
<td><p>符号付き 32 ビット整数</p></td>
<td><p>4</p></td>
</tr>
<tr class="even">
<td><p><strong>uint32</strong></p></td>
<td><p>32 ビット符号なし整数</p></td>
<td><p>4</p></td>
</tr>
<tr class="odd">
<td><p><strong>sint64</strong></p></td>
<td><p>符号付き 64 ビット整数</p></td>
<td><p>8</p></td>
</tr>
<tr class="even">
<td><p><strong>uint64</strong></p></td>
<td><p>64 ビット符号なし整数</p></td>
<td><p>8</p></td>
</tr>
<tr class="odd">
<td><p><strong>datetime</strong></p></td>
<td><p>絶対日付または時間間隔を指定する固定長 25 文字 Unicode 文字列。 A <strong>datetime</strong>値には、次の形式。</p>
<p><em>yyyymmddhhmmss.mmmmmmsutc</em></p>
<p>それぞれの文字の説明は次のとおりです。</p>
<p><em>yyyy</em>は 4 桁の年</p>
<p><em>mm</em>は 2 桁の月</p>
<p><em>dd</em>は月の 2 桁の日</p>
<p><em>hh</em>は 24 時間制に基づいて時間です</p>
<p><em>mm</em>分は、</p>
<p><em>ss</em>は、秒です</p>
<p><em>mmmmmm</em>はマイクロ秒数です</p>
<p><em>s</em>がプラス記号 (+) またはマイナス記号 (-) を示すかどうか<em>utc</em> 、正または負の値からオフセット時刻を調整しますまたは、コロン (:)、ことを示す、 <strong>datetime</strong>値は、。間隔。</p>
<p><em>utc</em>は Universal Time 調整から分単位のオフセット。 場合<em>utc</em> 0 (000)、 <strong>datetime</strong>値が間隔。</p>
<p>値はゼロで埋めますをする必要があります。 アスタリスク (*) では、重要ではないフィールドを入力することができます。</p></td>
<td><p>2</p></td>
</tr>
</tbody>
</table>

 

 

 




