---
title: IEEE 1394 デバイスの等時性トークのオプション
description: IEEE 1394 デバイスの等時性トークのオプション
ms.assetid: b3df5dd5-9903-48b4-9cb2-17b8d3a08f8f
keywords:
- バス I/O WDK の IEEE 1394 アイソクロナス トーク オプション
- WDK の IEEE 1394 のオプションのバスを説明します。
- WDK の IEEE 1394 ヘッダー バス
- 固定サイズのデータ パケット WDK IEEE 1394 バス
- 可変サイズ データ パケット WDK IEEE 1394 バス
- ヘッダー要素 WDK IEEE 1394 バス
- WDK の IEEE 1394 をバッファー処理します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12ac524be304111e23ac2964158d3662ed58e498
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385762"
---
# <a name="isochronous-talk-options-for-ieee-1394-devices"></a>IEEE 1394 デバイスの等時性トークのオプション





アイソクロナス トーク操作で出力データを整理するための 3 つの方法: ヘッダー、ヘッダー、固定サイズのデータ パケットと可変サイズのデータのパケット ヘッダーを持つパケット。

### <a name="packets-with-no-headers"></a>ヘッダーなしでパケット

既定では、ホスト コント ローラーは、接続されているバッファー内のデータを送信で示される、 **Mdl**のメンバー、 [**アイソクロナス\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/1394/ns-1394-_isoch_descriptor)構造体で、バッファーが接続されている順序。 既定では、ホスト コント ローラーが自動的に分割、バッファー サイズのパケットに以内で指定されている、 **nMaxBytesPerFrame**のバッファーのアイソクロナス メンバー\_記述子構造体。

たとえば、512 バイトのパケットでそのデータを受信するが必要とするデバイスのドライバーが含まれます次バッファーのアイソクロナスの宣言で\_記述子。

```cpp
/* elsewhere, the buffer has declared: */
/*        ISOCH_DESCRIPTOR isoch_descriptor; */
isoch_descriptor->nMaxBytesPerFrame = 512;
```

### <a name="fixed-size-data-packets-with-headers"></a>固定サイズのデータ パケットのヘッダーを含む

一部のデバイスでは、いくつかのヘッダー情報が、デバイスが受け取る各パケットに前置することが必要です。 (このヘッダーの情報が挿入、データの前に、IEEE 1394 標準 isochronous パケット ヘッダーの後です。)、このインスタンスでは、ドライバーは、ヘッダーのバッファーと、データのバッファーをアセンブルし、ホスト コント ローラーが自動的に、ヘッダー、デバイスに送信するデータ パケットを先頭に追加します。 ドライバーは、バッファーには記述子を指定することでヘッダーの一覧が含まれていることを示します\_ヘッダー\_散布図\_ギャザー フラグでは、そのバッファーのアイソクロナス\_記述子構造体。 データ パケットに付加できるヘッダーの 2 種類があります。 固定および可変サイズ。

ドライバーを固定サイズのヘッダーには、ヘッダーのサイズを指定します、 **nMaxBytesPerFrame** 、アイソクロナスのメンバー\_記述子構造体。 ホスト コント ローラーはこのバッファーし、次のバッファーをペアとして扱います。 ヘッダーのバッファーとデータ バッファー。 データ パケットを組み立てます、ときに、データ バッファーからヘッダーのバッファーから 1 つのフレームと 1 つのフレームを受け取りをスプライスする次のデバイスに送信するパケットを形成します。

たとえば、デバイスが 8 バイトのヘッダーの前に各 512 バイトのデータ バッファーが必要です。 ドライバーはアイソクロナスのペアを宣言できます\_記述子構造体の次のようにします。

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

すべてのホスト コント ローラー記述子をサポートする\_ヘッダー\_散布図\_ギャザー フラグ。 ホスト コント ローラーが、サポートしているかを判断するクエリで、バス ドライバー、 [**要求\_取得\_ローカル\_ホスト\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff537644)要求で**nLevel** = GET\_ホスト\_機能します。 バス ドライバーは、ホストを設定\_情報\_サポート\_ISO\_HDR\_の挿入のフラグ、 **HostCapabilities**の GET メンバー\_ローカル\_ホスト\_情報 2 構造を返します。

