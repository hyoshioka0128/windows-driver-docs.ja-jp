---
title: KMDF ドライバーでのページング可能なコードの作成
description: KMDF ドライバーでのページング可能なコードの作成
ms.assetid: 5c694ae2-2a16-4c2f-84b0-62e26f4121bc
keywords:
- ページング可能なドライバー WDK KMDF
- KMDF WDK、ページング可能なドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7cc4b4be6d98f53cfd2042b7475aadf1d6843087
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382367"
---
# <a name="creating-pageable-code-in-a-kmdf-driver"></a>KMDF ドライバーでのページング可能なコードの作成


*ページング可能なコード*コードが使用されていないときに、コンピューターのページング ファイルに書き込むことができるコードに示します。 ページングのイメージ読み込みに、初期読み込みの時間を削減し、コンピューターの限られた非ページ メモリ プールを使用するドライバーのコードの量を削減するには、ドライバーの一部を作成できます。

ページング可能なコードやデータが、ドライバーの適切かどうかを判断するために、次の操作を行います。

1.  ページング可能なセクションでは、ドライバーを特定します。

    ページング可能なセクションでは必要になるまでメモリに読み込まれません。 ドライバーではページング可能なセクションを作成する方法については、次を参照してください。[ドライバー ページングを行う](https://docs.microsoft.com/windows-hardware/drivers/kernel/making-drivers-pageable)します。

2.  ページングされたドライバーのコードが低電力状態からすばやくがスリープ解除するコンピューターの機能を阻害していないことを確認します。

    IRQL でドライバーを提供するすべてのデバイス オブジェクトのコールバック関数が呼び出される = パッシブ\_レベルで、作成するコードをページングすることができます (」の説明に従って[ドライバー ページングを行う](https://docs.microsoft.com/windows-hardware/drivers/kernel/making-drivers-pageable))。

    ただし、ことは避けてくださいコールバック関数のコード ページの場合は、フレームワークは、デバイスが低電力状態のまま、作業 (D0) 状態に戻すときにコールバック関数を呼び出します。

    このようなコードがページング可能な場合は、コンピューターがスリープ状態に入る前に、ページング ファイルに、コードを記述する場合があります。 そのため、コンピューターは、コードを再読み込みすることはできません (およびそのため、デバイスが完全に動作になることはできません) ためがスリープ解除する遅くなりますページング ディスクの電源が復元されるまでです。

    そのため、記載されているコールバック関数、[の操作の状態にするデバイスを返します。](a-device-returns-to-its-working-state.md)トピックをページングすることはできません。

3.  ドライバーがドライバー ファイル、レジストリなどの外部のページング可能なデータにアクセスする必要がありますまたは電源の遷移中にページ プール、かどうかを決定します。

    有効にして、電源の遷移中にページング可能なデータにアクセスするドライバーの機能を無効にする方法については、次を参照してください[ **WdfDeviceInitSetPowerPageable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpageable)と[  **。WdfDeviceInitSetPowerNotPageable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowernotpageable)します。

    ときに、ドライバーが非ページング状態を確認する方法については、次を参照してください。 [ **WdfDevStateIsNP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevstateisnp)します。

 

 





