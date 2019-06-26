---
title: パケット表示形式
description: パケット表示形式
ms.assetid: 37ee6db6-2f0e-4987-85e9-5362d23d7b27
keywords:
- WDK Windows フィルタ リング プラットフォーム パケットを示す値
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bac82e6838c9578aca4b08635714137ffd453ade
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376423"
---
# <a name="packet-indication-format"></a>パケット表示形式


NDIS net バッファーのリストとして WFP でネットワーク データが示されます ([**NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list))。 **[次へ]** のメンバー、 **NET\_バッファー\_一覧**構造の記述に使用できます、*チェーン*net バッファーのリスト。 WFP は吹き出しに 1 つのネットワーク バッファーのリストのみを示します (つまり、netBufferList -&gt;Next = = **NULL**)、次の場合を除いて。

-   WFP は、Stream の層から、吹き出しに net バッファー リストのチェーンを指定できます。

-   WFP は吹き出しに転送パスで IP パケットのフラグメントのグループは分類と吹き出しに net バッファー リストのチェーンを示します。 チェーン内の各 net バッファー リストには、1 つのフラグメントがについて説明します。

Net バッファー リストは、レイヤーの種類に応じて、パケット全体を記述できますが、WFP は IP ヘッダーの先頭からさまざまなオフセット位置に吹き出しに net バッファーのリストを示します。 たとえば、受信ネットワーク層、IP ヘッダーの後、net バッファー リストが開始中に、受信トランスポート層で、net バッファー リストが表示されるトランスポート ヘッダーの後。 最初の ip アドレスとトランスポート ヘッダーは常に説明されている[ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer) net バッファー リスト内の構造体。

使用して、吹き出しに net バッファーのリストにオフセットが示されます、 **ipHeaderSize**と**transportHeaderSize**のメンバー、 [ **FWPS\_受信\_メタデータ\_VALUES0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/ns-fwpsk-fwps_incoming_metadata_values0_)構造体。 コールアウトは、NDIS 関数を使用して[ **NdisRetreatNetBufferDataStart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisretreatnetbufferdatastart)と[ **NdisAdvanceNetBufferDataStart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisadvancenetbufferdatastart)を調整する、指定された net バッファーのオフセットが一覧表示します。 ただしこの場合、引き出し線取り消す必要があります、オフセットの調整から返す前に、 [ *classifyFn* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nc-fwpsk-fwps_callout_classify_fn0)関数。

呼び出しで、 *classifyFn*送信データは、関数、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list) 1 つ以上含めることができます[ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)構造体、IP パケットをそれぞれについて説明します。 Net のバッファーの一覧でいくつかのパケット (net バッファーなど) が、許容される場合、されないものもありますコールアウト ドライバーを次の操作する必要があります。

1.  クローンを作成し、ネットワーク全体のバッファーの一覧をブロックします。

2.  Net バッファーの許容可能なサブセットを表す新しい net バッファー リストを作成します。

3.  送信パスに戻るには、新しい net バッファー リストを挿入します。

または、引き出し線は、net バッファーの一覧から不要な net バッファーのリンクを解除し、変更の net バッファーの一覧を送信パスに挿入します。 ただし、この場合、コールアウト ドライバー取り消す必要があります net バッファーを複製されたリストには、この変更を呼び出す前に、 [ **FwpsFreeCloneNetBufferList0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsfreeclonenetbufferlist0)関数。 コールアウト ドライバーは、その状態データの一部として元の net バッファー リンケージ情報を保存もする必要があります。

WFP によって使用されるデータのオフセットの詳細については、次を参照してください。[データ オフセット位置](https://docs.microsoft.com/windows-hardware/drivers/network/data-offset-positions)します。

**注**  復号化された IPSec ESP パケットを使用する引き出し線付きのデータ長を使用する必要があります、 [ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)構造を決定する MDL データではなく、パケットの長さ。 データの長さを取得する、 [ **NET\_バッファー\_データ\_長さ**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-data-length)マクロ。 詳細については、次を参照してください。 [IPsec と互換性のあるコールアウト ドライバーの開発](developing-ipsec-compatible-callout-drivers.md)します。

 

 

 





