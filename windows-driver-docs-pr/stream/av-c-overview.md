---
title: AV/C の概要
description: AV/C の概要
ms.assetid: ff9e6dfc-7ab4-4b56-8b47-d3ea46b579e0
keywords:
- AV/C WDK、AV/C について
- Avc.sys function driver WDK
- ピア Avc.sys モード WDK AV/C
- 仮想 Avc.sys モード WDK AV/C
- Avc.sys 関数ドライバーに関する Avc.sys 関数ドライバー WDK、
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e01a56600aca0974afda1d4099d42cc4baad68a6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550468"
---
# <a name="avc-overview"></a>AV/C の概要





このセクションでは、Microsoft が提供について説明します*Avc.sys*関数ドライバー、オーディオ/ビデオ コントロールの IEEE 1394 (AV/C) プロトコルのサポートを提供します。 このセクションでは、AV/C に準拠しているデバイスの AV/C サブユニット ドライバーを開発するためのガイドラインも提供します。 AV/C プロトコルの詳細については 使用可能な[1394 業界団体](https://go.microsoft.com/fwlink/p/?linkid=518448)web サイト。 ベンダーが、Microsoft 提供のドライバーを使用する場合があります*Msdv.sys*または*Mstape.sys*、該当する場合は、そのテープのサブユニットをサポートするためにします。 これらの 2 つのクラス ドライバーでは、テープのサブユニット用のドライバーの記述が不要にします。

*Avc.sys* 2 つの動作モードを提供します。 ピア仮想と。 *Avc.sys*ピア モードは、外部の AV/C デバイスでのサブユニットをサポートしています。 *Avc.sys*仮想モードには、AV/C サブユニットとして公開するコンピューターの機能とそのためコンピューターを AV/C の有効なターゲット コマンド間での IEEE 1394 シリアル バス AV C/その他のデバイスから要求します。

*Avc.sys*別個のピアのサブユニットと仮想のサブユニットをサポートするドライバー スタック。 さまざまなモードが同一の機能をサポートしていないことに注意してください。 ピアのサブユニットと仮想のサブユニット ドライバー スタックの詳細については、次を参照してください。 [AV/C ドライバー スタック](av-c-driver-stacks.md)します。

*Avc.sys*ピアと仮想のサブユニットの両方のデバイス識別子 (Id) が生成されます。 デバイス識別子とを関連付ける正しい INF ファイルのサブユニット ドライバーのサブユニット。 AV/C をデバイスが、コンピューターに接続したときに*Avc.sys*ピアのサブユニットとしてアクティブのサブユニットを列挙します。 Windows は、サブユニットに対応するドライバーを読み込みます。 両方のピアと仮想のサブユニット デバイス識別子の文字列の書式設定に関する詳細については、次を参照してください。 [AV/C デバイス Id](av-c-device-identifiers.md)します。

*Avc.sys*次の機能を提供します。

-   ピアのサブユニット ドライバーに代わって AV/C 仕様で定義されている 100 ミリ秒要件内の暫定的な回答します。 *Avc.sys* AV/C コマンドまたはクエリの最後の応答のみを返します。 仮想のサブユニット ドライバーでは、中間および最終応答が生成もする必要があります。

-   AV/C サブユニットから、それぞれのサブユニット ドライバーへの応答をルーティングします。 サブユニット ドライバーは、自社のハードウェアのみからの応答を受信します。

-   IEC 61883 は、列挙およびカーネル ストリーミング (KS) フレームワーク内でコントロールを接続します。 プラグインの接続とデータの形式の詳細については、次を参照してください。 [AV/C サブユニットのプラグイン接続と形式管理](av-c-subunit-plug-connection-and-format-management.md)します。

サブユニット ドライバーには、Stream クラス インターフェイスまたは新しい AVStream インターフェイスを使用できます。 さらに、サブユニット ドライバーでは、独自 KS プロキシがユーザー モード アプリケーションへのカスタム プロパティ ページを公開するプラグインを提供できます。 詳細については、次を参照してください。 [AV/C カーネル ストリーミング インターフェイスと KS プロキシ プラグイン](av-c-kernel-streaming-interface-and-kernel-streaming-proxy-plug-ins.md)します。

通常、ベンダーをサポートするために、AV/C サブユニット ドライバーを記述します。

-   によって定義されているデバイスの種類に基づくサブユニットの制御、 [1394 貿易仕様](https://go.microsoft.com/fwlink/p/?LinkId=518448)web サイト

-   IEEE 1394 バスで IEC 61883 標準に基づくデータのストリームへのプラグイン接続を管理します。 61883 の標準の詳細については、次を参照してください。、 [IEC](https://go.microsoft.com/fwlink/p/?linkid=8732) web サイト。

 

 




