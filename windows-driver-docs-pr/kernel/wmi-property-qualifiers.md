---
title: WMI プロパティ修飾子
description: WMI プロパティ修飾子
ms.assetid: e2d281b3-913c-43ad-921c-80dc8be09aa0
keywords:
- MOF プロパティ修飾子 WDK WMI
- プロパティ修飾子 WDK WMI
- WDK の WMI の修飾子
- 標準の MOF 修飾子 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b4d168ae82784490422b5da3199ebdbb1e75793
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549484"
---
# <a name="wmi-property-qualifiers"></a>WMI プロパティ修飾子





次の表は、必須および省略可能な MOF プロパティ修飾子が WMI データまたはイベント ブロックで項目を定義するために使用できます。

標準の MOF 修飾子を次に示します:**キー**、**読み取り**、**書き込み**、 **ValueMap**、および**値**. これらおよびその他の標準的な MOF 修飾子の詳細については、次を参照してください。 [MOF データ型](https://msdn.microsoft.com/library/aa392392)します。

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
<td><p><strong>key</strong></p></td>
<td><p>データ項目が、クラスの各インスタンスを一意に識別するキー プロパティであることを示します。 InstanceName プロパティのみには、キーを宣言できます。</p></td>
</tr>
<tr class="even">
<td><p><strong>read</strong></p></td>
<td><p>WMI クライアントがデータ項目を読み取ることを示します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>書き込み</strong></p></td>
<td><p>WMI クライアントがデータ項目を設定できることを示します。</p></td>
</tr>
<tr class="even">
<td><p><strong>ビットマップ</strong></p></td>
<td><p>指定されている対応する文字列値のビット位置を指定します<strong>BitValues</strong>します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>BitValues</strong></p></td>
<td><p>データ項目で設定されたビットを表す文字列値 (フラグの名前) の一覧を指定します。 指定された対応する位置で、フラグのビット位置が定義されている<strong>ビットマップ</strong>します。</p></td>
</tr>
<tr class="even">
<td><p><strong>DefineValues</strong></p></td>
<td><p>WMI ツールのスイートに対応する一連のコンパイルを列挙した一覧を指定します #define ステートメント。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DisplayInHex</strong></p></td>
<td><p>プロパティの値を表示する任意の WMI クライアントが 16 進数でこれにを指定します。</p></td>
</tr>
<tr class="even">
<td><p><strong>DisplayName(&quot;</strong><em>string</em><strong>&quot;)</strong></p></td>
<td><p>プロパティ名として表示する WMI クライアントが使用できるキャプションを指定します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxLen(</strong><em>uint</em><strong>)</strong></p></td>
<td><p>文字列プロパティに<strong>MaxLen</strong>文字で、文字列の最大長を指定します。 <em>Uint</em>値は 32 ビット符号なし整数を指定できます。 MaxLen を省略した場合または<em>uint</em>が 0 の場合、文字列の長さは制限されています。</p></td>
</tr>
<tr class="even">
<td><p><strong>値</strong></p></td>
<td><p>このデータ項目に指定できる値の一覧を指定します。 データ項目が列挙体は場合、 <strong>ValueMap</strong>で指定された列挙値に対応するインデックス値を含む<strong>値</strong>します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ValueMap</strong></p></td>
<td><p>内の対応する文字列値の整数値を指定します<strong>値</strong>します。</p></td>
</tr>
<tr class="even">
<td><p><strong>WmiDataId(</strong><em>data-item-ID</em><strong>)</strong></p></td>
<td><p>(必須)データ ブロック内のデータ項目を識別します。 データ項目の Id は、必要な項目を除くブロック内のすべての項目に割り当てる必要があります<strong>InstanceName</strong>と<strong>Active</strong>します。 データ項目の Id は、1 から始まる連続した一連の割り当てる必要があります。 項目&#39;データ ID は、データ ブロックのインスタンスで、項目が表示される順序を決定しますMOF クラスの定義内の項目の順序は関係ありません。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WmiMethodId(</strong><em>method-item-ID</em><strong>)</strong></p></td>
<td><p>データ ブロック内でメソッドを識別します。</p></td>
</tr>
<tr class="even">
<td><p><strong>WmiSizeIs(&quot;</strong><em>data-item-name</em><strong>&quot;)</strong></p></td>
<td><p>このデータ項目に可変長配列の要素の数を示すこのブロックでは、別のデータ項目の名前を指定します。 <strong>WmiSizeIs</strong>配列を定義するデータ項目に対してのみ有効です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WmiScale(</strong><em>scale-factor</em><strong>)</strong></p></td>
<td><p>このデータ項目の値を返すときに、ドライバーが使用するには、10 の累乗としてスケール係数を指定します。 たとえば場合、<em>スケール ファクター</em>が 5 の場合、ドライバーによって返される値が 10⁵ 乗算されます。 場合<strong>WmiScale</strong>を省略すると、<em>スケール ファクター</em> 0 と見なさことができます。</p></td>
</tr>
<tr class="even">
<td><p><strong>WmiTimeStamp</strong></p></td>
<td><p>64 ビットのデータ項目にある 1/1/1601 以降を 100 ナノ秒単位のタイムスタンプを指定します。 <strong>WmiTimeStamp</strong>は 64 ビットのデータ項目でのみ有効です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WmiComplexity(</strong><em>level</em><strong>)</strong></p></td>
<td><p>データ項目のユーザーの複雑さのレベルを表す整数値を指定します。 WMI クライアントでは、初心者のユーザーが使用できる必要のあるデータ項目とより高度なユーザーに制限する必要がありますデータ項目を区別する、その値を使用できます。 最小の値は 0 ですし、ユーザーの複雑さの増加を示す値を大きくします。 <strong>WmiComplexity</strong> 0 を指定しない場合の既定値します。</p></td>
</tr>
<tr class="even">
<td><p><strong>WmiVolatility(</strong><em>interval</em><strong>)</strong></p></td>
<td><p>このデータ項目の更新プログラムの間のミリ秒、間隔を指定します。 たとえば、データ項目が 1 回更新された場合の各秒、<em>間隔</em>1000 になります。 WMI クライアント チェック<strong>WmiVolatility</strong>可能性のある新しい値に対してクエリを実行するには、多くの場合、方法を決定します。 場合<strong>WmiVolatility</strong>を省略すると、<em>間隔</em>が定義されていません。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WmiEventTrigger(</strong> <strong>&quot;</strong> <em>data-item-name</em><strong>&quot;)</strong></p></td>
<td><p>イベントのトリガーの値を定義する WMI クライアントが設定できる、イベント ブロックでは、データ項目の名前を指定します。 TooHot イベントで修飾する場合など、 <strong>WmiEventTrigger</strong>(&quot;TooHotTemperature&quot;)、WMI クライアントは TooHot イベントを送信するドライバーに指示する TooHotTemperature 設定でしたとデバイスTooHotTemperature のユーザーが指定した値に達しました。 通常、ドライバーは、トリガーの値を定義します。 公開することで、 <strong>WmiEventTrigger</strong>データ項目では、ドライバーにより、クライアントは、特定のイベントを発生するタイミングを制御します。</p></td>
</tr>
<tr class="even">
<td><p><strong>WmiEventRate(&quot;</strong><em>data-item-name</em><strong>&quot;)</strong></p></td>
<td><p>WMI クライアントがこのイベントを送信する頻度を制御する設定できる、イベント ブロックでは、データ項目の名前を指定します。 場合は、データ項目 TooHot はで修飾、たとえば、 <strong>WmiEventRate (&quot;</strong>SendEventRate<strong>&quot;)</strong>、WMI クライアントのユーザーがドライバーに送信するように指示する SendEventRate を設定できますユーザーが指定した間隔で TooHot します。</p></td>
</tr>
</tbody>
</table>

 

 

 




