---
title: 分類コールアウトの非同期の処理
description: 分類コールアウトの非同期の処理
ms.assetid: 1026f917-7b21-4b01-8cfd-4d14e92106fe
keywords:
- WFP 分類コールアウトの非同期処理 (WDK Windows フィルタリングプラットフォーム)
- Windows Filtering Platform コールアウトドライバーの WDK、分類のコールアウトの非同期処理
- 保留中の WFP 分類コールアウトの WDK Windows フィルタリングプラットフォーム
- コールアウトの分類 WDK Windows フィルタリングプラットフォーム、非同期処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f029c730dafb842ed99a49dd1e7189731c03dfb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843491"
---
# <a name="processing-classify-callouts-asynchronously"></a>分類コールアウトの非同期の処理


WFP コールアウトドライバーは、ネットワーク操作を承認または拒否したり、ネットワークパケットを許可または破棄したりできます。そのためには、アクションの種類として "**アクション\_許可**"、"取り消し **\_アクション\_続行**"、または " [*classid*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0)\_" コールアウト関数の "\_" アクション **\_ブロック**を返します。 多くの場合、コールアウトドライバーは、classifiable フィールド、メタデータ、パケットなどの情報が、ユーザーモードアプリケーションなどの別のコンポーネントに処理のために転送されるまで、*分類関数から*検査決定を返すことができません。 このような場合は、後で決定を非同期に行う必要があります。

### <a name="general-rules-for-asynchronous-processing"></a>非同期処理の一般的な規則

WFP は、 *classid*関数の非同期処理をサポートしています。 ただし、これを行うためのメカニズムは、レイヤーによって異なります。

<a href="" id="asynchronous-ale-classify-------"></a>**非同期の ALE 分類**   
コールアウトドライバーは、 *classid*から[**FwpsPendOperation0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpspendoperation0)関数を呼び出す必要があります。 非同期操作は、 [**FwpsCompleteOperation0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpscompleteoperation0)関数を呼び出すことによって完了する必要があります。

<a href="" id="asynchronous-packet-classify-------"></a>**非同期パケット分類**   
コールアウトドライバーは、 **\_アクション\_ブロック**を、 *classid*の年関数から返す必要があります。 **FWPS\_分類\_OUT\_フラグ**によってフラグが設定さ\_ます。 ネットワークパケットを参照または複製する必要があります。 非同期操作は、複製または変更されたパケットを reinjecting するか、パケットを暗黙的に破棄することによって完了します。

<a href="" id="asynchronous-ale-classify-that-includes-packets-------"></a>**パケットを含む非同期 ALE 分類**   
前の2つのプロシージャを組み合わせて使用します。分類操作が保留され、パケットが参照または複製されます。また、後で、 *classid*の呼び出しが完了し、複製されたパケットが再挿入または破棄されます。

### <a name="special-cases-and-considerations"></a>特別なケースと考慮事項

<a href="" id="ale-connect-vs--receive-accept-layers-------"></a>**ALE 接続と受信/受け入れレイヤー**   
**FwpsCompleteOperation0**を呼び出して、ale 接続レイヤーで保留分類操作を完了すると (**fwps\_レイヤー\_ale\_AUTH\_connect\_V4**または**FWPS\_layer\_ale\_AUTH\_connect\_V6**)、それぞれの ale 接続レイヤーで ale 再認証分類操作がトリガーされます。 コールアウトドライバーは、この再認証分類操作から検査決定を返す必要があります。 再認証フラグが設定されているかどうかを確認することによって **\_\_\_\_** 、ALE 再認証分類操作を検出できます。

コールアウトドライバーは、 **FwpsCompleteOperation0**によってトリガーされる再認証中に各分類操作の検査決定が検索されるように、保留中の ALE\_AUTH\_CONNECT 分類操作ごとに一意の状態を維持する必要があります。 保留中の ALE\_AUTH\_CONNECT 分類操作中にパケットが参照または複製されている場合 (たとえば、TCP 以外の接続の場合)、再認証が発生した後に再挿入することができます。

