---
title: MB インターフェイスモデルの補助
description: このセクションでは、MB インターフェイスモデル (MBIM) に関する補足情報を提供します。
ms.assetid: 577BCF39-868B-44F5-A5C0-75E28689C2B6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3545d115c28415f74af230571e6ccc1b150b73d9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844289"
---
# <a name="mb-interface-model-supplement"></a>MB インターフェイス モデルに関する補足条項


Microsoft OS 記述子は、次のセグメントに分割されています。

-   1つの Microsoft OS 文字列記述子
-   1つまたは複数の Microsoft OS 機能記述子

OS 記述子をサポートするには、デバイスが文字列記述子を実装する必要があります。
**文字列記述子**

Microsoft OS 文字列記述子は、文字列インデックス0xEE に格納される文字列です。 この文字列の形式は、適切に定義されています。

Microsoft OS 文字列記述子は、次の目的を達成するために使用されます。

-   Microsoft OS 文字列記述子が存在する場合は、Microsoft OS 機能記述子の形式で、デバイスに埋め込まれた情報があることをオペレーティングシステムに示します。
-   Microsoft OS 文字列記述子には、文字列インデックス0xEE のデバイス上で発生する可能性があるランダムな文字列と区別するために使用される、署名フィールドが埋め込まれています。
-   Microsoft OS 文字列記述子には、Microsoft OS 記述子の将来のリビジョンで使用できるバージョン番号も埋め込まれています。

1つのデバイスには、1つの Microsoft OS 文字列記述子だけが格納されます。 次のセクションでは、Microsoft OS 文字列記述子の構造とその取得手順について説明します。
**OS 文字列の構造**

文字列記述子の構造を次に示します。

*文字列記述子の構造*

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
<th align="left">Value</th>
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
<td align="left"><p>B記述子の種類</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x03</p></td>
<td align="left"><p>文字列記述子</p></td>
</tr>
<tr class="odd">
<td align="left"><p>qwSignature</p></td>
<td align="left"><p>14</p></td>
<td align="left"><p>"MSFT100"</p></td>
<td align="left"><p>署名フィールド (4D0053004600540031003000 3000)</p></td>
</tr>
<tr class="even">
<td align="left"><p>bMS_VendorCode</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>ベンダーコード</p></td>
<td align="left"><p>他の OS 機能記述子を取得するためのベンダーコード</p></td>
</tr>
<tr class="odd">
<td align="left"><p>bPad</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x00</p></td>
<td align="left"><p>埋め込みフィールド</p></td>
</tr>
</tbody>
</table>

 

Microsoft OS 文字列記述子の構造はバージョン1.00 に固定されており、全体の長さは18バイトです。 Microsoft OS 文字列記述子のバージョン番号は、 **Qwsignature**フィールドに表示されます。 **Bms\_VendorCode**フィールドに格納されている情報は、1バイト値である必要があります。 これは、Microsoft OS 機能記述子を取得するために使用されます。このバイト値は、次に示す**Bmrequesttype**フィールドで使用されます。

**OS 文字列記述子を取得しています**

文字列に格納されている情報を取得するには、標準の GET\_DESCRIPTOR 要求をデバイスに発行する必要があります。 要求の形式は次のとおりです。

*標準の Get\_記述子文字列要求*

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
<td align="left"><p>文字列を返します。</p></td>
</tr>
</tbody>
</table>

 

**Bmrequesttype**フィールドは、データ転送の方向、記述子の種類、および受信者という3つの部分で構成されるビットマップです。 USB 仕様によれば、 **Bmrequesttype**の値は 1000 0000b (0x80) に設定されています。

GET\_DESCRIPTOR 要求の場合、 **Wvalue**フィールドは2つの部分に分割されます。 上位バイトには記述子の種類が格納され、下位バイトには記述子インデックスが格納されます。 Microsoft OS 文字列記述子を取得するには、上位バイトを設定して文字列記述子を取得する必要があります (0x03)。 Microsoft OS 文字列記述子は常にインデックス0xEE に格納されるため、この文字列インデックスは**Wvalue**フィールドの下位バイトに格納されている必要があります。

