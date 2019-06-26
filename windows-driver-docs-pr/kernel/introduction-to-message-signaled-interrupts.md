---
title: メッセージ シグナル割り込みの概要
description: メッセージ シグナル割り込みの概要
ms.assetid: 035207a1-762d-463e-822e-64ac4833afa4
keywords:
- メッセージ シグナル割り込み WDK カーネル
- Msi WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9110bf7890c3d370c9e636eb6725e2c9e01dfbe5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369932"
---
# <a name="introduction-to-message-signaled-interrupts"></a>メッセージ シグナル割り込みの概要


メッセージ シグナル割り込み (Msi) は、行ベースの割り込みの代替として、PCI 2.2 仕様で導入されました。 割り込みをトリガーする専用の pin を使用する代わりには、Msi を使用するデバイスは、特定のメモリ アドレスに値を記述することで、割り込みをトリガーします。 PCI 3.0 と呼ばれる、MSI の拡張の形式を定義する*MSI X*、大きいプログラミングできるようにします。 Windows Vista および Windows の以降のバージョンは、MSI と MSI X をサポートします。 1 つのデバイスには、MSI と MSI X の両方をサポートできます。 このようなデバイスでは、オペレーティング システムが MSI X 自動的を使用します。

*割り込みメッセージ*は特定の値をデバイスは、割り込みを発生させる特定のアドレスに書き込みます。 行ベースの割り込みとは異なりは、メッセージ シグナル割り込みは、edge のセマンティクスを持ちます。 デバイスは、メッセージを送信しますが、割り込みを受信したハードウェア受信確認応答を受信しません。

PCI 2.2 では、メッセージは、アドレスと部分的に非透過的な 16 ビット値で構成されます。 各デバイスには、1 つのアドレスが割り当てられます。 デバイスは、複数のメッセージを送信するには、メッセージを区別するためにメッセージの値の下位 4 ビットを使用できます。 そのため、PCI 2.2 では、デバイスは、最大 16 個のメッセージをサポートできます。

PCI 3.0 では、メッセージは、アドレスと非透過の 32 ビット値で構成されます。 それぞれ別のメッセージが、独自の一意のアドレス。 異なり PCI 2.2 では、デバイスは値は変更されません。 PCI 3.0 では、デバイスはさまざまなメッセージの最大長は 2,048 をサポートできます。 PCI 3.0 MSI-x をサポートするデバイスには、デバイスの割り込みのソースの各エントリを含むハードウェアの動的プログラミング可能なテーブルが機能します。 このテーブル内の各エントリは、デバイスに割り当てられているし、しない個別にマスクできるメッセージのいずれかでプログラミングできます。 ドライバーは、テーブル エントリとエントリのマスクが指定されているかどうかにある interrupt メッセージのプログラミングを変更できます。 詳細については、次を参照してください。[動的に構成する MSI-x](dynamically-configuring-msi-x.md)します。

ドライバーは、1 つを登録できます[ *InterruptMessageService* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kmessage_service_routine)個人またはすべての可能なメッセージを処理するルーチン[ *InterruptService* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kservice_routine)メッセージごとのルーチンです。

ドライバーは、デバイスが送信する次のように Msi を処理できます。

1.  ドライバーのインストール中に、レジストリで Msi を有効にします。 デバイスの割り当てへのメッセージの数を指定するのにレジストリを使用することもできます。 詳細については、次を参照してください。 [Enabling Message-Signaled がレジストリへの割り込み](enabling-message-signaled-interrupts-in-the-registry.md)します。

2.  必要に応じて、割り込みメッセージの数を増やすし、応答することで、いくつかのメッセージごとの設定を保存、 [ **IRP\_MN\_フィルター\_リソース\_要件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-filter-resource-requirements)要求。 詳細については、次を参照してください。 [Interrupt リソースの記述子を使用して](using-interrupt-resource-descriptors.md)します。

3.  用のドライバーのディスパッチ ルーチンで[ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)、呼び出す[ **IoConnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioconnectinterruptex)を登録する、 *InterruptService*または*InterruptMessageService*にデバイスの割り込みサービス ルーチン。 接続を使用して\_完全\_の指定されたバージョン**IoConnectInterruptEx**を登録する、 *InterruptService*特定のメッセージまたは CONNECTの日常的な\_メッセージ\_ベース バージョンの**IoConnectInterruptEx** 、1 つを登録する*InterruptMessageService*ルーチンのすべてのメッセージ。 詳細については、次を参照してください[、CONNECT を使用して\_メッセージ\_IoConnectInterruptEx のバージョンのベース](using-the-connect-message-based-version-of-ioconnectinterruptex.md)と[、CONNECT を使用して\_完全\_バージョンの指定。IoConnectInterruptEx](using-the-connect-fully-specified-version-of-ioconnectinterruptex.md)します。

4.  ドライバーは、デバイスからサービスの割り込みを不要になったが後で呼び出す[ **IoDisconnectInterruptEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodisconnectinterruptex) (後に、デバイスの割り込みを無効にする) を削除するには、割り込みサービスを登録ルーチン。

複数のメッセージを使用するように設計されたドライバーは予想メッセージ数が割り当てられていることをチェックします。 場合は、プラグ アンド プレイ (PnP) マネージャーでは、要求されたメッセージ数を割り当てることができません、代わりに、デバイスを正確に 1 つのメッセージを割り当てます。 ドライバーは、次の方法のいずれかで実際に割り当てられているメッセージの数を確認できます。

-   PnP マネージャーでは、生のリソースの記述子の一覧に割り当てられているメッセージの数を報告します。 詳細については、次を参照してください。 [Interrupt リソースの記述子を使用して](using-interrupt-resource-descriptors.md)します。

-   ときに**IoConnectInterruptEx** 、設定を返します*パラメーター*-&gt;**MessageBased.ConnectContext.InterruptMessageTable-&gt;MessageCount**に割り当てられているメッセージの数。

 

 




