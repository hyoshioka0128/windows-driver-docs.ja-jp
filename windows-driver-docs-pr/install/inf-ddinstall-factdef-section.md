---
title: INF DDInstall.FactDef セクション
description: このセクションでは、エンドユーザーがインストールされる手動でインストールされている、非 PnP デバイスの INF で使用する必要があります。
ms.assetid: df2d46da-4e69-4e3c-b208-1ae0a0f771c9
keywords:
- INF DDInstall.FactDef セクションのデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF DDInstall.FactDef Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60f599ee65e3f3cd977cdd8a8d474bdd8dd2a6be
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574172"
---
# <a name="inf-ddinstallfactdef-section"></a>INF DDInstall.FactDef セクション


**注**  ユニバーサルまたはモバイルのドライバー パッケージを作成している場合は、このセクションが無効です。 参照してください[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

 

このセクションでは、エンドユーザーがインストールされる手動でインストールされている、非 PnP デバイスの INF で使用する必要があります。 このセクションでは、出荷時の既定のハードウェア構成など、設定、バス相対 I/O ポートと IRQ (ある場合)、このようなカードを指定します。

```ini
[install-section-name.FactDef] |
[install-section-name.nt.FactDef] | 
[install-section-name.ntx86.FactDef] | 
[install-section-name.ntarm.FactDef] |  (Windows 8 and later versions of Windows)
[install-section-name.ntarm64.FactDef] | (Windows 10 version 1709 and later versions of Windows)
[install-section-name.ntia64.FactDef] |  (Windows XP and later versions of Windows)
[install-section-name.ntamd64.FactDef]  (Windows XP and later versions of Windows)
 
ConfigPriority=Priority-Value
[DMAConfig=[DMAattrs:]DMANum]
[IOConfig=io-range]
[MemConfig=mem-range]
[IRQConfig=[IRQattrs:]IRQNum]
... 
```

## <a name="entries"></a>エントリ


<a href="" id="configpriority-priority-value"></a>**ConfigPriority =**<em>優先度値</em>  
この出荷時の既定の論理構成の優先度値は次のいずれかを指定します。

| 優先順位の値 | 説明                                                                                                                                                                                                   |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| FORCECONFIG    | デバイスに割り当てる必要があります、PnP マネージャーのリソースを識別する変更不可の構成を指定します。                                                                                            |
| 必要な        | デバイスの最上位のパフォーマンスを提供します。 PnP マネージャーでは、この構成では、デバイスを動的に構成することができます。                                                                                    |
| NORMAL         | SUBOPTIMAL より大きいデバイスのパフォーマンスが必要なよりも低パフォーマンスを提供します。 これは、一般的な優先度の値です。 PnP マネージャーでは、この構成では、デバイスを動的に構成することができます。 |
| 最適ではないです。     | デバイスの最下位のパフォーマンスを提供します。 この構成が望ましくないは機能します。 PnP マネージャーでは、この構成を動的に構成できます。                                              |
| 再起動        | システムの再起動が必要です。                                                                                                                                                                                |
| 再起動         | システムの再起動が必要です。                                                                                                                                                                                |
| 電源オフ       | 電源サイクルが必要です。                                                                                                                                                                                   |
| HARDRECONFIG   | ジャンパー変更が必要です。                                                                                                                                                                                 |
| 固定      | 変更することはできません。                                                                                                                                                                                        |
| 無効になっています。       | デバイスが無効になっていることを示します。                                                                                                                                                                    |

 

<a href="" id="dmaconfig--dmaattrs--dmanum"></a>**DMAConfig =**\[<em>DMAattrs</em>**:**\]*DMANum*  
10 進数として、バス相対 DMA チャネルを指定します。 *DMAattrs*デバイスが唯一の 8 ビット DMA チャネルを持つバスに接続されているし、デバイスは、標準のシステム DMA を使用する場合は省略可能です。 文字のいずれかを指定、それ以外の場合、 **D**を 32 ビットの DMA **W**を 16 ビットの DMA と**N**を 8 ビットの DMA で**M**デバイスで使用する場合バス マスター DMA を使用する DMA チャネルの種類を示す次の (相互に排他的) 文字のいずれかを使用して。**A**、 **B**、または**F**します。None の場合**A**、 **B**、または**F**が指定すると、標準の DMA チャネルが使用されます。

<a href="" id="ioconfig-io-range"></a>**IOConfig =**<em>io 範囲</em>  
次の形式で、デバイスの I/O ポートの範囲を指定します。

```ini
start-end[([decode-mask][:alias-offset][:attr])]
```

<a href="" id="start"></a>*開始*  
64 ビットの 16 進数値として I/O ポートの範囲の (バスを基準) 開始アドレスを指定します。

<a href="" id="end-"></a>*終わり*   
64 ビットの 16 進値としても、I/O ポートの範囲の終了アドレスを指定します。

<a href="" id="decode-mask-"></a>*デコード マスク*   
別名型を定義して、次のいずれかを指定できます。

| マスクの値 | 説明         | IOR_Alias 値 |
|------------|-----------------|------------------|
| **3ff**    | 10 ビットをデコードします。   | 0x04             |
| **fff**    | 12 ビットをデコードします。   | 0x10             |
| **ffff**   | 16 ビットをデコードします。   | 0x00             |
| **0**      | 正の値をデコードします。 | 0 xff の場合             |

 

<a href="" id="alias-offset"></a>*エイリアスのオフセット値*  
使用されません。

<a href="" id="attr"></a>*attr*  
文字を指定**M**システム メモリ内での指定した範囲がある場合。 省略した場合、指定された範囲は I/O ポートの領域では。

<a href="" id="memconfig-mem-range"></a>**MemConfig=**<em>mem-range</em>  
次の形式で、デバイスのメモリの範囲を指定します。

```ini
start-end[(attr)]
```

<a href="" id="start"></a>*開始*  
64 ビットの 16 進値として、デバイスのメモリの範囲の開始 (バスを基準) アドレスを指定します。

<a href="" id="end-"></a>*終わり*   
64 ビットの 16 進値としても、メモリの範囲の終了アドレスを指定します。

<a href="" id="attr"></a>*attr*  
1 つまたは複数の次の文字として、メモリ範囲の属性を指定します。

-   **R** (読み取り専用)
-   **W** (書き込み専用)
-   **RW** (読み取り/書き込み)
-   **C** (書き込みが許可されている結合)
-   **H** (キャッシュ可能)
-   **F** (プリフェッチ可能な)
-   **D** (カードのデコードの代わりに 32 ビット アドレス指定が 24 ビット)

両方**R**と**W**が指定されてか、どちらも指定しない場合、読み取り/書き込みが想定されています。

<a href="" id="irqconfig--irqattrs--irqnum"></a>**IRQConfig =**\[<em>IRQattrs</em>**:**\]*IRQNum*  
10 進数として、デバイスを使用するバス相対 IRQ を指定します。 *IRQattrs*デバイス bus 相対の edge によってトリガーされる IRQ を使用している場合を省略するとします。 それ以外の場合、指定**L**レベルによってトリガーされる IRQ を示すと **%.*ls**場合は、デバイスは、このエントリで示された IRQ 行を共有できます。

<a name="remarks"></a>コメント
-------

指定した*DDInstall* - 製造元でデバイスに固有のエントリでは、セクションを参照する必要があります*モデル*INF ファイルのセクション。 大文字の拡張機能を*インストール セクション名*に示すように正式な構文でステートメントを挿入できる、 <em>DDInstall</em>**します。FactDef**クロス オペレーティング システムやクロス プラットフォーム INF ファイルでセクション名。 これらのシステム定義された拡張機能の詳細については、[INF ファイルを作成する](overview-of-inf-files.md)を参照してください。

このセクションでは、1 つのデバイスをインストールするための完全な工場出荷時の既定の情報を含める必要があります。 INF では、このドライバーがそのデバイスを初期化する方法に適した最高の順序でエントリのセットを指定する必要があります。 必要に応じて、特定の種類のエントリの 1 つ以上のことができます。

たとえば、2 つの DMA チャネルを使用するデバイスの INF があるが 2 つ**DMAConfig =** 内の行の<em>DDInstall</em>**します。FactDef**セクション。

手動でインストールされたデバイスを出荷時の既定の論理構成設定を変更できますの INF ファイルを使用する必要がありますも、 **LogConfig**ディレクティブで、 *DDInstall*セクション。 一般に、このような INF する必要がありますエントリを指定して各ログの構成セクションとでその<em>DDInstall</em>**します。FactDef**セクションと同じ順序で。

<a name="examples"></a>使用例
--------

これは、 **IOConfig**エントリは、I/O ポート リージョン 2F8 で開始できますが、サイズ 8 バイトを指定します。

```ini
IOConfig=2F8-2FF
```

これは、 **MemConfig** D0000 で開始できますが 32 K バイトのメモリ領域を指定します。

```ini
MemConfig=D0000-D7FFF
```

## <a name="see-also"></a>関連項目


[***DDInstall***](inf-ddinstall-section.md)

[**LogConfig**](inf-logconfig-directive.md)

 

 






