---
title: INF LogConfig ディレクティブ
description: LogConfig ディレクティブは、1 つまたは複数 INF ライター定義のセクションでは、それぞれ指定するハードウェア リソースの論理構成を参照します。
ms.assetid: 6b60c3eb-bf70-42f7-bed7-a856fd626d8c
keywords:
- INF LogConfig ディレクティブ デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF LogConfig Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76b4fddfb7ba74d4a9784cdafd54d15f32bfbb67
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350391"
---
# <a name="inf-logconfig-directive"></a>INF LogConfig ディレクティブ


**注**  ユニバーサルまたはモバイルのドライバー パッケージを作成している場合は、このディレクティブが無効です。 参照してください[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

 

A **LogConfig**ディレクティブは、1 つまたは複数 INF ライター定義のセクションでは、ハードウェア リソース − の論理構成を指定の割り込み要求の行を参照、メモリの範囲、I/O ポート、および DMA いるチャネルがあることができますデバイスによって使用されます。 各*ログの構成 セクションで*代替デバイスで使用できるバス相対ハードウェア リソースのセットを指定します。

```ini
[DDInstall] | 
[DDInstall.LogConfigOverride] 
  
LogConfig=log-config-section[,log-config-section]...
```

非 PnP デバイスの INF ファイルでは、このディレクティブを使用して、基本的な構成を作成します。

PnP デバイスの INF ファイルは、上書きの構成を作成する場合にのみ、このディレクティブを使用します。

セクションによって参照される各名前付き、 **LogConfig**ディレクティブは、次の形式。

```ini
[log-config-section]
 
ConfigPriority=priority-value[,config-type]
[DMAConfig=[DMAattrs:]DMANum[,DMANum]...]
[IOConfig=io-range[,io-range]...]
[MemConfig=mem-range[,mem-range]...]
[IRQConfig=[IRQattrs:]IRQNum[,IRQNum]...]
[PcCardConfig=ConfigIndex[:[MemoryCardBase1][:MemoryCardBase2]][(attrs)]]
[MfCardConfig=ConfigRegBase:ConfigOptions[:IoResourceIndex][(attrs)]...]
...
```

## <a name="entries"></a>エントリ


<a href="" id="configpriority-priority-value"></a>**ConfigPriority =**<em>優先度値</em>  
次のいずれかとして、この論理構成での優先順位の値を指定します。

<a href="" id="desired"></a>必要な  
論理的な構成、最適です。

<a href="" id="normal"></a>標準  
論理的な構成済みより少ない最適な DESIRED します。 これは、一般的な設定です。

場合、標準を指定する必要があります、*ログの構成 セクションで*で定義された、 [ * **DDInstall *。LogConfigOverride** ](inf-ddinstall-logconfigoverride-section.md)セクション、および no *config 型*値を指定することができます。

<a href="" id="suboptimal"></a>最適ではないです。  
論理的な構成済みより少ない最適な法線。

<a href="" id="hardreconfig"></a>HARDRECONFIG  
ジャンパー変更を再構成する必要があります。

<a href="" id="hardwired"></a>固定  
変更することはできません。

<a href="" id="restart"></a>再起動  
再起動を有効にする必要があります。

<a href="" id="reboot"></a>再起動  
これは、再起動と同じです。

<a href="" id="poweroff"></a>電源オフ  
電源サイクルを有効にする必要があります。

<a href="" id="disabled"></a>無効になっています。  
ハードウェアまたはデバイスが無効です。

<a href="" id="dmaconfig--dmaattrs--dmanum--dmanum-----"></a>**DMAConfig =**\[*DMAattrs:*\]*DMANum*\[<strong>、</strong>DMANum\].\]  
*DMAattrs*デバイスが唯一の 8 ビット DMA チャネルを持つバスに接続されているし、デバイスは、標準のシステム DMA を使用する場合は省略可能です。 それ以外の場合、次の文字のいずれかを指定できます。

| 文字 | 説明    |
|--------|------------|
| **D**  | 32 ビットの DMA |
| **W**  | 16 ビット DMA |
| **N**  | 8 ビット DMA  |

 

使用する必要がある、デバイスは、バス マスター DMA を使用している場合**M**使用 DMA チャネルの種類を示す次の (相互に排他的) 文字のいずれかの。**A**、 **B**、または**F**します。どちらの場合**A**、 **B**、または**F**は指定すると、標準の DMA チャネルが使用されます。