ALE 受信/受け入れレイヤーで分類操作を行っているときに**FwpsCompleteOperation0**が呼び出された場合 (**fwps\_レイヤー\_ale\_認証\_受信\_\_V4**または**FWPS\_レイヤー\_ale\_AUTH\_receive\_Accept\_V6**)、 **FwpsCompleteOperation0**は ale 再認証をトリガーしません。 代わりに、変更がフィルターをバイパスするのに十分ではない場合に、複製されたパケットが再挿入受信されると、 *classid*の新しい呼び出しが行われます。 ALE\_受信\_受け入れレイヤーからの自己挿入された複製を許可すると、受信接続が効果的に承認されます。 受信接続を許可しない場合は、 **FwpsCompleteOperation0**を呼び出した後に受信パケットを破棄します。

<a href="" id="ale-reauthorization-------"></a>**ALE 再認証**   
ポリシーの変更 (レイヤーでのフィルターの追加または削除など)、新しい到着インターフェイスの検出、IPsec を使用した接続の再処理などのイベントについて、ALE 接続または受信/受け入れレイヤーでコールアウトドライバーを再分類できます。 このような再認証は、 **FwpsCompleteOperation0**を呼び出すことによって保留することはできません。これを行う必要はありません。 コールアウトドライバーは、前に示したルールを使用して、再認証中に示されているパケットを処理する必要があります。

着信パケットと発信パケットの両方を、ALE\_AUTH\_CONNECT または ALE\_受信\_受け入れレイヤーに再承認できることに注意してください。 たとえば、着信パケットは、ALE\_AUTH\_CONNECT レイヤーで再承認できます。 コールアウトドライバーは、パケットの方向が接続方向と同じであると想定してはいけません。

<a href="" id="ale-flow-established-layers-------"></a>**ALE\_フロー\_確立**されたレイヤー   
非同期処理は、これらのレイヤーではサポートされていません (**fwps\_レイヤー\_ale\_flow\_確立\_V4**または**FWPS\_レイヤー\_ALE\_フロー\_確立**された\_V6)。

<a href="" id="inbound-transport-layers-------"></a>**受信\_トランスポート層**   
コールアウトドライバーは、受信 (受信) トランスポート層 (**fwps\_レイヤー\_受信\_トランスポート\_V4**または**FWPS\_レイヤー\_受信\_トランスポート\_V6**) で、ALE 分類処理を必要とするパケットの非同期処理を実行することはできません。 これにより、フローの作成が妨げられる可能性があります。 WFP が入力方向のトランスポート層で*classid*を呼び出すためのコールアウト関数を呼び出すと、ale 分類処理を必要とするパケットに対して、 **FWPS\_メタデータ\_フィールド\_ale\_分類\_必要**フラグが設定されます。 コールアウトドライバーは、受信\_トランスポート層からのこのようなパケットを許可する必要があります。また、パケットが ALE\_受信\_受け入れレイヤーに達するまで、そのパケットの処理を遅延させる必要があります。

<a href="" id="stream-layers-------"></a>**ストリームレイヤー**   
ストリームレイヤー (**fwps\_レイヤー\_stream\_V4**または**FWPS\_layer\_V6**) では、IP または tcp ヘッダーではなく tcp データセグメントが示されます。\_ また、このストリームレイヤーでは、複数の net バッファーリストのチェーンを、 *classid*関数のコールアウト関数の1回の呼び出しで示すことができます。 WFP は、ストリームレイヤーのコールアウトで使用するために、 [**FwpsCloneStreamData0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsclonestreamdata0)および[**FwpsStreamInjectAsync0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsstreaminjectasync0)という特殊な複製および挿入関数を使用できるようにします。

ストリーミングレイヤーデータは順次配送されるので、ストリームデータがまだ保留中である限り、コールアウトドライバーは引き続きデータの複製と吸収を行う必要があります。 特定のストリームフローに対して非同期操作と同期操作を混在させると、未定義の動作が発生する可能性があります。

 

 





