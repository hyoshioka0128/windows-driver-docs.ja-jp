---
title: NDIS バージョンの概要
description: NDIS バージョンの概要
ms.assetid: 6ecd4040-2831-4238-8080-97edc6a7c3ba
keywords:
- ネットワーク ドライバー WDK、NDIS バージョン
- NDIS WDK、ネットワーク ドライバーのバージョン
- 旧バージョンと互換性の WDK ネットワーク
- 互換性の WDK ネットワーク
ms.date: 05/03/2019
ms.localizationpriority: medium
ms.openlocfilehash: ed2f1c0546c4aa1186f152d87fdcab10a86d2733
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384377"
---
# <a name="overview-of-ndis-versions"></a>NDIS バージョンの概要

Microsoft Windows の複数のバージョンの NDIS ドライバーを記述する場合は使用している機能は、各 Windows バージョンではサポートします。 新機能が、各リリースでは、NDIS に追加されました。 その他の機能が使用できなくなったし、以降のバージョンの NDIS から削除されました。

Windows Vista と以降のオペレーティング システムおよび NDIS 6.0 以降のドライバーは、この設計ガイド ドキュメントのセットを対象します。 Windows および NDIS の以前のバージョンのドキュメントは、ドキュメントの以前のリリースに含まれます。 Windows XP および NDIS 5.1 ドキュメントについては、次を参照してください。 [Windows 2000 および Windows XP のネットワーク設計ガイド](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565849(v=vs.85))します。

> [!NOTE]
> ドライバーは呼び出すことで NDIS バージョンをクエリすることができます、 [**エミュレーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisreadconfiguration) 関数と、 *キーワード* パラメーターに設定 **NdisVersion**. 

Windows オペレーティング システム、Microsoft Windows Driver Kit (WDK)、およびバージョンの NDIS ドライバー開発キット (DDK) バージョンでサポートおよび NDIS のバージョン間での主な NDIS 機能のサポートについては、次の表で説明します。

