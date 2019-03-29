---
title: MB インターフェイス モデルの補足
description: このセクションでは、MB インターフェイス モデル (MBIM) 用の補足情報を提供します。
ms.assetid: 577BCF39-868B-44F5-A5C0-75E28689C2B6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cdbc2f5019b71faefb9b29343e41bb00ac7eaeac
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464088"
---
# <a name="mb-interface-model-supplement"></a>MB インターフェイス モデルに関する補足条項


Microsoft OS ディスクリプターは、次のセグメントに分割されます。

-   1 つの Microsoft OS 文字列記述子
-   1 つまたは複数の Microsoft OS 機能ディスクリプター

OS の記述子をサポートするために、デバイスは、文字列記述子を実装する必要があります。
**文字列記述子**

Microsoft OS 文字列記述子は、文字列インデックス 0 xee に格納されている文字列です。 この文字列の形式が定義されています。

Microsoft OS の文字列記述子は、次の目標を達成するために使用します。

-   Microsoft OS 文字列記述子のプレゼンスはオペレーティング システムにデバイスが Microsoft OS 機能記述子の形式で、そこに埋め込まれた情報を持っていることを示します。
-   Microsoft OS 文字列記述子では、文字列インデックス 0 xee 位置にあるデバイス上に存在する可能性があるランダムな文字列を区別するために使用される埋め込み署名フィールドがあります。
-   Microsoft OS 文字列記述子では、Microsoft OS ディスクリプターの将来のリビジョンの埋め込みのバージョン番号もあります。

1 つだけの Microsoft OS 文字列記述子は、デバイスに格納されます。 次のセクションでは、Microsoft OS 文字列記述子と取得の手順の構造について説明します。
**OS の文字列の構造**

文字列記述子の構造を次に示します。

*文字列記述子構造体*

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">フィールド</th>
<th align="left">長さ (バイト)</th>
<th align="left">[値]</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>bLength</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x12</p></td>
<td align="left"><p>記述子の長さ</p></td>
</tr>
<tr class="even">
<td align="left"><p>bDescriptorType</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x03</p></td>
<td align="left"><p>文字列記述子</p></td>
</tr>
<tr class="odd">
<td align="left"><p>qwSignature</p></td>
<td align="left"><p>14</p></td>
<td align="left"><p>"MSFT100"</p></td>
<td align="left"><p>署名フィールド (値で 00530046005400310030003000)</p></td>
</tr>
<tr class="even">
<td align="left"><p>bMS_VendorCode</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>仕入先のコード</p></td>
<td align="left"><p>その他の OS をフェッチするベンダー コード記述子を機能します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>bPad</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x00</p></td>
<td align="left"><p>パッドのフィールド</p></td>
</tr>
</tbody>
</table>

 

Microsoft OS 文字列記述子の構造は、1.00 のバージョンは固定され、18 バイトの全体的な長さ。 Microsoft OS 文字列記述子のバージョン番号が記載されて、 **qwSignature**フィールド。 格納されている情報、 **bMS\_VendorCode**フィールドが 1 バイトの値を指定する必要があります。 Microsoft OS 機能の記述子を取得するために使用され、このバイト値がで使用される、 **bmRequestType**次のように記述されるフィールド。

**OS の文字列記述子を取得します。**

標準の取得、文字列に格納されている情報を取得する\_記述子の要求は、デバイスに発行する必要があります。 要求の形式を次に示します。

*標準的な Get\_記述子文字列の要求*

<table style="width:100%;">
<colgroup>
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">bmRequestType</th>
<th align="left">bRequest</th>
<th align="left">wValue</th>
<th align="left">wIndex</th>
<th align="left">wLength</th>
<th align="left">データ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1000 0000b</p></td>
<td align="left"><p>GET_DESCRIPTOR</p></td>
<td align="left"><p>0x03EE</p></td>
<td align="left"><p>0x0000</p></td>
<td align="left"><p>0x12</p></td>
<td align="left"><p>文字列を返します</p></td>
</tr>
</tbody>
</table>

 

**BmRequestType**フィールドが 3 つの部分で構成されるビットマップでは、データ転送、記述子の型、および受信者の方向。 値は、USB 仕様に従って**bmRequestType** 1000 0000b (0x80) に設定されます。

