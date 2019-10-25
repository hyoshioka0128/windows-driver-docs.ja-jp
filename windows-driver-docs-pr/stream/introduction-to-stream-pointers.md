---
title: ストリーム ポインターの紹介
description: ストリーム ポインターの紹介
ms.assetid: 2682b145-5148-4301-b382-9811bb5e8fa6
keywords:
- ストリームポインター WDK AVStream、ストリームポインターについて
- ストリームポインターの進め WDK AVStream
- ストリームポインター WDK AVStream、前進
- フレーム参照カウント WDK AVStream
- 参照カウント WDK ストリームポインター
- カウント参照の WDK ストリームポインター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1c1b155756088fab574819eaf30dba79da2d9b9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845563"
---
# <a name="introduction-to-stream-pointers"></a>ストリーム ポインターの紹介





以前のストリームクラスモデルでは、ミニドライバーは独自のデータストリーム要求ブロック (SRB) キューを維持します。 AVStream は、ストリームポインターの抽象化によってこの機能を提供します。 ストリームポインターは、特定の AVStream データフレームへの参照です。

[Pin 中心の処理](pin-centric-processing.md)(ほとんどのハードウェアドライバー) を使用するミニドライバーは、ストリームポインターを使用して、pin キューを管理します。 各ピンには、データバッファーの独立したキューがあります。 データパケットが pin (読み取り要求または書き込み要求) に到達すると、AVStream はパケットをキューに追加し、pin のプロセスディスパッチを呼び出す可能性があります。

フィルター中心の処理を使用するミニドライバーでは、ストリームポインターを直接使用しないでください。 詳細については[、「フィルター中心の処理](filter-centric-processing.md)」を参照してください。

既定では、各キューには最先端のストリームポインターがあります。 必要に応じて、末尾のエッジフラグが指定されている場合は、末尾のエッジストリームポインターを持つことができます。 ミニドライバーは、 [**Ksk Streamポインタ clone**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerclone)を呼び出すことで、新しいストリームポインターを作成できます。

ストリームポインターは、1つの方向にのみ移動できます。 これを、ストリームポインターの進め方と呼びます。

### <a name="advancing-a-stream-pointer"></a>ストリームポインターを進める

ストリームポインターを進める場合は、新しいフレームに移動するか、現在のフレーム内にいくつかのバイトを進めます。 たとえば、ミニドライバーは、最初のフレーム到着から2番目のフレーム到着までのストリームポインターを進めることができます。

ストリームポインターを進めるために、ピン中心のフィルターは、 *Eject*パラメーターを**TRUE**に設定して、 [**Ksstreampointer advance**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointeradvance)または[**ksstreampointer unlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerunlock)を呼び出すことができます。

### <a name="frame-reference-counts"></a>フレーム参照カウント

ストリームポインターをポイントしているフレームは参照カウントされます。これは、先頭と末尾のエッジの間のウィンドウ内のフレームです。

ストリームポインターでミニドライバーが終了したときに、必要に応じて[**Ksk streampointer Setstatuscode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointersetstatuscode)を呼び出して、指定された i/o 要求パケット (IRP) を完了するためのエラーコードを指定できます。 次に、ミニドライバーは、 [**Ksstreamポインター delete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerdelete)を呼び出す必要があります。 AVStream は、削除されたストリームポインターが以前に参照したフレームの参照カウントをデクリメントします。 先頭と末尾のストリームポインターを削除することはできません。

 

 