*DMANum*コンマ (,) で次の各区切りの 10 進数として 1 つまたは複数のバス相対 DMA チャネルを指定します。

<a href="" id="ioconfig-io-range--io-range----"></a>**IOConfig =**<em>io 範囲</em>\[**、**<em>io 範囲</em>\].  
形式は次のいずれかで、デバイスの 1 つまたは複数の I/O ポート範囲を指定します。

<a href="" id="start-end---decode-mask---alias-offset---attr------type-1-i-o-range-"></a>*開始から終了*\[**(**\[*デコード マスク*\]\[*: エイリアス オフセット*\]\[ *: attr*\]**)** \] (種類 1 の I/O の範囲)  

<a href="" id="start"></a>*開始*  
64 ビットの 16 進数のアドレスとして、I/O ポートの範囲の開始アドレスを指定します。

<a href="" id="end"></a>*終わり*  
64 ビットの 16 進数のアドレスとしても、I/O ポートの範囲の終了アドレスを指定します。

<a href="" id="decode-mask"></a>*デコード マスク*  
別名型を定義して、次のいずれかを指定できます。

| マスクの値 | 説明         | IOR_Alias 値 |
|------------|-----------------|------------------|
| **3ff**    | 10 ビットをデコードします。   | 0x04             |
| **fff**    | 12 ビットをデコードします。   | 0x10             |
| **ffff**   | 16 ビットをデコードします。   | 0x00             |
| **0**      | 正の値をデコードします。 | 0 xff の場合             |

 

<a href="" id="alias-offset-"></a>*エイリアスのオフセット値*   
使用されません。

<a href="" id="attr"></a>*attr*  
文字を指定**M**システム メモリ内の特定の範囲がある場合。 省略した場合、特定の範囲は I/O ポートの領域では。

<a href="" id="size-min-max--align-mask----decode-mask---alias-offset---attr------type-2-i-o-range-"></a><em>サイズ</em>**@**<em>最小-最大</em>\[**%**<em>align マスク</em>\] \[ **(**\[*デコード マスク*\]\[**:**<em>エイリアス オフセット</em>\] \[ **:**<em>attr</em>\])\] (種類 2 の I/O の範囲)  

<a href="" id="size"></a>*サイズ*  
32 ビット 16 進数の値として、I/O ポートの範囲に必要なバイト数を指定します。

<a href="" id="min"></a>*最小値*  
64 ビットの 16 進数のアドレスとして I/O ポートの範囲の最小可能な開始アドレスを指定します。

<a href="" id="max"></a>*最大*  
64 ビットの 16 進数のアドレスとして、I/O ポートの範囲の終了アドレス可能な最高レベルを指定します。

<a href="" id="align-mask"></a>*align マスク*  
ビットごとの AND 演算を整数 (通常、32 ビットまたは 64 ビット) のアドレスの境界上の I/O ポートの範囲の開始を配置するために使用される 64 ビットマスクを指定します。

<a href="" id="decode-mask"></a>*デコード マスク*  
別名型を定義して、次のいずれかを指定できます。

| マスクの値 | 説明         | IOR_Alias 値 |
|------------|-----------------|------------------|
| **3ff**    | 10 ビットをデコードします。   | 0x04             |
| **fff**    | 12 ビットをデコードします。   | 0x10             |
| **ffff**   | 16 ビットをデコードします。   | 0x00             |
| **0**      | 正の値をデコードします。 | 0 xff の場合             |

 

<a href="" id="alias-offset-"></a>*エイリアスのオフセット値*   
使用されません。

<a href="" id="attr"></a>*attr*  
文字を指定**M**システム メモリ内の特定の範囲がある場合。 省略した場合、特定の範囲は I/O ポートの領域では。

<a href="" id="memconfig-mem-range--mem-range----"></a>**MemConfig =**<em>メモリ範囲</em>\[**、**<em>メモリ範囲</em>\].  
次の形式のいずれかでは、デバイスの 1 つ以上のメモリ範囲を指定します。

```ini
start-end[(attr)] | size@min-max[%align-mask][(attr)]
```

<a href="" id="start"></a>*開始*  
64 ビットの 16 進値として、デバイスのメモリの範囲の開始 (バス単位) の物理アドレスを指定します。

<a href="" id="end"></a>*終わり*  
64 ビットの 16 進値としても、メモリの範囲の終了の物理アドレスを指定します。

<a href="" id="attr"></a>*attr*  
1 つまたは複数の次の文字として、メモリ範囲の属性を指定します。

