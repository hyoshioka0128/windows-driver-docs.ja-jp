---
Description: このトピックでは、クライアント ドライバーでは、リモート ウェイク アップ機能を実装する方法のベスト プラクティスについて説明します。
title: USB デバイスのリモート ウェイクアップ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce455952b0b6b5dbf7624194a033c616ac0b90d9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358351"
---
# <a name="remote-wakeup-of-usb-devices"></a>USB デバイスのリモート ウェイクアップ


このトピックでは、クライアント ドライバーでは、リモート ウェイク アップ機能を実装する方法のベスト プラクティスについて説明します。

中断している間に外部ウェイク信号に対応できる、USB デバイスがあると言われて、*リモート ウェイク アップ*機能します。 リモート ウェイク アップ機能を搭載するデバイスの例として、マウス、キーボード、USB ハブをモデム (ウェイク リング上)、Nic、wake on ケーブル挿入します。 これらすべてのデバイスは、リモート ウェイク信号を生成できます。 リモート ウェイク信号を生成するのに対応していないデバイスには、ビデオ_カメラ、大容量記憶装置デバイス、オーディオ デバイス、およびプリンターが含まれます。

リモート ウェイク アップ通知をサポートしているデバイスのドライバーを発行する必要があります、 [ **IRP\_MN\_待機\_WAKE** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake) IRP とも呼ばれる、待機ウェイク IRP、arm デバイスをリモート ウェイク アップします。 待機のスリープ解除メカニズムが、セクションで説明した[をサポートしているデバイスをあるウェイク アップ機能](https://docs.microsoft.com/windows-hardware/drivers/kernel/supporting-devices-that-have-wake-up-capabilities)します。

## <a name="when-does-the-system-enable-remote-wakeup-on-a-usb-leaf-device"></a>システムは USB リーフ デバイス上のリモート ウェイク アップを場合は有効にします。


リモート ウェイク アップの USB 用語では、USB デバイスが有効なときにそのデバイス\_リモート\_ウェイク アップ機能が設定されます。 USB 仕様では、ホスト ソフトウェアが「のみだけ前」に、デバイスを配置することをスリープ状態のデバイスにリモート ウェイク アップ機能を設定する必要がありますを指定します。

このため、USB スタックが設定されていないデバイス\_リモート\_デバイスの待機ウェイク IRP を受信した後、デバイス上でウェイク アップ機能。 受け取るまでに待機する代わりに、 [ **IRP\_MN\_設定\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power) D1 または D2 に WDM デバイスのデバイスの状態を変更する要求。 ほとんどの状況では、USB スタックは、この要求を受信すると両方、デバイスにリモート ウェイク アップ機能を設定し、デバイスのアップ ストリームのポートを中断することによってスリープ状態にデバイスを配置します。 設計には、ドライバーをデバッグすると、取り組まソフトウェアでウェイク アップの USB デバイスの間で疎関係があることに注意してください、待機を使用して wake IRP、およびリモート ウェイク アップ機能を設定して、デバイスのハードウェアでウェイク アップを作動する必要があります。

USB スタックは D3 内のデバイス、WDM power モデルに応じたシステムをスリープ解除できないため、デバイスを D3 のスリープ状態に変更する要求を受け取ったときに、デバイスをリモート ウェイク アップ有効になりません。

## <a name="why-does-attaching-or-detaching-my-device-produce-a-different-wakeup-behavior-in-windows-xp-and-windows-vista-and-later-versions-of-windows"></a>アタッチするか、デバイス生成される可能性を Windows XP および Windows Vista 以降のバージョンの Windows ウェイク アップは異なる動作にデタッチはなぜですか。


WDM 電源モードの USB の実装のもう 1 つの一意な側面は、リモート ウェイク アップの USB ハブの作動します。 Microsoft Windows XP ホスト コント ローラーと USB デバイスの間のすべてのハブ デバイスがウェイク アップ武装したときに、ウェイク アップされている USB デバイスです。 意外な結果が生成されますスリープ状態のデバイスがデタッチされると、システムが wake されます。

Windows Vista および以降のバージョンの Windows では、バス上の USB リーフ デバイスのスリープ解除されている場合、USB スタックは、ウェイク アップの USB ホスト コント ローラーを arm もが、必須ではありませんが、arm USB ハブは、デバイスのアップ ストリームのいずれか。 USB ハブ ドライバー アームでシステムをスリープ解除する USB スタックが構成されている場合にのみリモート ウェイク アップのハブのアタッチし、(プラグ/取り外し) イベントをデタッチします。

**注**  せず UHCI (ユニバーサル ホスト コント ローラー インターフェイス) USB ホスト コント ローラーにリモート ウェイク信号を区別してくださいルート ハブのポートでの変更イベントを接続します。 つまり、システムは常にからの復帰に低いシステム電源の状態、USB デバイスに接続されているか、ルート ハブのポートから切断されている場合のウェイク アップされている、UHCI コント ローラーの背後にある少なくとも 1 つのデバイスがある場合。

 

## <a name="related-topics"></a>関連トピック
[USB 電源管理](usb-power-management.md)  



