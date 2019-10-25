---
title: メッセージ シグナル割り込みの概要
description: メッセージ シグナル割り込みの概要
ms.assetid: 035207a1-762d-463e-822e-64ac4833afa4
keywords:
- メッセージシグナル割り込み (WDK カーネル)
- Msi WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8aa41f84a55415070c884bc5d916c82d0ddf1fef
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828193"
---
# <a name="introduction-to-message-signaled-interrupts"></a>メッセージ シグナル割り込みの概要


行ベースの割り込みの代わりとして、PCI 2.2 仕様では、メッセージシグナル割り込み (Msi) が導入されました。 専用の pin を使用して割り込みをトリガーするのではなく、Msi を使用するデバイスは、特定のメモリアドレスに値を書き込むことによって割り込みをトリガーします。 PCI 3.0 では、より高度なプログラミングを可能にする Msi の拡張形式 ( *msi-X*) が定義されています。 Windows Vista 以降のバージョンの Windows では、MSI と MSI-X がサポートされています。 1つのデバイスで MSI と MSI-X の両方をサポートできます。 このようなデバイスの場合、オペレーティングシステムは自動的に MSI-X を使用します。

*割り込みメッセージ*は、デバイスが特定のアドレスに書き込んで割り込みをトリガーする特定の値です。 行ベースの割り込みとは異なり、メッセージシグナルの割り込みにはエッジセマンティクスがあります。 デバイスはメッセージを送信しますが、割り込みを受信したハードウェア受信確認は受け取りません。

PCI 2.2 の場合、メッセージは、アドレスと部分的に不透明な16ビット値で構成されます。 各デバイスには1つのアドレスが割り当てられます。 複数のメッセージを送信する場合、デバイスはメッセージ値の下位4ビットを使用してメッセージを区別できます。 したがって、PCI 2.2 では、デバイスは最大16個のメッセージをサポートできます。

PCI 3.0 の場合、メッセージはアドレスと非透過的な32ビット値で構成されます。 各メッセージには、独自の一意のアドレスがあります。 PCI 2.2 とは異なり、デバイスは値を変更しません。 PCI 3.0 では、デバイスは最大2048の異なるメッセージをサポートできます。 PCI 3.0 の MSI-X 機能をサポートするデバイスは、デバイス内の各割り込みソースのエントリを含む動的にプログラミング可能なハードウェアテーブルを提供します。 このテーブルの各エントリは、デバイスに割り当てられているメッセージの1つを使用してプログラミングできます。また、個別にマスクすることもできます。 ドライバーは、割り込みメッセージのプログラミングをテーブルエントリに変更したり、エントリがマスクされているかどうかを変更したりすることができます。 詳細については、「 [MSI-X を動的に構成する](dynamically-configuring-msi-x.md)」を参照してください。

ドライバーは、各メッセージに対して可能なすべてのメッセージまたは個別の[*InterruptService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine)ルーチンを処理する1つの[*InterruptMessageService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kmessage_service_routine)ルーチンを登録できます。

ドライバーは、デバイスが送信する Msi を次のように処理できます。

1.  ドライバーのインストール中に、レジストリで Msi を有効にします。 また、レジストリを使用して、デバイスに割り当てるメッセージの数を指定することもできます。 詳細については、「[レジストリでのメッセージシグナル割り込みの有効化](enabling-message-signaled-interrupts-in-the-registry.md)」を参照してください。

2.  必要に応じて、割り込みメッセージの数を増やし、メッセージごとの設定を保存します。これには、 [**IRP\_\_フィルター\_リソース\_要件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-filter-resource-requirements)の要求に応答します。 詳細については、「[割り込みリソース記述子の使用](using-interrupt-resource-descriptors.md)」を参照してください。

3.  [**IRP\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)のドライバーのディスパッチルーチンで\_デバイスを起動し、デバイスの割り込みを処理する*InterruptService*または*InterruptMessageService*ルーチンを登録するには、 [**IoConnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex)を呼び出します. 指定されたバージョンの**IoConnectInterruptEx**\_完全に接続\_を使用して、特定のメッセージに対する*InterruptService*ルーチン、または IOCONNECTINTERRUPTEX の CONNECT\_message\_BASED バージョンを登録します。すべてのメッセージに対して1つの*InterruptMessageService*ルーチンを登録します。 詳細については、「 [connect\_MESSAGE\_BASED バージョンの IoConnectInterruptEx](using-the-connect-message-based-version-of-ioconnectinterruptex.md) 」を参照してください。また、 [Connect\_を使用して、指定したバージョンの IoConnectInterruptEx を完全に\_](using-the-connect-fully-specified-version-of-ioconnectinterruptex.md)します。

4.  ドライバーがデバイスからの割り込みを処理しないようになったら、(デバイスの割り込みを無効にした後) [**IoDisconnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodisconnectinterruptex)を呼び出して、登録されている割り込みサービスルーチンを削除します。

複数のメッセージを使用するように設計されたドライバーは、予想される数のメッセージが割り当てられていることを確認する必要があります。 プラグアンドプレイ (PnP) マネージャーが、要求された数のメッセージを割り当てることができない場合は、そのデバイスにメッセージを1つだけ割り当てます。 ドライバーは、次のいずれかの方法で実際に割り当てられたメッセージの数を確認できます。

-   PnP マネージャーは、未加工のリソース記述子の一覧に、割り当てられたメッセージの数を報告します。 詳細については、「[割り込みリソース記述子の使用](using-interrupt-resource-descriptors.md)」を参照してください。

-   **IoConnectInterruptEx**がを返すと、&gt;**Messagebased. InterruptMessageTable-&gt;Messagecount**-*パラメーター*が割り当てられたメッセージの数に設定されます。

 

 




