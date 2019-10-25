---
title: ビデオ ミニポート ドライバーへのコールバック関数の登録
description: ビデオミニポートドライバーに個別に登録されたコールバック関数
ms.assetid: 18469b9b-aca4-4225-97d0-8cafe64b8e1f
keywords:
- ビデオミニポートドライバー WDK Windows 2000、コールバック関数
- コールバック関数 WDK ビデオミニポート
- 個別に登録されたコールバック関数 WDK ビデオミニポート
- 登録されたコールバック関数 WDK ビデオミニポート
- 一時的な登録 WDK ビデオミニポート
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 425682003f57d1680e65707c60de08d437b89dbf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840381"
---
# <a name="registering-callback-functions-in-video-miniport-drivers"></a>ビデオ ミニポート ドライバーへのコールバック関数の登録

特定のインスタンスでは、ベンダーから提供されたビデオミニポートドライバーとシステムによって提供されるビデオポートドライバーの間の通信は次のように行われます。

1.  ビデオミニポートドライバーは、ビデオポートドライバーの関数を呼び出します。

2.  ビデオポートドライバーの機能が完了する前に、ビデオミニポートドライバーをコールバックしてサポートします。

ビデオミニポートドライバーがビデオポートドライバー関数を呼び出すと、コールバック関数へのポインターが渡されます。 たとえば、ビデオミニポートドライバーが[**Videoportstartdma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportstartdma)を呼び出すと、 *HwVidExecuteDma* callback 関数 (ビデオミニポートドライバーによって実装される) へのポインターが渡されます。

ビデオミニポートドライバーがコールバック関数のアドレスをビデオポートドライバー関数に渡すと、コールバック関数がビデオポートドライバーに*登録*されます。 登録は、ビデオポートドライバーがコールバック関数ポインターを永続的に格納しないという意味で、一時的なものです。 代わりに、ビデオポートドライバーは、コールバックを実行する関数の実行中にのみ、関数ポインターを保持します。 このような一時的な登録は、多くのビデオミニポートドライバー機能の永続的な登録とは対照的です。 たとえば、ビデオミニポートドライバーは**Driverentry**中に一連の関数を登録し、ビデオポートドライバーはこれらの関数ポインターをデバイス拡張機能に永続的に格納します。

場合によっては、ビデオミニポートドライバーがいくつかの関数を実装することが理にかなっています。各関数は、特定のビデオポートドライバー関数のコールバック関数として機能します。 たとえば、ビデオミニポートドライバーでは、 *HwVidQueryDeviceCallback*関数のいくつかのバリエーションを実装し、 [**Videoportgetdevicedata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportgetdevicedata)の特定の呼び出しで選択のバリエーションを渡すことができます。

ビデオミニポートドライバーによって実装できるコールバック関数の一覧と、それらのコールバック関数の登録方法については、「[個別に登録されたビデオミニポートドライバー関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。