GET の\_記述子の要求、 **wValue**フィールドは、2 つの部分に分割されます。 上位バイトの記述子の種類を格納して、下位バイトの記述子のインデックスを格納します。 文字列記述子を取得する Microsoft OS 文字列記述子を取得するには、上位バイトを設定する必要があります: 0x03 します。 下位バイトに、この文字列のインデックスを保存するか、Microsoft OS 文字列記述子は、常に 0 xee のインデックス位置にある格納、ため、 **wValue**フィールド。

**WIndex**言語 ID を格納するために使用が Microsoft OS 文字列記述子の場合は 0 に設定する必要があります。

**WLength**フィールドを取得する文字列記述子の長さを示すために使用します。 デバイスは、0x02 – 0 xff から任意の有効な範囲に応答する必要があります。

デバイスには、対応するアドレス (0 xee) で有効な記述子がない場合、要求エラーまたは停止に応答します。 失速でデバイスが応答しないときに単一終了 0 個のリセットに発行されます (場合に回復するには、不明な状態に移動する必要がありますが) デバイス。

**OS の記述子の整合性を検証します。**

任意の文字列 ID を使用して、情報を格納するには、ベンダーが許可されている、ため、インデックス 0 xee に格納された文字列は、Microsoft OS 文字列記述子では実際のオペレーティング システムする必要がありますを確認します。 これを確認するには、次のテストを実施するは。 いずれかのエラーは、Microsoft OS 機能の記述子の取得が禁止されます。

-   仕入先は、インデックス位置 0 xee で文字列を保存する場合、オペレーティング システムは文字列を取得し、クエリを実行するかどうかは、Microsoft OS 文字列を参照してください。 これは、前に指定した署名フィールドのエントリを文字列の署名フィールドを比較することで確認できます。 さらに、文字列の解析に不一致ができなくなります。
-   2 番目のテスト署名フィールドで指定されたバージョン番号に基づく文字列の長さの検証が含まれます。 (文字列"MSFT100") で指定されたバージョン番号は、1.00 です。 これは、18 バイト文字列記述子に対応します。

**Microsoft OS 文字列記述子の制約**

Microsoft OS 文字列記述子と、検索に、次の制約が適用されます。

