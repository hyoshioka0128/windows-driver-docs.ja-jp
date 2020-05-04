---
title: INF LogConfig ディレクティブ
description: LogConfig ディレクティブは、1つまたは複数の INF ライターで定義されたセクションを参照し、それぞれがハードウェアリソースの論理構成を指定します。
ms.assetid: 6b60c3eb-bf70-42f7-bed7-a856fd626d8c
keywords:
- INF LogConfig ディレクティブデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF LogConfig Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf30685d53937cacc96590473d9f3ff5f78b5397
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223144"
---
# <a name="inf-logconfig-directive"></a>INF LogConfig ディレクティブ


**注**  ユニバーサルまたはモバイルのドライバーパッケージをビルドする場合、このディレクティブは無効です。 「[ユニバーサル INF ファイルの使用」を](using-a-universal-inf-file.md)参照してください。

 

**Logconfig**ディレクティブは、1つまたは複数の INF ライターで定義されたセクションを参照します。各セクションは、ハードウェアリソースの論理構成 (割り込み要求行、メモリ範囲、i/o ポート、およびデバイスで使用できる DMA チャネル) を指定します。 各*ログ構成セクション*では、デバイスで使用できるバス相対ハードウェアリソースの代替セットを指定します。

```inf
[DDInstall] | 
[DDInstall.LogConfigOverride] 
  
LogConfig=log-config-section[,log-config-section]...
```

PnP 以外のデバイスの INF ファイルこのディレクティブを使用して、基本的な構成を作成します。

PnP デバイス用の INF ファイルこのディレクティブは、上書き構成を作成する場合にのみ使用します。

**Logconfig**ディレクティブによって参照される名前付きセクションには、次の形式があります。

