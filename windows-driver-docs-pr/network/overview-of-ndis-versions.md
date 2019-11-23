---
title: NDIS バージョンの概要
description: NDIS バージョンの概要
ms.assetid: 6ecd4040-2831-4238-8080-97edc6a7c3ba
keywords:
- ネットワークドライバー WDK、NDIS バージョン
- NDIS WDK、ネットワークドライバーのバージョン
- 旧バージョンとの互換性 WDK ネットワーク
- 互換性 WDK ネットワーク
ms.date: 05/03/2019
ms.localizationpriority: medium
ms.openlocfilehash: 5a46a05075d88c707567f5a8445e135cdf993aa5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843734"
---
# <a name="overview-of-ndis-versions"></a>NDIS バージョンの概要

複数のバージョンの Microsoft Windows 用の NDIS ドライバーを作成する場合は、使用している機能が Windows の各バージョンでサポートされていることを確認してください。 各リリースで、新しい機能が NDIS に追加されました。 その他の機能は互換性のために残されており、以降のバージョンの NDIS からは削除されました。

この一連の設計ガイドドキュメントは、Windows Vista 以降のオペレーティングシステムおよび NDIS 6.0 以降のドライバーを対象としています。 以前のバージョンの Windows と NDIS のドキュメントは、ドキュメントの前のリリースに含まれています。 Windows XP および NDIS 5.1 のドキュメントについては、「 [windows 2000 および WINDOWS XP ネットワーク設計ガイド](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565849(v=vs.85))」を参照してください。

> [!NOTE]
> ドライバーは呼び出すことで NDIS バージョンをクエリすることができます、 [**エミュレーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreadconfiguration) 関数と、 *キーワード* パラメーターに設定 **NdisVersion**. 

次の表では、windows オペレーティングシステム、Microsoft Windows Driver Kit (WDK)、およびドライバー開発キット (DDK) バージョンの NDIS バージョンサポート、および ndis バージョン間での主要な NDIS 機能のサポートについて説明します。