-   Microsoft OS ディスクリプター仕様、デバイスに準拠している情報を格納する必要がありますいずれかであるし、Microsoft OS のみの文字列に記載されている情報に準拠している記述子[Microsoft OS ディスクリプター](https://go.microsoft.com/fwlink/p/?linkid=308932)します。
-   デバイスの製造元は自由に任意の値を使用して、 **bMS\_VendorCode** Microsoft OS 文字列記述子フィールド

**機能の記述子**

機能の記述子は、特定の目的で定義されている固定形式の記述子です。

**OS の機能記述子を取得します。**

特別な GET Microsoft OS 機能記述子を取得する\_MS\_記述子の要求は、デバイスに発行される必要があります。 要求の形式を次に示します。

*標準のデバイス要求の形式*

<table style="width:100%;">
<colgroup>
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">bmRequestType</th>
<th align="left">bRequest</th>
<th align="left">wValue</th>
<th align="left">wIndex</th>
<th align="left">wLength</th>
<th align="left">データ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1100 0000b</p></td>
<td align="left"><p>GET_MS_DESCRIPTOR</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>インデックスの機能</p></td>
<td align="left"><p>長さ</p></td>
<td align="left"><p>記述子を返します</p></td>
</tr>
</tbody>
</table>

 

**BmRequestType**フィールドは 3 つの部分で構成されるビットマップ — データ転送、記述子の型、および受信者の方向-USB 仕様に従って、します。 Microsoft OS 機能の記述子は、ベンダー固有記述子とデータ転送の方向は、デバイスからホストにします。 値ではそのため、 **bmRequestType** 1100 0000b (0xC0) に設定されます。

**BRequest**フィールドは、要求の形式を示すために使用します。 Microsoft OS 機能の記述子を取得する、 **bRequest**特別な GET のフィールドを代入する\_MS\_記述子バイト。 このバイトの値が付いて、 **bMS\_VendorCode**Microsoft の文字列記述子から取得します。 Microsoft OS 文字列記述子の基準取得に関する詳細については、次を参照してください。 **OS 文字列記述子を取得する**します。

**WValue**フィールドは、特別な用途し、は、上位バイトと下位バイトに分割されます。 高位のバイトを使用して、インターフェイスの数を格納します。 これは複合デバイスは、特に用のインターフェイスごとに機能の記述子を格納するために不可欠なまたはデバイスを[複数のインターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff537102)します。 ほとんどの場合、0 のインターフェイスが使用されます。 下位バイトを使用して、ページ番号を格納します。 この機能は 64 KB のサイズの境界の記述子を防止 (のサイズによって設定された制限、 **wLength**フィールド)。 記述子は、ページの値を 0 に初期設定がフェッチされます。 完全な記述子の場合 (サイズは 64 KB) が受信されると、ページの値は 1 つずつ増えます、記述子の要求が再度送信されます (この時点で、インクリメントは、値をページ)。 このプロセスは、64 KB 未満のサイズの記述子が受信されるまで繰り返されます。 ページの最大数は 255 に、記述子のサイズに対して 16 MB の制限が適用されるに注意してください。

**WIndex**フィールドには、Microsoft OS 機能記述子を取得するの機能のインデックス番号が格納されます。 Microsoft では、この Microsoft OS 機能ディスクリプターとインデックスの一覧を維持します。 詳細については、Microsoft OS 機能ディスクリプターを参照してください。 [Microsoft OS ディスクリプター](https://go.microsoft.com/fwlink/p/?linkid=308932)します。

**WLength**フィールドをフェッチする記述子の長さを指定します。 記述子に記載されているバイト数よりも長いかどうか、 **wLength**フィールドに、記述子の最初のバイトのみが返されます。 指定された値よりも短い場合、 **wLength**フィールドに、短いパケットが返されます。

特定の OS 記述子が存在しない場合、デバイスは、要求エラーまたは停止に発行されます。

**Microsoft OS 機能記述子の制約**

Microsoft OS 機能ディスクリプターと、検索に、次の制約が適用されます。

-   すべての Microsoft OS 機能ディスクリプターが定義され、標準化します。 ベンダーは、変更、追加、または Microsoft から直接同意を得ず Microsoft OS 機能ディスクリプターを作成するのには使用できません。
-   すべての Microsoft OS 機能ディスクリプターに埋め込まれているサイズとバージョン番号になります。 これらの値は、オペレーティング システムに正しい情報を常に報告する必要があります。
-   デバイスを 1 つ以上の Microsoft OS 機能の記述子がファームウェアに埋め込まれていることができます。
-   他のユーザーはデバイスに一意なインターフェイスごとのレベルでいくつかの Microsoft OS 機能ディスクリプターが格納されます。 デバイス レベルの Microsoft OS 機能の記述子は、0 として wValue フィールドの高位バイトを設定する必要があります。

**機能の記述子の構造**

MBIM をサポートできるとして識別、デバイスをする必要がありますもサポート拡張の構成記述子では、定義されている機能の記述子の 1 つであります。 この記述子の構造は次のとおりです。

**ヘッダー セクション**

ヘッダー セクションには、拡張の構成記述子の残りの部分に関する情報が格納されます。 **DwLength**フィールドには全体の拡張の構成記述子の長さが含まれています。 ヘッダー セクションには、1.00 (0100 H) に初期設定は、バージョン番号も含まれています。 この記述子の将来のリビジョンは、後の段階でリリースされた可能性があります。 注拡張構成記述子の将来のバージョンがので、ヘッダー セクション内のエントリの数を増やす必要がありますもこの数が正確に、デバイスに格納されているし、オペレーティング システムによって読み取られたことを確認してください。

*拡張の構成記述子のヘッダー セクション*

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
<th align="left">Offset</th>
<th align="left">フィールド</th>
<th align="left">サイズ</th>
<th align="left">値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>dwLength</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>符号なしの DWORD</p></td>
<td align="left"><p>[長さ] フィールドには、(バイト単位)、拡張の構成記述子の長さがについて説明します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>bcdVersion</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>BCD</p></td>
<td align="left"><p>バイナリ コード化された 10 進数 (たとえば、1.00 は 0100 H バージョン) で構成記述子のリリース番号を拡張します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>6</p></td>
<td align="left"><p>wIndex</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>WORD</p></td>
<td align="left"><p>固定 0x0004 を =</p></td>
</tr>
<tr class="even">
<td align="left"><p>8</p></td>
<td align="left"><p>bCount</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>BYTE</p></td>
<td align="left"><p>ヘッダー セクションの後に続くセクションでは関数の合計数 = 0x01</p></td>
</tr>
<tr class="odd">
<td align="left"><p>9</p></td>
<td align="left"><p>予約されています</p></td>
<td align="left"><p>7</p></td>
<td align="left"><p></p></td>
<td align="left"><p>予約されています</p></td>
</tr>
</tbody>
</table>

 

**関数のセクション**

関数のセクションでは、2 つの重要な情報を提供します。 関数のグループに同じ目的に使用する連続したインターフェイスをグループ化され、各関数の互換性があり、subcompatible の Id を提供します。

MBIM デバイスによって使用される値を含む関数のセクションの形式を次に示します。

*拡張の構成記述子関数セクション*

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
<th align="left">Offset¹</th>
<th align="left">フィールド</th>
<th align="left">サイズ</th>
<th align="left">値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>bFirstInterfaceNumber</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>バイト</p></td>
<td align="left"><p>この関数のインターフェイスの数を開始 = 0x00</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>bInterfaceCount</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>バイト</p></td>
<td align="left"><p>この関数からを含める必要があるインターフェイスの合計数 = 0x01</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>CompatibleID</p></td>
<td align="left"><p>8</p></td>
<td align="left"><p>Bytes</p></td>
<td align="left"><p>互換性 ID</p></td>
</tr>
<tr class="even">
<td align="left"><p>10</p></td>
<td align="left"><p>subCompatibleID</p></td>
<td align="left"><p>8</p></td>
<td align="left"><p>Bytes</p></td>
<td align="left"><p>Subcompatible ID</p></td>
</tr>
<tr class="odd">
<td align="left"><p>18</p></td>
<td align="left"><p>予約されています</p></td>
<td align="left"><p>6</p></td>
<td align="left"><p></p></td>
<td align="left"><p>予約済み = 0</p></td>
</tr>
</tbody>
</table>

 

カスタム プロパティ セクションの ¹Offset をゼロにリセットされました。 拡張構成記述子の先頭からのフィールドのオフセットを計算するには、直前のセクションでは、の長さを追加します。

*互換性のある、MBIM 関数を公開する構成に基づいて Subcompatible Id*

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">bConfiguration</th>
<th align="left">CompatibleID</th>
<th align="left">subCompatibleID</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>ALTRCFG</p>
<p>(0x41 0x4C 0x54 0x52 0x43 0x46 0x47 0x00)</p></td>
<td align="left"><p>20000000</p>
<p>(0x32 0x00 0x00 0x00 0x00 0x00 0x00 0x00)</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>ALTRCFG</p>
<p>(0x41 0x4C 0x54 0x52 0x43 0x46 0x47 0x00)</p></td>
<td align="left"><p>30000000</p>
<p>(0x33 0x00 0x00 0x00 0x00 0x00 0x00 0x00)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p>ALTRCFG</p>
<p>(0x41 0x4C 0x54 0x52 0x43 0x46 0x47 0x00)</p></td>
<td align="left"><p>40000000</p>
<p>(0x34 0x00 0x00 0x00 0x00 0x00 0x00 0x00)</p></td>
</tr>
</tbody>
</table>

 

-   **bConfiguration**を指す、 **bConfiguration** MBIM 関数を公開する構成の USB 構成記述子内の値。 **bConfiguration** CDROM 関数のみを公開する既定の構成があるために、1 をすることはできません。 **bConfiguration** 4; より大きい値にすることはできません、最初の 4 つの構成内では、MBIM 関数を公開する必要があります。
-   compatibleID は、すべての構成は同じままです。 構成に基づく subcompatibleID 変更

**例**

次の表では、複数の構成シナリオの例を示します。 表には、各構成し、これらの構成ごとに異なるバージョンのオペレーティング システムの動作で使用できる関数を示します。

*複数の構成のモバイル ブロード バンド デバイスの例*

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
<th align="left">bConfiguration</th>
<th align="left">1 (Windows 7 構成)</th>
<th align="left">2 (IHV 対 NCM の 1.0 の構成)</th>
<th align="left">3 (Windows 8 構成)</th>
<th align="left">3 (IHV 対 NCM の 2.0 の構成)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>公開される関数</p></td>
<td align="left"><p>CD-ROM ドライブ</p>
<p>SD</p></td>
<td align="left"><p>CD-ROM (CD-ROM)</p>
<p>SD</p>
<p>NCM1.0</p>
<p>モデム</p>
<p>TV</p>
<p>GPS</p>
<p>FP</p>
<p>PC/SC スマート カード</p>
<p>音声</p>
<p>診断</p></td>
<td align="left"><p>CD-ROM (CD-ROM)</p>
<p>SD</p>
<p>MBIM</p></td>
<td align="left"><p>CD-ROM (CD-ROM)</p>
<p>SD</p>
<p>NCM2.0</p>
<p>モデム</p>
<p>TV</p>
<p>GPS</p>
<p>FP</p>
<p>PC/SC スマート カード</p>
<p>音声</p>
<p>診断</p></td>
</tr>
</tbody>
</table>

 

次の表は、Microsoft OS 文字列記述子によって使用される値を表示して、Microsoft OS は、前のサンプルの複数の構成シナリオの構成機能の記述子を拡張します。

*複数の構成のモバイル ブロード バンド デバイスの例*

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">フィールド</th>
<th align="left">長さ (バイト)</th>
<th align="left">値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>bLength</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x12</p></td>
</tr>
<tr class="even">
<td align="left"><p>bDescriptorType</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x03</p></td>
</tr>
<tr class="odd">
<td align="left"><p>qwSignature</p></td>
<td align="left"><p>14</p></td>
<td align="left"><p>' MSFT100'</p>
<p>0x4D 0x00 0x53 0x00 0x46 0x00 0x54 0x00 0x31 0x00 0x30 0x00 0x30 0x00</p></td>
</tr>
<tr class="even">
<td align="left"><p>bMS_VendorCode</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0xA5</p></td>
</tr>
<tr class="odd">
<td align="left"><p>bPad</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x00</p></td>
</tr>
</tbody>
</table>

 

*Microsoft OS 構成の拡張機能記述子ヘッダーの例*

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Offset</th>
<th align="left">フィールド</th>
<th align="left">サイズ</th>
<th align="left">値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>dwLength</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>16</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>bcdVersion</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>0100 H</p></td>
</tr>
<tr class="odd">
<td align="left"><p>6</p></td>
<td align="left"><p>wIndex</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>0x0004</p></td>
</tr>
<tr class="even">
<td align="left"><p>8</p></td>
<td align="left"><p>bCount</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>9</p></td>
<td align="left"><p>予約されています</p></td>
<td align="left"><p>7</p></td>
<td align="left"><p></p></td>
</tr>
</tbody>
</table>

 

*構成機能の記述子の関数の拡張例 Microsoft OS*

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Offset²</th>
<th align="left">フィールド</th>
<th align="left">サイズ</th>
<th align="left">値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>bFirstInterfaceNumber</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p></p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>bInterfaceCount</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p></p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>CompatibleID</p></td>
<td align="left"><p>8</p></td>
<td align="left"><p></p></td>
</tr>
<tr class="even">
<td align="left"><p>10</p></td>
<td align="left"><p>subCompatibleID</p></td>
<td align="left"><p>8</p></td>
<td align="left"><p></p></td>
</tr>
<tr class="odd">
<td align="left"><p>18</p></td>
<td align="left"><p>予約されています</p></td>
<td align="left"><p>6</p></td>
<td align="left"><p></p></td>
</tr>
</tbody>
</table>

 

カスタム プロパティ セクションの ²Offset をゼロにリセットされました。 拡張構成記述子の先頭からのフィールドのオフセットを計算するには、直前のセクションでは、の長さを追加します。

 

 





