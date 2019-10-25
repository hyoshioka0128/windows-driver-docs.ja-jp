---
title: SAN ネイティブ アドレスへの変換
description: SAN ネイティブ アドレスへの変換
ms.assetid: 959c66f2-4801-47d5-9e80-f18f17057e23
keywords:
- プロキシドライバー WDK San、ネイティブアドレス変換
- SAN プロキシドライバー WDK、ネイティブアドレス変換
- ネイティブアドレス変換 WDK San
- ネイティブアドレス WDK San の変換
- AF_INET が WDK San に対応
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0720b6679dbc66ecbb2e017a3ed6769359d6cde6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841776"
---
# <a name="translating-to-a-san-native-address"></a>SAN ネイティブ アドレスへの変換





Windows ソケットスイッチでは、SAN のネイティブアドレスファミリではなく、常に[Wsk アドレスファミリ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt808757(v=vs.85))を使用して san サービスプロバイダーとやり取りします。 そのため、SAN サービスプロバイダーのプロキシドライバーは、WSK アドレスファミリとネイティブアドレスの間で変換を行う必要があります。

プロキシドライバーは、「 [SAN NIC 通知の登録](registering-for-san-nic-notifications.md)」で説明されているように、制御下にある各 NIC に割り当てられた IP アドレスの一覧を維持するために、TDI プラグアンドプレイ (PnP) 通知を使用します。 プロキシドライバーは、この一覧を使用して、ネイティブの SAN アドレスと IP アドレスの間で変換を行います。

プロキシドライバーは、IP アドレスを含む SAN サービスプロバイダーからの要求を受信します。 これらの要求には、たとえば、特定の NIC にバインドする要求や、リモートピアに接続するための要求などがあります。 これらの要求を完了するには、プロキシドライバーがネイティブ SAN アドレスに変換される必要があります。 プロキシドライバーは、これらのリモートピアの SAN ネイティブアドレスを含むリモートピアからの受信接続要求も受信します。 これらの要求を完了するには、プロキシドライバーがこれらのリモートピアの IP アドレスに変換される必要があります。

Windows Vista 以降では、Microsoft Windows のバージョンでは TDI はサポートされませ**ん  。** 代わりに、 [Windows フィルタリングプラットフォーム](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)または[Winsock カーネル](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)を使用してください。

 

 

 





