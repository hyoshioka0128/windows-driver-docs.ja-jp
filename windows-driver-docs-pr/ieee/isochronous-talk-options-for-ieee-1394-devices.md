---
title: IEEE 1394 デバイスの等時性トークのオプション
description: IEEE 1394 デバイスの等時性トークのオプション
ms.assetid: b3df5dd5-9903-48b4-9cb2-17b8d3a08f8f
keywords:
- アイソクロナス i/o WDK IEEE 1394 bus、トークオプション
- オプション (WDK IEEE 1394 バス)
- ヘッダー WDK IEEE 1394 bus
- 固定サイズのデータパケット WDK IEEE 1394 バス
- 可変サイズデータパケット WDK IEEE 1394 バス
- ヘッダー要素 WDK IEEE 1394 bus
- バッファー WDK IEEE 1394 バス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7eab9ca2f9174e84662a74402280952617643b10
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841532"
---
# <a name="isochronous-talk-options-for-ieee-1394-devices"></a>IEEE 1394 デバイスの等時性トークのオプション





アイソクロナス操作での出力データの整理には、ヘッダーのないパケット、ヘッダーを使用した固定サイズのデータパケット、ヘッダーを使用した可変サイズのデータパケットなど、3つの方法があります。

### <a name="packets-with-no-headers"></a>ヘッダーのないパケット

既定では、ホストコントローラーは、アタッチされたバッファーのデータを送信します。このデータは、 [**ISOCH\_DESCRIPTOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/1394/ns-1394-_isoch_descriptor)構造体の**Mdl**メンバーによって示され、バッファーがアタッチされた順序で送信されます。 既定の場合、ホストコントローラーはバッファーをバッファーの ISOCH\_記述子構造体の**Nmaxbytesperframe**メンバーに指定されているサイズを超えるサイズのパケットに自動的に分割します。

たとえば、512バイトのパケットでデータを受信することを想定しているデバイスのドライバーでは、バッファーの ISOCH\_記述子の宣言に次のものが含まれます。

```cpp
/* elsewhere, the buffer has declared: */
/*        ISOCH_DESCRIPTOR isoch_descriptor; */
isoch_descriptor->nMaxBytesPerFrame = 512;
```

### <a name="fixed-size-data-packets-with-headers"></a>ヘッダーを持つ固定サイズのデータパケット

一部のデバイスでは、デバイスが受信する各パケットの前にヘッダー情報が付加されている必要があります。 (このヘッダー情報はデータの前に挿入されますが、IEEE 1394 標準のアイソクロナスパケットヘッダーの後に挿入されます)。この場合、ドライバーはヘッダーのバッファーとデータのバッファーをアセンブルできます。また、ホストコントローラーは、デバイスに送信するデータパケットにヘッダーを自動的に付加します。 ドライバーは、記述子\_ヘッダーを指定することによって、ヘッダーの一覧が含まれていることを示しています。これは、そのバッファーの ISOCH\_記述子構造体で\_スキャッター\_GATHER フラグを指定することによって行います。 データパケットの前に付加できるヘッダーには、固定サイズと可変サイズの2種類があります。

固定サイズのヘッダーを使用する場合、ドライバーは、ISOCH\_記述子構造体の**Nmaxbytesperframe**メンバーのヘッダーサイズを指定します。 ホストコントローラーは、このバッファーと次のバッファーをペアとして扱います。これはヘッダーバッファーとデータバッファーです。 データパケットをアセンブルするときには、ヘッダーバッファーから1フレームを取得し、データバッファーから1フレームを取得し、それらを連結して、デバイスに送信する次のパケットを形成します。

たとえば、デバイスで512バイトの各データバッファーの前に8バイトのヘッダーがあることが想定されているとします。 ドライバーは、次のように ISOCH\_記述子構造体のペアを宣言できます。

```cpp
/* elsewhere, the buffer has declared: */
/*        ISOCH_DESCRIPTOR isoch_descriptor_1, isoch_descriptor_2; */
/*        #define NUM_HEADERS to be the number of headers included in  */
/*        the first buffer */
 
isoch_descriptor_1->fulFlags = DESCRIPTOR_HEADER_SCATTER_GATHER;
isoch_descriptor_1->ulLength = 8 * NUM_HEADERS;
isoch_descriptor_1->nMaxBytesPerFrame = 8;
       .
       .
       .
isoch_descriptor_2->ulLength = 512 * NUM_HEADERS;
isoch_descriptor_2->nMaxBytesPerFrame = 512;
```

