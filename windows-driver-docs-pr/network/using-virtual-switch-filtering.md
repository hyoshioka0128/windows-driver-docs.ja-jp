---
title: 仮想スイッチ フィルターの使用
description: 仮想スイッチ フィルターの使用
ms.assetid: 09325037-F9A4-45C8-97E0-8FCA7D42A120
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c48c44856961ddf2b5cc7ee8abddda0289b13344
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361808"
---
# <a name="using-virtual-switch-filtering"></a>仮想スイッチ フィルターの使用

## <a name="overview-of-virtual-switch-filtering"></a>仮想スイッチのフィルタ リングの概要

仮想スイッチのフィルター処理は、Windows 8 および Windows の以降のバージョンでサポートされます。

この WFP 機能は、仮想スイッチ仮想ポート (VPort) と仮想マシンの識別子 (VM ID) などの特定のフィールドと同様に、MAC ヘッダー、IP ヘッダーと上位のプロトコルのポートのフィールドでフィルター処理を使用できます。 これらの層は、仮想スイッチを通過するすべてのパケットのパケット単位ごとに呼び出されます。 これらの層は、仮想スイッチ拡張機能フィルターからアクセスされます — NDIS lightweight filter (LWF) ドライバーの種類。

コールアウト ドライバーは呼び出し、 [ **FwpsvSwitchEventsSubscribe0** ](https://msdn.microsoft.com/library/windows/hardware/hh439687)仮想スイッチのレイヤーのイベントのコールバックのエントリ ポイントを登録する関数。

コールバックの通知関数のエントリ ポイントがで指定された、 [ **FWPS\_VSWITCH\_イベント\_ディスパッチ\_TABLE0** ](https://msdn.microsoft.com/library/windows/hardware/hh451263)構造体. 使用できるコールバック関数は次のとおりです。

* [*FWPS\_VSWITCH\_FILTER\_ENGINE\_REORDER\_CALLBACK0*](https://msdn.microsoft.com/library/windows/hardware/hh451267)
* [*FWPS\_VSWITCH\_インターフェイス\_イベント\_CALLBACK0*](https://msdn.microsoft.com/library/windows/hardware/hh451269)
* [*FWPS\_VSWITCH\_有効期間\_イベント\_CALLBACK0*](https://msdn.microsoft.com/library/windows/hardware/hh451271)
* [*FWPS\_VSWITCH\_ポリシー\_イベント\_CALLBACK0*](https://msdn.microsoft.com/library/windows/hardware/hh451272)
* [*FWPS\_VSWITCH\_ポート\_イベント\_CALLBACK0*](https://msdn.microsoft.com/library/windows/hardware/hh451276)
* [*FWPS\_VSWITCH\_ランタイム\_状態\_復元\_CALLBACK0*](https://msdn.microsoft.com/library/windows/hardware/hh451281)
* [*FWPS\_VSWITCH\_RUNTIME\_STATE\_SAVE\_CALLBACK0*](https://msdn.microsoft.com/library/windows/hardware/hh451286)

[ **FWPS\_VSWITCH\_イベント\_型**](https://msdn.microsoft.com/library/windows/hardware/hh451265)列挙の値を定義する、 *eventType*仮想のパラメーター通知関数を切り替えます。

最終的にコールアウト ドライバーを呼び出す必要があります[ **FwpsvSwitchEventsUnsubscribe0** ](https://msdn.microsoft.com/library/windows/hardware/hh439691)システム リソースを解放します。

コールアウト ドライバーの状態を返す場合\_WFP 通知関数からの保留、WFP の状態は返します\_OID 要求ハンドラーを保留します。 コールアウト ドライバーを呼び出す必要があります、 [ **FwpsvSwitchNotifyComplete0** ](https://msdn.microsoft.com/library/windows/hardware/hh439695)関数が保留中の操作を完了します。 後に、 **FwpsvSwitchNotifyComplete0**呼び出すには、WFP 呼び出し、 [ **NdisFOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff561833)関数が仮想スイッチの OID を完了します。

コールバックを追加または通知関数のコンテキストで同期的に WFP フィルターを削除しない必要があります。 さらに、通知機能の状態を返すコールバックを許可する場合\_PENDING、および状況コールアウト。\_保留中、吹き出しする必要がありますいないを追加または削除 WFP フィルター、通知を完了する前にします。

## <a name="wfp-virtual-switch-filter-layer-and-fields"></a>WFP 仮想スイッチのフィルター レイヤーとフィールド

[実行時のフィルター処理レイヤー識別子](https://msdn.microsoft.com/library/windows/hardware/ff570731)仮想スイッチがフィルター処理が含まれます。

* FWPS\_レイヤー\_イングレス\_VSWITCH\_イーサネット
* FWPS\_レイヤー\_エグレス\_VSWITCH\_イーサネット
* FWPS\_レイヤー\_イングレス\_VSWITCH\_トランスポート\_V4
* FWPS\_レイヤー\_イングレス\_VSWITCH\_トランスポート\_V6
* FWPS\_レイヤー\_エグレス\_VSWITCH\_トランスポート\_V4
* FWPS\_レイヤー\_エグレス\_VSWITCH\_トランスポート\_V6

[データ フィールドの識別子](https://msdn.microsoft.com/library/windows/hardware/ff546312)仮想スイッチがフィルター処理が含まれます。

* [**FWPS\_フィールド\_エグレス\_VSWITCH\_イーサネット**](https://msdn.microsoft.com/library/windows/hardware/hh439709)
* [**FWPS\_フィールド\_エグレス\_VSWITCH\_トランスポート\_V4**](https://msdn.microsoft.com/library/windows/hardware/hh439715)
* [**FWPS\_FIELDS\_EGRESS\_VSWITCH\_TRANSPORT\_V6**](https://msdn.microsoft.com/library/windows/hardware/hh439721)
* [**FWPS\_フィールド\_イングレス\_VSWITCH\_イーサネット**](https://msdn.microsoft.com/library/windows/hardware/hh439733)
* [**FWPS\_フィールド\_イングレス\_VSWITCH\_トランスポート\_V4**](https://msdn.microsoft.com/library/windows/hardware/hh439738)
* [**FWPS\_FIELDS\_INGRESS\_VSWITCH\_TRANSPORT\_V6**](https://msdn.microsoft.com/library/windows/hardware/hh439745)

## <a name="guidance-for-wfp-virtual-switch-callout-writers"></a>WFP 仮想スイッチのコールアウトのライターのガイダンス

### <a name="port-0-traffic"></a>ポート 0 のトラフィック

WFP 仮想スイッチのコールアウトのポート (既定のポートの ID) の 0 からのトラフィックが信頼されていると、フィルター処理する必要がありますされません。 これは、一般に、ポート 0 でのトラフィックは他の拡張機能ドライバー スタックの発生元し、特権と信頼されているデータ パスによって扱われるためです。 仮想スイッチ拡張機能は、フィルター処理され、基になる拡張機能によって拒否する必要があります、いないコントロール パケットを送信するなどの場合ポート 0 を使用して限定的に使用します。 HYPER-V 拡張可能スイッチ ソース ポート mofification の詳細については、次を参照してください。[データを変更するパケットの拡張可能スイッチ ソース ポート](modifying-a-packet-s-extensible-switch-source-port-data.md)します。

### <a name="callout-matching-rules"></a>照合ルールの吹き出し

フィルター処理するための照合ルールを定義するときに仮想スイッチのコールアウト使用しないでください、MAC アドレスを基準としての比較。 MAC アドレスは、実行時に変更して、いくつかのポートは複数の MAC アドレスからトラフィックを生成する可能性があります。 代わりに、コールアウトは、耐久性の照合ルールは変更されませんが、NIC ID などを使用する必要があります。

### <a name="io-virtualization-iov-and-wfp-coexistence"></a>I/O 仮想化 (IOV) と WFP の共存

WFP は、IOV で有効にすることはできません切り替えを有効にする試行が行われた場合に、OS によってブロックされます。

### <a name="enabling-or-disabling-wfp"></a>有効化または WFP を無効にします。

WFP 仮想スイッチのコールアウトのインストーラーは、WFP の拡張機能を有効になっている状態を変更しないでください。これは、する必要がありますを有効または WFP 自体を無効にします。



