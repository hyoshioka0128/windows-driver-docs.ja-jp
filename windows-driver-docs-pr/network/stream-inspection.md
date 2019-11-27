---
title: ストリームの検査
description: ストリームの検査
ms.assetid: 77e152bf-cb6b-4845-9a5e-9c37281f23f1
keywords:
- ストリーム検査 WDK Windows フィルタリングプラットフォーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3ae108552f7a5037d3fe1080dbcba62e5e44a47
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841816"
---
# <a name="stream-inspection"></a>ストリームの検査


## <a name="inline-stream-inspection"></a>インラインストリーム検査


インラインストリーム修飾子では、指定されたデータの一部を許可またはブロックすることによってストリームデータを編集できます。これを行うには、Fwps\_ストリームの**Countbytesenforced**メンバーの値を設定します。 [ **\_コールアウト\_IO\_PACKET0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_stream_callout_io_packet0_)構造体として設定します。これらの関数は、 [*classid*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0)の **\_アクション\_許可**または **.fwp\_\_アクション**を返します。 また、 [**FwpsStreamInjectAsync0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsstreaminjectasync0)関数を呼び出して、ストリームに新しいコンテンツを追加することもできます。 このコンテンツは、新しく追加することも、ブロックされたデータを置き換えることもできます。

指定されたセグメントの中央にあるパターン (たとえば、 *n*バイトの後に*p*バイトの後に*m*バイトが続くパターン) を置き換えるには、次の手順に従います。

1.  コールアウトの*classid*関数は、 *n* + *p* + *m*バイトを使用して呼び出されます。

2.  このコールアウトは、 **Countbytesenforced**メンバーを*n*に設定した場合に**許可\_\_アクション**を返します。

3.  吹き出しの*classid*関数は、 *p* + *m*バイトで再び呼び出されます。 **Countbytesenforced 適用**されている場合は、指定された量よりも少ない場合、WFP は*classid*を再び呼び出します。

4.  *Classid*の年関数から、コールアウトは*FwpsStreamInjectAsync0*関数を呼び出して置換パターン*p '* を挿入します。 次に、このコールアウトは、 **Countbytesenforced 適用**された **\_アクション\_BLOCK**を*p*に設定して返します。

5.  コールアウトの*classid*関数は、 *m*バイトで再び呼び出されます。

6.  このコールアウトは、 **Countbytesenforced 適用**された **\_アクション\_ブロック**を*m*に設定して返します。

指定されたデータが、検査の決定を行うために十分でない場合は、Fwps\_ストリームの**Streamaction**メンバーを設定できます。 [ **\_コールアウト\_IO\_PACKET0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_stream_callout_io_packet0_)構造体を**fwps\_ストリームに設定でき\_ACTION\_より多くの\_データを\_必要があり**ます。また、 **Countbytesrequired**メンバーには、データが再度表示される前に、最低限必要な量の最小値を設定します。 **Streamaction**が設定されている場合、コールアウトは、" *classid* " 関数から **[\_]\_アクション**を返します。

**Fwps\_stream\_アクション\_\_より多くの\_データ**を設定する必要がある場合、WFP は最大 8 MB のストリームデータを蓄積できます。 WFP は、コールアウトの*classid の classid*関数を呼び出してバッファー領域が使い果たされたときに、 **FWPS\_分類\_OUT\_フラグ\_buffer\_LIMIT\_に到達**するフラグを設定します。 後者のフラグが設定されている場合、コールアウトは、指定されたデータを完全に受け入れる必要があります。 コールアウトは**fwps\_STREAM\_** を返さないようにする必要があり\_**fwps\_** によって\_OUT\_フラグが分類され\_\_\_データフラグが\_ない場合に、データを\_必要があります。一連.

フラットバッファーからストリームパターンをスキャンできるようにするために、WFP には[**FwpsCopyStreamDataToBuffer0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpscopystreamdatatobuffer0) utility 関数が用意されています。これにより、指定されたストリームデータを連続したバッファーにコピーできます。

## <a name="out-of-band-stream-inspection"></a>帯域外のストリーム検査


帯域外検査または変更の場合、ストリームコールアウトは、パケットインスペクションコールアウトと同様のパターンに従います。最初に、すべての指定されたストリームセグメントを遅延処理のために複製し、次にこれらのセグメントをブロックします。 検査または変更されたデータは、後でデータストリームに挿入されます。 帯域外でデータを挿入するときに、コールアウトは、指定されたすべてのセグメントの **.fwp\_アクション\_ブロック**を返して、結果として得られるストリームの整合性を保証する必要があります。 アウトオブバンド検査モジュールは、送信データストリームに任意の FIN (送信側からのデータがこれ以上存在しないことを示す) を任意に挿入することはできません。 モジュールが接続を削除する必要がある場合、その*classid の classid*関数は、fwps\_ストリームの**streamaction**メンバー [ **\_コールアウト\_IO\_PACKET0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_stream_callout_io_packet0_)構造体を fwps\_ストリームに設定する必要があり **\_ACTION\_\_接続を削除**します。