**WIndex**は言語 ID を格納するために使用されますが、Microsoft OS 文字列記述子の場合は0に設定する必要があります。

**Wlength**フィールドは、取得する文字列記述子の長さを示すために使用されます。 デバイスは、0x02 ~ 0xFF の有効な範囲に応答する必要があります。

デバイスに対応するアドレス (0xEE) に有効な記述子がない場合、デバイスは要求エラーまたは停止で応答します。 デバイスが停止しても応答しない場合、デバイスに対して1終了のゼロリセットが発行されます (状態が不明になった場合は、それを回復します)。

**OS 記述子の整合性を確認しています**

ベンダーは、任意の文字列 ID を使用して情報を格納できるため、インデックス0xEE に格納されている文字列が実際に Microsoft OS 文字列記述子であることを確認する必要があります。 これを確認するために、次のテストが実行されます。 いずれかのエラーが発生すると、Microsoft OS 機能記述子の取得が禁止されます。

-   ベンダーがインデックス位置0xEE に文字列を格納している場合、オペレーティングシステムは文字列を取得してクエリを実行し、Microsoft OS 文字列であるかどうかを確認します。 これを確認するには、文字列の signature フィールドを、前に指定した署名フィールドエントリと比較します。 不一致があると、文字列をさらに解析できなくなります。
-   2番目のテストでは、[署名] フィールドに指定されているバージョン番号に基づいて、文字列の長さの確認が含まれます。 指定されたバージョン番号 (文字列 "MSFT100" 内) は1.00 です。 これは18バイトの文字列記述子に対応します。

**Microsoft OS 文字列記述子の制約**

Microsoft OS 文字列記述子とその取得には、次の制約が適用されます。

