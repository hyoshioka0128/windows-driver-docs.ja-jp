---
title: KMDF ドライバーではページング可能なコードを作成します。
description: KMDF ドライバーではページング可能なコードを作成します。
ms.assetid: 5c694ae2-2a16-4c2f-84b0-62e26f4121bc
keywords:
- ページング可能なドライバー WDK KMDF
- KMDF WDK、ページング可能なドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0984215e80be19dca7079e6c595cbf25c04bbca9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556757"
---
# <a name="creating-pageable-code-in-a-kmdf-driver"></a>KMDF ドライバーではページング可能なコードを作成します。


*ページング可能なコード*コードが使用されていないときに、コンピューターのページング ファイルに書き込むことができるコードに示します。 ページングのイメージ読み込みに、初期読み込みの時間を削減し、コンピューターの限られた非ページ メモリ プールを使用するドライバーのコードの量を削減するには、ドライバーの一部を作成できます。

ページング可能なコードやデータが、ドライバーの適切かどうかを判断するために、次の操作を行います。

1.  ページング可能なセクションでは、ドライバーを特定します。

    ページング可能なセクションでは必要になるまでメモリに読み込まれません。 ドライバーではページング可能なセクションを作成する方法については、[ドライバー ページングを行う](https://msdn.microsoft.com/library/windows/hardware/ff554346)を参照してください。

2.  ページングされたドライバーのコードが低電力状態からすばやくがスリープ解除するコンピューターの機能を阻害していないことを確認します。

    IRQL でドライバーを提供するすべてのデバイス オブジェクトのコールバック関数が呼び出される = パッシブ\_レベルで、作成するコードをページングすることができます (」の説明に従って[ドライバー ページングを行う](https://msdn.microsoft.com/library/windows/hardware/ff554346))。

    ただし、ことは避けてくださいコールバック関数のコード ページの場合は、フレームワークは、デバイスが低電力状態のまま、作業 (D0) 状態に戻すときにコールバック関数を呼び出します。

    このようなコードがページング可能な場合は、コンピューターがスリープ状態に入る前に、ページング ファイルに、コードを記述する場合があります。 そのため、コンピューターは、コードを再読み込みすることはできません (およびそのため、デバイスが完全に動作になることはできません) ためがスリープ解除する遅くなりますページング ディスクの電源が復元されるまでです。

    そのため、記載されているコールバック関数、[の操作の状態にするデバイスを返します。](a-device-returns-to-its-working-state.md)トピックをページングすることはできません。

3.  ドライバーがドライバー ファイル、レジストリなどの外部のページング可能なデータにアクセスする必要がありますまたは電源の遷移中にページ プール、かどうかを決定します。

    有効にして、電源の遷移中にページング可能なデータにアクセスするドライバーの機能を無効にする方法については、次を参照してください[ **WdfDeviceInitSetPowerPageable** ](https://msdn.microsoft.com/library/windows/hardware/ff546766)と[  **。WdfDeviceInitSetPowerNotPageable**](https://msdn.microsoft.com/library/windows/hardware/ff546147)します。

    ときに、ドライバーが非ページング状態を確認する方法については、[ **WdfDevStateIsNP**](https://msdn.microsoft.com/library/windows/hardware/ff546958)を参照してください。

 

 





