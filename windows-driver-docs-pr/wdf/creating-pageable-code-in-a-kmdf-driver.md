---
title: KMDF ドライバーでのページング可能なコードの作成
description: KMDF ドライバーでのページング可能なコードの作成
ms.assetid: 5c694ae2-2a16-4c2f-84b0-62e26f4121bc
keywords:
- ページング可能ドライバー WDK KMDF
- KMDF WDK、ページング可能ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a6e9963e90ab4957aac6698949c6c8d21f594ca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844677"
---
# <a name="creating-pageable-code-in-a-kmdf-driver"></a>KMDF ドライバーでのページング可能なコードの作成


*ページング*可能なコードとは、コードが使用されていないときにコンピューターのページングファイルに書き込むことができるコードのことです。 ドライバーの一部をページングして、読み込みイメージと初期読み込み時間を短縮し、コンピューターの制限された非ページメモリプールを使用するドライバーのコードの量を減らすことができます。

ページングできるコードまたはデータがドライバーに適しているかどうかを判断するには、次の手順を実行します。

1.  ドライバーのページング可能セクションを識別します。

    ページング可能なセクションは、必要になるまでメモリに読み込まれません。 ドライバーでページング可能なセクションを作成する方法の詳細については、「[ドライバーをページング](https://docs.microsoft.com/windows-hardware/drivers/kernel/making-drivers-pageable)可能にする」を参照してください。

2.  ページングされたドライバーコードによって、コンピューターが低電力状態から迅速に起動できないことを確認します。

    ドライバーが提供するすべてのデバイスオブジェクトコールバック関数は、IRQL = パッシブ\_レベルで呼び出されます。これにより、コードをページング可能にすることができます (「[ドライバーのページング](https://docs.microsoft.com/windows-hardware/drivers/kernel/making-drivers-pageable)の設定」を参照)。

    ただし、デバイスが低電力状態になったときにコールバック関数を呼び出し、その動作 (D0) 状態に戻る場合は、コールバック関数のコードをページングできないようにする必要があります。

    このようなコードがページング可能な場合は、コンピューターがスリープ状態になる前に、コードがページングファイルに書き込まれる可能性があります。 そのため、ページングディスクの電力が復元されるまで、コードを再読み込みできない (したがって、デバイスが完全に動作しなくなる) ため、コンピューターの処理速度が低下します。

    そのため、デバイスに一覧表示されているコールバック関数は、[作業状態](a-device-returns-to-its-working-state.md)のトピックにはページングできません。

3.  電源切り替え中に、ドライバーがドライバー外部のページング可能なデータ (ファイル、レジストリ、ページプールなど) にアクセスする必要があるかどうかを判断します。

    電源遷移中に、ページング可能なデータにアクセスするドライバーの機能を有効または無効にする方法については、「 [**wdfdeviceinitsetpowerpageable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpageable)と[**Wdfdeviceinitsetpowernotページング**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowernotpageable)」を参照してください。

    ドライバーが非ページング状態であることを確認する方法については、「 [**Wdfdevstateisnp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevstateisnp)」を参照してください。

 

 





