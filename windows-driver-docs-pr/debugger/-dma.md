---
title: dma
description: Dma 拡張機能には、ダイレクトメモリアクセス (DMA) サブシステムに関する情報と、Driver Verifier の DMA 検証オプションが表示されます。
ms.assetid: 4ccf679f-5804-4644-935a-18ff8711ae9a
keywords:
- DMA の検証 (ドライバーの検証ツール)
- dma Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dma
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c1d4a83031e8d8b568f93c92d8b8cdd95b741187
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025274"
---
# <a name="dma"></a>!dma


**! Dma**拡張機能には、ダイレクトメモリアクセス (dma) サブシステムに関する情報と、Driver Verifier の**dma 検証**オプションが表示されます。

```dbgcmd
!dma 
!dma Adapter [Flags]
```

## <a name="span-idddk__dma_pgspanspan-idddk__dma_pgspanparameters"></a><span id="ddk__dma_pg"></span><span id="DDK__DMA_PG"></span>パラメータ


<span id="_______Adapter______"></span><span id="_______adapter______"></span><span id="_______ADAPTER______"></span>*アダプター*   
表示する DMA アダプターの16進数のアドレスを指定します。 0の場合は、すべての DMA アダプターが表示されます。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*フラグ*   
表示に含める情報を指定します。 これは、次のビットの任意の組み合わせにすることができます。 既定値は0x1 です。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
表示に汎用アダプター情報が含まれるようにします。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
表示にマップレジスタ情報が含まれるようにします。 (DMA 検証がアクティブである場合のみ)。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>ビット 2 (0x4)  
表示に共通のバッファー情報が含まれるようにします。 (DMA 検証がアクティブである場合のみ)。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>ビット 3 (0x8)  
表示にスキャッター/ギャザーリスト情報が含まれるようにします。 (DMA 検証がアクティブである場合のみ)。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>ビット 4 (0x10)  
ハードウェアデバイスのデバイスの説明が表示されます。 (DMA 検証がアクティブである場合のみ)。

<span id="Bit_5__0x20_"></span><span id="bit_5__0x20_"></span><span id="BIT_5__0X20_"></span>ビット 5 (0x20)  
表示に待機コンテキストブロック情報が含まれるようにします。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>利用不可</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts .dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ドライバーの検証機能の詳細については、Windows Driver Kit (WDK) のドキュメントを参照してください。 DMA の詳細については、Windows Driver Kit (WDK) のドキュメントおよび*Microsoft windows の内部*(Mark Russinovich David ソロモン) を参照してください。

<a name="remarks"></a>コメント
-------

無効な引数 (例、 **! dma 1**) は、簡単なヘルプテキストを生成します。

パラメーターなしで **! dma**拡張を使用すると、すべての dma アダプターとそのアドレスの簡潔な一覧が表示されます。 これは、このコマンドの長いバージョンで使用するアダプターのアドレスを取得するために使用できます。

ドライバー検証ツールの**DMA 検証**オプションがアクティブになっている場合に、この拡張機能を使用する方法の例を次に示します。

```dbgcmd
0:kd> !dma

Dumping all DMA adapters...

Adapter: 82faebd0     Owner: SCSIPORT!ScsiPortGetUncachedExtension 
Adapter: 82f88930     Owner: SCSIPORT!ScsiPortGetUncachedExtension 
Adapter: 82f06cd0     Owner: NDIS!NdisMAllocateMapRegisters 
Master adapter: 80076800
```

この出力から、システムに3つの DMA アダプターがあることがわかります。 SCSI ポート2と NDIS は、3番目のを所有します。 NDIS アダプターの詳細を確認するには、次のように、 **! dma**拡張機能とそのアドレスを使用します。

