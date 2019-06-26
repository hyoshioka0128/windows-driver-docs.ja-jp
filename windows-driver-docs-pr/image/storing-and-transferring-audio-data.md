---
title: オーディオ データの保存と転送
description: オーディオ データの保存と転送
ms.assetid: c8d0af2f-1c3d-49d5-96ca-de1703f85448
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ef08aba4f5a851d41dc43289a98882807cfd696
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358238"
---
# <a name="storing-and-transferring-audio-data"></a>オーディオ データの保存と転送





Microsoft Windows Me、Windows XP の場合は、いくつか WIA ドライバーでは、オーディオ データを格納するのに、次の 3 つ WIA プロパティを使用しました。

[**WIA\_IPC\_オーディオ\_利用可能**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipc-audio-available)

[**WIA\_IPC\_オーディオ\_データ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipc-audio-data)

[**WIA\_IPC\_オーディオ\_データ\_形式**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipc-audio-data-format)

これらのプロパティは廃止され、使用する必要があります。

画像項目のオーディオは、添付ファイルとして表される必要があります。 これは、WIA ミニドライバーをサポートするすべてのオーディオ形式に簡単にアクセスを提供します。 オーディオのコンテンツは、WIA 項目ツリーの他のアイテムが転送されることと同じ方法で転送されます。

 

 