```inf
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


<a href="" id="configpriority-priority-value"></a>**Configpriority =**<em>priority-値</em>  
次のいずれかの論理構成の優先順位値を指定します。

<a href="" id="desired"></a>望む  
ソフト構成、最適。

<a href="" id="normal"></a>通常  
ソフトに構成されており、必要以上に最適化されていません。 これは、一般的な設定です。

通常は、 *log-config-section* [ *ddinstall * でログ構成セクションが定義されている場合に指定する必要があります。LogConfigOverride](inf-ddinstall-logconfigoverride-section.md)セクション。 *config 型の*値を指定することはできません。

<a href="" id="suboptimal"></a>最適で  
ソフト構成、通常よりも最適化されていません。

<a href="" id="hardreconfig"></a>HARDRECONFIG  
ジャンパー変更を再構成する必要があります。

<a href="" id="hardwired"></a>固定  
を変更することはできません。

<a href="" id="restart"></a>一度  
再起動が有効になる必要があります。

<a href="" id="reboot"></a>再起動  
これは再起動と同じです。

<a href="" id="poweroff"></a>保管済み  
電源サイクルを有効にする必要があります。

<a href="" id="disabled"></a>無効に  
ハードウェア/デバイスが無効になっています。

<a href="" id="dmaconfig--dmaattrs--dmanum--dmanum-----"></a>**Dmaconfig =**\[*DMAattrs:*\]*dmanum*\[<strong>、</strong>dmanum\]...\]  
*DMAattrs*は、デバイスが8ビットの dma チャネルのみを搭載し、デバイスが標準のシステム DMA を使用するバス上で接続されている場合は省略可能です。 それ以外の場合は、次のいずれかの文字を使用できます。

| 文字 | 意味    |
|--------|------------|
| **D**  | 32ビット DMA |
| **W**  | 16ビット DMA |
| **N**  | 8ビット DMA  |

 

デバイスでバスマスタ DMA を使用する場合は、使用する DMA チャネルの種類 ( **A**、 **B**、または**F**) を示す、次の (相互に排他的な) 文字のいずれかを使用して**M**を使用する必要があります。**A**、 **B**、または**F**のいずれも指定しない場合は、標準の DMA チャネルが想定されます。

*Dmanum*は、1つまたは複数のバス相対 DMA チャネルを10進数として指定し、それぞれが次のコンマ (,) で区切られます。

<a href="" id="ioconfig-io-range--io-range----"></a>**Ioconfig =**<em>io 範囲</em>\[**、**<em>io 範囲</em>\]...  
次のいずれかの形式で、デバイスの1つ以上の i/o ポート範囲を指定します。

<a href="" id="start-end---decode-mask---alias-offset---attr------type-1-i-o-range-"></a>*start-end*\[**(**\[*デコードマスク*\]\[*: エイリアス-オフセット*\]\[*: attr*\]**)** \] (Type 1 i/o range)  

<a href="" id="start"></a>*着手*  
I/o ポート範囲の開始アドレスを、64ビットの16進アドレスとして指定します。

<a href="" id="end"></a>*終わり*  
I/o ポート範囲の終了アドレスを、64ビットの16進数アドレスとして指定します。

<a href="" id="decode-mask"></a>*デコード-マスク*  
エイリアスの種類を定義します。次のいずれかを指定できます。

| マスク値 | 意味         | IOR_Alias 値 |
|------------|-----------------|------------------|
| **3ff**    | 10ビットデコード   | 0x04             |
| **fff**    | 12ビットデコード   | 0x10             |
| **ffff**   | 16ビットデコード   | 0x00             |
| **0**      | 正のデコード | 0xFF             |

 

<a href="" id="alias-offset-"></a>*エイリアス-オフセット*   
使用されていません。

<a href="" id="attr"></a>*attr*  
指定された範囲がシステムメモリ内にある場合は、文字**M**を指定します。 省略した場合、指定された範囲は i/o ポート領域にあります。

<a href="" id="size-min-max--align-mask----decode-mask---alias-offset---attr------type-2-i-o-range-"></a><em>サイズ</em>**@**<em>の最小値と最大値</em>\[**%** の<em>調整マスク</em>\]\[**(**\[*デコードマスク*\]\[**:**<em>エイリアス-オフセット</em>\]\[**:**<em>attr</em>\])\] (型2の i/o 範囲)  

<a href="" id="size"></a>*幅*  
I/o ポート範囲に32ビットの16進値として必要なバイト数を指定します。

<a href="" id="min"></a>*」*  
I/o ポート範囲の使用可能な最小の開始アドレスを、64ビットの16進アドレスとして指定します。

<a href="" id="max"></a>*制限*  
I/o ポート範囲の有効な最大終了アドレスを64ビットの16進アドレスとして指定します。

<a href="" id="align-mask"></a>*アラマスク*  
必要に応じて、整数 (通常は32ビットまたは64ビット) アドレス境界の i/o ポート範囲の開始を揃えるためにビットごとの AND 演算で使用される64ビットマスクを指定します。

<a href="" id="decode-mask"></a>*デコード-マスク*  
エイリアスの種類を定義します。次のいずれかを指定できます。

| マスク値 | 意味         | IOR_Alias 値 |
|------------|-----------------|------------------|
| **3ff**    | 10ビットデコード   | 0x04             |
| **fff**    | 12ビットデコード   | 0x10             |
| **ffff**   | 16ビットデコード   | 0x00             |
| **0**      | 正のデコード | 0xFF             |

 

<a href="" id="alias-offset-"></a>*エイリアス-オフセット*   
使用されていません。

<a href="" id="attr"></a>*attr*  
指定された範囲がシステムメモリ内にある場合は、文字**M**を指定します。 省略した場合、指定された範囲は i/o ポート領域にあります。

<a href="" id="memconfig-mem-range--mem-range----"></a>**Memconfig =**<em>メモリ</em>\[範囲 **、**<em>メモリ範囲</em>\]...  
次のいずれかの形式で、デバイスの1つ以上のメモリ範囲を指定します。

```inf
start-end[(attr)] | size@min-max[%align-mask][(attr)]
```

<a href="" id="start"></a>*着手*  
デバイスメモリ範囲の開始 (バス相対) 物理アドレスを、64ビットの16進値として指定します。

<a href="" id="end"></a>*終わり*  
メモリ範囲の終了物理アドレスを指定します。これは、64ビットの16進値としても指定します。

<a href="" id="attr"></a>*attr*  
メモリ範囲の属性を、次の1つ以上の文字として指定します。

| 文字 | 意味                                             |
|--------|-----------------------------------------------------|
| **R**  | 読み取り専用                                           |
| **W**  | 書き込み専用                                          |
| **RW** | 読み取り/書き込み                                          |
| **C**  | 結合書き込み許可                              |
| **H**  | キャッシュ可能                                           |
| **F**  | プリフェッチ可能                                        |
| **D**  | カードデコードのアドレス指定は、24ビットではなく32ビットです。 |

 

**R**と**W**の両方が指定されている場合、またはどちらも指定されていない場合は、読み取り/書き込みが想定されます。

<a href="" id="size-"></a>*幅*   
メモリ範囲に32ビットの16進値として必要なバイト数を指定します。

<a href="" id="min--"></a>*」*   
64ビットの16進値として、デバイスのメモリ範囲の最小有効開始アドレスを指定します。

<a href="" id="max"></a>*制限*  
メモリ範囲の最大有効終了アドレスを64ビットの16進値として指定します。

<a href="" id="align-mask-"></a>*アラマスク*   
必要に応じて、整数 (通常は64ビット) アドレス境界のデバイスメモリ範囲の開始位置を揃えるためにビットごとの AND 演算で使用される64ビットマスクを指定します。

アラマスクを省略した場合、既定のメモリアラインメントは4K 境界 (FFFFF000) になります。

<a href="" id="irqconfig--irqattrs--irqnum--irqnum----"></a>**IRQConfig =**\[*IRQattrs:*\]*IRQNum*\[**、**<em>IRQNum</em>IRQNum\]...  
デバイスがバスによって、エッジによってトリガーされた IRQ を使用する場合、 *IRQattrs*は省略されます。 それ以外の場合は、このエントリに示されている IRQ 行をデバイスが共有できる場合は、 **L**を指定して、レベルでトリガーされる Irq と**LS**を指定します。

*IRQNum*は、デバイスが次のコンマ (,) で区切られた10進数として使用できるバス相対 irq を1つ以上指定します。

<a href="" id="pccardconfig-configindex---memorycardbase1---memorycardbase2----attrs--"></a>**Pccardconfig =**<em>configindex</em>\[**:**\[*MemoryCardBase1*\]\[**:**<em>MemoryCardBase2</em>\]MemoryCardBase2\]**(**<em>attrs</em>(attrs **)** )\[\]  
は、CardBus レジスタを構成します。または、デバイスの属性空間にマップされる永続的なメモリウィンドウを最大2つ作成します。 ドライバーは、メモリウィンドウを使用して、ISR から属性空間にアクセスできます。 すべての数値を16進数形式で指定します。

**Pccardconfig**エントリの要素は次のとおりです。

<a href="" id="configindex"></a>*ConfigIndex*  
PCMCIA バス上のデバイスの8ビット PCMCIA 構成インデックスを指定します。

<a href="" id="memorycardbase1"></a>*MemoryCardBase1*  
必要に応じて、最初のメモリウィンドウの32ビットベースアドレスを指定します。

<a href="" id="memorycardbase2"></a>*MemoryCardBase2*  
必要に応じて、2番目のメモリウィンドウの32ビットベースアドレスを指定します。

<a href="" id="attrs"></a>*attrs*  
必要に応じて、デバイスの1つまたは複数の属性をスペースで区切って指定します。 無効な属性指定子により、 **Pccardconfig**エントリ全体が無効になります。 特定の属性に対して複数の指定子が指定されている場合、属性はデバイスの個々の i/o ウィンドウまたはメモリウィンドウに適用されます。 指定子が1つしか指定されていない場合は、その属性がすべてのウィンドウに適用されます (次の例を参照してください)。

具体的には、複数の指定子が指定されている場合、最初の指定子が左から右に読み取られ、2番目のウィンドウに次の指定子が適用されます。 最大2つの i/o ウィンドウと2つのメモリウィンドウは、1つの**Pccardconfig**エントリによって制御できます。 デバイスに3つ以上のメモリウィンドウがある場合は、2番目の**Pccardconfig**エントリを含める必要があります。

次の属性があります。

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
<td align="left"><p>16ビット i/o データパス。</p>
<p>INF で<strong>Logconfig</strong>ディレクティブが指定されている場合、既定値は8ビットです。 <strong>Logconfig</strong>ディレクティブが指定されていない場合、ドライバーは16ビットの i/o を使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>S</strong><em>n</em></td>
<td align="left"><p>~ IOCS16 source。</p>
<p><em>N</em>が0の場合、~ IOCS16 は datasize ビットの値に基づいています。 N が1の場合、~ IOCS16 はデバイスからの ~ IOIS16 信号に基づいています。 既定値は<strong>S</strong>です。1.</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>Z</strong><em>n</em></td>
<td align="left"><p>I/o 8 ビット、待機状態をゼロにします。</p>
<p><em>N</em>が1の場合、8ビットの i/o アクセスは、追加の待機状態がゼロの場合に発生します。 <em>N</em>が0の場合、追加の待機状態でアクセスが発生します。 このフラグは、16ビットの i/o には意味がありません。 既定値は<strong>Z</strong>です。0.</p></td>
</tr>
<tr class="even">
<td align="left"><strong>Xl</strong><em>n</em></td>
<td align="left"><p>I/o 待機状態。</p>
<p>N が1の場合、1つの追加の待機状態で16ビットシステムアクセスが発生します。 既定値は<strong>Xl</strong>です。1.</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>M</strong></td>
<td align="left">16ビットメモリデータパス。 既定値は8ビットです。</td>
</tr>
<tr class="even">
<td align="left"><strong>M8</strong></td>
<td align="left">8ビットメモリデータパス。</td>
</tr>
<tr class="odd">
<td align="left"><strong>Xm</strong><em>n</em></td>
<td align="left"><p>メモリ待機状態。 n には0、1、2、または3を指定できます。</p>
<p>この値は、メモリウィンドウへの16ビットアクセスに対する追加の待機状態の数を決定します。 既定値は<strong>Xm</strong>です。3.</p></td>
</tr>
<tr class="even">
<td align="left"><strong>A</strong></td>
<td align="left">属性メモリとしてマップされるメモリ範囲。</td>
</tr>
<tr class="odd">
<td align="left"><strong>C</strong></td>
<td align="left">共通メモリとしてマップされるメモリ範囲 (既定値)。</td>
</tr>
</tbody>
</table>

 

たとえば、attrs 値 (WB CA M XM1 XI0) は次のように変換されます。

1番目の i/o ウィンドウは16ビットです

2番目の i/o ウィンドウ8ビット

最初のメモリウィンドウは共通

2番目のメモリウィンドウは属性です

メモリは16ビットです。

メモリウィンドウで1つの待機状態

I/o ウィンドウの待機状態がゼロの場合

<a href="" id="mfcardconfig-configregbase-configoptions--ioresourceindex---attrs-----"></a>**Mfcardconfig =**<em>configregbase</em>**:**<em>configoptions</em>\[**:**<em>IoResourceIndex</em>\]\[**(**<em>attrs</em>**)**\]...次に示すように、多機能デバイスの1つの機能に対して、一連の構成レジスタの属性メモリの場所を指定します。

<a href="" id="configregbase"></a>*ConfigRegBase*  
多機能デバイスのこの機能の構成レジスタの属性オフセットを指定します。

<a href="" id="configoptions-"></a>*ConfigOptions*   
8ビットの PCMCIA 構成オプションの登録を指定します。

<a href="" id="ioresourceindex-"></a>*IoResourceIndex*   
構成 i/o ベースのプログラミングとレジスタの制限に使用するバスドライバーの**Ioconfig**エントリのインデックスを指定します。 このインデックスは0から始まります。つまり、0は、この*ログ構成セクション*の初期**ioconfig**エントリを指定します。

<a href="" id="attrs-"></a>*attrs*   
文字**A**に設定されている場合、は、構成および状態のレジスタで audio enable をオンにするように PCMCIA バスドライバーに指示します。

各**Mfcardconfig**エントリは、多機能デバイスの1つの機能に関する情報を提供します。 一連の**logconfig**ディレクティブが、それぞれが INF の*log-config-section* [ *ddinstall * の個別のログ構成セクションを参照している場合。LogConfigOverride](inf-ddinstall-logconfigoverride-section.md)セクションでは、各*ログ構成セクション*に、同じ順序で一覧表示される、 **mfcardconfig**エントリを含むエントリが含まれている必要があります。

<a name="remarks"></a>解説
-------

**Logconfig**ディレクティブは、製造元ごと、モデルごとの[**inf *ddinstall*セクション**](inf-ddinstall-section.md)、または[**inf *ddinstall*で指定できます。LogConfigOverride セクション**](inf-ddinstall-logconfigoverride-section.md)。

複数の代替論理構成をサポートする非 PnP デバイス用の INF では、通常、 *Ddinstall*セクションの下に一連の*ログ構成セクション*が定義されています。 各*ログ構成セクション*では、個別の論理構成リソースのセットを指定します。 また、 **Configpriority**エントリも含まれています。これは、デバイスとドライバーのパフォーマンスに対する影響、初期化の容易さなどに基づいて各論理構成にランクを付けます。

Pnp デバイスの場合、PnP マネージャーは各 PnP デバイスに論理ハードウェアリソースのセットを割り当てます。 つまり、PnP マネージャーは、システムバスドライバーに対してクエリを実行し、デバイスごとの i/o バス構成リソースが使用されていることをレポートします。また、論理ハードウェアリソースのデバイスごとのセットを割り当てて、そのようなリソースすべての使用において最適なシステム全体のバランスを実現します。

その結果、PnP デバイスの場合、 *Ddinstall*セクションの**logconfig**ディレクティブは無視されます。 PnP デバイス用にバスによって報告されたリソースを上書きするには、 **logconfig**ディレクティブを[ *ddinstall * の下に追加します。LogConfigOverride](inf-ddinstall-logconfigoverride-section.md)セクション。 この場合、バスによって報告されたリソースではなく、*ログ構成セクション*で指定されたリソースが使用されます。

プラットフォーム拡張機能は、 **logconfig**ディレクティブを含む*ddinstall*セクション、または[ *ddinstall * に追加できます。LogConfigOverride](inf-ddinstall-logconfigoverride-section.md)セクション。プラットフォーム固有または OS 固有の論理構成を指定します。 詳細については、「 [INF ファイルの作成](overview-of-inf-files.md)」を参照してください。

指定された*ログ構成セクション*名は inf ファイルに対して一意である必要がありますが、同じデバイスの他の INF *Ddinstall*セクションの**logconfig**ディレクティブで参照できます。 各 INF ライターで作成されたセクション名は、INF ファイル内で一意である必要があります。また、セクション名を定義するための一般的な規則に従う必要があります。 これらの規則の詳細については、「 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)」を参照してください。

各*ログ構成セクション*で使用できる**configpriority**エントリは1つだけです。 デバイスのハードウェアリソース要件に応じて、他の各エントリの1つ以上を指定できます。

1つ以上の**Mfcardconfig =** エントリは、 <em>Ddinstall</em>の**logconfig**ディレクティブによって参照されている*ログ構成セクション*でのみ使用でき**ます。** 多機能デバイス用の INF の LogConfigOverride セクション。 多機能デバイスの INF ファイルの詳細については、「[多機能デバイスのサポート](https://docs.microsoft.com/windows-hardware/drivers/multifunction/index)」を参照してください。

### <a name="logconfig-referenced-section-entries-and-values"></a>LogConfig-参照されたセクションのエントリと値

*ログ構成セクション*から、システムインストーラーはバイナリ論理構成レコードを構築し、レジストリに格納します。

INF ファイルには、デバイスごとの*ログ構成セクション*をいくつでも含めることができます。 ただし、各セクションには、1つのデバイスをインストールするための完全な情報が含まれている必要があります。 一般に、INF は各*ログ構成セクション*のエントリを同じ順序で指定する必要があります。 INF は、ドライバーがデバイスを初期化する方法に最も適した順序でエントリの各セットを指定する必要があります。

特定のデバイスに複数の*ログ構成セクション*が存在する場合、インストール時には、これらの INF セクションのうち1つだけが使用されます。 このような INF ファイルでは、このようなセクションが、このような各*ログ構成セクション*で提供される**configpriority**値と共に使用されます。 つまり、システムインストーラーは INF ファイル内の構成の優先順位を使用しようとしますが、既にインストールされているデバイスとの競合が見つかった場合は、低いランクの論理構成を選択することがあります。

インストール中、特定の*ログ構成セクション*内の各エントリのリソースが1つだけ選択され、特定のデバイスに割り当てられます。 特定のデバイスに同じ種類のリソースが複数必要な場合は、その種類のエントリのセットをその*ログ構成セクション*で使用する必要があります。

たとえば、特定のデバイスに対して2つの i/o ポート範囲を確保するには、そのデバイスの*ログ構成セクション*で2つの**ioconfig =** エントリを指定する必要があります。 一方、デバイスに IRQ が必要でない場合*は、その*INF で**IRQConfig**エントリを省略できます。

<a name="examples"></a>例
--------

この例では、PCMCIA デバイスの有効な**Pccardconfig**エントリをいくつか示します。

```inf
PcCardConfig=0:E0000:F0000(W)
PcCardConfig=0:E0000(M)
PcCardConfig=0::(W)
PcCardConfig=0(W)
```

次の例では、 **Ioconfig**エントリで型1の i/o 範囲を指定しています。 I/o ポート領域を指定します。サイズは8バイトで、1F8、2F8、または3F8 から開始できます。

```inf
IOConfig=1F8-1FF, 2F8-2FF, 3F8-3FF
```

これに対し、この例では、 **Ioconfig**エントリに型2の i/o 範囲が指定されています。 I/o ポート領域は8バイトで、300、308、310、318、320、または328で開始できます。

```inf
IOConfig=8@300-32F%FF8
```

次の例では、4つのポートのデバイスの**Ioconfig**エントリのセットを示しています。各デバイスは、次の中から0x400 バイトでオフセットされた i/o ポート範囲を指定しています。

```inf
IoConfig=0x200-0x21f
IoConfig=0x600-0x61f
IoConfig=0xA00-0xA1f
IoConfig=0xE00-0xE1f
```

次の2つの例は、一般的な**Memconfig**エントリを示しています。

この例では、C0000 または D0000 のいずれかで開始できる32K バイトのメモリ領域を指定します。

```inf
MemConfig=C0000-C7FFF, D0000-D7FFF
```

この例では、64K 境界で始まる32k バイトのメモリ領域を指定します。

```inf
MemConfig=8000@C0000-D7FFF%F0000
```

この例では、システム HDC クラス INF ファイルが汎用の ESDI ハードディスクコントローラーのいくつかの*ログ構成セクション*を設定し、 [ *ddinstall * を使用する方法を示します。](inf-ddinstall-logconfigoverride-section.md)特定の IDE コントローラーの LogConfigOverride セクション。

```inf
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

**Mfcardconfig**エントリを使用する方法の例については、「[不完全な構成レジスタアドレスを持つ PC カードのサポート](https://docs.microsoft.com/windows-hardware/drivers/multifunction/supporting-pc-cards-that-have-incomplete-configuration-register-addres)」を参照してください。

## <a name="see-also"></a>関連項目


[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall *。FactDef**](inf-ddinstall-factdef-section.md)

 

 






