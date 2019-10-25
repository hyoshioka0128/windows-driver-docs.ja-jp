---
title: コールアウト ドライバーのプログラミングに関する考慮事項
description: コールアウト ドライバーのプログラミングに関する考慮事項
ms.assetid: e470202a-bc3b-41ac-8156-8aac8cd976cd
keywords:
- Windows フィルタリングプラットフォームのコールアウトドライバーの WDK、プログラミングに関する考慮事項
- コールアウトドライバー WDK Windows フィルタリングプラットフォーム、プログラミングに関する考慮事項
- ALE フローが確立したフィルターレイヤー WDK Windows フィルタリングプラットフォーム
- カーネルモードコールアウトドライバーの WDK Windows フィルタリングプラットフォーム
- ユーザーモードのコールアウトドライバーの WDK Windows フィルタリングプラットフォーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e857538a8631ac77839dd848cce5d4ea80241c0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838218"
---
# <a name="callout-driver-programming-considerations"></a>コールアウト ドライバーのプログラミングに関する考慮事項


Windows フィルタリングプラットフォームのコールアウトドライバーをプログラミングするときは、次のトピックを考慮してください。

### <a href="" id="user-mode-vs--kernel-mode"></a>ユーザーモードとカーネルモードの比較

Windows フィルタリングプラットフォームに組み込まれている標準のフィルター処理機能を使用して目的のフィルター処理を実行できる場合、独立系ソフトウェアベンダー (Isv) は、フィルターエンジンを構成するためのユーザーモード管理アプリケーションを作成する必要があります。カーネルモードのコールアウトドライバーを記述する。 カーネルモードのコールアウトドライバーは、標準の組み込みフィルター処理機能では処理できない方法でネットワークデータを処理する必要がある場合にのみ書き込む必要があります。 ユーザーモードの Windows フィルタリングプラットフォーム管理アプリケーションを作成する方法の詳細については、Microsoft Windows SDK の[Windows フィルタリングプラットフォーム](https://go.microsoft.com/fwlink/p/?linkid=90220)のドキュメントを参照してください。

### <a name="choice-of-filtering-layer"></a>フィルターレイヤーの選択

コールアウトドライバーは、ネットワークスタック内で可能な限り多くのフィルター処理レイヤーでネットワークデータをフィルター処理する必要があります。 たとえば、目的のフィルター処理タスクをストリームレイヤーで処理できる場合は、ネットワーク層で実装しないようにする必要があります。 Windows での IPsec との互換性を保証するためにドライバーで使用する必要があるフィルター処理レイヤーの推奨事項の詳細については、「 [ipsec と互換性のあるコールアウトドライバーの開発](developing-ipsec-compatible-callout-drivers.md)」を参照してください。

### <a href="" id="blocking-at-the-application-layer-enforcement--ale--flow-established-l"></a>アプリケーションレイヤー強制 (ALE) フローによって確立されたレイヤーをブロックする

通常、 *ale フロー*によって確立されたフィルター処理レイヤーの1つでフィルターエンジンにコールアウトが追加されている場合 (FWPM\_レイヤー\_ALE\_FLOW\_確立\_V4 または FWPM\_レイヤー\_ALE\_flow)\_V6) によって確立された\_、その[*classid*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0)関数は、アクションに対して、.FWP\_アクション\_ブロックを返さないようにする必要があります。 接続を承認または拒否するかどうかは、確立されているいずれかのフィルター処理レイヤーで作成しないでください。 このような決定は、常に他のいずれかの ALE フィルターレイヤーで行う必要があります。

このような[*classid*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0)を返すために、アクションの\_ブロックを\_返すための有効な理由は、確立された接続が終了しない場合にセキュリティ上のリスクが生じる可能性のあるエラーが発生した場合です。 この場合、アクションに対して .FWP\_ACTION\_BLOCK を返すと、セキュリティリスクの可能性が悪用されるのを防ぐために接続が閉じられます。

### <a name="callout-function-execution-time"></a>コールアウト関数の実行時間

通常、フィルターエンジンは、IRQL = ディスパッチ\_レベルでコールアウトのコールアウト関数を呼び出します。そのため、これらの関数は、システムを効率的に実行するために、できるだけ迅速に実行を完了するようにしてください。 IRQL = DISPATCH\_レベルでの拡張実行は、システムの全体的なパフォーマンスに悪影響を及ぼす可能性があります。

### <a name="injecting-into-the-receive-data-path"></a>受信データパスへの挿入

受信データパスに挿入される[パケット挿入関数](packet-injection-functions.md)を呼び出す前に、コールアウトは ip チェックサムを再計算する必要があります。これは、パケットが ip パケットフラグメントから再構築された場合、元のパケットのチェックサムが正しくない可能性があるためです。 Net バッファーリストがフラグメントから再構築されるかどうかを示す、信頼性の高いメカニズムはありません。

### <a name="inline-injection-of-tcp-packet-from-transport-layers"></a>トランスポート層からの TCP パケットのインライン挿入

TCP スタックのロック動作により、トランスポート層のコールアウトは、Classid を作成するために、新しい TCP パケットまたは複製された TCP パケットを[classid](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)の関数のコールアウト関数から挿入することはできません。 インライン挿入が必要な場合、挿入を実行するために、コールアウトは DPC をキューに挿入する必要があります。

### <a name="outgoing-ip-header-alignment"></a>発信 IP ヘッダーの配置

Net バッファーリスト内の IP ヘッダーを記述する MDL (net[ **\_buffer\_CURRENT\_MDL**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-current-mdl)([**net\_buffer\_list\_FIRST\_NB**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-first-nb)(*netBufferList*))) は、1つの場合にポインターでアラインされている必要があります。パケット[挿入関数](packet-injection-functions.md)は、パケットデータを発信パスに挿入するために使用されます。 着信パケットの IP ヘッダー MDL はポインターで固定されている可能性があるため、受信パケットを送信パスに挿入するときに、コールアウトは IP ヘッダーを再構築する必要があります (まだ固定されていない場合)。

## <a name="related-topics"></a>関連トピック


[Windows フィルタリング プラットフォーム コールアウト ドライバー](windows-filtering-platform-callout-drivers2.md)

 

 






