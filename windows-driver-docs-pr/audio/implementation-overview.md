---
title: 実装の概要
description: このトピックでは、ハードウェア オフロードされたオーディオ ストリームを処理できるオーディオのアダプターのドライバーを開発する際に、対応する必要のある実装重要な点の概要を示します。
ms.assetid: B93B9A6D-7317-482B-A0B8-298CE8F21193
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb5fcb1a691f139e962039c0d64889ed0c5381c4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532132"
---
# <a name="implementation-overview"></a>実装の概要


このトピックでは、ハードウェア オフロードされたオーディオ ストリームを処理できるオーディオのアダプターのドライバーを開発する際に、対応する必要のある実装重要な点の概要を示します。

## <a name="span-idthenewksfiltertopologyspanspan-idthenewksfiltertopologyspanspan-idthenewksfiltertopologyspanthe-new-ks-filter-topology"></a><span id="The_New_KS_Filter_Topology"></span><span id="the_new_ks_filter_topology"></span><span id="THE_NEW_KS_FILTER_TOPOLOGY"></span>新しい KS フィルター トポロジ


Windows 8 およびそれ以降のオペレーティング システムでは、オンボード ハードウェア オーディオ エンジンを使用して、オーディオ ストリームを処理できるオーディオのアダプターの新しい型のサポートが指定されています。 このようなオーディオ アダプターを開発する際に関連付けられているオーディオ ドライバーは、オーディオ システムは、検出、使用、および正しくこのアダプターとそのドライバーの機能を公開できるように、特定の方法でこの事実をユーザー モードのオーディオ システムを公開する必要があります。

これらの新しいオーディオ アダプターのハードウェア機能を公開するオーディオ ドライバーを可能には、Windows 8 には、ドライバーを使用する必要がある、新しい KS フィルター トポロジが導入されています。

![新しい ks フィルター トポロジ、プロセスの入力ピン、オフロードされたオーディオ入力ピン、およびループバックの出力ピンにホストを表示します。 オーディオ処理がオフロードされたオーディオのオーディオ ストリームに適用し、ホスト プロセス pins.the ループバック パスはの最終処理ステージの出力から取得され、ks フィルター トポロジから直接つながります。 他の 2 つは、dac を使用し、ks フィルター トポロジからフローをストリームします。](images/audio-engine-ksftopology.png)

前の図に示すように、KS フィルター トポロジは、ハードウェアによるデータのパスを表すし、もそれらのパスで使用できる関数を示しています。 オフロードされたオーディオを処理できるオーディオ アダプターの場合、次のような入力と出力を (ピンと呼ばれます) にある KS フィルター。

-   1 つのホスト プロセスのピン留めします。 これは、ソフトウェアのオーディオ エンジンからは、KS フィルターへの入力を表します。

-   Loopback pin は 1 つ。 Windows の音声セッション API (WASAPI) 層に、ハードウェアのオーディオ エンジンから出力を表します。

-   Offloaded オーディオ ピンの数。 図には、この型の 1 つだけの pin が表示されます、IHV は pin の任意の数 (n) を実装するために無料に。

この新しい種類の KS フィルター トポロジ内のピンの詳細については、次を参照してください。[アーキテクチャの概要](architectural-overview.md)します。
オーディオのアダプターとそのドライバーの検出には、「リード」、AudioEndpointBuilder がユーザー モード オーディオ システムで実際のサービスです。 AudioEndpointBuilder サービス モニター、 **KSCATEGORY\_オーディオ**デバイス インターフェイスの到着と削除のためのクラス。 オーディオ ドライバーでの新しいインスタンスを登録するときに、 **KSCATEGORY\_オーディオ**デバイス インターフェイス クラスでは、デバイス インターフェイスの到着の通知が発生します。 AudioEndpointBuilder サービスでは、デバイス インターフェイスの到着の通知を検出し、適切なアクションを実行できるように、システムのオーディオ デバイスのトポロジを検査するアルゴリズムを使用します。

オフロードされたオーディオの処理に対応しているアダプターをサポートするために、オーディオ ドライバーを開発する際に、ドライバーが新たに定義されたを使用する必要がありますように[ **KSNODETYPE\_オーディオ\_エンジン**](https://msdn.microsoft.com/library/windows/hardware/hh450866)ハードウェア オーディオ エンジンの機能を公開するオーディオのエンドポイント。 オーディオのエンドポイントの検出プロセスの詳細については、次を参照してください。[オーディオ エンドポイント ビルダー アルゴリズム](audio-endpoint-builder-algorithm.md)します。

## <a name="span-iduserinterfaceconsiderationsspanspan-iduserinterfaceconsiderationsspanspan-iduserinterfaceconsiderationsspanuser-interface-considerations"></a><span id="User_Interface_Considerations"></span><span id="user_interface_considerations"></span><span id="USER_INTERFACE_CONSIDERATIONS"></span>ユーザー インターフェイスに関する考慮事項


オフロードされたオーディオを処理できるオーディオのアダプターの基になるハードウェアの能力を制御する、オーディオ ドライバーを開発しました。 これは、ドライバーが、アダプターの機能を制御する方法について最良の情報を持っていることを意味します。 そのオプションが選択を有効にするや無効にすることができますの形式でエンドユーザーに、アダプターの機能を公開する UI を開発する必要があります。

ただし、開発したオーディオ処理オブジェクト (APOs) を制御するために使用される UI が既にあるを場合、この UI は、新しいオーディオ アダプターを使用する拡張でした。 ここでは、UI の拡張機能は、APOs のコントロールをソフトウェアとハードウェアのコントロール アダプターを確保します。

## <a name="span-idapplicationimpactspanspan-idapplicationimpactspanspan-idapplicationimpactspanapplication-impact"></a><span id="Application_Impact"></span><span id="application_impact"></span><span id="APPLICATION_IMPACT"></span>アプリケーションへの影響


WASAPI、メディア ファンデーション、メディアのエンジンまたは HTML 5 を使用して UWP アプリでのこの新しい種類のオーディオのアダプターとその関連するドライバー、説明されている機能を使用できる&lt;オーディオ&gt;タグ。 UWP アプリに使用可能でないと Wave と DSound ことはできませんを使用することに注意してください。 デスクトップ アプリケーションがハードウェア オフロードされたオーディオをサポートするオーディオのアダプターのオフロード機能を使用できないことにも注意してください。 これらのアプリケーションでは、ソフトウェア オーディオ エンジンの利用に暗証番号 (pin) ホストからのみ、オーディオを引き続きレンダリングできます。

UWP アプリは、メディア コンテンツをストリームし、メディア ファンデーション、メディアのエンジンまたは HTML 5 を使用する場合&lt;オーディオ&gt;タグ、アプリは自動的に選択 - ハードウェア オフロード ストリームの適切なオーディオ カテゴリが設定されている限り、します。 ハードウェアでオプトイン オフロードあたりストリームごとに行われます。

WASAPI または通信のストリーミングを使用する UWP アプリでは、ハードウェアのオフロードを明示的にオプトインする必要があります。

 

 