| 文字 | 説明                                             |
|--------|-----------------------------------------------------|
| **R**  | 読み取り専用です。                                           |
| **W**  | 書き込みのみ                                          |
| **RW** | 読み取り/書き込み                                          |
| **C**  | 結合の書き込みが許可されています。                              |
| **H**  | キャッシュ可能                                           |
| **F**  | プリフェッチ可能です                                        |
| **D**  | カードのデコードの代わりに 32 ビット アドレス指定が 24 ビット |

 

両方**R**と**W**が指定されてか、どちらも指定しない場合、読み取り/書き込みが想定されています。

<a href="" id="size-"></a>*サイズ*   
32 ビット 16 進数の値として、メモリ範囲で必要なバイト数を指定します。

<a href="" id="min--"></a>*最小値*   
64 ビットの 16 進値として、デバイスのメモリの範囲の最小可能な開始アドレスを指定します。

<a href="" id="max"></a>*最大*  
64 ビットの 16 進値として、メモリ範囲の終了アドレス可能な最高レベルを指定します。

<a href="" id="align-mask-"></a>*align マスク*   
ビットごとの AND 演算を整数 (通常は 64 ビット) のアドレスの境界上のデバイスのメモリの範囲の開始を配置するために使用される 64 ビットマスクを指定します。

Align マスクを省略すると、メモリの既定の配置は、4 K の境界 (FFFFF000) では。

<a href="" id="irqconfig--irqattrs--irqnum--irqnum----"></a>**IRQConfig =**\[*IRQattrs:*\]*IRQNum*\[**、**<em>IRQNum</em>\]...  
*IRQattrs*デバイス bus 相対の edge によってトリガーされる IRQ を使用している場合を省略するとします。 それ以外の場合、指定**L**レベルによってトリガーされる IRQ を示すと **%.*ls**場合は、デバイスは、このエントリに記載の IRQ ラインを共有できます。

*IRQNum*デバイスを 10 進数として使用できる 1 つまたは複数のバス相対 Irq を指定します、次のコンマ (,) で区切っています。

<a href="" id="pccardconfig-configindex---memorycardbase1---memorycardbase2----attrs--"></a>**PcCardConfig=**<em>ConfigIndex</em>\[**:**\[*MemoryCardBase1*\]\[**:**<em>MemoryCardBase2</em>\]\]\[**(**<em>attrs</em>**)**\]  
CardBus レジスタを構成します。 または、デバイスの属性の領域にマップされる最大 2 つの永続的なメモリ ウィンドウを作成します。 ドライバーは、[メモリ] ウィンドウを使用して、ISR. から属性の領域にアクセスすることができます。 すべての数値を 16 進形式で指定します。

要素を**PcCardConfig**エントリは、次のとおり。

<a href="" id="configindex"></a>*ConfigIndex*  
PCMCIA バス上のデバイスの 8 ビット PCMCIA 構成のインデックスを指定します。

<a href="" id="memorycardbase1"></a>*MemoryCardBase1*  
最初の [メモリ] ウィンドウの 32 ビットのベース アドレスを指定します。

<a href="" id="memorycardbase2"></a>*MemoryCardBase2*  
必要に応じて 2 つ目の [メモリ] ウィンドウの 32 ビットのベース アドレスを指定します。

<a href="" id="attrs"></a>*属性*  
必要に応じてスペースで区切られた、デバイスの 1 つまたは複数の属性を指定します。 無効な属性指定子は、全体を無効に**PcCardConfig**エントリ。 特定の属性の 1 つ以上の指定子が指定されている場合、属性は、個々 の I/O またはデバイスの [メモリ] ウィンドウに適用されます。 のみ 1 つの指定子を指定すると、その属性は、(次の例を参照してください)、すべてのウィンドウに適用されます。

具体的には、複数の指定子が指定されている場合、最初の指定子左から右への読み取りは、最初のウィンドウと 2 番目のウィンドウに適用される次の指定子に適用されますが見つかりました。 1 つで 2 つの I/O ウィンドウと 2 つのメモリ ウィンドウの最大数を制御することが**PcCardConfig**エントリ。 デバイスに 3 つ以上のメモリ windows し、1 秒あたり場合、 **PcCardConfig**エントリを含める必要があります。

