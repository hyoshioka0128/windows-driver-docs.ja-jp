---
title: 受信トレイのドライバーのビルドでプライベートのインストールの概要
description: 受信トレイのドライバーのビルドでプライベートのインストールの概要
ms.assetid: eec9474c-5aad-4b81-b7df-5e89cbfe92ab
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81b932c128bc20b87c13ad617e99ef47ea6ebbf6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556662"
---
# <a name="overview-of-installing-private-builds-of-inbox-drivers"></a>受信トレイのドライバーのビルドでプライベートのインストールの概要


プラグ アンド プレイ (PnP) デバイスがコンピューター システムにインストールされている場合は、Windows vista では、以降、Windows の選択などのいくつかの要因に基づいて、ドライバー、[ハードウェア ID](hardware-ids.md)または[互換性 ID](compatible-ids.md)日付、およびバージョン。 Windows では、ドライバーがデバイスに一致する度合いを示すランクを割り当てるこれらの要因を分析します。 ランク、一致するドライバーが高まりますが、デバイスは低くなります。

また、以降、Windows Vista では、ドライバーには、Windows の署名機関 (Microsoft 署名) からの署名が含まれている場合、Windows ランク付けで署名されているデバイスに対する別のドライバーよりも優れています。

-   サード パーティ製のリリースの署名。 この種類の署名の生成を使用して、[ソフトウェア発行元の証明書](software-publisher-certificate.md)このような証明書を発行するために Microsoft によって承認されて、サード パーティの証明機関 (CA) から取得しました。

-   Windows のバージョンよりも前の Microsoft の署名、 [LowerLogoVersion](lowerlogoversion.md)のドライバーの値[デバイス セットアップ クラス](device-setup-classes.md)します。

Microsoft 署名の種類を以下に示します。

-   Premium WHQL 署名と標準 WHQL 署名

-   受信トレイのドライバーの署名

-   Windows Sustained Engineering (Windows SE) の署名

-   同じである Windows バージョンについては、WHQL 署名で指定されている Windows バージョンよりも、 [LowerLogoVersion](lowerlogoversion.md)ドライバーのデバイス セットアップ クラスが設定されている値

**注**  Windows が Microsoft 署名を持つドライバーを選択して、デバイスに適しているサード パーティ製のシグネチャを持つドライバー場合。 パブリッシャー id 証明書を使用して\[PIC\]のサード パーティの署名には、この動作は変わりません。

 

以降、Windows Vista では、 [ **AllSignersEqual**グループ ポリシー](allsignersequal-group-policy--windows-vista-and-later-.md) Windows が Microsoft によって署名されたドライバーとサード パーティの署名されたドライバーにランク付けを制御します。 ときに**AllSignersEqual**が有効にすると、Windows すべての Microsoft の署名およびサード パーティの署名として扱いますランクに関して等しいデバイスに最適なものであるドライバーを選択するとします。

**注**  で Windows Vista および Windows Server 2008 では、 **AllSignersEqual**グループ ポリシーが既定で無効になっています。 Windows 7 以降、このグループ ポリシーは既定で有効にします。

 

受信トレイのドライバーのプライベート ビルドをインストールするには、次の操作を行う必要があります。

-   受信トレイのドライバーのプライベート バージョンをビルドします。 署名が均等に扱われた場合に、プライベート ビルドで、Microsoft によって署名されたバージョンを outranks することを確認する必要があります。 WDK で提供されるツールを使用してプライベートのビルドはデジタル署名もする必要があります。

    詳細については、[受信トレイのドライバーのプライベート ビルドを作成する](creating-a-private-build-of-an-in-box-driver.md)を参照してください。

-   有効にする、 [AllSignersEqual グループ ポリシー](allsignersequal-group-policy--windows-vista-and-later-.md)ターゲット システムにようにドライバーを選択するとすべての Microsoft 署名の種類とサード パーティの署名とランクが等しいとしてをオペレーティング システムがビューであることをデバイスに最適なものです。

    詳細については、[に均等にドライバー署名を順位を構成する Windows](configuring-windows-to-rank-driver-signatures-equally.md)を参照してください。

Windows ドライバーをランク付けする方法の詳細については、[Windows ドライバーを選択する方法](how-setup-selects-drivers.md)を参照してください。

 

 





