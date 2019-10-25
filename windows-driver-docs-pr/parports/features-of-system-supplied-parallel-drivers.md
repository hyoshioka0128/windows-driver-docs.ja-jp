---
title: システム提供のパラレル ドライバーの機能
description: システム提供のパラレル ドライバーの機能
ms.assetid: 6d579a88-4608-4333-9789-e10c562fc644
keywords:
- システム提供のパラレルドライバー WDK、システム提供のパラレルドライバーについて
- Parclass ドライバー
- Parport ドライバー
- 機能デバイスオブジェクトの WDK ポート
- FDOs WDK ポート
- IEEE 1284 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8b7d9be6ebaa7e400fab3ff127e0a4ee0eac336
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831477"
---
# <a name="features-of-system-supplied-parallel-drivers"></a>システム提供のパラレル ドライバーの機能





このセクションでは、並列ポートおよびパラレルポートに接続されているデバイス用のシステム提供のパラレルドライバーの機能について説明します。

Windows 2000 以降では、64ビットバージョンの Microsoft Windows を除き、パラレルポート関数ドライバーと、パラレルポートに接続されているプラグアンドプレイデバイス用のパラレルポートバスドライバーが提供されます。 Microsoft では、64ビットバージョンの Windows 用のパラレルドライバーは提供していません。

Windows 2000 には、次のドライバーが含まれています。

-   *Parclass*は、パラレルポートに接続されているデバイスのパラレルポートバスドライバーです。 Parclass の実行可能イメージは、 *.sys*です。

-   *Parport*はパラレルポート関数ドライバーです。 Parport の実行可能イメージは*Parport*です。

Parclass と Parport の操作は、並列ポートおよび[パラレルポートコールバックルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)[に対する内部デバイス制御要求](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を介して密接に接続されています。

Windows XP 以降では、Parclass が削除され、Parport はパラレルポート関数ドライバーとパラレルポートバスドライバーの両方の機能を提供します。 Windows XP での Parport の実行可能イメージは*Parport*です。

パラレルポート用のシステム提供の関数ドライバーは、システムで列挙された各パラレルポートを表す機能デバイスオブジェクト (FDO) を作成します。 パラレルポート用のシステム提供のバスドライバーは、バスドライバーがポートで列挙する各並列デバイスを表す物理デバイスオブジェクト (PDO) を作成します。 [ベンダーが提供するパラレルドライバー](vendor-supplied-parallel-drivers.md)などのクライアントは、並列デバイスの PDO によって提供されるインターフェイスと、デバイスの親ポートの FDO を介して並列デバイスを操作します。

並列ドキュメントに記載されている軽微な操作上の相違点を除いて、[クライアントインターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)は、windows XP 以降の場合と同じように、windows 2000 でも同じです。

システムで提供されるパラレルドライバーは、次の機能をサポートしています。

-   レガシパラレルポート、標準パラレルポートデバイス、IEEE 1284 互換デバイス、IEEE 1284 準拠デバイス、ieee 1284.3 デイジーチェーンデバイス

-   ほとんどの通信モード (セントロニクスモード、IEEE 1284 モード、拡張機能ポート (ECP) モード、および拡張パラレルポート (EPP) モードを含む)

-   プラグアンドプレイ、電源管理、および Windows Management Instrumentation (WMI)

-   システムにインストールされているすべてのパラレルポートへの共有アクセス

-   すべての並列デバイスへの生のアクセス

-   パラレルポートとデバイスを操作するための Ioctl とコールバック--[パラレルポートとデバイスに対する ioctl およびコールバックのサポート](ioctl-and-callback-support-for-parallel-ports-and-devices.md)

システムによって提供されるパラレルドライバーは、IEEE 1284.3 デバイスの次の*部分的*なサポートを提供します。

- *サービスプロバイダーインターフェイス*と機能的に等価なデバイスコントロール要求とコールバックルーチンの組み合わせ。 「IEEE P 1284.3 仕様」の「 *Service Provider Interface (SPI)* 」を参照してください。

- Ieee P 1284.3 仕様の*デイジー*チェーン句で定義され<em>ているように、</em>複数の ieee 1284.3 デイジーチェーンデバイスとチェーン終了デバイスの選択と操作。

- データリンク層をサポートするための基本サービス (IEEE P 1284.3 仕様の*data link layer*句で指定)。「 [Ieee 1284.3 データリンクデバイスへの接続](connecting-to-an-ieee-1284-3-data-link-device.md)」を参照してください。

システム提供のパラレルドライバーでは、次の IEEE 1284.3 仕様は*サポートされていません*。

-   Multiplexors。 IEEE P 1284.3 仕様の*マルチプレクサーです*句で指定されています。

    今後のリリースの Windows では、この機能をサポートする予定はありません。

-   IEEE 1284.3 デイジーチェーンデバイスの割り込み。

システムによって提供されるパラレルドライバーは、次のものを作成します。

-   デバイスオブジェクト、インターフェイス、および保護されていないシンボリックリンク。「[パラレルポートとデバイスのデバイススタック](device-stacks-for-parallel-ports-and-devices.md)」で説明されています。

-   各パラレルポートの作業キュー。

    パラレルポート用のシステム提供の関数ドライバーは、パラレルポートを割り当て、パラレルポートに接続されている IEEE 1284.3 デバイスを選択するために、i/o 要求をキューに配置します。

-   各並列デバイスのワーカースレッドと作業キュー。

    パラレルポート用のシステム提供のバスドライバーは、読み取り、書き込み、デバイスコントロール、および内部デバイスコントロールをすぐに完了できない場合に、次の i/o 要求をキューに置いています。

パラレルポートおよびパラレルポートに接続されているデバイスを操作する方法の詳細については、以下を参照してください。

[パラレル ポートとデバイスの概要](introduction-to-parallel-ports-and-devices.md)

[ベンダー提供のパラレル ドライバー](vendor-supplied-parallel-drivers.md)

[システム提供のパラレルドライバーへのクライアントインターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

パラレルポートとデバイス標準の詳細については、次の仕様を参照してください。

-   パーソナルコンピューター用の双方向パラレル周辺インターフェイスの ieee Std 1284-1994 (IEEE Standard シグナリング方式)

-   Ieee P 1284.3、インターフェイスとプロトコル拡張機能、IEEE 1284-1994 準拠の周辺機器とホストアダプター、Draft D 6.00、12月3日、1998

 

 