すべてのホストコントローラーが記述子\_ヘッダー\_スキャッター\_GATHER フラグをサポートしているわけではありません。 ホストコントローラーでサポートされているかどうかを判断するには、要求を使用してバスドライバーにクエリを実行し、 **Nlevel** = GET\_HOST\_機能を使用して[ **\_ローカル\_ホストの\_情報要求\_取得**](https://msdn.microsoft.com/library/windows/hardware/ff537644)します。 バスドライバーは、GET\_LOCAL\_HOST\_INFO2 構造体の**Hostcapabilities**メンバーの\_ISO\_HDR\_挿入フラグをサポート\_\_情報をホストに設定します。

### <a name="variable-size-data-packets-with-headers"></a>ヘッダーを持つ可変サイズのデータパケット

この例は、固定サイズのパケットケースに似ています。 固定サイズの場合と同様に、ドライバーでは、次のように、ヘッダーバッファーの ISOCH\_記述子構造で、記述子\_HEADER\_スキャッター\_GATHER フラグを設定する必要があります。

```cpp
isoch_descriptor_1->fulFlags = DESCRIPTOR_HEADER_SCATTER_GATHER;
```

ただし、変数サイズの場合は、ドライバーが要求を使用してリソースを割り当てるときに、IRB の**IsochAllocateResources**に ISOCH\_PAYLOAD フラグのリソース\_\_変数も設定する必要があり[ **\_ISOCH\_リソース要求を\_割り当て**](https://msdn.microsoft.com/library/windows/hardware/ff537649)ています。

また、可変サイズのデータパケットの場合、ドライバーは固定サイズの場合のようにヘッダーのバッファーをアセンブルする必要があります。 ただし、可変サイズのパケットの場合は、固定サイズのパケットとは異なり、ドライバーは各パケットのサイズを、各ヘッダーに付加するスキャッター/gather*ヘッダー要素*に記録する必要があります。

ヘッダー要素は、次のように、 *1394*で見つかった構造によって定義されます。

```cpp
typedef struct _IEEE1394_SCATTER_GATHER_HEADER {
  USHORT  HeaderLength;
  USHORT  DataLength;
  UCHAR  HeaderData;
} IEEE1394_SCATTER_GATHER_HEADER, *PIEEE1394_SCATTER_GATHER_HEADER;
```

Header 要素は、ヘッダーの長さとデータの長さの両方を示します。 このため、可変サイズのデータパケットでは、*データ*記述子の**Nmaxsizebytesperframe**メンバーが個々のデータパケットのサイズを示すことはなくなりました。 各データパケットは、対応するヘッダー要素に示されているサイズとは異なる場合があります。 *ヘッダー*記述子の**Nmaxsizebytesperframe**メンバーは、次のように定義されています。

```cpp
IsochDescriptor->nMaxBytesPerFrame = MAX_HEADER_DATA_SIZE+FIELD_OFFSET(HeaderElement,HeaderData)
```

MAX\_HEADER\_DATA\_SIZE は、各データパケットの先頭に付加するヘッダーのサイズを示します。また、FIELD\_OFFSET (HeaderElement, Headerelement) は、ヘッダー要素の長さをそれぞれの直前に挿入します。項目.

**Nmaxbytesperframe**の定義に関しては、ドライバーが "トークモード" で可変サイズのパケットを送信するたびに、はらみに注意する必要があります。 ドライバーが**Nmaxbytesperframe**を定義する必要があるケースが2つあります。どちらの場合も、ホストコントローラードライバーは、 **nmaxbytesperframe**に割り当てられた値を最大値ではなく、*最小*フレームサイズとして解釈します。サイズが可変のフレームを送信する。

-   要求\_\_\_リソースの要求を割り当てるときに、ドライバーは[**IRB のの**](https://docs.microsoft.com/windows-hardware/drivers/ddi/1394/ns-1394-_irb)の**ISOCH のフレーム**サイズを示す必要があります。

-   \_要求の実行中に\_バッファーの\_をアタッチする要求では、ドライバーは[**ISOCH\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/1394/ns-1394-_isoch_descriptor)の**Nmaxbytesperframe**メンバーのフレームサイズを示す必要があります。

フレームが小さいほど、ホストコントローラードライバーが転送バッファーに格納できるフレームが増えます。 各フレームにはタイムスタンプや状態情報などのシステムリソースが必要であるため、より小さなフレームではシステムリソースがより迅速に消費されます。 ホストコントローラードライバーは、 **Nmaxbytesperframe**の値に基づいて、バッファーに格納されるフレームの数と、それらのフレームに必要なリソースの数を計算します。 **Nmaxbytesperframe**に示されているサイズよりも小さいフレームがある場合、リソースを必要とするフレームの数は、ホストコントローラードライバーによって計算された値よりも大きくなるため、エラーが発生する可能性があります。

これらの考慮事項は、ドライバーがデータを受信するときには適用されません。これは、ドライバーが "トークモード" で可変サイズのフレームを送信する場合のみです。 ドライバーは、要求を使用してチャネルのリソースハンドルを取得するときに、特定のチャネルに関連付けられているデータ転送の種類を指定し[ **\_ISOCH\_\_リソース**](https://msdn.microsoft.com/library/windows/hardware/ff537649)の要求を割り当てます。 ドライバーは、この要求時に**IsochAllocateResources flags**の ISOCH\_PAYLOAD フラグにリソース\_\_変数を設定して、変数サイズのフレームを送信することを示します。 ドライバーは、データを受信するのではなく、チャネルを使用して送信することを示すために、 **IsochAllocateResources フラグ**で\_\_使用されるリソース\_を設定します。 リソース割り当て要求中に、ドライバーがこれらの両方のフラグを設定した場合にのみ、ホストコントローラードライバーは**Nmaxbytesperframe**を最大値ではなく、最小値として解釈します。

[**IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/1394/ns-1394-_irb)の**IsochAllocateResources**メンバーは常に最大値であることに注意してください。

ドライバーは、ヘッダー要素の**DataLength**メンバーをゼロに設定するだけで、ヘッダーのみのデータパケットを送信できるようになりました。

```cpp
HeaderElement->DataLength = 0
```

ヘッダー記述子バッファーの長さの合計は、記述子の**Ullength**メンバーを介して通常の方法で示されます。 この値は、次のようにヘッダーのスキャッター/gather 要素の数の倍数である必要があります。

```cpp
IsochDescriptor->ulLength = IsochDescriptor->nMaxBytesPerFrame * NUMBER_OF_PACKETS;
```

\_パケットの\_数は、送信されるパケットの数です (ヘッダーのみのパケットを含む)。

Header 要素構造の3番目のメンバーである**Headerdata**は、ヘッダーデータの開始位置を示すプレースホルダーにすぎません。 次の図は、8バイトの CIP ヘッダーのアセンブルされたバッファーの例を示しています。

![8バイトの cip ヘッダーのバッファーを示す図](images/hdrelem.png)

特定の記述子のすべてのヘッダーは、同じ長さである必要があります。 これにより、OHCI ポートドライバー (*ohci1394*) は、固定サイズの要素の配列のように、ヘッダー記述子を解析できます。 データパケットはサイズが異なる場合がありますが、"ホール" なしで連続している必要があります。

ヘッダーとデータ記述子の両方のデータは、ページに配置されている必要があります。 データパケットのサイズに制限はありませんが、ヘッダーとデータパケットはどちらもページ境界をまたがることはできません。 ドライバーは、*バッファー用に MDL を設定する前に、* 記述子バッファーを適切に配置する必要があります。

たとえば、ドライバーが12バイトのヘッダー要素と4バイトのヘッダー要素を含むヘッダー記述子をアセンブルする場合、各データパケットの先頭に16バイトのデータが付加されます。 16バイトは4096バイトのページに正確に256回配置されるため、先頭にデータが1つでもページ境界またがっされることはありません。

一方、ドライバーが8バイトのヘッダー要素と4バイトのヘッダー要素を含むヘッダー記述子をアセンブルする場合、各データパケットの先頭に12バイトのデータが付加されます。 4096バイトページは12の整数の倍数ではないため、ヘッダーの及ぶがページ境界から除外されるのを防ぐために、ヘッダー記述子のサイズは4096バイト未満である必要があります。 ただし、次の擬似コードに示すように、バッファーのベースアドレスを調整することで、ヘッダー記述子バッファーのサイズを2ページまで拡張できます。

```cpp
// First find the number of headers (together with header elements)
// that will fit in a page. Use a floor function that rounds down to 
// the nearest integer
PrependData = sizeof(header) + 8; // First two fields of header element take up 8 bytes
NumHeaders =floor(PAGE_SIZE/PrependData);
// By forcing the buffer address defined in the MDL to begin at the appropriate offset,
// the driver can guarantee that the last header in the buffer will be aligned on a page 
// boundary. That way, DMA can continue across at least one page boundary.
r = PAGE_SIZE - (NumHeaders*12).
// BufferAddress = the page-aligned address returned by a memory allocation routine
// Adjust buffer starting address
BufferAddress += r;
isochDescriptor->mdl = IoAllocateMdl(BufferAddress, ... and so on.)
```

 

 




