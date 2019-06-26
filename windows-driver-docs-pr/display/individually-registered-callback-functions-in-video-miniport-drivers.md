---
title: ビデオ ミニポート ドライバーへのコールバック関数の登録
description: ビデオのミニポート ドライバーでコールバック関数を個別に登録
ms.assetid: 18469b9b-aca4-4225-97d0-8cafe64b8e1f
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000 では、コールバック関数
- コールバック関数 WDK のビデオのミニポート
- 個別に登録されたコールバック関数 WDK のビデオのミニポート
- 登録済みのコールバック関数 WDK のビデオのミニポート
- 一時的な登録 WDK ビデオのミニポート
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 263f4321db3524750611cc2ac9e887d9b8b5e7e6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385813"
---
# <a name="registering-callback-functions-in-video-miniport-drivers"></a>ビデオ ミニポート ドライバーへのコールバック関数の登録

特定のインスタンスでベンダーから提供されたビデオのミニポート ドライバーとシステム提供のビデオ ポート ドライバー間の通信は、次のように処理されます。

1.  ビデオのミニポート ドライバーでは、ビデオ ポート ドライバーで関数を呼び出します。

2.  ビデオ ポート ドライバー関数が完了する前に、コールバック、ビデオのミニポート ドライバーにアシスタンスをします。

ビデオのミニポート ドライバー、ビデオ ポート ドライバー関数を呼び出すと、コールバック関数へのポインターを渡します。 たとえば、ビデオのミニポート ドライバーを呼び出すと[ **VideoPortStartDma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportstartdma)へのポインターを渡す、 *HwVidExecuteDma* (ビデオによって実装されるコールバック関数ミニポート ドライバーの場合)。

ビデオのミニポート ドライバーがビデオ ポート ドライバー関数では、コールバック関数のアドレスを渡すときに、*登録*ビデオ ポート ドライバーを使用して、コールバック関数。 登録は、ビデオ ポート ドライバーがコールバック関数のポインターを完全に保存していないことの意味では一時的です。 代わりに、ビデオ ポート ドライバーは、コールバック関数の実行時にのみ、関数ポインターを保持します。 この種の一時的な登録では、ビデオのミニポート ドライバー関数の多くの永続的な登録とは対照的です。 たとえば、ビデオのミニポート ドライバーは登録中に関数のセットを**DriverEntry**、し、ビデオ ポート ドライバー格納これらの関数ポインター永続的にデバイスの拡張機能。

場合によっては、それぞれが特定のビデオ ポート ドライバーの関数のコールバック関数として使用できるいくつかの関数を実装するビデオのミニポート ドライバーの意味をほうです。 たとえば、ビデオのミニポート ドライバーを実装のいくつかのバリエーション、 *HwVidQueryDeviceCallback*関数を任意のバリエーションを特定の呼び出しに渡す[ **VideoPortGetDeviceData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportgetdevicedata).

ビデオのミニポート ドライバーで実装できるコールバック関数の一覧とそれらのコールバック関数を登録する方法についてを参照して[個別に登録されているビデオ ミニポート ドライバー機能](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。