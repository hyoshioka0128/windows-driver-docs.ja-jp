---
title: コールアウト ドライバーのプログラミングに関する考慮事項
description: コールアウト ドライバーのプログラミングに関する考慮事項
ms.assetid: e470202a-bc3b-41ac-8156-8aac8cd976cd
keywords:
- Windows Filtering Platform コールアウト ドライバー WDK、プログラミングの考慮事項
- コールアウト ドライバー WDK Windows フィルタ リング プラットフォーム、プログラミングの考慮事項
- ALE フローには、フィルター処理レイヤー WDK Windows フィルタ リング プラットフォームが確立されています。
- カーネル モード コールアウト ドライバー WDK Windows フィルタ リング プラットフォーム
- ユーザー モード コールアウト ドライバー WDK Windows フィルタ リング プラットフォーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b71ca15eb81e6704484a734f9e42e159282587c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369074"
---
# <a name="callout-driver-programming-considerations"></a>コールアウト ドライバーのプログラミングに関する考慮事項


Windows フィルタ リング プラットフォームのコールアウト ドライバーをプログラミングするときは、次のトピックを検討してください。

### <a href="" id="user-mode-vs--kernel-mode"></a>ユーザー モードとします。カーネル モード

標準を使用して必要なフィルター処理を行うことができる場合、Windows フィルタ リングのプラットフォーム、独立系ソフトウェア ベンダーに組み込まれている機能をフィルター処理 (Isv) 書き込む必要がありますユーザー モードの代わりに、フィルター エンジンを構成する管理アプリケーションカーネル モードのコールアウト ドライバーを記述します。 カーネル モードのコールアウト ドライバーは、標準的な組み込みのフィルター機能で処理できない方法でネットワーク データを処理する必要がありますとだけ記述する必要があります。 ユーザー モードの Windows フィルタ リング プラットフォームの管理アプリケーションを記述する方法については、次を参照してください。、 [Windows フィルタ リング プラットフォーム](https://go.microsoft.com/fwlink/p/?linkid=90220)Microsoft Windows SDK のドキュメント。

### <a name="choice-of-filtering-layer"></a>レイヤーをフィルター処理の選択

コールアウト ドライバーは、ネットワーク スタックで最高の使用可能なフィルター処理層でネットワーク データをフィルター処理する必要があります。 たとえば、ストリーム レイヤーでは、必要なフィルター処理タスクを処理することができる場合する必要があります実装されません、ネットワーク層で。 ドライバーを Windows で IPsec との互換性を保証するために使用する必要があります、フィルタ リング層の推奨事項の詳細については、次を参照してください。 [IPsec と互換性のあるコールアウト ドライバーの開発](developing-ipsec-compatible-callout-drivers.md)します。

### <a href="" id="blocking-at-the-application-layer-enforcement--ale--flow-established-l"></a>レイヤーが確立されている、アプリケーション レイヤーの強制 (ALE) フローでブロック

通常のいずれかのフィルター エンジンに吹き出しが追加されたかどうか、 *ALE フローが確立されている*レイヤーをフィルター処理 (FWPM\_レイヤー\_ALE\_フロー\_確立した\_V4または FWPM\_レイヤー\_ALE\_フロー\_確立した\_V6)、その[ *classifyFn* ](https://msdn.microsoft.com/library/windows/hardware/ff544890)コールアウト関数しないでください。返す FWP\_アクション\_のアクションをブロックします。 フィルター レイヤーを確立するは、意思決定を承認または却下 ALE フローのいずれかの接続を確立できません必要があります。 このような意思決定は、常に、その他の ALE フィルタ リング層のいずれかで行われます。

このような唯一の有効な理由、 [ *classifyFn* ](https://msdn.microsoft.com/library/windows/hardware/ff544890)コールアウト FWP を返す関数\_アクション\_ブロック アクションは、エラーが発生した場合、潜在的なセキュリティ リスクをもたらす可能性があります確立された接続は終了しません。 場合、 この場合は、FWP を返す\_アクション\_ブロック アクションは、潜在的なセキュリティ リスクが悪用されることを防ぐために接続を閉じます。

### <a name="callout-function-execution-time"></a>引き出し線の関数の実行時間

通常、フィルター エンジンは IRQL で吹き出しのコールアウトの関数を呼び出すために = ディスパッチ\_レベルでは、これらの関数が効率的に実行しているシステムを維持するには、可能な限り早くその実行を完了することを確認します。 延長実行 IRQL でディスパッチを =\_レベルでは、システムの全体的なパフォーマンスに悪影響を与えることができます。

### <a name="injecting-into-the-receive-data-path"></a>挿入する、データ パスが表示されます。

呼び出しの前に、吹き出しに IP チェックサムが再計算する必要があります[パケット インジェクション関数](packet-injection-functions.md)IP からパケットが再構築時に、元のパケットでチェックサムの正しいできないため、受信データ パスに挿入します。パケットのフラグメント。 フラグメントから net バッファーのリストが再構築するかどうかを示す信頼性の高いメカニズムはありません。

### <a name="inline-injection-of-tcp-packet-from-transport-layers"></a>トランスポート層から TCP パケットのインラインの挿入

動作のロックのため、TCP スタック、トランスポート層でのコールアウトがから新規または複製された TCP パケットを挿入できません、 [classifyFn](https://msdn.microsoft.com/library/windows/hardware/ff544887)コールアウト関数。 インラインの挿入を使用する場合は、引き出し線は、DPC、挿入を実行するをキューする必要があります。

### <a name="outgoing-ip-header-alignment"></a>送信 IP ヘッダーの配置

Net のバッファーの一覧で IP ヘッダーを表す MDL ([**NET\_バッファー\_現在\_MDL**](https://msdn.microsoft.com/library/windows/hardware/ff568379)([**NET\_バッファー\_一覧\_最初\_NB**](https://msdn.microsoft.com/library/windows/hardware/ff568394)(*netBufferList*))) する必要がありますがポインターで固定されたときのいずれか、[パケットの挿入関数](packet-injection-functions.md)出力方向のパスにパケット データを挿入するために使用します。 着信パケットの IP ヘッダー MDL には、ポインターで固定された可能性があります、ため、コールアウトする必要がありますを再構築 IP ヘッダー (整列されていない) 場合、送信パスに、着信パケットを挿入するときに。

## <a name="related-topics"></a>関連トピック


[Windows フィルタリング プラットフォーム コールアウト ドライバー](windows-filtering-platform-callout-drivers2.md)

 

 