### <a name="variable-size-data-packets-with-headers"></a>可変サイズ データ パケットとヘッダー

この場合は、固定サイズのパケットの場合と似ています。 固定サイズの場合と、ドライバーが記述子を設定する必要があります\_ヘッダー\_散布図\_ヘッダーのバッファーのアイソクロナス ギャザー フラグ\_記述子は次のように構造体します。

```cpp
isoch_descriptor_1->fulFlags = DESCRIPTOR_HEADER_SCATTER_GATHER;
```

可変サイズの場合、ドライバー、設定する必要がもリソース\_変数\_アイソクロナス\_ペイロード フラグ、 **u.IsochAllocateResources.fulFlags**を割り当てるときの IRB のメンバー使用したリソースを[**要求\_アイソクロナス\_ALLOCATE\_リソース**](https://msdn.microsoft.com/library/windows/hardware/ff537649)要求。

また、可変サイズ データ パケットの場合、ドライバーは、固定サイズの場合と同様のヘッダーのバッファーをアセンブルする必要があります。 ただしを固定サイズのパケットとは異なり、可変サイズのパケット ドライバーする必要がありますレコードの各パケットのサイズでは、スキャッター/ギャザー*ヘッダー要素*の各ヘッダーの先頭に付加します。

ヘッダー要素は、次の構造によって定義されます*1394.h*:

```cpp
typedef struct _IEEE1394_SCATTER_GATHER_HEADER {
  USHORT  HeaderLength;
  USHORT  DataLength;
  UCHAR  HeaderData;
} IEEE1394_SCATTER_GATHER_HEADER, *PIEEE1394_SCATTER_GATHER_HEADER;
```

ヘッダー要素は、ヘッダーの長さとデータの長さの両方を示します。 そのため、可変サイズのデータのパケットで、 **nMaxSizeBytesPerFrame**のメンバー、*データ*記述子が不要になった、個々 のデータ パケットのサイズを示します。 各データ パケット ヘッダーの対応する要素で指定されたサイズが異なることができます。 **NMaxSizeBytesPerFrame**のメンバー、*ヘッダー*記述子は次のように定義されます。

```cpp
IsochDescriptor->nMaxBytesPerFrame = MAX_HEADER_DATA_SIZE+FIELD_OFFSET(HeaderElement,HeaderData)
```

MAX が\_ヘッダー\_データ\_サイズは各データ パケットに追加され、フィールドに、ヘッダーのサイズを示します\_OFFSET(HeaderElement,HeaderData) が挿入されるヘッダー要素の長さを示します直前の各ヘッダー。

定義に関して注意の注意すべき**nMaxBytesPerFrame**ドライバーが「トーク モード」で可変サイズのパケットを転送するたびにします。 2 つのケースでは、ドライバーを定義する必要があります**nMaxBytesPerFrame**、どちらの場合も、ホスト コント ローラー ドライバーに割り当てられた値を解釈および**nMaxBytesPerFrame**として、*最小*フレーム、最大ではなく、サイズの場合は、ドライバーが可変サイズのフレームを送信します。

-   要求中に\_アイソクロナス\_ALLOCATE\_リソース要求に、ドライバーは内のフレーム サイズを示す必要があります、 **u.IsochAllocateResources.nMaxBytesPerFrame**のメンバー [ **IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/1394/ns-1394-_irb)します。

-   要求中に\_アイソクロナス\_アタッチ\_バッファー要求では、ドライバーは内のフレーム サイズを示す必要があります、 **nMaxBytesPerFrame**のメンバー [**アイソクロナス\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/1394/ns-1394-_isoch_descriptor)します。

小さいほど、フレーム、以上のフレームは、ホスト コント ローラーのドライバーが転送バッファーに適合できます。 各フレームは、タイムスタンプ、およびステータス情報などのシステム リソースを必要とするため、フレームが小さいがより迅速にシステム リソースを消費します。 ホスト コント ローラーのドライバーは、バッファー内に収まるフレームの数との値に基づいて、それらのフレームに必要なリソースの数を計算**nMaxBytesPerFrame**します。 フレームがあるよりも小さい場合に指定したサイズ**nMaxBytesPerFrame**このエラーになる可能性やリソースを必要とするフレームの数が、ホスト コント ローラー ドライバーで計算された値よりも大きくなります。

ドライバーがデータを受信するときに、これらの考慮事項が適用されません、ドライバーが可変サイズのフレームを転送場合にのみ「応答モード」。 ドライバーを持つ、チャネルのリソース ハンドルを取得するときに、特定のチャネルに関連付けられているデータ転送の種類を指定する、 [**要求\_アイソクロナス\_ALLOCATE\_のリソース**](https://msdn.microsoft.com/library/windows/hardware/ff537649)要求。 ドライバーの設定、リソース\_変数\_アイソクロナス\_ペイロード フラグ**u.IsochAllocateResources.fulFlags**可変サイズのフレームを送信するかを示すには、この要求中にします。 ドライバーの設定、リソース\_使用\_IN\_説明フラグ**u.IsochAllocateResources.fulFlags**データを受信するのではなく、送信するチャネルを使用することを示す。 のみ、ドライバーでは、これらのフラグの両方を設定、リソース割り当ての要求中には、ホスト コント ローラー ドライバー解釈**nMaxBytesPerFrame**最大値ではなく、最小値として。

なお、 **u.IsochAllocateResources.nMaxBufferSize**のメンバー [ **IRB** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/1394/ns-1394-_irb)は常に、最大値。

ドライバー設定するだけでヘッダーのみのデータ パケットを送信できるようになりました、 **DataLength**を 0 に、ヘッダー要素のメンバー。

```cpp
HeaderElement->DataLength = 0
```

ヘッダーの記述子のバッファーの合計の長さがの通常の方法で示される、 **ulLength**記述子のメンバー。 整数ヘッダー スキャッター/ギャザー要素の数の倍数で。

```cpp
IsochDescriptor->ulLength = IsochDescriptor->nMaxBytesPerFrame * NUMBER_OF_PACKETS;
```

位置番号\_の\_パケットは、(ヘッダーのみのパケット) を含む送信するパケットの数。

3 番目のヘッダー要素の構造体のメンバー **HeaderData**はヘッダー データの開始位置を示すプレース ホルダーだけです。 次の図は、8 バイト CIP ヘッダーの組み立てられたバッファーの例を示します。

![8 バイト cip ヘッダーのバッファーを示す図](images/hdrelem.png)

指定された記述子のすべてのヘッダーは、同じ長さでなければなりません。 これにより、OHCI ポート ドライバー (*ohci1394.sys*) を固定サイズの要素の配列のようにヘッダー記述子を解析します。 データ パケットは、サイズを変更できるが、連続したなし「ホール」である必要があります。

ヘッダーとデータ記述子の両方のデータは、ページに配置する必要があります。 データ パケットのサイズに制限はありませんが、ヘッダーもデータ パケットがページ境界をまたがるを許可します。 ドライバーでは、記述子のバッファーを正しく配置する必要があります*MDL バッファーをセットアップする前に*します。

たとえば、ドライバーは、12 バイト ヘッダーと 4 バイトのヘッダー要素を持つヘッダー記述子をアセンブル場合、各データ パケットは 16 バイトの先頭に追加されたデータがあります。 16 バイトでは、正確に 256 回 4,096 バイトのページに収まる、ため、先頭に追加されたデータは何もこれまでページ境界を 。

その一方で、ドライバーは、8 バイト ヘッダーと 4 バイトのヘッダー要素を持つヘッダー記述子をアセンブル場合、各データ パケットは、12 バイトの先頭に追加されたデータがあります。 4,096 バイトのページが整数ではないため、複数ヘッダー記述子 12 の 4,096 バイトのヘッダーがページの境界をまたぐことを防ぐためにサイズをする必要があります。 ただし、ヘッダーの記述子のバッファーのサイズによって拡張できます。 最大 2 つのページに続く擬似コードに示すように、バッファーのベース アドレスを調整することです。

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

 

 




