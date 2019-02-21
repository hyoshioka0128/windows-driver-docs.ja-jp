---
title: dma
description: Dma 拡張機能では、ダイレクト メモリ アクセス (DMA) サブシステムおよび Driver Verifier の DMA の検証オプションについての情報が表示されます。
ms.assetid: 4ccf679f-5804-4644-935a-18ff8711ae9a
keywords:
- DMA の検証 (Driver Verifier)
- Windows デバッグ dma
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dma
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 87d2e51a4c4170d2d4a22b91b52d3802270b4546
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532257"
---
# <a name="dma"></a>! dma


**! Dma**拡張機能は、ダイレクト メモリ アクセス (DMA) サブシステムに関する情報を表示し、 **DMA Verifier** Driver Verifier のオプション。

```dbgcmd
!dma 
!dma Adapter [Flags]
```

## <a name="span-idddkdmapgspanspan-idddkdmapgspanparameters"></a><span id="ddk__dma_pg"></span><span id="DDK__DMA_PG"></span>パラメーター


<span id="_______Adapter______"></span><span id="_______adapter______"></span><span id="_______ADAPTER______"></span> *アダプター*   
表示される DMA アダプターの 16 進数のアドレスを指定します。 これは、0、DMA のすべてのアダプターが表示されます。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
表示に含める情報を指定します。 次のビットの任意の組み合わせを指定できます。 既定では 0x1 です。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
汎用アダプターの情報が追加表示をによりします。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
マップの登録情報が追加ディスプレイをによりします。 (だけ DMA の検証がアクティブです。)

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>ビット 2 (0x4)  
バッファーの一般的な情報が追加ディスプレイをによりします。 (だけ DMA の検証がアクティブです。)

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>ビット 3 (0x8)  
スキャッター/ギャザー一覧の情報が追加ディスプレイをによりします。 (だけ DMA の検証がアクティブです。)

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>ビット 4 (0x10)  
ハードウェア デバイスのデバイスの説明が表示をによりします。 (だけ DMA の検証がアクティブです。)

<span id="Bit_5__0x20_"></span><span id="bit_5__0x20_"></span><span id="BIT_5__0X20_"></span>Bit 5 (0x20)  
待機コンテキスト ブロック情報が追加ディスプレイをによりします。

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
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

Driver Verifier については、Windows Driver Kit (WDK) ドキュメントを参照してください。 DMA の詳細については、Windows Driver Kit (WDK) ドキュメントを参照してくださいと*Microsoft Windows internals 』* Mark Russinovich David Solomon、します。 (これらのリソースできない場合がありますのいくつかの言語および国。)

<a name="remarks"></a>注釈
-------

引数が無効です (たとえば、 **! dma 1**) 簡単なヘルプ テキストを生成します。

ときに、 **! dma**パラメーターなしで拡張機能が使用される、DMA のすべてのアダプターとその住所の正確な一覧が表示されます。 このコマンドの長いバージョンで使用するため、アダプターのアドレスを取得するために使用できます。

この拡張機能をする方法の例を次に示す際に使用される Driver Verifier の**DMA の検証**オプションがアクティブ。

```dbgcmd
0:kd> !dma

Dumping all DMA adapters...

Adapter: 82faebd0     Owner: SCSIPORT!ScsiPortGetUncachedExtension 
Adapter: 82f88930     Owner: SCSIPORT!ScsiPortGetUncachedExtension 
Adapter: 82f06cd0     Owner: NDIS!NdisMAllocateMapRegisters 
Master adapter: 80076800
```

この出力から、システムの 3 つの DMA アダプターがあることがわかります。 SCSIPORT を所有する 2 つと、NDIS は、3 つ目を所有しています。 NDIS アダプターの詳細を確認するには、使用、 **! dma**アドレスを持つ拡張機能。

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

データの最初のブロックは、問題をデバッグする HAL の開発者が使用できる特定の情報です。 「Dma の検証ツールの追加情報」の下のデータが、目的には興味深いです。 この例では、NDIS が 0x840 マップ レジスタを割り当てられることが表示されます。 これは、NDIS の 2 つのマップのレジスタの最大値を使用することが予定されていた示されるため、特に膨大な数です。 どうやら、このアダプターは、スキャッター/ギャザーのリストを使用しませんし、そのアダプターのすべてのチャネルを作るにします。 さらに詳しくマップ レジスタを見てください。

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

この例では、特定のマップのレジスタが割り当てられていることが表示されます。 各*マップ登録ファイル*がドライバーによってマップ レジスタ割り当てられます。 つまり、1 回の呼び出しを表す**AllocateAdapterChannel**します。 NDIS は、一部のドライバーを作成してそれらの dispose の日時に 1 つが終了したら、これらのマップ登録ファイルの数が多いを収集します。

マップの登録ファイルも、デバイス名"MapRegisterBase"の下に返されるアドレス。 DMA の検証ツールが各ドライバーの最初の 64 個のマップ レジスタのみフックすることに注意してください。 (各マップ レジスタは、次の 3 つの物理ページを表します) 領域の上の理由から残りの部分は無視されます。

この例では、2 つのマップのファイルが使用されて登録をします。 これは、ハードウェアに表示されるように、ドライバーでバッファーがマップすることを意味します。 最初のケースでは、0xBC バイトは、システムの仮想アドレス 0xF83C003C にマップされます。

一般的なバッファーの検査が表示されます。

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

これはかなり単純です。さまざまな長さの 4 つの一般的なバッファーがあります。 物理および仮想のアドレスがすべて提供されます。

 

 