```dbgcmd
0:kd> !dma  82f06cd0
Adapter: 82f06cd0     Owner: NDIS!NdisMAllocateMapRegisters (0x9fe24351)
 MasterAdapter:       00000000
   Adapter base Va      00000000
   Map register base:   00000000
 WCB:                 82f2b604
   Map registers: 00000000 mapped, 00000000 allocated, 00000002 max

   Dma verifier additional information:
   DeviceObject: 82f98690
   Map registers:        00000840 allocated, 00000000 freed
   Scatter-gather lists: 00000000 allocated, 00000000 freed
   Common buffers:       00000004 allocated, 00000000 freed
   Adapter channels:     00000420 allocated, 00000420 freed
   Bytes mapped since last flush: 000000f2
```

最初のデータブロックは、HAL 開発者が問題をデバッグするために使用できる固有の情報です。 目的に応じて、"Dma 検証ツールの追加情報" の下にあるデータは興味深いものです。 この例では、NDIS によって0x840 マップレジスタが割り当てられていることがわかります。 これは、特に、最大2つのマップレジスタを使用することが計画されていることを示すため、非常に大きな数値です。 このアダプターは、スキャッター/ギャザーリストを使用せず、すべてのアダプターチャネルを使用しません。 マップレジスタの詳細については、次を参照してください。

```dbgcmd
0:kd> !dma  82f06cd0 2
Adapter: 82f06cd0     Owner: NDIS!NdisMAllocateMapRegisters 
...

  Map register file 82f06c58 (0/2 mapped)
     Double buffer mdl: 82f2c188
     Map registers:
        82f06c80: Not mapped
        82f06c8c: Not mapped

  Map register file 82f06228 (1/2 mapped)
     Double buffer mdl: 82f1b678
     Map registers:
        82f06250: 00bc bytes mapped to f83c003c
        82f0625c: Not mapped

  Map register file 82fa5ad8 (1/2 mapped)
     Double buffer mdl: 82f1b048
     Map registers:
        82fa5b00: 0036 bytes mapped to 82d17102
        82fa5b0c: Not mapped
...
```

この例では、特定のマップレジスタがマップされていることがわかります。 各*マップレジスタファイル*は、ドライバーによってマップレジスタが割り当てられます。 つまり、 **Allocateadapterchannel**の1回の呼び出しを表します。 NDIS は、多数のマップレジスタファイルを収集します。一部のドライバーでは、それらを一度に1つずつ作成し、完了時に破棄します。

マップレジスタファイルは、"MapRegisterBase" という名前の下にあるデバイスに返されるアドレスでもあります。 DMA 検証ツールでは、各ドライバーの最初の64マップレジスタのみがフックされることに注意してください。 領域の理由では、残りは無視されます (各マップレジスタは3つの物理ページを表します)。

この例では、2つのマップレジスタファイルが使用されています。 これは、ドライバーがハードウェアから認識できるようにバッファーをマップしたことを意味します。 最初の例では、0xBC バイトはシステム仮想アドレス0xF83C003C にマップされます。

共通バッファーを調べると、次のようになります。

```dbgcmd
0:kd> !dma  82f06cd0 4
Adapter: 82f06cd0     Owner: NDIS!NdisMAllocateMapRegisters 
...
   Common buffer allocated by NDIS!NdisMAllocateSharedMemory:
      Length:           1000
      Virtual address:  82e77000
      Physical address: 2a77000

   Common buffer allocated by NDIS!NdisMAllocateSharedMemory:
      Length:           12010
      Virtual address:  82e817f8
      Physical address: 2a817f8

   Common buffer allocated by NDIS!NdisMAllocateSharedMemory:
      Length:           4300
      Virtual address:  82e95680
      Physical address: 2a95680

   Common buffer allocated by NDIS!NdisMAllocateSharedMemory:
      Length:           4800
      Virtual address:  82e9d400
      Physical address: 2a9d400
```

これは非常に簡単です。長さが異なる4つの一般的なバッファーがあります。 物理アドレスと仮想アドレスはすべて指定されています。

 

 





