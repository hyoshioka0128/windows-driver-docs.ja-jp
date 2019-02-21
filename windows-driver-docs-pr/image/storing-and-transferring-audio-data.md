---
title: 格納して、オーディオ データを転送します。
description: 格納して、オーディオ データを転送します。
ms.assetid: c8d0af2f-1c3d-49d5-96ca-de1703f85448
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb77c1a22006a25e216c1a863c3ae3ad14eda680
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538505"
---
# <a name="storing-and-transferring-audio-data"></a>格納して、オーディオ データを転送します。





Microsoft Windows Me、Windows XP の場合は、いくつか WIA ドライバーでは、オーディオ データを格納するのに、次の 3 つ WIA プロパティを使用しました。

[**WIA\_IPC\_オーディオ\_利用可能**](https://msdn.microsoft.com/library/windows/hardware/ff552530)

[**WIA\_IPC\_オーディオ\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff552534)

[**WIA\_IPC\_オーディオ\_データ\_形式**](https://msdn.microsoft.com/library/windows/hardware/ff552538)

これらのプロパティは廃止され、使用する必要があります。

画像項目のオーディオは、添付ファイルとして表される必要があります。 これは、WIA ミニドライバーをサポートするすべてのオーディオ形式に簡単にアクセスを提供します。 オーディオのコンテンツは、WIA 項目ツリーの他のアイテムが転送されることと同じ方法で転送されます。

 

 




