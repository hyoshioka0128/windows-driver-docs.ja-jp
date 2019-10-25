---
title: Wi-fi デバイスの初期化
description: このトピックでは、電源オン後の Wi-fi デバイスの初期化について説明します。
ms.assetid: EDF04E40-C278-42CE-8E17-F5AB0C1651EF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4cdab5af2eb22c89f84cdaba76fdba2b8c78d152
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842924"
---
# <a name="wi-fi-device-initialization"></a>Wi-fi デバイスの初期化


このトピックでは、電源オン後の Wi-fi デバイスの初期化について説明します。 電源をオンにすると、ほとんどの Wi-fi デバイスは初期化されていないモードで起動します。 Wi-fi デバイスは、ファームウェアを保持するのに十分な ROM を持っていません。そのため、IHV コンポーネント/ドライバーは、デバイスの起動時に、ファームウェアを使用してデバイスをプログラムします。 次の図は、バス/相互接続に依存しない方法での初期化シーケンスを示しています。

![wdi 初期化シーケンス](images/wdi-initialization-sequence.png)

1.  IHV コンポーネントは、アダプターの電源が入っているときに、アダプターにファームウェアをダウンロードします。 ファームウェアをダウンロードするための正確なメカニズムは、バスに依存します。 この操作は、 [*Miniportwdiopenadapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_open_adapter)呼び出しのコンテキストで実行されます。 これは非同期操作です。 ホストは、アダプターが完全に初期化されており、コマンドを処理する準備ができていることを確認してから、コマンドを送信します。 正確なメカニズムは相互接続に依存します。
2.  アダプターが初期化されると、ホストは、さまざまな Wi-fi プロパティをアダプターに照会し、プロパティを設定して、ミニポートの初期化の一部としてポート (Mac) を作成します。
3.  ポートが作成され、初期化されると、アダプターはタスクおよびプロパティコマンドを受け取ることができます。

 

 