属性は次のとおりです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">属性</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>W</strong></td>
<td align="left"><p>16 ビットの I/O のデータのパス。</p>
<p>既定値は 8 ビット、INF が指定されている場合、 <strong>LogConfig</strong>ディレクティブ。 ない場合は<strong>LogConfig</strong>ディレクティブを指定すると、ドライバーは 16 ビットの I/O を使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>S</strong><em>n</em></td>
<td align="left"><p>~ IOCS16 ソース。</p>
<p>場合<em>n</em>は 0 です。 ~ IOCS16 が datasize ビットの値に基づきます。 N が 1、~ IOCS16 がに基づいて、~、デバイスから IOIS16 信号。 既定値は<strong>S</strong>1.</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>Z</strong><em>n</em></td>
<td align="left"><p>8 ビット、I/O 待機状態は 0。</p>
<p>場合<em>n</em> 0 個の追加の待機状態で 8 ビットの I/O アクセスが発生する 1 に設定されています。 場合<em>n</em> 0 の場合は、多少の待機状態でアクセスが発生します。 このフラグには、16 ビットの I/O の意味はありません。 既定値は<strong>Z</strong>0.</p></td>
</tr>
<tr class="even">
<td align="left"><strong>Xl</strong><em>n</em></td>
<td align="left"><p>I/O 待機の状態。</p>
<p>N が 1 の場合は、1 つの追加の待機状態で 16 ビットのシステムへのアクセスが発生します。 既定値は<strong>Xl</strong>1.</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>M</strong></td>
<td align="left">16 ビットのメモリ データのパス。 既定では 8 ビットです。</td>
</tr>
<tr class="even">
<td align="left"><strong>M8</strong></td>
<td align="left">8 ビットのメモリ データのパス。</td>
</tr>
<tr class="odd">
<td align="left"><strong>XM</strong><em>n</em></td>
<td align="left"><p>メモリは待機状態、0、1、2 または 3 n を使用できる場所です。</p>
<p>この値は、[メモリ] ウィンドウへのアクセスを 16 ビットの多少の待機状態の数を決定します。 既定値は<strong>XM</strong>3.</p></td>
</tr>
<tr class="even">
<td align="left"><strong>A</strong></td>
<td align="left">メモリの属性としてマップするメモリの範囲です。</td>
</tr>
<tr class="odd">
<td align="left"><strong>C</strong></td>
<td align="left">一般的なメモリ (既定値) としてマップするメモリの範囲です。</td>
</tr>
</tbody>
</table>

 

たとえば、(WB CA M XM1 XI0) の属性値は、次に変換されます。

1 日の I/O ウィンドウは、16 ビット

2 番目の I/O ウィンドウ 8 ビット

第 1 の [メモリ] ウィンドウは共通

2 番目の [メモリ] ウィンドウは、属性

メモリが 16 ビットです。

[メモリ] ウィンドウで 1 つの待機の状態

ゼロ待機 I/O windows 上の状態

<a href="" id="mfcardconfig-configregbase-configoptions--ioresourceindex---attrs-----"></a>**MfCardConfig =**<em>ConfigRegBase</em>**:**<em>ConfigOptions</em>\[**:** <em>IoResourceIndex</em>\]\[**(**<em>属性</em>**)**\].次のように登録、多機能端末の 1 つの関数の構成のセットの属性、メモリの場所を指定します。

<a href="" id="configregbase"></a>*ConfigRegBase*  
構成の多機能デバイスには、この関数のレジスタの属性のオフセットを指定します。

<a href="" id="configoptions-"></a>*ConfigOptions*   
8 ビット PCMCIA の構成オプションのレジスタを指定します。

<a href="" id="ioresourceindex-"></a>*IoResourceIndex*   
インデックスを指定、 **IOConfig**バス ドライバーの構成の基本 I/O をプログラミングで使用して、レジスタの制限を入力します。 このインデックスは 0 から始まる、ゼロによる初期の指定は、 **IOConfig**このエントリ*ログの構成 セクションで*します。

<a href="" id="attrs-"></a>*属性*   
場合、文字に設定**A**、構成および状態のレジスタにオーディオの有効化を有効にする PCMCIA バス ドライバーに指示します。

各**MfCardConfig**エントリは、多機能デバイスの 1 つの関数についての情報を提供します。 ときに一連の**LogConfig**各ディレクティブを個別参照*ログの構成 セクションで*INF ので[ * **DDInstall *。LogConfigOverride** ](inf-ddinstall-logconfigoverride-section.md)セクションの各*ログの構成 セクションで*など、そのエントリがあります。 **MfCardConfig**エントリ、同じ順序で一覧表示します。

