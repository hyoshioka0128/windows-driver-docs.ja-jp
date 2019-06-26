---
title: クライアント ドライバー スタックの IEC-61883 プロトコル ドライバー
description: クライアント ドライバー スタックの IEC-61883 プロトコル ドライバー
ms.assetid: cee0c0ee-7326-421c-af5a-b483c878b289
keywords:
- IEC 61883 クライアント ドライバー WDK IEEE 1394 バス
- 61883 WDK IEEE 1394 バス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4375607a13af97ae75a87115a30d7c5604999072
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385786"
---
# <a name="iec-61883-protocol-driver-in-a-client-driver-stack"></a>クライアント ドライバー スタックの IEC-61883 プロトコル ドライバー





IEC 61883 クライアント ドライバーが依存*61883.sys* IEC 61883 プロトコルを使用して自分のデバイスと通信します。

次の図の例を示しています、 *61883.sys* AV/C のドライバー スタックにします。 AV/C サブユニットのベンダーから提供されたドライバーは、この例では IEC 61883 クライアントです。

![iec 61883 クライアントのドライバー スタックを示す図](images/61883stk.png)

図の上部から開始。

-   Stream クラス ドライバー, *stream.sys*DVD、ビデオのキャプチャ、および外部サウンド デバイスなどのデバイス ドライバーをストリーミングするカーネルをサポートしています。 ストリーム クラスのドライバーが記載されて、[ストリーミング ミニドライバー](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)します。

-   この例では、IEC 61883 クライアントは、ベンダーから提供された AV/C サブユニット ドライバーです。 これは、 [Stream ミニドライバーの書き込み](https://docs.microsoft.com/windows-hardware/drivers/stream/writing-a-stream-minidriver)AV/C のスタックの下位のドライバーによって提供される機能を使用して、そのデバイスを制御します。 (AV/C サブユニット ドライバーの詳細については、次を参照してください[AV/C クライアント ドライバー](https://docs.microsoft.com/windows-hardware/drivers/stream/av-c-client-drivers2)。)。

    AV/C サブユニット ドライバーのセットアップでは、接続およびストリームを接続し、サブユニット コントロール、状態、および通知を公開します。 ピン留めする汎用的なプロパティのセットとデバイス固有のプロパティとイベントのセットを公開するのに framework をストリーミングするカーネルを使用します。

-   AV/C ストリーム フィルター ドライバー、 *avcstrm.sys*サブユニットのドライバーの処理をストリームに固有の書式を分離 WDM フィルター ドライバーします。 AV/C ストリーム フィルター ドライバーは、サード パーティ製の INF ファイルで下位のドライバーとして指定されます。 サブユニット ドライバーの DV および MPEG ストリームの形式をサポートし、CMP ヘルパー関数を組み合わせて提供*avc.sys*します。 また、カーネル ストリーミング データの構造とデータの積集合のハンドラーを提供します。

-   AV/C プロトコル ドライバー、 *avc.sys*、WDM Irp をマップ AV/C コマンドについては、(たとえば、サブユニットがビジー状態)、要求は Irp とにルート応答に保留中として中間の応答を処理する再試行の種類、ID、に基づいて正しいサブユニット ドライバーおよびオペレーション コード。 Microsoft Windows XP 以降、 *avc.sys*プラグ接続の管理も提供します。 (AV/C プロトコルの Microsoft が提供するサポートの詳細については、次を参照してください[AV/C クライアント ドライバー](https://docs.microsoft.com/windows-hardware/drivers/stream/av-c-client-drivers2)。)。

-   IEC 61883 プロトコル ドライバー、 *61883.sys*、関数制御プロトコル (FCP)、共通 isochronous パケット (CIP) の形式、および接続管理の手順 (CMP) 処理要求の送信、AV/C ドライバー スタック。

-   1394 バス ドライバー、 *1394bus.sys*、IEEE 1394 バス上のデバイスを列挙し、プラグ アンド プレイし、ユーザーに代わって power management Irp に応答します。

-   ホスト コント ローラーのポートのドライバーでは、IEEE 1394 バス ハードウェアに依存しないインターフェイスを提供します。 ポート ドライバーでは、一部の Irp を処理し、マザーボードのホスト コント ローラーのポート ドライバーに他のユーザーを転送します。 Microsoft 提供の標準ポート ドライバー *ohci1394.sys*、条件を満たすホスト コント ローラーの*1394 オープン ホスト コント ローラー インターフェイス仕様*、これは、からダウンロードできます[IEEE 1394 テクノロジ](https://go.microsoft.com/fwlink/p/?linkid=8729)web サイト。

AV/C サブユニット ドライバーは、IEC 61883 クライアント ドライバーの種類の 1 つにすぎません。 別の例には、IEC 61883 の上に配置 HAVi プロトコルを使用するドライバーがあります。 *61883.sys* 、IEC 61883 プロトコルには、すべて AV/C または HAVi の依存関係のクライアントはありません。 *61883.sys*さまざまな制約の下で動作できます。 たとえば、AV/C サブユニット ドライバーは、通常、クライアントの*avc.sys*FCP 関連の機能を提供して、FCP 関連の要求の送信からブロック上のレベルのドライバーによって処理されるスタックの下、 *61883.sys*.

 

 