-   Microsoft OS 記述子の仕様に準拠して情報を格納するには、microsoft [os 記述子に](https://go.microsoft.com/fwlink/p/?linkid=308932)記載されている情報に準拠している microsoft os 文字列記述子がデバイスに1つだけ必要です。
-   デバイスベンダーは、Microsoft OS 文字列記述子の**Bms\_VendorCode**フィールドの任意の値を自由に使用することが可能です。

**機能記述子**

機能記述子は、特定の目的に対して定義されている固定形式の記述子です。

**OS 機能記述子を取得しています**

Microsoft OS 機能記述子を取得するには、特別な GET\_MS\_記述子要求をデバイスに発行する必要があります。 要求の形式は次のとおりです。

*標準デバイス要求の形式*

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
<td align="left"><p>X</p></td>
<td align="left"><p>機能インデックス</p></td>
<td align="left"><p>長さ</p></td>
<td align="left"><p>記述子を返します</p></td>
</tr>
</tbody>
</table>

 

**Bmrequesttype**フィールドは、データ転送の方向、記述子の種類、受信者の3つの部分で構成されるビットマップで、USB 仕様に従っています。 Microsoft OS 機能記述子はベンダー固有の記述子で、データ転送の方向はデバイスからホストへとなります。 このため、 **Bmrequesttype**の値は 1100 0000b (0xC0) に設定されます。

**Brequest**フィールドは、要求の形式を示すために使用されます。 Microsoft OS 機能記述子を取得するには、 **Brequest**フィールドに特別な GET\_MS\_記述子バイトを入力する必要があります。 このバイトの値は、Microsoft 文字列記述子から取得される**Bms\_VendorCode**によって示されます。 Microsoft OS 文字列記述子の取得の詳細については、「 **os 文字列記述子の取得**」を参照してください。

**Wvalue**フィールドは特殊な用途に使用され、上位バイトと下位バイトに分割されます。 上位バイトは、インターフェイス番号を格納するために使用されます。 これは、インターフェイスごとに機能記述子を格納するために不可欠です。複合デバイスの場合は特に、[複数のインターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を持つデバイスの場合に必要です。 ほとんどの場合、インターフェイス0が使用されます。 下位バイトは、ページ番号を格納するために使用されます。 この機能により、記述子のサイズの境界が 64 KB ( **Wlength**フィールドのサイズによって設定された制限) になるのを防ぐことができます。 最初のページ値が0に設定された状態で、記述子がフェッチされます。 完全な記述子 (サイズが 64 KB) を受信した場合、ページの値は1ずつ増加し、記述子の要求は再送信されます (今回はインクリメントされたページの値を使用します)。 このプロセスは、サイズが 64 KB 未満の記述子を受信するまで繰り返されます。 最大ページ数は255であることに注意してください。これにより、記述子サイズに 16 MB の制限が適用されます。

**WIndex**フィールドには、取得する Microsoft OS 機能記述子の機能インデックス番号が格納されます。 Microsoft OS 機能の記述子とインデックスの一覧は、microsoft によって管理されます。 Microsoft OS 機能記述子の詳細については、「 [MICROSOFT Os 記述子](https://go.microsoft.com/fwlink/p/?linkid=308932)」を参照してください。

**Wlength**フィールドは、フェッチする記述子の長さを指定します。 記述子が、 **Wlength**フィールドに記述されたバイト数よりも長い場合は、記述子の最初のバイトだけが返されます。 **Wlength**フィールドに指定された値より短い場合は、短いパケットが返されます。

特定の OS 記述子が存在しない場合、デバイスは要求エラーまたは停止を発行します。

**Microsoft OS 機能記述子の制約**

Microsoft OS の機能記述子とその取得には、次の制約が適用されます。

-   すべての Microsoft OS 機能記述子が定義され、標準化されています。 Microsoft から直接同意されていない場合、ベンダーは Microsoft OS 機能記述子の変更、追加、または作成を行うことはできません。
-   すべての Microsoft OS 機能記述子には、サイズとバージョン番号が埋め込まれています。 これらの値は、常にオペレーティングシステムに正しい情報を報告する必要があります。
-   デバイスは、ファームウェアに複数の Microsoft OS 機能記述子を埋め込むことができます。
-   一部の Microsoft OS 機能記述子は、インターフェイスごとのレベルに格納されていますが、デバイスに固有のものもあります。 デバイスレベルの Microsoft OS 機能記述子は、wValue フィールドの上位バイトを0として設定する必要があります。

**フィーチャー記述子の構造**

MBIM をサポートできるものとして識別するには、デバイスは、定義されている機能記述子の1つである拡張構成記述子もサポートする必要があります。 この記述子の構造は次のとおりです。

**ヘッダーセクション**

ヘッダーセクションには、拡張構成記述子の残りの部分に関する情報が格納されます。 **Dwlength**フィールドには、拡張された構成記述子全体の長さが含まれます。 ヘッダーセクションにはバージョン番号も含まれており、これは最初に 1.00 (0100H) に設定されます。 この記述子の今後のリビジョンは、後の段階でリリースされる可能性があります。 拡張構成記述子の将来のバージョンでも、ヘッダーセクションのエントリ数を増やす必要があることに注意してください。そのため、この数値がデバイスに正確に格納され、オペレーティングシステムによって読み取られていることを確認してください。

*拡張構成記述子ヘッダーセクション*

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
<th align="left">Size</th>
<th align="left">Value</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>dwLength</p></td>
<td align="left"><p>ホーム フォルダーが置かれているコンピューターにアクセスできない</p></td>
<td align="left"><p>符号なし DWORD</p></td>
<td align="left"><p>長さフィールドは、拡張構成記述子の長さをバイト単位で示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ホーム フォルダーが置かれているコンピューターにアクセスできない</p></td>
<td align="left"><p>bcdVersion</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>BCD</p></td>
<td align="left"><p>バイナリでコード化された10進数の拡張構成記述子のリリース番号 (たとえば、バージョン1.00 は 0100H)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>6</p></td>
<td align="left"><p>wIndex</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>テキスト</p></td>
<td align="left"><p>Fixed = 0x0004</p></td>
</tr>
<tr class="even">
<td align="left"><p>8</p></td>
<td align="left"><p>bCount</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>BYTE</p></td>
<td align="left"><p>ヘッダーセクションの後に続く関数セクションの合計数 = 0x01</p></td>
</tr>
<tr class="odd">
<td align="left"><p>9</p></td>
<td align="left"><p>確保</p></td>
<td align="left"><p>7</p></td>
<td align="left"><p></p></td>
<td align="left"><p>確保</p></td>
</tr>
</tbody>
</table>

 

**Function セクション**

関数セクションでは、2つの重要な情報を提供します。 これは、類似した目的を果たす連続するインターフェイスを関数グループにグループ化し、各関数に互換性のある Id と互換性のある Id を提供します。

MBIM デバイスで使用する必要がある値を含む、関数セクションの形式を次に示します。

*拡張構成記述子関数セクション*

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
<th align="left">オフセット¹</th>
<th align="left">フィールド</th>
<th align="left">Size</th>
<th align="left">Value</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>bFirstInterfaceNumber</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>バイト</p></td>
<td align="left"><p>この関数のインターフェイス番号0x00 を開始しています</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>bInterfaceCount</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>バイト</p></td>
<td align="left"><p>この関数からに含める必要があるインターフェイスの合計数 = 0x01</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>互換 Id</p></td>
<td align="left"><p>8</p></td>
<td align="left"><p>Bytes</p></td>
<td align="left"><p>互換性 ID</p></td>
</tr>
<tr class="even">
<td align="left"><p>10</p></td>
<td align="left"><p>Sub互換 Id</p></td>
<td align="left"><p>8</p></td>
<td align="left"><p>Bytes</p></td>
<td align="left"><p>Subcompatible ID</p></td>
</tr>
<tr class="odd">
<td align="left"><p>18</p></td>
<td align="left"><p>確保</p></td>
<td align="left"><p>6</p></td>
<td align="left"><p></p></td>
<td align="left"><p>予約済み = 0</p></td>
</tr>
</tbody>
</table>

 

¹カスタムプロパティセクションのオフセットが0にリセットされました。 拡張構成記述子の先頭からフィールドのオフセットを計算するには、その前にあるセクションの長さを追加します。

*MBIM 関数を公開する構成に基づく、互換性のある Id と互換 Id*

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">bConfiguration</th>
<th align="left">互換 Id</th>
<th align="left">Sub互換 Id</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>ALTRCFG</p>
<p>(0x41 0X41 0x54 0x54 0x41 0x41 0x41 0x00)</p></td>
<td align="left"><p>2000万</p>
<p>(0x32 0x00 0x00 0x00 0x00 0x00)</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>ALTRCFG</p>
<p>(0x41 0X41 0x54 0x54 0x41 0x41 0x41 0x00)</p></td>
<td align="left"><p>3000万</p>
<p>(0x33 0x00 0x00 0x00 (0x00 0x00 0x00)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ホーム フォルダーが置かれているコンピューターにアクセスできない</p></td>
<td align="left"><p>ALTRCFG</p>
<p>(0x41 0X41 0x54 0x54 0x41 0x41 0x41 0x00)</p></td>
<td align="left"><p>4000万</p>
<p>(0x34 0x00 0x00 0x00 0x00 0x00 0x00)</p></td>
</tr>
</tbody>
</table>

 

-   **Bconfiguration**とは、mbim 関数を公開する構成の USB 構成記述子内の**bconfiguration**値を指します。 **Bconfiguration**を1にすることはできません。これは、CDROM 関数のみを公開する既定の構成であるためです。 **Bconfiguration**を4より大きくすることはできません。つまり、MBIM 関数は、最初の4つの構成内で公開する必要があります。
-   互換 Id は、すべての構成で同じままです。 構成に基づいて、Sub互換 Id が変更されます。

**例**

次の表は、サンプルのマルチ構成シナリオを示しています。 次の表に、各構成で使用可能な関数と、オペレーティングシステムのさまざまなバージョンがそれぞれの構成に対して実行するアクションを示します。

*マルチ構成モバイルブロードバンドデバイスの例*

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
<th align="left">1 (Windows-7-構成)</th>
<th align="left">2 (IHV-NCM-1.0-Configuration)</th>
<th align="left">3 (Windows-8-構成)</th>
<th align="left">3 (IHV-NCM-2.0-Configuration)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>公開された関数</p></td>
<td align="left"><p>CDROM</p>
<p>SD</p></td>
<td align="left"><p>CD-ROM</p>
<p>SD</p>
<p>NCM 1.0</p>
<p>モデム</p>
<p>TV</p>
<p>GPS</p>
<p>レジスタ</p>
<p>PC/SC スマートカード</p>
<p>音声</p>
<p>斜め</p></td>
<td align="left"><p>CD-ROM</p>
<p>SD</p>
<p>MBIM</p></td>
<td align="left"><p>CD-ROM</p>
<p>SD</p>
<p>NCM 2.0</p>
<p>モデム</p>
<p>TV</p>
<p>GPS</p>
<p>レジスタ</p>
<p>PC/SC スマートカード</p>
<p>音声</p>
<p>斜め</p></td>
</tr>
</tbody>
</table>

 

次の表は、Microsoft OS 文字列記述子と、前のサンプルのマルチ構成シナリオ用の Microsoft OS 拡張構成機能記述子によって使用される値を示しています。

*マルチ構成モバイルブロードバンドデバイスの例*

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
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>bLength</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x12</p></td>
</tr>
<tr class="even">
<td align="left"><p>B記述子の種類</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x03</p></td>
</tr>
<tr class="odd">
<td align="left"><p>qwSignature</p></td>
<td align="left"><p>14</p></td>
<td align="left"><p>'MSFT100'</p>
<p>0x4D 0x00 0x53 0x00 0x4d 0x00 0x53 0x00 0x31 0x00 0x30 0x00 0x30 0x00</p></td>
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

 

*Microsoft OS 拡張構成機能の記述子ヘッダーの例*

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
<th align="left">Size</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>dwLength</p></td>
<td align="left"><p>ホーム フォルダーが置かれているコンピューターにアクセスできない</p></td>
<td align="left"><p>16</p></td>
</tr>
<tr class="even">
<td align="left"><p>ホーム フォルダーが置かれているコンピューターにアクセスできない</p></td>
<td align="left"><p>bcdVersion</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>0100H</p></td>
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
<td align="left"><p>確保</p></td>
<td align="left"><p>7</p></td>
<td align="left"><p></p></td>
</tr>
</tbody>
</table>

 

*Microsoft OS 拡張構成機能の記述子関数の例*

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">オフセット²</th>
<th align="left">フィールド</th>
<th align="left">Size</th>
<th align="left">Value</th>
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
<td align="left"><p>互換 Id</p></td>
<td align="left"><p>8</p></td>
<td align="left"><p></p></td>
</tr>
<tr class="even">
<td align="left"><p>10</p></td>
<td align="left"><p>Sub互換 Id</p></td>
<td align="left"><p>8</p></td>
<td align="left"><p></p></td>
</tr>
<tr class="odd">
<td align="left"><p>18</p></td>
<td align="left"><p>確保</p></td>
<td align="left"><p>6</p></td>
<td align="left"><p></p></td>
</tr>
</tbody>
</table>

 

カスタムプロパティセクションの²オフセットが0にリセットされました。 拡張構成記述子の先頭からフィールドのオフセットを計算するには、その前にあるセクションの長さを追加します。

 

 





