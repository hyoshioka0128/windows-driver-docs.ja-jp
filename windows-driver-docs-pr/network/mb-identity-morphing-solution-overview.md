---
title: MB id モーフィング ソリューションの概要
description: ソリューションは、モーフィング、デバイスの USB の構成を一連の USB 関数にマップします。
ms.assetid: 4A3EDD12-00CC-48A0-BCD9-8F64E90FA9F6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0ed2366c45c5dc523cd77a0d9f0d9156d5d1495
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573511"
---
# <a name="mb-identity-morphing-solution-overview"></a>MB ID モーフィング ソリューションの概要


ソリューションは、モーフィング、デバイスの USB の構成を一連の USB 関数にマップします。 任意の時点では、(構成) を使用して関数の 1 つのセットは、ホストに公開されます。 ソリューションでは、これらの構成を切り替えることによって変換は実現します。

## <a name="logical-configurations"></a>論理構成


デバイスに存在する関数は、次の論理セットにグループ化されます。

*関数の論理セット*

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数の論理セット</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Windows 7 の構成</p></td>
<td align="left"><p>モーフィング デバイスは、最初に、ホストに挿入したときに、Windows 7 と Windows の以前のバージョンによって選択されている構成。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 8 の構成</p></td>
<td align="left"><p>モーフィング デバイスは、ホストに挿入したときに、Windows 8 で選択を構成します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IHV NCM 1.0 構成</p></td>
<td align="left"><p>ドライバー パッケージをインストールした後は、Windows 7 および Windows の以前のバージョンにインストールされている IHV ソフトウェアによって選択された構成。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IHV NCM 2.0 構成</p></td>
<td align="left"><p>ドライバー パッケージをインストールした後は、Windows 8 にインストールされている IHV ソフトウェアによって選択された構成。</p></td>
</tr>
</tbody>
</table>

 

次の表では、可能なインターフェイス、および機能と共に、前の表に示す USB 構成を示します。 残りのサブトピックでは、各構成の追加要件がについて説明します。

*USB の構成*

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">構成 1 (Windows 7 構成)</th>
<th align="left">構成 2(IHV–NCM-10-Configuration)</th>
<th align="left">構成 3 (Windows 8 の構成)</th>
<th align="left">4 の構成 (IHV NCM 対 20 の構成)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>大容量 CD-ROM</p>
<p>大容量の SD</p></td>
<td align="left"><p>大容量 CD-ROM</p>
<p>大容量の SD</p>
<p>NCM1.0</p>
<p>モデム</p>
<p>TV</p>
<p>GPS</p>
<p>FP</p>
<p>PC/SC スマート カード</p>
<p>音声</p>
<p>診断</p></td>
<td align="left"><p>大容量 CD-ROM</p>
<p>大容量の SD</p>
<p>MBIM</p></td>
<td align="left"><p>大容量 CD-ROM</p>
<p>大容量の SD</p>
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

 

ソリューションの目標

-   Windows 7、ユーザーはデバイスをモーフィングでモバイル ブロード バンド関数を使用する前にドライバー パッケージのインストールの余分な手順を実行する必要があります。
-   Windows 8 でユーザーいないモーフィング MBIM 仕様に準拠しているデバイスにモバイル ブロード バンド関数を使用するドライバー パッケージをインストールするための追加の手順を実行するが必要です。
-   Windows 8 で、ユーザーは、受信トレイのドライバーがないデバイスをモーフィングで IHV 関数を使用する前にドライバー パッケージのインストールの余分な手順を実行する必要があります。

**前提条件**

MBIM には、NCM 1.0 用の旧バージョンとの互換性も含まれています。

## <a name="supported-transitions"></a>サポートされている遷移


Windows 8 向け

未構成の&gt;Windows 8 の構成

Windows-8-構成 -&gt; IHV NCM 2.0 構成

Windows 7 の

未構成の&gt;Windows 7 の構成

Windows-7-構成 -&gt; IHV NCM 対 1.0 の構成

![windows 7 および windows 8 の移行パスの構成](images/mbim7.png)

Windows 7 および Windows 8 用の構成の移行パス

任意の遷移が示されていません以前がサポートされていないことに注意してください。

## <a name="transition-details"></a>遷移の詳細


その構成では、次の機能を使用したサンプル USB モーフィング デバイスを検討してください。

![usb を 4 つの異なる構成でのデバイスとその機能をモーフィング](images/mbim8.png)

複数の関数と USB デバイス

**Windows 8**

Windows 8 の構成

モーフィング デバイスが Windows 8 を実行しているコンピューターに接続されているときに Windows 8 構成は、選択する MBIM 関数を公開します。 MBIM 関数で、Windows 8 モバイル ブロード バンド クラス ドライバー (MBCD) が読み込まれます。 次の例では、3 の構成は、MBIM 関数を含む、Windows-8-構成です。

![モバイル ブロード バンド デバイス用の windows 8 と 4 つ構成します。 3 つの構成が強調表示されます。](images/mbim9.png)

Windows 8 デバイスを接続した後にドライバー スタックとデバイスの構成

IHV NCM 2.0 構成

Windows-8-構成では、モーフィング デバイスは IHV ドライバー パッケージをインストールするユーザーを許可する大容量記憶装置関数もあります。 大容量記憶装置関数からドライバー パッケージのインストール後、デバイスは、IHV-NCM-2.0 の構成で関数を公開する変形されます。 この構成では、GPS、診断などの追加の IHV 関数があります。 次の図に 4 の構成では、IHV-NCM-2.0 の構成を表します。

![windows 8 (ドライバー インストールの後処理) およびモバイル ブロード バンド デバイスの 4 つの構成。 4 つの構成が強調表示されます。](images/mbim10.png)

Windows 8 ユーザーが IHV ドライバー パッケージをインストールした後でドライバー スタックとデバイスの構成

**Windows 7**

Windows 7 の構成

モーフィング デバイスが Windows 7 または Windows の以前のバージョンを実行するコンピューターに接続されているときに Windows 7 構成は、選択する大容量記憶装置の関数を公開します。 これによって、ユーザーが大容量記憶装置関数から IHV ドライバー パッケージをインストールします。

次の例では、構成の 1 は Windows 7 の構成

![モバイル ブロード バンド デバイス用の windows 7 と 4 つ構成します。 1 つの構成が強調表示されます。](images/mbim11.png)

ユーザーが、IHV ドライバー パッケージをインストールしていないときに、Windows 7 でドライバー スタックとデバイスの構成

IHV NCM 1.0 構成

Windows 7 では、ユーザーは、大容量記憶装置関数からドライバー パッケージをインストールできます。 ドライバー ソフトウェアをインストールすると共に、IHV ソフトウェアは IHV-NCM-1.0 の構成に Windows 7 構成からデバイスを変形もします。

![モバイル ブロード バンド デバイス用の windows 7 と 4 つ構成します。 2 つの構成が強調表示されます。](images/mbim12.png)

ユーザーは、IHV ドライバー パッケージをインストールした後、Windows 7 でドライバー スタックとデバイスの構成

 

 





