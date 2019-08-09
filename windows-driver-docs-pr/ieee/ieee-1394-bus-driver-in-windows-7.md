---
title: Windows 7 の IEEE 1394 バス ドライバー
description: Windows 7 には、1394ohci.sys、IEEE 1394 b 仕様で定義されている、高速と別のメディアをサポートする新しい IEEE 1394 バス ドライバーが含まれています。
ms.assetid: 3744C1D5-E411-4E47-9154-40E15626250D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0be9334833e1f4b8644e5b67a15c135c30eed56
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385775"
---
# <a name="ieee-1394-bus-driver-in-windows-7"></a>Windows 7 の IEEE 1394 バス ドライバー

Windows 7 には、1394ohci.sys、IEEE 1394 b 仕様で定義されている、高速と別のメディアをサポートする新しい IEEE 1394 バス ドライバーが含まれています。 1394ohci.sys バス ドライバーは、カーネル モード ドライバー フレームワーク (KMDF) を使用して実装された、単一 (モノリシック) のデバイス ドライバーです。 (以前のバージョンの Windows で使用可能) のレガシ 1394 バス ドライバーには、ポート/ミニポート構成では、Windows Driver Model (WDM) を使用して実装された複数のデバイス ドライバーが含まれています。 1394ohci.sys バス ドライバーには、レガシ ポート ドライバー、1394bus.sys、およびプライマリ ミニポート ドライバー、ochi1394.sys が置き換えられます。

新しい 1394ohci.sys バス ドライバーは、レガシ バス ドライバーと完全に下位互換性です。 このトピックでは、新しいと、従来の 1394 バス ドライバーの動作の既知の違いについて説明します。

> [!NOTE]
> 1394ohci.sys ドライバーは、Windows に含まれているシステム ドライバーです。 1394 コント ローラーをインストールするときに自動的に読み込まれます。 これは、個別にダウンロードできる再頒布可能パッケージ、ドライバーではありません。

