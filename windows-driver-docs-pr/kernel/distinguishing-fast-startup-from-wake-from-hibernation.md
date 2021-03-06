---
title: 休止状態からのウェイクと高速スタートアップの区別
description: Windows 8 以降、高速スタートアップ モードは、従来のコールド起動時が通常よりも短時間でコンピューターを起動します。
ms.assetid: 1768F739-619A-441F-B270-029DD1F72953
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6e336c2915898fc5d72abfffd9a8a515273a8674
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384966"
---
# <a name="distinguishing-fast-startup-from-wake-from-hibernation"></a>休止状態からのウェイクと高速スタートアップの区別


Windows 8 以降、高速スタートアップ モードは、従来のコールド起動時が通常よりも短時間でコンピューターを起動します。 高速スタートアップは、コールド起動と休止状態-のウェイク アップのスタートアップのハイブリッド組み合わせです。 多くの場合、カーネル モード デバイス ドライバーは、自分のデバイスがユーザーの期待どおりに動作できるように、休止状態-のスリープ解除からから高速スタートアップを区別するために必要があります。 ドライバーがで提供される情報の使用時に区別する、[システム電源 Irp](power-irps-for-the-system.md)します。

、コールド起動中には、ブート ローダーは、Windows カーネルのファイルのセクションでは、をメモリに読み込むと、リンクすることによってカーネル メモリのイメージを構築します。 次に、カーネルはコアのシステム関数を構成します、コンピューターに接続されているデバイスを列挙し、それらのドライバーを読み込みます。

これに対し、この高速スタートアップは単に、休止状態ファイル (Hiberfil.sys) を Windows カーネルと読み込まれているドライバーの以前に保存したイメージを復元するメモリに読み込みます。 高速スタートアップをコールド起動に比べて大幅に少ない時間がかかる傾向があります。

を高速スタートアップを準備するには、Windows は、ハイブリッドのシャット ダウン シーケンスは完全にシャット ダウン シーケンスの要素を結合して、休止状態-の準備のシーケンスを実行します。 最初に、完全にシャット ダウンのように、Windows はすべてのアプリケーションを終了し、すべてのユーザー セッションをログオフします。 この段階で、システムの状態がだけが開始されるコンピューターに似ていますが、アプリケーションが実行されていないが、Windows カーネルが読み込まれ、システムのセッションが実行されています。 次に、電源マネージャはシステムを休止状態にするようにデバイスを準備することを通知するデバイス ドライバーをで電源の Irp に送信します。 最後に、Windows は Hiberfil.sys に (読み込まれたカーネル モード ドライバーを含む)、カーネル メモリのイメージを保存し、コンピューターをシャット ダウンします。

既定では、Windows 8 は、コールド起動の代わりに高速スタートアップを使用します。 ユーザーは通常、高速とコールドの新興企業間の違いを無視が、ユーザーの期待を満たすためには、高速スタートアップする必要があります動作コールド起動の場合と同じです。 具体的には、コンピューターに接続されているデバイスには、コールド起動の場合と同じ高速スタートアップを同じように構成します。

デバイスのドライバーがコールド起動時または休止からのスリープ解除が発生したかどうかに応じて異なる方法でデバイスを構成した場合このドライバーは、高速の起動後にデバイスを構成いなくても (ウェイク-から-休止状態) ではなく、コールド起動発生しました。 たとえば、システム提供の NDIS ドライバーには、ミニポート ウェイク アップ機能休止からのスリープ解除ではなく高速スタートアップが無効にします。

休止からのスリープ解除から高速スタートアップを区別するために、ドライバーがシステム セット電源の情報を確認できます ([**IRP\_MN\_設定\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)) IRPコンピューターが、S0 を入力したこと、ドライバーに通知する (操作) の状態。 ドライバーの[I/O スタックの場所](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)この IRP が含まれています、 **Power**は電源関連の情報を格納する構造体のメンバー。 以降、Windows Vista では、 **Power**メンバー構造に含まれる、 **SystemPowerStateContext**は、メンバー、 [**システム\_POWER\_状態\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_system_power_state_context)前のシステム電源の状態に関する情報を含む構造体。 この情報は、ビット フィールドでエンコード、**システム\_POWER\_状態\_コンテキスト**構造体。

ほとんどのビット フィールドの**システム\_POWER\_状態\_コンテキスト**構造がシステム用に予約されているし、ドライバーには見えません。 ただし、この構造体には、2 つのビット フィールドが含まれる**TargetSystemState**と**EffectiveSystemState**、高速スタートアップかどうかを判断するドライバーによって読み取ることができる、または休止からのスリープ解除が発生しました。

**TargetSystemState**と**EffectiveSystemState**ビット フィールドに設定されます[**システム\_POWER\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_system_power_state)列挙値。 場合**TargetSystemState** = **PowerSystemHibernate**と**EffectiveSystemState** = **PowerSystemHibernate**、休止からのスリープ解除が発生しました。 ただし場合、 **TargetSystemState** = **PowerSystemHibernate**と**EffectiveSystemState**  =  **PowerSystemShutdown**、高速スタートアップが発生しました。

**TargetSystemState**ビット フィールドは、ドライバーがコンピューターをシャット ダウンまたは休止状態を入力する前にシステムの電源 IRP を受け取ったの最後のシステム電源状態遷移を指定します。 **EffectiveSystemState**ユーザーによって認識されたビット フィールドをデバイスの以前システム電源の有効な状態を示します。 **TargetSystemState**と**EffectiveSystemState**場合、ドライバーが休止状態が、ハイブリッドへの切り替えを保留中のシステムの通知を受信するなど、値が一致しないがありますその後、シャット ダウンが発生しました。

詳細については、次を参照してください。 [**システム\_POWER\_状態\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_system_power_state_context)します。

 

 