| オペレーティング システム | 開発キット | サポートされている NDIS バージョン | CoNDIS | 逆シリアル化されたドライバー | 中間ドライバー |
| --- | --- | --- | --- | --- | --- |
| Windows 95 | Windows NT 4.0 DDK または Windows 95 DDK | 3.1 |  |  |  |
|  |  | ミニポートドライバーとプラグアンドプレイのサポートが追加されました。 |
| Windows 95 OSR2 | Windows NT 4.0 DDK または Windows 95 DDK | 4.0 |  |  |  |
|  |  | プロトコルドライバーは、vxd 型のドライバーです。 |
| Windows 98 | Windows NT 4.0 DDK または Windows 98 DDK | 4.1 | X | X | X |
|  |  | プロトコルドライバーは、vxd 型のドライバーです。 |
| Windows 98 SE | Windows NT 4.0 DDK または Windows 98 DDK | 5.0 | X | X | X |
|  |  | 電源管理と WMI のサポートが追加されました。 |
| Windows Me | Windows NT 4.0 DDK または Windows 98 DDK (Vxd 用) | 5.0 | X | X | X |
| Windows NT 3.5 | Windows NT 3.5 DDK | 3.0 |  |  |  |
| Windows NT 4.0 | Windows NT 4.0 DDK | 4.0 |  |  |  |
|  |  | 次の機能が追加されました。 <ul><li>[**MiniportSendPackets**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff550524(v=vs.85))</li><li>[**ProtocolReceivePacket**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff563251(v=vs.85))</li><li>[**MiniportAllocateComplete**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff549352(v=vs.85))</li></ul> |
| Windows NT 4.0 SP3 | 更新された NDIS ヘッダーとライブラリを含む Windows NT DDK | 4.1 | X | X | X |
| Windows 2000 | Windows 2000 DDK | 5.0 | X | X | X |
|  |  | 次のサポートが追加されました。 <ul><li>Windows 95/98/Me と互換性のある新しい INF ファイル形式</li><li>プラグ アンド プレイと電源管理</li><li>WMI に関するページ</li><li>LBFO</li><li>逆シリアル化されたミニポートドライバーについて、スキャッター/ギャザー DMA サポート</li></ul> |
| Windows XP | 「 [Windows ハードウェア開発用キットのダウンロード」を](https://go.microsoft.com/fwlink/p/?linkid=239721)参照してください。 | 5.1 | X | X | X |
|  |  | 次のサポートが追加されました。 <ul><li>[**MiniportCancelSendPackets**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff549359(v=vs.85))</li><li>[**MiniportPnPEventNotify**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff550487(v=vs.85))</li><li>[**MiniportShutdown**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff550533(v=vs.85))</li><li>[**NdisCancelSendPackets**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff550821(v=vs.85))</li><li>[**NdisCopyFromPacketToPacketSafe**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff551071(v=vs.85))</li><li>[**NdisGeneratePartialCancelId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgeneratepartialcancelid)</li><li>[**NdisGetFirstBufferFromPacketSafe**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff552066(v=vs.85))</li><li>[**NdisGetPoolFromPacket**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff552090(v=vs.85))</li><li>[**NdisGetSharedDataAlignment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetshareddataalignment)</li><li>[**NdisIMGetCurrentPacketStack**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff552155(v=vs.85))</li><li>[**NdisIMNotifyPnPEvent**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff552203(v=vs.85))</li><li>[**NdisQueryPendingIOCount**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff554456(v=vs.85))</li><li>[**NDIS\_\_パケットの取得\_キャンセル\_ID**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff556988(v=vs.85))</li><li>[**NDIS\_設定\_パケット\_キャンセル\_ID**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557195(v=vs.85))</li><li>[OID\_GEN\_マシン\_名](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-machine-name)</li><li>新しいミニポートドライバーの属性フラグ</li><li>64ビット統計カウンター</li><li>リモート NDIS</li><li>シリアル化および逆シリアル化されたミニポートドライバーの両方のサポートをスキャッター/ギャザーする</li><li>中間ドライバーのパケットスタック</li><li>VLAN タグ付け</li><li>UDP カプセル化された ESP パケットの処理のオフロード (Windows Server 2003 のみ)</li><li>Windows XP SP1 における wi-fi Protected Access (WPA)</li></ul> |
|  |  | 次のサポートがドロップされました: <ul><li>完全な Mac ドライバー</li><li>NDIS 3.0 プロトコル</li><li>**NdisQueryMapRegisterCount**</li><li>EISA バス</li></ul> |
| Windows Vista | 「 [Windows ハードウェア開発用キットのダウンロード」を](https://go.microsoft.com/fwlink/p/?linkid=239721)参照してください。 | 6.0 | X | X | X |
|  |  | 次の主な機能強化により、クライアントとサーバーの両方でパフォーマンスが大幅に向上します。 <ul><li>ネットワークデータのパッケージ化</li><li>送信パスと受信パス</li><li>実行時の再構成機能</li><li>スキャッター/ギャザー DMA</li><li>フィルター ドライバー</li><li>受信したデータ処理のマルチプロセッサスケーリング</li><li>Nic への TCP タスクのオフロード</li></ul> |
|  |  | 次の機能強化により、ドライバーの開発が簡素化されます。 <ul><li>効率的なドライバーの初期化</li><li>NDIS インターフェイスのバージョン管理のサポート</li><li>簡略化されたリセット処理</li><li>管理情報を取得するための標準インターフェイス</li><li>フィルター中間ドライバーを置き換えるフィルタードライバーモデル</li></ul> |
|  |  | NDIS 6.0 の機能の詳細については、「 [ndis 6.0 の概要](introduction-to-ndis-6-0.md)」を参照してください。 |
|  |  | NDIS 6.0 ドライバーでサポートされていない旧バージョンとの互換性および旧バージョンの機能については、「 [ndis 6.0 の旧バージョン](https://docs.microsoft.com/previous-versions/windows/hardware/network/ndis-6-0-backward-compatibility)との互換性」を参照してください。 |
| Windows Vista Service Pack 1 (SP1) および Windows Server 2008 | 「 [Windows ハードウェア開発キットのダウンロード」を](https://go.microsoft.com/fwlink/p/?linkid=239721)参照してください。 | 6.1 | X | X | X |
|  |  | NDIS 6.1 の機能の詳細については、「 [ndis 6.1 の概要](introduction-to-ndis-6-1.md)」を参照してください。 |
| Windows 7、Windows Server 2008 R2 | 「 [Windows ハードウェア開発キットのダウンロード」を](https://go.microsoft.com/fwlink/p/?linkid=239721)参照してください。 | 6.20 | X | X | X |
|  |  | NDIS 6.20 の機能の詳細については、「 [ndis 6.20 の概要](introduction-to-ndis-6-20.md)」を参照してください。 |
|  |  | NDIS 6.20 ドライバーでサポートされていない旧バージョンとの互換性および旧バージョンの機能については、「 [ndis 6.20 の旧バージョン](ndis-6-20-backward-compatibility.md)との互換性」を参照してください。 |
| Windows 8、Windows Server 2012 | 「 [Windows ハードウェア開発キットのダウンロード」を](https://go.microsoft.com/fwlink/p/?linkid=239721)参照してください。 | 6.30 | X | X | X |
|  |  | NDIS 6.30 の機能の詳細については、「 [ndis 6.30 の概要](introduction-to-ndis-6-30.md)」を参照してください。 |
| Windows 8.1、Windows Server 2012 R2 | 「 [Windows ハードウェア開発キットのダウンロード」を](https://go.microsoft.com/fwlink/p/?linkid=239721)参照してください。 | 6.40 | X | X | X |
|  |  | NDIS 6.40 の機能の詳細については、「 [ndis 6.40 の概要](introduction-to-ndis-6-40.md)」を参照してください。 |
| Windows 10 バージョン1507 | 「 [Windows ハードウェア開発キットのダウンロード」を](https://go.microsoft.com/fwlink/p/?linkid=239721)参照してください。 | 6.50 | X | X | X |
|   |   | NDIS 6.50 の機能の詳細については、「 [ndis 6.50 の概要](introduction-to-ndis-6-50.md)」を参照してください。 | 
| Windows 10 バージョン 1511 | 「 [Windows ハードウェア開発キットのダウンロード」を](https://go.microsoft.com/fwlink/p/?linkid=239721)参照してください。 | 6.51 | X | X | X |
| Windows 10、バージョン1607、および Windows Server 2016 | 「 [Windows ハードウェア開発キットのダウンロード」を](https://go.microsoft.com/fwlink/p/?linkid=239721)参照してください。 | 6.60 | X | X | X |
|   |   | NDIS 6.60 の機能の詳細については、「 [ndis 6.60 の概要](introduction-to-ndis-6-60.md)」を参照してください。 | 
| Windows 10 Version 1703 | 「 [Windows ハードウェア開発キットのダウンロード」を](https://go.microsoft.com/fwlink/p/?linkid=239721)参照してください。 | 6.70 | X | X | X |
|   |   | NDIS 6.70 coincided には、ネットワークアダプター WDF クラス拡張のプレビューリリースがあります。 [NetAdapterCx](../netcx/index.md)。<p>NDIS 6.70 の機能の詳細については、「 [ndis 6.70 の概要](introduction-to-ndis-6-70.md)」を参照してください。</p> |
| Windows 10 バージョン 1709 | 「 [Windows ハードウェア開発キットのダウンロード」を](https://go.microsoft.com/fwlink/p/?linkid=239721)参照してください。 | 6.80 | X | X | X |
|   |   | NDIS 6.80 の機能の詳細については、「 [ndis 6.80 の概要](introduction-to-ndis-6-80.md)」を参照してください。 | 
| Windows 10 バージョン 1803 | 「 [Windows ハードウェア開発キットのダウンロード」を](https://go.microsoft.com/fwlink/p/?linkid=239721)参照してください。 | 6.81 | X | X | X |
|   |   | NDIS 6.81 の機能の詳細については、「 [ndis 6.81 の概要](introduction-to-ndis-6-81.md)」を参照してください。 |
| Windows 10 Version 1809 | 「 [Windows ハードウェア開発キットのダウンロード」を](https://go.microsoft.com/fwlink/p/?linkid=239721)参照してください。 | 6.82 | X | X | X |
|   |   | NDIS 6.82 の機能の詳細については、「 [ndis 6.82 の概要](introduction-to-ndis-6-82.md)」を参照してください。 |
| Windows 10 バージョン 1903 | 「 [Windows ハードウェア開発キットのダウンロード」を](https://go.microsoft.com/fwlink/p/?linkid=239721)参照してください。 | 6.83 | X | X | X |
|   |   | NDIS 6.83 の機能の詳細については、「 [ndis 6.83 の概要](introduction-to-ndis-6-83.md)」を参照してください。 |