ストリームデータは[**net\_buffer\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) chain として示されるため、 [**FwpsCloneStreamData0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsclonestreamdata0)は、net BUFFER list チェーンを操作する[**FwpsDiscardClonedStreamData0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsdiscardclonedstreamdata0)ユーティリティ関数を提供します。

また、受信方向のストリームデータの調整もサポートされています。 コールアウトが受信データレートを維持できない場合は、 **Fwps\_stream\_ACTION**を返すことができます。これにより、ストリームの "一時停止" に遅延\_ます。 その後、 [**FwpsStreamContinue0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsstreamcontinue0)関数を呼び出すことによって、ストリームを "再開" できます。 この関数を使用してストリームを遅延させると、TCP/IP スタックは受信データの ACK 処理を停止します。 これにより、TCP スライディングウィンドウが0方向に減少します。

帯域外ストリーム検査のコールアウトの場合、 **FwpsStreamInjectAsync0**関数の呼び出し中に[**FwpsStreamContinue0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsstreamcontinue0)を呼び出すことはできません。

挿入されたストリームデータは、コールアウトに再表示されませんが、低重みのサブレイヤーからのコールアウトに使用できるようになります。

GitHub の[windows ドライバーサンプル](https://go.microsoft.com/fwlink/p/?LinkId=616507)リポジトリにある[Windows フィルタリングプラットフォームストリームの編集サンプル](https://go.microsoft.com/fwlink/p/?LinkId=617933)は、ストリームレイヤーでインラインおよび帯域外編集を実行する方法を示しています。

**注**  Windows Server 2008 以降では、次のプロセスでのストリームフィルターの削除はサポートされていません。
-   コールアウトが帯域外パケット挿入を実行しています。

-   コールアウトは、Fwps\_ストリームの**Streamaction**メンバーを設定することによってより多くのデータを要求しています。これには、 [ **\_コールアウト\_IO\_PACKET0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_stream_callout_io_packet0_)構造体を**FWPS\_ストリーム\_操作\_必要\_@no ます。__ データ (_s)** \_

-   コールアウトは、Fwps\_ストリームの**Streamaction**メンバー [ **\_コールアウト\_IO\_PACKET0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_stream_callout_io_packet0_)構造体を**FWPS\_ストリーム\_アクション\_遅延**に設定することによってストリームを遅延します。

 

## <a name="dynamic-stream-inspection"></a>動的ストリーム検査


Windows 7 以降では、動的なストリーム検査がサポートされています。 動的ストリーム検査は、新しいストリームの作成と破棄ではなく、既存のストリームデータフローに対して動作します。 動的ストリーム検査を実行できるコールアウトドライバーでは、CALLOUT2 構造体の[**Fwps\_CALLOUT1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_callout1_)または[**Fwps\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_callout2_)の**Flags**メンバーで **\_MID\_stream\_インスペクションフラグ\_許可**するように、[.fwp\_] 吹き出し\_フラグを設定する必要があります。

## <a name="avoiding-unnecessary-inspections"></a>不要な検査の回避


ドライバーが興味を持っている接続でのみストリーム検査を実行する場合、コールアウトは、Fwps の**Flags**メンバーの **\_FLOW フラグに対して、[\_吹き出し\_フラグ\_条件付き\_を**設定でき[ **\_CALLOUT0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_callout0_)構造体。 このコールアウトは、他のすべての接続で無視されます。 パフォーマンスが向上し、ドライバーは不要な状態データを維持する必要がなくなります。

## <a name="stream-layer-waterfall-model"></a>ストリームレイヤーウォーターフォールモデル

WFP のストリームレイヤーは、厳密なウォーターフォールモデルに従います。つまり、このレイヤーのコールアウトは、前のコールアウト (存在する場合) が明示的に許可されている場合にのみ、ストリームセグメントを検査できます。 指定されたセグメントがコールアウトによってブロックされている場合、そのセグメントはストリームから完全に削除され、どのコールアウトも検査できません。

さらに：

1. ストリームレイヤーのすべての検査できないコールアウトは、そのパラメーターで以前に設定された値に関係なく、 *classifyOut*パラメーターの**actionType**メンバーに値を明示的に割り当てる必要があります。
2. *ClassifyOut*パラメーターの**権利**メンバーの**FWPS\_RIGHT\_ACTION\_WRITE**フラグには、WFP ストリームレイヤーには意味がありません。 このレイヤーのコールアウトは、このフラグの存在を確認することはできません。 コールアウトは、 *classifyOut*->**権限**の値に関係なく、指定された*レイヤーデータ*パラメーターを処理できます。

 

 