| オペレーティング システム | 開発キット | サポートされている NDIS バージョン | いる CoNDIS | 逆シリアル化されたドライバー | 中間ドライバー |
| --- | --- | --- | --- | --- | --- |
| Windows 95 | Windows NT 4.0 DDK、または Windows 95 DDK | 3.1 |  |  |  |
|  |  | ミニポート ドライバーとプラグ アンド プレイのサポートが追加されました。 |
| Windows 95 OSR2 | Windows NT 4.0 DDK、または Windows 95 DDK | 4.0 |  |  |  |
|  |  | プロトコル ドライバーには vxd 型です。 |
| Windows 98 | Windows NT 4.0 DDK、または Windows 98 DDK | 4.1 | X | X | X |
|  |  | プロトコル ドライバーには vxd 型です。 |
| Windows 98 SE | Windows NT 4.0 DDK、または Windows 98 DDK | 5.0 | X | X | X |
|  |  | 電源管理と WMI のサポートが追加されました。 |
| Windows Me | Windows NT 4.0 DDK または Vxd は、Windows 98 DDK | 5.0 | X | X | X |
| Windows NT 3.5 | Windows NT 3.5 DDK | 3.0 |  |  |  |
| Windows NT 4.0 | Windows NT 4.0 DDK | 4.0 |  |  |  |
|  |  | これらの機能を追加するには。 <ul><li>[**MiniportSendPackets**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff550524(v=vs.85))</li><li>[**ProtocolReceivePacket**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff563251(v=vs.85))</li><li>[**MiniportAllocateComplete**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff549352(v=vs.85))</li></ul> |
| Windows NT 4.0 SP3 | 更新の NDIS ヘッダーとライブラリを Windows NT DDK | 4.1 | X | X | X |
| Windows 2000 | Windows 2000 DDK | 5.0 | X | X | X |
|  |  | サポートが追加されました。 <ul><li>Windows 95/98/自分と互換性のある新しい INF ファイルの形式</li><li>プラグ アンド プレイと電源管理</li><li>WMI に関するページ</li><li>LBFO</li><li>スキャッター/ギャザー DMA を逆シリアル化されたミニポート ドライバー サポート</li></ul> |
| Windows XP | 参照してください[Windows ハードウェア開発キットのダウンロード](https://go.microsoft.com/fwlink/p/?linkid=239721) | 5.1 | X | X | X |
|  |  | サポートが追加されました。 <ul><li>[**MiniportCancelSendPackets**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff549359(v=vs.85))</li><li>[**MiniportPnPEventNotify**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff550487(v=vs.85))</li><li>[**MiniportShutdown**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff550533(v=vs.85))</li><li>[**NdisCancelSendPackets**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff550821(v=vs.85))</li><li>[**NdisCopyFromPacketToPacketSafe**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff551071(v=vs.85))</li><li>[**NdisGeneratePartialCancelId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisgeneratepartialcancelid)</li><li>[**NdisGetFirstBufferFromPacketSafe**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff552066(v=vs.85))</li><li>[**NdisGetPoolFromPacket**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff552090(v=vs.85))</li><li>[**NdisGetSharedDataAlignment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisgetshareddataalignment)</li><li>[**NdisIMGetCurrentPacketStack**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff552155(v=vs.85))</li><li>[**NdisIMNotifyPnPEvent**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff552203(v=vs.85))</li><li>[**NdisQueryPendingIOCount**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff554456(v=vs.85))</li><li>[**NDIS\_取得\_パケット\_キャンセル\_ID**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff556988(v=vs.85))</li><li>[**NDIS\_設定\_パケット\_キャンセル\_ID**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557195(v=vs.85))</li><li>[OID\_GEN\_マシン\_名](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-machine-name)</li><li>新しいミニポート ドライバー属性のフラグ</li><li>統計カウンターの 64 ビット</li><li>リモートの NDIS</li><li>スキャッター/ギャザーのサポートはシリアル化し、ミニポート ドライバーを逆シリアル化</li><li>中間ドライバー スタックのパケット</li><li>VLAN タグ付け</li><li>ESP の UDP カプセル化パケット (Windows Server 2003 のみ) の処理のオフロード</li><li>Wi-fi Protected Access (WPA) Windows XP sp1</li></ul> |
|  |  | ドロップのサポート: <ul><li>完全な Mac ドライバー</li><li>NDIS 3.0 プロトコル</li><li>**NdisQueryMapRegisterCount**</li><li>EISA バス</li></ul> |
| Windows Vista | 参照してください[Windows ハードウェア開発キットのダウンロード](https://go.microsoft.com/fwlink/p/?linkid=239721) | 6.0 | X | X | X |
|  |  | 次のように主要な機能強化は、クライアントとサーバーの両方のパフォーマンスが著しく向上を提供します。 <ul><li>ネットワーク データのパッケージ化</li><li>送信し、受信パス</li><li>実行時の再構成機能</li><li>DMA のスキャッター/ギャザー</li><li>フィルター ドライバー</li><li>受信したデータ処理のマルチプロセッサのスケーリング</li><li>Nic にオフロードすることの TCP タスク</li></ul> |
|  |  | 次の機能強化は、ドライバーの開発を簡略化します。 <ul><li>簡素化されたドライバーの初期化</li><li>NDIS インターフェイスのバージョン管理サポート</li><li>簡略化されたリセット処理</li><li>管理情報を取得するための標準インターフェイス</li><li>中間のフィルター ドライバーを置換するフィルター ドライバー モデル</li></ul> |
|  |  | NDIS 6.0 の機能の詳細については、次を参照してください。 [NDIS 6.0 の概要](introduction-to-ndis-6-0.md)します。 |
|  |  | 下位互換性と NDIS 6.0 のドライバーでサポートされていない古い機能については、次を参照してください。 [NDIS 6.0 の下位互換性](https://docs.microsoft.com/previous-versions/windows/hardware/network/ndis-6-0-backward-compatibility)します。 |
| Windows Vista Service Pack 1 (SP1) および Windows Server 2008 | 参照してください[Windows ハードウェア開発キットをダウンロード](https://go.microsoft.com/fwlink/p/?linkid=239721)します。 | 6.1 | X | X | X |
|  |  | NDIS 6.1 機能については、次を参照してください。 [NDIS 6.1 概要](introduction-to-ndis-6-1.md)します。 |
| Windows 7、Windows Server 2008 R2 | 参照してください[Windows ハードウェア開発キットをダウンロード](https://go.microsoft.com/fwlink/p/?linkid=239721)します。 | 6.20 | X | X | X |
|  |  | NDIS 6.20 機能については、次を参照してください。 [NDIS 6.20 が動作の概要](introduction-to-ndis-6-20.md)します。 |
|  |  | 下位互換性と NDIS 6.20 ドライバーでサポートされていない古い機能については、次を参照してください。 [NDIS 6.20 が動作の下位互換性](ndis-6-20-backward-compatibility.md)します。 |
| Windows 8、Windows Server 2012 | 参照してください[Windows ハードウェア開発キットをダウンロード](https://go.microsoft.com/fwlink/p/?linkid=239721)します。 | 6.30 | X | X | X |
|  |  | NDIS 6.30 機能については、次を参照してください。 [NDIS 6.30 概要](introduction-to-ndis-6-30.md)します。 |
| Windows 8.1、Windows Server 2012 R2 | 参照してください[Windows ハードウェア開発キットをダウンロード](https://go.microsoft.com/fwlink/p/?linkid=239721)します。 | 6.40 | X | X | X |
|  |  | NDIS 6.40 機能については、次を参照してください。 [NDIS 6.40 概要](introduction-to-ndis-6-40.md)します。 |
| Windows 10 バージョン 1507 | 参照してください[Windows ハードウェア開発キットをダウンロード](https://go.microsoft.com/fwlink/p/?linkid=239721)します。 | 6.50 | X | X | X |
|   |   | NDIS 6.50 機能の詳細については、次を参照してください。 [NDIS 6.50 概要](introduction-to-ndis-6-50.md)します。 | 
| Windows 10 バージョン 1511 | 参照してください[Windows ハードウェア開発キットをダウンロード](https://go.microsoft.com/fwlink/p/?linkid=239721)します。 | 6.51 | X | X | X |
| Windows 10、バージョン 1607 および Windows Server 2016 | 参照してください[Windows ハードウェア開発キットをダウンロード](https://go.microsoft.com/fwlink/p/?linkid=239721)します。 | 6.60 | X | X | X |
|   |   | NDIS 6.60 機能の詳細については、次を参照してください。 [NDIS 6.60 概要](introduction-to-ndis-6-60.md)します。 | 
| Windows 10 Version 1703 | 参照してください[Windows ハードウェア開発キットをダウンロード](https://go.microsoft.com/fwlink/p/?linkid=239721)します。 | 6.70 | X | X | X |
|   |   | 別名: coincided ネットワーク アダプター WDF クラス拡張機能のプレビュー リリースで NDIS 6.70 [NetAdapterCx](../netcx/index.md)します。<p>NDIS 6.70 機能の詳細については、次を参照してください。 [NDIS 6.70 概要](introduction-to-ndis-6-70.md)します。</p> |
| Windows 10 バージョン 1709 | 参照してください[Windows ハードウェア開発キットをダウンロード](https://go.microsoft.com/fwlink/p/?linkid=239721)します。 | 6.80 | X | X | X |
|   |   | NDIS 6.80 機能の詳細については、次を参照してください。 [NDIS 6.80 概要](introduction-to-ndis-6-80.md)します。 | 
| Windows 10 バージョン 1803 | 参照してください[Windows ハードウェア開発キットをダウンロード](https://go.microsoft.com/fwlink/p/?linkid=239721)します。 | 6.81 | X | X | X |
|   |   | NDIS 6.81 機能の詳細については、次を参照してください。 [NDIS 6.81 概要](introduction-to-ndis-6-81.md)します。 |
| Windows 10 Version 1809 | 参照してください[Windows ハードウェア開発キットをダウンロード](https://go.microsoft.com/fwlink/p/?linkid=239721)します。 | 6.82 | X | X | X |
|   |   | NDIS 6.82 機能の詳細については、次を参照してください。 [NDIS 6.82 概要](introduction-to-ndis-6-82.md)します。 |
| Windows 10 バージョン 1903 | 参照してください[Windows ハードウェア開発キットをダウンロード](https://go.microsoft.com/fwlink/p/?linkid=239721)します。 | 6.83 | x | X | x |
|   |   | NDIS 6.83 機能の詳細については、次を参照してください。 [NDIS 6.83 概要](introduction-to-ndis-6-83.md)します。 |