* [I/O 要求の完了](#io-request-completion)
* [ROM の構成の取得](#configuration-rom-retrieval)
* [IEEE 1394-1995 PHY サポート](#ieee-1394-1995-phy-support)
* [ノード\_デバイス\_拡張機能の構造体の使用](#node_device_extension-structure-usage)
* [間隔のカウントの最適化](#gap-count-optimization)
* [デバイス ドライバー インターフェイス (DDI) の変更](#device-driver-interface-ddi-changes)
* [関連トピック](#related-topics)

## <a name="io-request-completion"></a>I/O 要求の完了

新しい 1394 バス ドライバーに送信されるすべての I/O 要求が状態を返す\_PENDING は、1394ohci.sys バス ドライバーがあるために、WDM ではなく KMDF を使用して実装されます。 この動作は、どの特定の i/o 要求がすぐに完了、従来の 1394 バス ドライバーの動作とは異なります。

クライアント ドライバーは、新しい 1394 バス ドライバーに送信された I/O 要求が完了するまで待機する必要があります。 要求の完了後に呼び出される I/O 完了ルーチンを行うことができます。 IRP が完了した I/O 要求の状態です。

## <a name="configuration-rom-retrieval"></a>ROM の構成の取得

新しい 1394 バス ドライバーが、バス速度も速くで ROM. のノードの構成の内容を取得するトランザクションは非同期のブロックを使用しようとしています。 レガシ 1394 バス ドライバー S100 速度で作成されますが非同期の読み取りを使用して、または 100 メガ ビット/秒 (Mbps)。 1394ohci.sys バス ドライバーで指定されている値も使用して**生成**と**max\_rom**残りの取得を向上させるために、ノードの ROM 構成ヘッダーのエントリROM. 構成の内容 新しい 1394 バス ドライバーがノードの構成 ROM の内容を取得する方法の詳細については、次を参照してください。 [IEEE 1394 ノードの構成の ROM の内容を取得する](https://docs.microsoft.com/windows-hardware/drivers/ieee/retrieving-the-contents-of-a-ieee-1394-node-s-configuration-rom)します。

## <a name="ieee-1394-1995-phy-support"></a>IEEE 1394-1995 PHY サポート

1394ohci.sys バス ドライバーには、IEEE 1394 a または IEEE 1394 b をサポートする物理層 (PHY) が必要です。 IEEE 1394-1995 をサポートする PHY はサポートしません。 この要件は、1394ohci.sys バス ドライバーの短い (調停) バスのリセットを排他的に使用が原因です。

## <a name="node_device_extension-structure-usage"></a>ノード\_デバイス\_拡張機能の構造体の使用

クライアント ドライバーでは、クライアント ドライバーを制御するデバイスの物理デバイス オブジェクト (PDO) に関連付けられた 1394 バス ドライバーで、デバイスの拡張機能を参照できます。 このデバイスの拡張機能は、**ノード\_デバイス\_拡張子**構造。 1394ohci.sys、従来の 1394 バス ドライバーと同じ場所でこの構造体のままですが、構造体の非静的メンバーを有効にすることはできません。 クライアント ドライバーは、新しい 1394 バス ドライバーを使用して、ときに行う必要がありますで、データにアクセスすることを確認して**ノード\_デバイス\_拡張子**は有効です。 静的メンバー**ノード\_デバイス\_拡張子**有効なデータが含まれる、**タグ**、**デバイス オブジェクト**、および**PortDeviceObject**します。 その他のすべてのメンバー**ノード\_デバイス\_拡張子**は非 static は、クライアント ドライバーを参照する必要があります。

## <a name="gap-count-optimization"></a>間隔のカウントの最適化

1394ohci.sys バス ドライバーの既定の動作は、ローカル ノードを除く、1394 バス上の IEEE 1394 a デバイスのみを見つけたときに、間隔数を最適化するためには。 たとえば、1394ohci.sys を実行しているシステムが IEEE 1394 b に準拠しているホスト コント ローラー、バス上のすべてのデバイスが IEEE 1394 a に従っている場合は、間隔数を最適化するために新しい 1394 バス ドライバーが試みます。

間隔のカウントの最適化は、1394ohci.sys バス ドライバーでは、ローカル ノードがバス マネージャーであるかを決定します。 場合にのみ発生します。

1394ohci.sys バス ドライバーは、ノードの自動 id パケットの速度の設定での IEEE 1394 a にデバイスが準拠しているかどうかを決定します。 ノードの速度 (sp)、ビットの両方が設定されている場合、1394ohci.sys し、自動 id パケット内のフィールドは、IEEE 1394 b に準拠するノードを考慮します。 速度のフィールドにその他の値が含まれている場合は、1394ohci.sys が IEEE 1394 a に準拠するノードを検討します。 使用される間隔の数の値は、ホップ数の関数としての間隔カウントを提供する IEEE 1394 a 仕様内のテーブル E-1 に基づきます。 1394ohci.sys バス ドライバーでは、ギャップのカウントは計算されません。 既定の間隔数の動作を変更するには、レジストリ値を使用します。 詳細については、次を参照してください。 [IEEE 1394 バス ドライバーの既定の動作を変更する](https://docs.microsoft.com/windows-hardware/drivers/ieee/modifying-the-default-behavior-of-the-ieee-1394-bus-driver)します。

## <a name="device-driver-interface-ddi-changes"></a>デバイス ドライバー インターフェイス (DDI) の変更

Windows 7 では、1394 Ddi は 1394 b 仕様で定義されていると 1394 クライアント ドライバーの開発を簡略化の強化された速度をサポートするために変更されました。 新しい 1394 バス ドライバーがサポートする一般的な DDI 変更の詳細については、次を参照してください。 [Windows 7 のデバイス ドライバー インターフェイス (DDI) 変更](https://docs.microsoft.com/windows-hardware/drivers/ieee/device-driver-interface--ddi--changes-in-windows-7)します。

## <a name="related-topics"></a>関連トピック

[IEEE 1394 ドライバー スタック](https://docs.microsoft.com/windows-hardware/drivers/ieee/the-ieee-1394-driver-stack)  
[IEEE 1394 ノードの構成 ROM の内容を取得します。](https://docs.microsoft.com/windows-hardware/drivers/ieee/retrieving-the-contents-of-a-ieee-1394-node-s-configuration-rom)  
