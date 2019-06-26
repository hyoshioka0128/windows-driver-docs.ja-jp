---
title: D3cold への遷移の有効化
description: Windows のすべてのバージョンでは、D3cold にする (S1 S4 から、システム低電力状態のいずれか) で、コンピューターがスリープ状態中にデバイスを有効にします。
ms.assetid: C2C6166D-8269-4FCE-81A8-B350626052D4
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 110c9633e45e1e24da9398df5f1d76e62694f8d2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384945"
---
# <a name="enabling-transitions-to-d3cold"></a>D3cold への遷移の有効化


Windows のすべてのバージョンでは、D3cold にする (S1 S4 から、システム低電力状態のいずれか) で、コンピューターがスリープ状態中にデバイスを有効にします。 コンピューターでは、S0 が終了する前に関数ドライバー、バス ドライバー、およびフィルター ドライバー連携 D3hot にデバイスを移動します。 コンピューターが省電力 Sx 状態になったときこの遷移副作用 D3cold D3hot からデバイスに移動します。

Windows 8 以降では、デバイスは入力をコンピューターは、S0 でが保持されます、D3cold を終了します。 デバイスの電源ポリシー所有者 (PPO) であるドライバーを有効にして、D3cold にこれらの遷移を無効にすることができます。 ドライバーには、デバイス、必要な場合、D3cold からの復帰して D0 への移行後の通常の操作を再開しない限り、D3cold を入力するには、そのデバイスが有効にする必要があります。

デバイスには、D3 が入ると、最初に、D3hot 下位状態 D3 を入力します。 D3hot から、デバイスは、D0 または D3cold のいずれかを入力できます。 ウェイク イベントまたは I/O 要求に応答してでは、デバイスは、D3hot から D0 を入力します。 それ以外の場合、D3hot でデバイスが残る可能性があります。 またはには、D3cold D3hot から移動可能性があります。 これらの遷移の詳細については、デバイスの電源状態を参照してください。[ダイアグラム](device-power-states.md#power-state-diagram)で[デバイスの電源状態](device-power-states.md)します。

ドライバーは、D3hot から D3cold へのデバイスの移行を開始しません。 代わりに、このデバイスで共通の電源を共有する他のすべてのデバイスが D3hot では、D3cold を入力する準備がときに、この遷移が発生します。 これらのデバイスの最後には、D3hot が入るは、基になるバス ドライバーとシステム ファームウェアは、電源を削除し、デバイスを調和よく D3cold を入力します。

デバイスの PPO ドライバーは、D3hot から D3cold へのデバイスの移行を有効にするかどうかをオペレーティング システムに指示します。 ドライバーが、デバイスをインストールする INF ファイルでは、この情報を指定またはドライバーを呼び出すことができます、 [ *SetD3ColdSupport* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-set_d3cold_support)実行時に動的に有効または無効に、デバイスの日常的なD3cold に遷移します。 詳細については、次を参照してください。 [GUID を使用して\_D3COLD\_サポート\_ドライバー インターフェイス](using-guid-d3cold-support-interface.md)します。

D3cold を入力するデバイスを有効にすると、ドライバーは、次の動作を保証します。

-   デバイスは、コンピューターの S0 内に存続するとき、D3hot から D3cold への移行を許容できます。
-   D0 に D3cold から返されるときに、デバイスが正常に動作はします。

いずれかの要件を満たすために失敗したデバイスできない可能性があります、D3cold を入力すると、使用可能なコンピューターが再起動されるかがスリープ状態になるまでです。 デバイスは、それが入力する低電力 Dx 状態からウェイク イベントを通知できる必要がある場合、ドライバーは、特定のデバイスのウェイク信号 D3cold で動作する場合を除き、D3cold にエントリが有効にしない必要があります。

D3cold にデバイスを配置することは、必ずしもデバイスの電源のすべてのソースを削除されていることのみをバスを介してデバイスに通信を許可する能力のソースがなくなったことを意味します。 デバイスは、プロセッサにウェイク イベントを通知するための十分な電力を消費することがある可能性があります。 たとえばのイーサネット ネットワーク インターフェイス カード (NIC) が主電源ソースを削除では、イーサネット ケーブルから power を描画する可能性があります。

D3cold がバスは、デバイスとの通信に使用できない状態であるため、ドライバーことはできません、デバイス D3cold に直接配置します。 ドライバーを最初に呼び出す代わりに、 [ **PoRequestPowerIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-porequestpowerirp) D3 power IRP を要求するルーチン (、 [ **IRP\_MN\_設定\_電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)対象の状態を含む要求 = **PowerDeviceD3**) D0 から D3hot にデバイスを移動します。 D3hot を入力すると、デバイスによっては、D3hot から D3cold に移動できます。 デバイスは、バスに電源がオフ、親のバス ドライバー、バスをオフのときに発生する場合にのみ、またはシステム ファームウェアがハードウェア プラットフォームのセクションの電源をオフにする場合に、D3cold を入力します。

 

 




