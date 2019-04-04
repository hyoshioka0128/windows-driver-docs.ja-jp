---
title: AV/C ドライバー スタック
description: AV/C ドライバー スタック
ms.assetid: 7745c466-d16e-4af3-be09-7af01777b033
keywords:
- AV/C WDK、ドライバー スタック
- ドライバーは、WDK AV/C をスタックします。
- WDK AV/C のスタック
- Avc.sys 関数ドライバー WDK、ドライバー スタック
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e2bb1dbb60b82b71b1f971efc250810cde13899
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559204"
---
# <a name="avc-driver-stacks"></a>AV/C ドライバー スタック





AV/C デバイスに追加され、IEEE 1394 バスから削除、プラグ アンド プレイ マネージャーは読み込みし、対応するサブユニット ドライバーをアンロードします。 ベンダーは、Windows は、上記の IEEE 1394 スタックに読み込まれるサブユニット ドライバーを記述することで一意の AV/C サブユニット機能を実装*Avc.sys*します。 *Avc.sys*デバイスを制御して接続し、管理のプラグを基になる IEEE 1394 および IEC 61883 ドライバーによって提供される機能を使用します。 これらの基になるドライバー スタックの詳細については、[、IEEE 1394 ドライバー スタック](https://msdn.microsoft.com/library/windows/hardware/ff538867)と[IEC 61883 クライアント ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff537188)を参照してください。

ピアのドライバー スタックは、外部の AV/C デバイスでのサブユニットです。 これに対し、仮想ドライバー スタックは、IEEE 1394 バスに接続されている他の AV/C デバイス AV/C デバイスとしてコンピューターを公開する個別のドライバー スタックです。 次の図は、2 つの異なるを示します*Avc.sys*スタック。

![別のピア サブユニットと仮想のサブユニット スタックを示す図](images/avcdiag.gif)

スタックには、ドライバーの基本*1394ohci.sys*と*1394bus.sys*します。 これらのドライバーでは、IEEE 1394 バス インフラストラクチャの基本的なサポートを提供します。 システムには、これらの各物理の IEEE 1394 アダプターのドライバーのインスタンスがあります。

上に重ねて*1394ohci.sys*と*1394bus.sys*は*61883.sys*します。 インスタンスがある*61883.sys*の IEEE 1394 バスに各 IEC 61883-有効になっているノード。 ドライバーの*61883.sys* IEC 61883 プロトコルは、次のサポート。

-   接続の管理プロトコル (CMP) IEC 61883 1

-   一般的な Isochronous パケット (CIP) IEC 61883 1

-   関数制御プロトコル (FCP) IEC 61883 1

上記積み上げ*61883.sys*は*Avc.sys*AV/C プロトコルを各 AV/C デバイスでアクティブなサブユニットのプラグ アンド プレイの列挙をサポートして、AV/C サブユニットのプラグイン接続の管理および制御します。 プラグインの接続と形式の管理の詳細については、[AV/C サブユニットのプラグイン接続と形式管理](av-c-subunit-plug-connection-and-format-management.md)を参照してください。

上記のサブユニット ドライバーが積み重ねられている*Avc.sys*します。 これは、ベンダーが、AV/C サブユニットに一意の機能を実装するレイヤーです。 一般に、AV/C サブユニットの物理インスタンスがすべてではそのサブユニットのドライバの対応するインスタンスです。 つまり、各デバイス識別子 (ID) がのインスタンスで表されます*Avc.sys*します。 ただし、 *Avc.sys*に基づいてオーバーライドするには、この動作を許可、***ベンダー***や***モデル***AV/C 単位のデバイス識別子のフィールド。 詳細については、***ベンダー***、***モデル***、 ***SubunitType***、および***SubunitID***のデバイス識別子の文字列が生成されたフィールドによって*Avc.sys*を参照してください[AV/C デバイス Id](av-c-device-identifiers.md)します。

 

 




