---
title: 手順 1. 新しいデバイスを識別する
description: 手順 1. 新しいデバイスを識別する
ms.assetid: e0df70ca-cea3-44a1-b5ff-407f72a216f9
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: f0ab1d4c956403fb9fac8f2174594dd081f68e8d
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007639"
---
# <a name="step-1-the-new-device-is-identified"></a>手順 1:新しいデバイスが識別されます


新しいデバイス用のドライバーをインストールする前に、デバイスが接続されているバスまたはハブドライバーによって、デバイスに[ハードウェア識別子 (ID)](hardware-ids.md)が割り当てられます。 Windows はハードウェア Id を使用して、デバイスと、デバイスのドライバーを含む[ドライバーパッケージ](driver-packages.md)との間で最も近い一致を見つけます。 ハードウェア Id の詳細については、「[デバイス Id 文字列](device-identification-strings.md)」を参照してください。

ハードウェア ID の形式は、通常、次のように構成されています。

-   バス固有のプレフィックス (PCI @ no__t-0、USB @ no__t など)。
-   ベンダー、モデル、リビジョン識別子など、デバイスのベンダー固有の識別子。 ハードウェア ID 内のこれらの識別子の形式は、バスドライバーにも固有です。

独立系ハードウェアベンダー (IHV) は、デバイスに対して1つ以上の[互換性のある id](compatible-ids.md)を定義することもできます。 互換性 Id はハードウェア Id と同じ形式です。ただし、通常はハードウェア Id より汎用的で、特定の製造元やモデル情報は必要ありません。 Windows では、デバイスのハードウェア ID と一致するドライバーパッケージが見つからない場合に、これらの識別子を使用してデバイスの[ドライバーパッケージ](driver-packages.md)を選択します。 Ihv は、ドライバーパッケージの[INF ファイル](overview-of-inf-files.md)内のデバイスに対して、互換性のある id を1つ以上指定します。

Windows では、ハードウェア Id と互換性 Id を使用して、デバイスの[ドライバーパッケージ](driver-packages.md)を検索します。 デバイスのハードウェア Id と互換性のある Id を、パッケージの[INF ファイル](overview-of-inf-files.md)内で指定されている id と比較することによって、デバイスに一致するドライバーパッケージを検索します。

たとえば、ユーザーがワイヤレスローカルエリアネットワーク (WLAN) アダプターをコンピューターに接続されている USB ハブのポートに接続すると、次の手順が実行されます。

1.  デバイスは、USB hub ドライバーによって検出されます。 アダプターからクエリを行う情報に基づいて、ハブドライバーはデバイスのハードウェア ID を作成します。

    たとえば、USB ハブドライバーは、次のように、WLAN アダプターの USB @ no__t-0VID_1234 & PID_5678 & REV_0001 のハードウェア ID を作成できます。

    -   VID_1234 は、ベンダーの識別子です。
    -   PID_5678 は、デバイスの製品 (モデル) 識別子です。
    -   REV_0001 は、デバイスのリビジョン識別子です。

    USB ハードウェア Id の形式の詳細については、「 [Usb デバイスの識別子](identifiers-for-usb-devices.md)」を参照してください。

2.  USB hub ドライバーは、新しいデバイスが検出されたことを[プラグアンドプレイ (PnP) マネージャー](pnp-manager.md)に通知します。 PnP マネージャーは、すべてのデバイスのハードウェア Id をハブドライバーに照会します。 ハブドライバーは、同じデバイスに対して複数のハードウェア Id を作成できます。

3.  [PnP マネージャー](pnp-manager.md)は、新しいデバイスをインストールする必要があることを Windows に通知します。 この通知の一部として、ハードウェア Id の一覧が Windows に付属しています。

4.  Windows は、デバイスのハードウェア Id のいずれかに一致する[ドライバーパッケージ](driver-packages.md)の検索を開始します。 一致するハードウェア ID が見つからない場合は、デバイスの互換性 ID が一致するドライバーパッケージを検索します。

    このプロセスの詳細については、次を参照してください [Step 2:デバイスのドライバーが選択されています @ no__t-0 です。

各バスドライバーは、独自のバス固有の方法でハードウェア Id を構築します。

他のバスの標準化された識別子の例については、次を参照してください。

*  [PCI デバイスの識別子](identifiers-for-pci-devices.md)
*  [SCSI デバイスの識別子](identifiers-for-scsi-devices.md)
*  [IDE デバイスの識別子](identifiers-for-ide-devices.md)
*  [PCMCIA デバイスの識別子](identifiers-for-pcmcia-devices.md)
*  [ISAPNP デバイスの識別子](identifiers-for-isapnp-devices.md)
*  [1394デバイスの識別子](identifiers-for-1394-devices.md)
*  [セキュアデジタル (SD) デバイスの識別子](identifiers-for-secure-digital--sd--devices.md)
*  [USB デバイスの識別子](identifiers-for-usb-devices.md)


 





