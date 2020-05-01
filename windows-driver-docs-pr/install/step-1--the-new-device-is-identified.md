---
title: 手順 1 新しいデバイスが識別される
description: 手順 1 新しいデバイスが識別される
ms.assetid: e0df70ca-cea3-44a1-b5ff-407f72a216f9
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: f0ab1d4c956403fb9fac8f2174594dd081f68e8d
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "72007639"
---
# <a name="step-1-the-new-device-is-identified"></a>手順 1:新しいデバイスが識別されます


新しいデバイス用のドライバーをインストールする前に、デバイスが接続されているバス ドライバーまたはハブ ドライバーによって、デバイスに[ハードウェア識別子 (ID)](hardware-ids.md) が割り当てられます。 Windows では、デバイスと、デバイスのドライバーが含まれる[ドライバー パッケージ](driver-packages.md)との間で最も近い一致を見つけるため、ハードウェア ID が使用されます。 ハードウェア ID の詳細については、「[デバイスの識別用文字列](device-identification-strings.md)」を参照してください。

通常、ハードウェア ID の形式は次の要素で構成されています。

-   PCI\\ や USB\\ など、バス固有のプレフィックス。
-   ベンダー識別子、モデル識別子、リビジョン識別子など、デバイスのベンダー固有の識別子。 ハードウェア ID 内のこれらの識別子の形式は、バス ドライバーにも固有です。

独立系ハードウェア ベンダー (IHV) は、デバイスに対して[互換性 ID](compatible-ids.md) を 1 つ以上定義することもできます。 互換性 ID はハードウェア ID と同じ形式です。ただし、通常はハードウェア ID より汎用的で、特定の製造元情報やモデル情報は必要ありません。 Windows では、これらの識別子を使用して、デバイスのハードウェア ID と一致するドライバー パッケージが見つからない場合に、デバイスに対して[ドライバー パッケージ](driver-packages.md)が選択されます。 IHV は、ドライバー パッケージの [INF ファイル](overview-of-inf-files.md)内のデバイスに対して、互換性のある ID を 1 つ以上指定します。

Windows では、ハードウェア ID と互換性 ID を使用して、デバイスに対応する[ドライバー パッケージ](driver-packages.md)を検索します。 デバイスのハードウェア ID と互換性 ID を、パッケージの [INF ファイル](overview-of-inf-files.md)内で指定されている ID と比較することによって、デバイスに対応するドライバー パッケージを検索します。

たとえば、ユーザーがワイヤレス ローカルエリア ネットワーク (WLAN) アダプターをコンピューターに接続されている USB ハブのポートに接続すると、次の手順が実行されます。

1.  デバイスが、USB ハブ ドライバーによって検出されます。 ハブ ドライバーは、アダプターから照会した情報に基づいて、デバイスのハードウェア ID を作成します。

    たとえば、USB ハブ ドライバーは、次のように、WLAN アダプター用の USB\\VID_1234&PID_5678&REV_0001 のハードウェア ID を作成できます。

    -   VID_1234 は、ベンダーの識別子です。
    -   PID_5678 は、デバイスの製品 (モデル) 識別子です。
    -   REV_0001 は、デバイスのリビジョン識別子です。

    USB ハードウェア ID の形式の詳細については、「[USB デバイスの識別子](identifiers-for-usb-devices.md)」を参照してください。

2.  USB ハブ ドライバーは、新しいデバイスが検出されたことを[プラグ アンド プレイ (PnP) マネージャー](pnp-manager.md)に通知します。 PnP マネージャーは、すべてのデバイスのハードウェア ID をハブ ドライバーに照会します。 ハブ ドライバーは、同じデバイスに対して複数のハードウェア ID を作成できます。

3.  [PnP マネージャー](pnp-manager.md)は、新しいデバイスをインストールする必要があることを Windows に通知します。 この通知の一部として、ハードウェア ID の一覧が Windows に提供されます。

4.  Windows では、デバイスのハードウェア ID のいずれかに一致する[ドライバー パッケージ](driver-packages.md)の検索が開始されます。 対応するハードウェア ID が見つからない場合は、デバイスの互換性 ID が一致するドライバー パッケージを検索します。

    このプロセスの詳細については、「[手順 2: デバイスのドライバーが選択されます](step-2--a-driver-for-the-device-is-selected.md)」を参照してください。

各バス ドライバーでは、それぞれのバス固有の方法でハードウェア ID が構築されます。

他のバスの標準化された識別子の例については、次を参照してください。

*  [PCI デバイスの識別子](identifiers-for-pci-devices.md)
*  [SCSI デバイスの識別子](identifiers-for-scsi-devices.md)
*  [IDE デバイスの識別子](identifiers-for-ide-devices.md)
*  [PCMCIA デバイスの識別子](identifiers-for-pcmcia-devices.md)
*  [ISAPNP デバイスの識別子](identifiers-for-isapnp-devices.md)
*  [1394 デバイスの識別子](identifiers-for-1394-devices.md)
*  [Secure Digital (SD) デバイスの識別子](identifiers-for-secure-digital--sd--devices.md)
*  [USB デバイスの識別子](identifiers-for-usb-devices.md)


 





