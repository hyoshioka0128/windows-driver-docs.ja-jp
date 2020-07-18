---
title: 休止状態からのウェイクと高速スタートアップの区別
description: Windows 8 以降では、高速スタートアップモードを使用して、従来のコールドスタートで通常必要とされるよりも短時間でコンピューターを起動することができます。
ms.assetid: 1768F739-619A-441F-B270-029DD1F72953
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4381a50f288114ce36b57588eb6298d74290686f
ms.sourcegitcommit: 0d89fc46058efb2ebc6ed9bd8f638c3f8cc1a678
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2020
ms.locfileid: "86459246"
---
# <a name="distinguishing-fast-startup-from-wake-from-hibernation"></a>休止状態からのウェイクと高速スタートアップの区別


Windows 8 以降では、高速スタートアップモードを使用して、従来のコールドスタートで通常必要とされるよりも短時間でコンピューターを起動することができます。 高速スタートアップとは、コールド起動と休止状態からの復帰を組み合わせたものです。 多くの場合、カーネルモードのデバイスドライバーは、デバイスがユーザーの期待どおりに動作するように、高速スタートアップと休止状態からの復帰を区別する必要があります。 この区別を行うために、ドライバーは[システムの電源 irp](power-irps-for-the-system.md)で使用できる情報を使用できます。

コールド起動中、ブートローダーは、Windows カーネルファイルのセクションをメモリに読み込み、それらをリンクすることで、カーネルメモリイメージを構築します。 次に、カーネルはコアシステム関数を構成し、コンピューターに接続されているデバイスを列挙し、ドライバーを読み込みます。

これに対して、高速スタートアップは、休止状態ファイル (Hiberfil.sys) をメモリに読み込み、以前に保存された Windows カーネルおよび読み込まれたドライバーのイメージを復元します。 高速スタートアップは、コールドスタートよりも大幅に時間がかかる傾向があります。

高速スタートアップの準備として、Windows は、完全シャットダウンシーケンスと休止状態の準備の要素を組み合わせたハイブリッドシャットダウンシーケンスを実行します。 まず、完全なシャットダウンと同様に、Windows はすべてのアプリケーションを閉じ、すべてのユーザーセッションからログオフします。 この段階では、システム状態は、起動したばかりのコンピューターと似ていますが、アプリケーションは実行されていませんが、Windows カーネルが読み込まれ、システムセッションが実行されています。 次に、電源マネージャーは、デバイスドライバーにシステム電源 Irp を送信し、デバイスが休止状態に入る準備をするように指示します。 最後に、Windows は、カーネルメモリイメージ (読み込まれたカーネルモードドライバーを含む) を Hiberfil.sys に保存し、コンピューターをシャットダウンします。

既定では、Windows 8 はコールドスタートの代わりに高速スタートアップを使用します。 通常、高速スタートアップとコールドスタートの違いはユーザーが無視できますが、ユーザーの期待に応えるために、高速スタートアップはコールドスタートと同じように動作します。 特に、コールド起動の場合と同じように、コンピューターに接続されているデバイスを高速スタートアップ用に同じように構成する必要があります。

デバイスのドライバーで、コールドスタートまたは休止状態が発生したかどうかによってデバイスが異なる方法で構成されている場合、このドライバーでは、高速スタートアップの後に、コールド起動 (休止状態からではなく) としてデバイスを構成する必要があります。 たとえば、システムによって提供される NDIS ドライバーは、高速起動時にミニポートウェイクアップ機能を無効にしますが、休止状態からは無効にします。

復帰と休止状態からの高速スタートアップを区別するために、ドライバーは、コンピューターが S0 (動作) 状態になったことをドライバーに通知するシステムセット-電源 (Irp) irp の情報を検査できます。[** \_ \_ \_ **](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power) この IRP 内のドライバーの[i/o スタックの場所](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)には、電源に関連する情報を含む構造体である**電源**メンバーが含まれています。 Windows Vista 以降では、**電源**メンバー構造に**Systempowerstatecontext**メンバーが含まれています。これは、以前のシステム電源の状態に関する情報を含む[**システム \_ 電源 \_ 状態の \_ コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_system_power_state_context)構造です。 この情報は、**システムの \_ 電源 \_ 状態 \_ コンテキスト**構造のビットフィールドでエンコードされます。

**システムの \_ 電源 \_ 状態 \_ コンテキスト**構造のビットフィールドの大部分は、システムで使用するために予約されており、ドライバーに対しては非透過的です。 ただし、この構造体には、 **Targetsystemstate**と**EffectiveSystemState**という2つのビットフィールドが含まれており、これをドライバーで読み取って、高速スタートアップまたは休止状態からの復帰が発生したかどうかを判断できます。

**Targetsystemstate**および**EffectiveSystemState**ビットフィールドは、[**システム \_ 電源 \_ 状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_system_power_state)の列挙値に設定されます。 **Targetsystemstate**  =  **powersystemhibernate**と**EffectiveSystemState**  =  **powersystemhibernate**の場合、休止状態から復帰します。

ただし、 **targetsystemstate**  =  **powersystemshutdown**と**EffectiveSystemState**  =  **powersystemshutdown**の場合、高速スタートアップが発生しました。

**Targetsystemstate**ビットフィールドは、コンピューターがシャットダウンまたは休止状態になる前に、ドライバーがシステム電源 IRP を受信した最後のシステム電源状態の移行を指定します。 **EffectiveSystemState**ビットフィールドは、ユーザーが認識している、デバイスの以前のシステム電源の有効な状態を示します。 たとえば、ドライバーが保留中のシステム遷移の通知を休止状態にしたが、その後にハイブリッドシャットダウンが発生した場合、 **Targetsystemstate**と**EffectiveSystemState**の値が一致しない可能性があります。

詳細については、「[**システム \_ 電源 \_ 状態の \_ コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_system_power_state_context)」を参照してください。

 

 




