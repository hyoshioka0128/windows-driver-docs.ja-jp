---
title: システム提供のパラレル ドライバーの機能
description: システム提供のパラレル ドライバーの機能
ms.assetid: 6d579a88-4608-4333-9789-e10c562fc644
keywords:
- システムから提供された並列ドライバー WDK、システム提供平行ドライバーについて
- Parclass ドライバー
- Parport ドライバー
- 機能のデバイス オブジェクトの WDK ポート
- Fdo WDK ポート
- IEEE 1284 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a3069fb56abe1b79b2817f593c7fcd56f154dc6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382077"
---
# <a name="features-of-system-supplied-parallel-drivers"></a>システム提供のパラレル ドライバーの機能





このセクションでは、パラレル ポートおよびパラレル ポートに接続されているデバイスのシステム提供平行ドライバーの機能について説明します。

Microsoft Windows の 64 ビット バージョンを除いては、Windows 2000 以降は、パラレル ポートに接続されているプラグ アンド プレイ デバイスのパラレル ポート関数ドライバーおよびパラレル ポート バス ドライバーを提供します。 マイクロソフトでは、Windows の 64 ビット バージョンの並列のドライバーを提供していません。

Windows 2000 には、次のドライバーが含まれています。

-   *Parclass*パラレル ポートに接続されているデバイスのパラレル ポート バス ドライバーです。 Parclass の実行可能イメージが *, 176 parallel.sys*します。

-   *Parport*パラレル ポート関数ドライバーです。 Parport の実行可能イメージが*parport.sys*します。

Parclass と Parport の操作が密接にを介して接続されている[パラレル ポートの内部デバイス制御要求](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)と[ポート コールバック ルーチンを並列](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

Windows XP 以降では、Parclass が削除され、Parport パラレル ポート機能のドライバーと、パラレル ポート バス ドライバーの両方の機能を提供します。 Windows XP で Parport の実行可能イメージが*parport.sys*します。

パラレル ポートのシステムによって提供される関数のドライバーでは、システムに列挙された各パラレル ポートを表すオブジェクト (FDO) の機能のデバイスを作成します。 パラレル ポートのシステム提供のバス ドライバーでは、バス ドライバーは、ポートを列挙する並列各デバイスを表すオブジェクト (PDO) の物理デバイスを作成します。 たとえばクライアント[並列ドライバーのベンダーから提供された](vendor-supplied-parallel-drivers.md)、並列のデバイスの PDO とデバイスの親のポートの FDO によって提供されるインターフェイスを使用して並列デバイスを操作します。

並列のドキュメントで説明されている運用マイナーの相違点を除いて、[システム提供平行ドライバーへのクライアント インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)は Windows 2000 と Windows XP のようにその後で同じです。

システム提供平行ドライバーのサポート:

-   従来のパラレル ポート、パラレル ポートの標準的なデバイス、IEEE 1284 と互換性のあるデバイス、IEEE 1284 に準拠したデバイス、および IEEE 1284.3 デイジー チェーン デバイス

-   セントロニクス モード、IEEE 1284 モード、拡張機能ポート (ECP) モード、および強化されたパラレル ポート (EPP) モードを含めて、ほとんどの通信モード

-   プラグ アンド プレイ、電源管理、および Windows Management Instrumentation (WMI)

-   システムにインストールされているすべてのパラレル ポートへのアクセスを共有

-   並列のすべてのデバイスへの生のアクセス

-   Ioctl およびパラレル ポートやデバイスを操作するコールバックを参照してください[IOCTL およびパラレル ポートとデバイスのコールバック サポート。](ioctl-and-callback-support-for-parallel-ports-and-devices.md)

次を提供するシステム提供平行ドライバー*部分*IEEE 1284.3 デバイスのサポートします。

- 機能的に等価であるコントロールとデバイスの要求とコールバック ルーチンの組み合わせ、*サービス プロバイダー インターフェイス*します。 参照してください*サービス プロバイダー インターフェイス (SPI)* IEEE P1284.3 仕様。

- 選択と 1 つ以上の IEEE 1284.3 デイジー チェーン接続デバイスと、最後のチェーンのデバイスの操作<em>、として</em>で定義されている、*デイジー チェーン*IEEE P1284.3 仕様の句。

- データをサポートするための基本的なサービスで指定されているレイヤーをリンクする、*データ リンク層*IEEE P1284.3 仕様--の句を参照してください[IEEE 1284.3 データ リンク デバイスへの接続](connecting-to-an-ieee-1284-3-data-link-device.md)します。

システム提供平行ドライバー*をサポートしていない*次の IEEE 1284.3 仕様。

-   指定されている、multiplexors、*マルチプレクサ*IEEE P1284.3 仕様の句。

    Windows の将来のリリースでこの機能をサポートする予定はありません。

-   デバイスの IEEE 1284.3 デイジー チェーンの中断します。

システム提供平行ドライバーを作成します。

-   デバイス オブジェクト、インターフェイス、および保護されていないシンボリック リンクで説明するよう[パラレル ポートやデバイスのデバイス スタック](device-stacks-for-parallel-ports-and-devices.md)します。

-   パラレル ポートごとの作業キュー。

    パラレル ポートを割り当てると、パラレル ポートに接続されている IEEE 1284.3 デバイスを選択する、パラレル ポート キュー I/O 要求のシステムによって提供される関数ドライバー。

-   ワーカー スレッドと作業を並列デバイスごとにキューします。

    パラレル ポートのシステム提供のバス ドライバーは、それらをすぐに完了できない場合に、次の I/O 要求をキュー: 読み取り、書き込み、デバイスの制御、および内部のデバイスの制御。

パラレル ポートおよびパラレル ポートに接続されたデバイスが動作する方法の詳細についてを参照してください。

[パラレル ポートとデバイスの概要](introduction-to-parallel-ports-and-devices.md)

[ベンダー提供のパラレル ドライバー](vendor-supplied-parallel-drivers.md)

[システム提供平行ドライバーへのクライアント インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

パラレル ポートとのデバイス標準については、次の仕様を参照してください。

-   IEEE Std 1284 1994 年、IEEE 標準のパーソナル コンピューター用の双方向の平行周辺インターフェイスのメソッドをシグナル通知

-   IEEE P1284.3、インターフェイスとプロトコルの拡張に準拠している周辺機器の IEEE 1284 1994、ホスト アダプターの Standard ドラフト D6.00、1998 年 12 月 3 日

 

 




