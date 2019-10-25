---
title: AVStream のクロック
description: AVStream のクロック
ms.assetid: fc1d5bca-72e3-48e2-b46f-09a13bba83b4
keywords:
- 時計 WDK AVStream
- AVStream の時計 WDK
- pin の時計 WDK AVStream
- タイマー WDK AVStream
- 時間 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 319d699d1aba3d64a1329c0d2f0fef37799b8357
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845018"
---
# <a name="avstream-clocks"></a>AVStream のクロック





AVStream フィルターでは、ピンの時計がサポートされています。

AVStream の pin が時計を公開することを示すには、KSPIN\_フラグを設定し\_最初の[**kspin\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)の**Flags**メンバーに\_クロックを実装します。これは、KSK フィルターの**pindescriptors**メンバーの例\_[ **_t_11_ 記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_descriptor)。

[**Kspin\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_dispatch)の[**ksclock\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksclock_dispatch)構造体へのポインターも提供します。

クロック要求を行うには、 [Iksreferenceclock](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nn-ks-iksreferenceclock)インターフェイスに定義されているメソッドを使用します。 [**Kspingetreferenceclockinterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspingetreferenceclockinterface)を呼び出すことによって、 *Iksk referenceclock*インターフェイスを取得できます。 AVStream ミニドライバーは、完了時にインターフェイスを解放する役割を担います。

[**Ksk ストリーム\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)の**プレゼンテーション時間**フィールドに配置するタイマー値を取得するには、 [**iksk Referenceclock:: GetCorrelatedTime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-iksreferenceclock-getcorrelatedtime)を呼び出します。

時計が選択されている場合でも、[GraphEdit] に時計が表示されないことに注意してください。

クロックが選択されていることを確認するには、 [Iksreferenceclock](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nn-ks-iksreferenceclock)メソッドの呼び出しによって、KSCLOCK\_dispatch に指定されたディスパッチルーチンの呼び出しが生成されることを確認します。

フィルターグラフマネージャーは、グラフが一時停止状態に遷移するときにクロックを選択します。 プッシュソースであるフィルター (たとえばキャプチャフィルター) は、クロックプロバイダーとして設定されます。

 

 