<a name="remarks"></a>コメント
-------

A **LogConfig**すべてあたり-の製造元、モデルごとでディレクティブを指定することができます[ **INF *DDInstall*セクション**](inf-ddinstall-section.md)または[ **INF *DDInstall*します。LogConfigOverride セクション**](inf-ddinstall-logconfigoverride-section.md)します。

通常いくつかの代替論理構成をサポートする非 PnP デバイスに対して、INF のセットを定義する*ログ-構成-セクション*下、 *DDInstall*セクション。 各*ログの構成 セクションで*個別の論理構成リソースのセットを指定します。 含まれています、 **ConfigPriority**各論理構成に従って、デバイスとドライバーのパフォーマンスに対するその影響をランク付けのエントリが、初期化の容易さなどです。

PnP デバイスの場合は、PnP マネージャーは、一連の論理ハードウェア リソースを各 PnP デバイスに割り当てます。 つまり、PnP マネージャー、システム バス ドライバーのクエリを実行デバイス当たりの I/O バス構成リソースのレポートを使用してで受信、このようなすべてのリソースの使用量のシステム全体の最適なバランスを実現するために論理ハードウェア リソースのセットをデバイスごとの代入.

結果として、 **LogConfig** ディレクティブを*DDInstall* PnP デバイスは、セクションは無視されます。 PnP デバイスのバスによって報告されたリソースをオーバーライドするには、 **LogConfig** ディレクティブを[ * **DDInstall *。LogConfigOverride** ](inf-ddinstall-logconfigoverride-section.md)セクション。 ここで指定のリソース、*ログの構成 セクションで*バスによって報告された代わりに使用されます。

プラットフォーム拡張機能に追加できる、 *DDInstall*を含むセクションを**LogConfig**ディレクティブ、または、 [ * **DDInstall *。LogConfigOverride** ](inf-ddinstall-logconfigoverride-section.md)セクションで、プラットフォーム固有または OS 固有の論理構成を指定します。 詳細については、次を参照してください。 [INF ファイルを作成する](overview-of-inf-files.md)します。

指定された*ログの構成 セクションで*名は、INF ファイルに固有である必要がありますが、それを参照できます**LogConfig**他 INF でディレクティブ*DDInstall*セクションに、同じデバイス. 各 INF ライター作成セクション名は、INF ファイル内で一意である必要があり、セクション名を定義するための一般的な規則に従う必要があります。 これらの規則の詳細については、次を参照してください。 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)します。

1 つだけ**ConfigPriority**エントリは、それぞれで使用できる*ログの構成 セクションで*します。 ありますの各デバイスのハードウェア リソース要件に応じて、その他のエントリの 1 つ以上。

