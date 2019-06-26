---
title: Wi-fi デバイスの初期化
description: このトピックでは、電源オン後に Wi-fi デバイスの初期化について説明します。
ms.assetid: EDF04E40-C278-42CE-8E17-F5AB0C1651EF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 250ec8ee8a365ebb0cf002374f5d19f0cc3fd532
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374709"
---
# <a name="wi-fi-device-initialization"></a>Wi-fi デバイスの初期化


このトピックでは、電源オン後に Wi-fi デバイスの初期化について説明します。 電源投入 ほとんどのデバイスの Wi-fi は初期化されていないモードで起動します。 Wi-fi デバイスには、IHV コンポーネント/ドライバー プログラムの起動時のデバイスの一部として、デバイスのファームウェアのために、ファームウェアを保持するための十分な ROM はありません。 次の図は、バス/相互接続の独立した方法で初期化シーケンスを示します。

![wdi 初期化シーケンス](images/wdi-initialization-sequence.png)

1.  IHV コンポーネントは、アダプターの電源投入時に、アダプターにファームウェアをダウンロードします。 ファームウェアをダウンロードする正確なメカニズムは、バス依存です。 この操作のコンテキストで実行されますが、 [ *MiniportWdiOpenAdapter* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-miniport_wdi_open_adapter)呼び出します。 これは、非同期操作です。 ホストは、アダプターが完全に初期化され、さらにコマンドに送信される前に、コマンドを処理する準備があることを保証します。 正確なメカニズムが相互接続依存です。
2.  アダプターが初期化されると、ホストのクエリのさまざまな Wi-fi プロパティ、アダプター プロパティを設定し、ミニポートの初期化の一部として (Mac) のポートを作成します。
3.  ポートを作成および初期化後、アダプターは、タスクとプロパティのコマンドを受信できます。

 

 





