---
title: 手順 1 の新しいデバイスを識別します。
description: 手順 1 の新しいデバイスを識別します。
ms.assetid: e0df70ca-cea3-44a1-b5ff-407f72a216f9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 176fe9318ae5339fb42984174bf8f040458f9db6
ms.sourcegitcommit: 6dff49ca5880466c396be5b889c44481dfed44ec
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2019
ms.locfileid: "67161522"
---
# <a name="step-1-the-new-device-is-identified"></a>手順 1:新しいデバイスが識別されます


デバイスが接続されている割り当てに新しいデバイス、バス、またはハブ ドライバーのドライバーをインストールする前に、[ハードウェア識別子 (ID)](hardware-ids.md)デバイスにします。 Windows がハードウェア Id を使用して、デバイス間で最も近い一致を見つけ、[ドライバー パッケージ](driver-packages.md)デバイスのドライバーを格納しています。 ハードウェア Id の詳細については、次を参照してください。[識別文字列](device-identification-strings.md)します。

通常、ハードウェア ID の形式は、次ので構成されます。

-   PCI などのバス固有プレフィックス\\または USB\\します。
-   仕入先、モデル、およびリビジョン識別子など、デバイスのベンダー固有の識別子です。 ハードウェア ID 内でこれらの識別子の形式は、バス ドライバーにもできます。

独立系ハードウェア ベンダー (IHV) が 1 つまたは複数定義することも[互換性 Id](compatible-ids.md)デバイス。 互換性 Id があるハードウェア Id と同じ形式ただし、これらは通常、ハードウェア Id よりも汎用的な特定の製造元またはモデルの情報は必要ありません。 Windows では、これらの識別子を使用して、選択、[ドライバー パッケージ](driver-packages.md)オペレーティング システムでは、デバイスのハードウェア ID の一致するドライバー パッケージが見つからない場合、デバイスの Ihv は、ドライバー パッケージ内のデバイスの 1 つ以上の互換性のある Id を指定[INF ファイル](overview-of-inf-files.md)します。

Windows ハードウェア Id および互換性 Id を使用して検索を[ドライバー パッケージ](driver-packages.md)デバイス。 デバイスのハードウェア Id および互換性 Id に対して、パッケージ内の指定されているこれらの Id を比較することによって、デバイスに一致するドライバー パッケージを見つけた[INF ファイル](overview-of-inf-files.md)します。

たとえば、ユーザーには、コンピューターに接続されている USB ハブのポートにワイヤレス ローカル エリア ネットワーク (WLAN) アダプターが接続されるため、次の手順が発生します。

1.  デバイスは、USB ハブのドライバーで検出されます。 アダプターからのクエリ情報に基づいて、ハブのドライバーは、デバイスのハードウェア ID を作成します。

    たとえば、USB ハブのドライバーを作成、ハードウェア ID の USB\\VID_1234 & PID_5678 REV_0001、WLAN アダプターの場所。

    -   VID_1234 は、仕入先の識別子です。
    -   PID_5678 は、デバイスの製品、またはモデルの識別子です。
    -   REV_0001 は、デバイスのリビジョン識別子です。

    USB ハードウェア Id の形式の詳細については、次を参照してください。 [USB デバイスの識別子](identifiers-for-usb-devices.md)します。

2.  USB ハブのドライバーに通知、[プラグ アンド プレイ (PnP) manager](pnp-manager.md)を新しいデバイスが検出されました。 PnP マネージャーでは、デバイスのハードウェア Id のすべてのハブのドライバーをクエリします。 ハブのドライバーでは、同じデバイスに複数のハードウェア Id を作成できます。

3.  [PnP マネージャー](pnp-manager.md)インストールする必要がある新しいデバイスを Windows に通知します。 この通知の一部として、Windows は、ハードウェア Id の一覧で提供されます。

4.  Windows の検索を開始する、[ドライバー パッケージ](driver-packages.md)デバイスのハードウェア Id のいずれかに一致します。 Windows では、一致するハードウェア ID を見つけられない場合は、デバイスの場合は、一致する互換性のある ID を持つドライバー パッケージを検索します。

    このプロセスの詳細については、次を参照してください。[手順 2。デバイスのドライバーが選択されている](step-2--a-driver-for-the-device-is-selected.md)します。

各バス ドライバーでは、バスに固有の方法は、独自のハードウェア Id を構築します。

他のバスの標準化された識別子の例についてを参照してください。

*  [PCI デバイスの識別子](identifiers-for-pci-devices.md)
*  [SCSI デバイスの識別子](identifiers-for-scsi-devices.md)
*  [IDE デバイスの識別子](identifiers-for-ide-devices.md)
*  [PCMCIA デバイスの識別子](identifiers-for-pcmcia-devices.md)
*  [ISAPNP デバイスの識別子](identifiers-for-isapnp-devices.md)
*  [1394 デバイスの識別子](identifiers-for-1394-devices.md)
*  [セキュア デジタル (SD) デバイスの識別子](identifiers-for-secure-digital--sd--devices.md)
*  [USB デバイスの識別子](identifiers-for-usb-devices.md)


 