1 つまたは複数**MfCardConfig =** エントリでのみ表示されます、*ログの構成 セクションで*によって参照される、 **LogConfig**ディレクティブで、 <em>DDInstall</em>**.LogConfigOverride**の多機能デバイスに対して、INF セクション。 多機能デバイスの INF ファイルの詳細については、次を参照してください。[多機能デバイスをサポートしている](https://msdn.microsoft.com/library/windows/hardware/ff542743)します。

### <a name="logconfig-referenced-section-entries-and-values"></a>LogConfig 参照セクションのエントリと値

*ログの構成 セクションで*システムのインストーラーがバイナリ論理構成レコードを作成し、レジストリに格納します。

デバイスごとの任意の数を含めることができます、INF ファイル*ログ-構成-セクション*します。 ただし、このような各セクションでは、1 つのデバイスをインストールするための完全な情報を含める必要があります。 一般に、INF はの各エントリを指定する必要があります、*ログ-構成-セクション*同じ順序で。 INF ドライバーがそのデバイスを初期化する方法に適した最高の順序でエントリの各セットを指定する必要があります。

1 つ以上の場合*ログの構成 セクションで*インストール中に、特定のデバイス INF セクションではこれらの 1 つだけが使用されますが、存在します。 このような INF ファイルでこのようなセクションが使用されるコントロールでは部分的に、 **ConfigPriority**でこれらの各提供値*ログの構成 セクションで*します。 つまり、システムのインストーラーは、INF ファイルですべての構成の優先度を使用しようとしますを既にインストールされているデバイスとの競合が見つかった場合、下のランク付けされた論理構成を選択可能性があります。

インストール中に、内の各エントリからリソースを 1 つだけを指定した*ログの構成 セクションで*を選択し、特定のデバイスに割り当てられています。 その型のエントリのセットを使用する必要があります、特定のデバイスでは、同じ型の 1 つ以上のリソースを必要とする場合、*ログ-構成-セクション*します。

たとえば、特定のデバイス用の 2 つの I/O ポート範囲を確認する 2 つ**IOConfig =** エントリを指定する必要があります、*ログの構成 セクションで*デバイスにします。 その一方で、デバイスに IRQ が必要としない場合、INF を省略できます、 **IRQConfig**エントリから、*ログ-構成-セクション*します。

<a name="examples"></a>使用例
--------

この例がいくつか有効では**PcCardConfig** PCMCIA デバイス用のエントリ。

```ini
PcCardConfig=0:E0000:F0000(W)
PcCardConfig=0:E0000(M)
PcCardConfig=0::(W)
PcCardConfig=0(W)
```

この例での型 1 I/O 範囲指定、 **IOConfig**エントリ。 これには、I/O ポート領域、1F8、2F8、または 3F8 で開始できますが、サイズ 8 バイトを指定します。

```ini
IOConfig=1F8-1FF, 2F8-2FF, 3F8-3FF
```

これに対し、この例での型の 2 I/O 範囲指定、 **IOConfig**エントリ。 これには、I/O ポート領域、300、308、310、318、320、または 328 で開始できますが、サイズ 8 バイトを指定します。

```ini
IOConfig=8@300-32F%FF8
```

この例のセットを示しています。 **IOConfig** 4 ポート デバイスのエントリは、I/O を指定する各ポートを次から 0x400 バイト オフセットである範囲。

```ini
IoConfig=0x200-0x21f
IoConfig=0x600-0x61f
IoConfig=0xA00-0xA1f
IoConfig=0xE00-0xE1f
```

次の 2 つの例を表示する一般的な**MemConfig**エントリ。

この例では、C0000 または D0000 のいずれかで始まる 32 K バイトのメモリ領域を指定します。

```ini
MemConfig=C0000-C7FFF, D0000-D7FFF
```

この例では、64 K の境界上で 32 k バイトのメモリ領域を指定します。

```ini
MemConfig=8000@C0000-D7FFF%F0000
```

この例では、いくつかのシステム HDC クラス INF ファイルを設定する方法*ログ-構成-セクション*の汎用の ESDI ハード ディスク コント ローラーとは、 [ * **DDInstall *。LogConfigOverride** ](inf-ddinstall-logconfigoverride-section.md) IDE コント ローラーの特定のセクション。

```ini
[MS_HDC] ; per-manufacturer Models section
%FujitsuIdePccard.DeviceDesc% = 
          atapi_fujitsu_Inst, PCMCIA\FUJITSU-IDE-PC_CARD-DDF2
%*PNP0600.DeviceDesc% = atapi_Inst, *PNP0600 ; generic ESDI HDCs
%PCI\CC_0101.DeviceDesc% = pciide_Inst,,PCI\CC_0101

; ... other manufacturers' Models sections omitted

[atapi_Inst]
CopyFiles = @atapi.sys
LogConfig = esdilc1, esdilc2, esdilc3, esdilc4

; ... [atapi_Inst.Services] + service/EventLog-install omitted here

[esdilc1]
ConfigPriority=HARDWIRED
IOConfig=1f0-1f7(3ff::)
IoConfig=3f6-3f6(3ff::)
IRQConfig=14

[esdilc2]
ConfigPriority=HARDWIRED
IOConfig=170-177(3ff::)
IoConfig=376-376(3ff::)
IRQConfig=15

[esdilc3]
ConfigPriority=HARDWIRED
IOConfig=1e8-1ef(3ff::)
IoConfig=3ee-3ee(3ff::)
IRQConfig=11

[esdilc4]
; ...

[atapi_fujitsu_Inst.LogConfigOverride]
LogConfig = fujitsu.LogConfig0

[fujitsu.LogConfig0]
ConfigPriority=NORMAL
IOConfig=10@100-400%fff0
IRQConfig=14,15,5,7,9,11,12,3
PcCardConfig=1:0:0(W)
```

方法の例をいくつかの**MfCardConfig**エントリが使用されるを参照してください[をサポートしている PC カードことがある不完全な登録アドレス構成](https://msdn.microsoft.com/library/windows/hardware/ff542774)します。

## <a name="see-also"></a>関連項目


[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall*.FactDef**](inf-ddinstall-factdef-section.md)

 

 






