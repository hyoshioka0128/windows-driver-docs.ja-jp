---
title: INF DDInstall.FactDef セクション
description: このセクションは、エンドユーザーがインストールする可能性のある手動でインストールされた非 PnP デバイスの INF で使用する必要があります。
ms.assetid: df2d46da-4e69-4e3c-b208-1ae0a0f771c9
keywords:
- INF DDInstall. FactDef セクションデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF DDInstall.FactDef Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e793bef975503628e28cd4cc1519a1fd6107d9c2
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223252"
---
# <a name="inf-ddinstallfactdef-section"></a>INF DDInstall.FactDef セクション


**注**  ユニバーサルまたはモバイルのドライバーパッケージを作成する場合、このセクションは無効です。 「[ユニバーサル INF ファイルの使用」を](using-a-universal-inf-file.md)参照してください。

 

このセクションは、エンドユーザーがインストールする可能性のある手動でインストールされた非 PnP デバイスの INF で使用する必要があります。 このセクションでは、このようなカードのバス相対 i/o ポートや IRQ (存在する場合) など、工場出荷時の既定のハードウェア構成設定を指定します。

```inf
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


<a href="" id="configpriority-priority-value"></a>**Configpriority =**<em>Priority-値</em>  
このファクトリの既定の論理構成について、次のいずれかの優先順位値を指定します。

| 優先順位の値 | 意味                                                                                                                                                                                                   |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| FORCECONFIG    | PnP マネージャーがデバイスに割り当てる必要のあるリソースを識別する、強制構成を指定します。                                                                                            |
| 望む        | デバイスの最高のパフォーマンスを提供します。 PnP マネージャーは、この構成を使用してデバイスを動的に構成できます。                                                                                    |
| NORMAL         | は、最適なデバイスパフォーマンスよりも優れていますが、パフォーマンスは必要以上に劣ります。 これは、一般的な優先度の値です。 PnP マネージャーは、この構成を使用してデバイスを動的に構成できます。 |
| 最適で     | デバイスのパフォーマンスが最も低いことを示します。 この構成は望ましくありませんが、機能します。 PnP マネージャーでは、この構成を動的に構成できます。                                              |
| RESTART        | システムの再起動が必要です。                                                                                                                                                                                |
| 再起動         | システムの再起動が必要です。                                                                                                                                                                                |
| 保管済み       | 電源サイクルが必要です。                                                                                                                                                                                   |
| HARDRECONFIG   | ジャンパーの変更が必要です。                                                                                                                                                                                 |
| 固定      | を変更することはできません。                                                                                                                                                                                        |
| DISABLED       | デバイスが無効になっていることを示します。                                                                                                                                                                    |

 

<a href="" id="dmaconfig--dmaattrs--dmanum"></a>**Dmaconfig =**\[<em>DMAattrs</em>**:**\]*dmanum*  
バス相対 DMA チャネルを10進数として指定します。 *DMAattrs*は、デバイスが8ビットの dma チャネルのみを搭載し、デバイスが標準のシステム DMA を使用するバス上で接続されている場合は省略可能です。 それ以外の場合は、32ビット DMA の場合は**D** 、16ビット dma の場合は**W** 、8ビット Dma の場合は**N** 、デバイスでバスマスタ Dma を使用する場合は**M** 、使用する DMA チャネルの種類を示す次の (相互に排他的な) 文字のいずれかを指定できます。 **A**、 **B**、または**F**。**A**、 **B**、または**F**のいずれも指定されていない場合は、標準の DMA チャネルが想定されます。

<a href="" id="ioconfig-io-range"></a>**Ioconfig =**<em>io 範囲</em>  
デバイスの i/o ポート範囲を次の形式で指定します。

```inf
start-end[([decode-mask][:alias-offset][:attr])]
```

<a href="" id="start"></a>*着手*  
I/o ポート範囲の開始アドレス (バス相対) を64ビットの16進値として指定します。

<a href="" id="end-"></a>*終わり*   
I/o ポート範囲の終了アドレスを、64ビットの16進値として指定します。

<a href="" id="decode-mask-"></a>*デコード-マスク*   
エイリアスの種類を定義します。次のいずれかを指定できます。

| マスク値 | 意味         | IOR_Alias 値 |
|------------|-----------------|------------------|
| **3ff**    | 10ビットデコード   | 0x04             |
| **fff**    | 12ビットデコード   | 0x10             |
| **ffff**   | 16ビットデコード   | 0x00             |
| **0**      | 正のデコード | 0xFF             |

 

<a href="" id="alias-offset"></a>*エイリアス-オフセット*  
使用されていません。

<a href="" id="attr"></a>*attr*  
指定された範囲がシステムメモリ内にある場合は、文字**M**を指定します。 省略した場合、指定された範囲は i/o ポート領域にあります。

<a href="" id="memconfig-mem-range"></a>**Memconfig =**<em>メモリ範囲</em>  
デバイスのメモリ範囲を次の形式で指定します。

```inf
start-end[(attr)]
```

<a href="" id="start"></a>*着手*  
デバイスメモリ範囲の開始 (バス相対) アドレスを64ビットの16進値として指定します。

<a href="" id="end-"></a>*終わり*   
メモリ範囲の終了アドレスを指定します。これは、64ビットの16進値としても指定します。

<a href="" id="attr"></a>*attr*  
メモリ範囲の属性を、次の1つ以上の文字として指定します。

-   **R** (読み取り専用)
-   **W** (書き込み専用)
-   **RW** (読み取り/書き込み)
-   **C** (組み合わせた書き込みを許可)
-   **H** (キャッシュ可能)
-   **F** (プリフェッチ可能)
-   **D** (カードデコードのアドレス指定は、24ビットではなく32ビット)

**R**と**W**の両方が指定されている場合、またはどちらも指定されていない場合は、読み取り/書き込みが想定されます。

<a href="" id="irqconfig--irqattrs--irqnum"></a>**IRQConfig =**\[<em>IRQattrs</em>**:**\]*IRQNum*  
デバイスが10進数として使用するバス相対 IRQ を指定します。 デバイスがバスによって、エッジによってトリガーされた IRQ を使用する場合、 *IRQattrs*は省略されます。 それ以外の場合は、レベルでトリガーされる IRQ を示す**L**を指定し、このエントリに示されている irq 線をデバイスが共有できる場合は**LS**を指定します。

<a name="remarks"></a>解説
-------

指定された*Ddinstall*セクションは、INF ファイルの "製造元別*モデル*" セクションのデバイス固有のエントリで参照される必要があります。 正式な構文のステートメントに示されている*インストールセクション名*の大文字と小文字を区別しない拡張機能は、このような<em>ddinstall</em>に挿入でき**ます。** クロスオペレーティングシステムまたはクロスプラットフォームの INF ファイルの FactDef セクション名。 これらのシステム定義の拡張機能の詳細については、「 [INF ファイルの作成](overview-of-inf-files.md)」を参照してください。

このセクションには、1つのデバイスをインストールするための完全なファクトリの既定情報が含まれている必要があります。 INF は、ドライバーがデバイスを初期化する方法に最も適した順序でこの一連のエントリを指定する必要があります。 必要に応じて、特定の種類のエントリを複数含めることができます。

たとえば、2つの DMA チャネルを使用したデバイスの INF では、 <em>Ddinstall</em>に**Dmaconfig =** という2つの行があり**ます。FactDef**セクション。

工場出荷時の既定の論理構成設定を変更できる、手動でインストールされたデバイスの INF ファイルでは、 *Ddinstall*セクションの**logconfig**ディレクティブも使用する必要があります。 一般に、このような INF では、各ログ構成セクションと<em>Ddinstall</em>にエントリを指定する必要があり**ます。FactDef**セクションを同じ順序で並べ替えます。

<a name="examples"></a>例
--------

この**Ioconfig**エントリでは、i/o ポート領域 (サイズは8バイト) を指定します。これは2f8 から開始できます。

```inf
IOConfig=2F8-2FF
```

この**Memconfig**エントリは、D0000 で開始できる32k バイトのメモリ領域を指定します。

```inf
MemConfig=D0000-D7FFF
```

## <a name="see-also"></a>関連項目


[***DDInstall***](inf-ddinstall-section.md)

[**LogConfig**](inf-logconfig-directive.md)

 

 






