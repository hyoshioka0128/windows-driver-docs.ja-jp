---
title: フィルター中心の処理
description: フィルター中心の処理
ms.assetid: e56c5102-7ea6-4687-ae5e-1550db9500f0
keywords:
- フィルター中心のフィルター (WDK AVStream)
- AVStream フィルター中心フィルター WDK
- フィルターの種類 WDK AVStream
- AVStrMiniFilterProcess
ms.date: 06/18/2020
ms.localizationpriority: medium
ms.openlocfilehash: 6da9748243c2c5a7eadc758afb34fe55d892a5fa
ms.sourcegitcommit: 8143bb312ead6582b4b3e0ad34b6266dcfd74fb5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "84992474"
---
# <a name="filter-centric-processing"></a>フィルター中心の処理

フィルター中心の処理を使用するフィルターでは、各ピンインスタンスで使用できるデータフレームがあるときに、AVStream はミニドライバーが提供する[*Avstrminifilterprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnksfilterprocess)コールバックルーチンを呼び出します。 ミニドライバーは、 [**Kspin \_ 記述子 \_ EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)構造体の**Flags**メンバーを設定することによって、この既定の動作を変更できます。

フィルター中心の処理を実装するには、 [**Ksk フィルター \_ ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_dispatch)構造体の**プロセス**メンバーで、ミニドライバーによって提供される[*avstrminifilterprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnksfilterprocess)コールバックルーチンへのポインターを指定します。 [**Kspin \_ DISPATCH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_dispatch)の**プロセス**メンバーを**NULL**に設定します。

AVStream は、次のすべての条件が満たされた場合にのみ[*Avstrminifilterprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnksfilterprocess)を呼び出します。

- フレームは、処理のためにフレームを必要とするピンで使用できます。 ミニドライバーは、 [**Kspin \_ 記述子 \_ EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)の**flags**メンバーでフラグを設定することによって、処理動作を変更できます。 相互排他的なフラグの組み合わせに特に注意してください \_ \_ \_ 。処理に必要ない kspin フラグのフレームと、 \_ \_ \_ \_ \_ \_ \_ 処理に必要ないくつかのフレームを \_ 処理 \_ するために kspin フラグを使用します。 ミニドライバーは、 [**KsPinAttachAndGate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspinattachandgate)または[**KsPinAttachOrGate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspinattachorgate)ルーチンを使用してフレームを必要とする pin のセットを変更することもできます。

- Pin インスタンスの数が、 [**Kspin \_ 記述子 \_ EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)構造体の**InstancesNecessary**メンバー以上です。 [**Kspin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin)構造体の**clientstate**メンバーは、pin が現在設定されている特定の[**ksstate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ne-ks-ksstate)列挙子を指定します。 **InstancesNecessary**が満たされた後は、 **ksk 状態の \_ 停止**状態の追加のピンによってフィルター処理が妨げられることはありません。

- 必要な pin インスタンスの数が満たされています ( [**Kspin \_ 記述子 \_ EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)構造体の**InstancesNecessary**メンバーによって指定されています)。

- ミニドライバーは、**Ksgate * * * Xxx*関数を使用して、フィルターのプロセス制御ゲートを閉じていません。

[*Avstrminifilterprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnksfilterprocess)コールバックルーチンでは、ミニドライバーは[**ksk processpin \_ indexentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksprocesspin_indexentry)構造体の配列へのポインターを受け取ります。 AVStream は、KSK の配列を \_ ピン ID で並べ替えます。

次のコード例は、プロセスのピン構造を使用する方法を示しています。 このコードは、フィルター中心のキャプチャドライバーを記述する方法を示す[Avstream フィルター中心のシミュレートされたキャプチャドライバー (Avssamp)](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/avstream-filter-centric-simulated-capture-sample-driver-avssamp/)サンプルから取得されます。 このサンプルのソースコードと説明は、Windows Driver Kit サンプルのダウンロードに含まれています。

ミニドライバーは、 \_ フィルター処理ディスパッチで KSK PROCESSPIN indexentry 構造体の配列を受け取ります。 この例では、ミニドライバーは、index VIDEO PIN ID の KSPROCESSPIN indexentry 構造から最初の KSK PROCESSPIN 構造体を抽出し \_ \_ \_ ます。

```cpp
NTSTATUS
CCaptureFilter::
Process (
    IN PKSPROCESSPIN_INDEXENTRY ProcessPinsIndex
    )
{
PKSPROCESSPIN VideoPin = NULL;
...
VideoPin = ProcessPinsIndex [VIDEO_PIN_ID].Pins [0];
...
}
```

ミニドライバーで**ProcessPinsIndex** n を参照することはできません \[ *n* \] 。**Pins** \[ \] **ProcessPinsIndex** n の**Count**メンバー \[ *n* \] が少なくとも1つあること、*または*ピン0に含まれる kspin 記述子 EX 構造体の**InstancesNecessary**メンバーが少なくとも1つあることを確認する前に、0をピン留め \_ \_ **Pins** \[ \] します。 (後者が true の場合、pin は存在することが保証されます)。

次に、フレームをキャプチャするピンを指定するために、 [*Avstrminifilterprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnksfilterprocess)コールバックルーチンは、 *CaptureFrame*へのポインター (ベンダが提供するキャプチャルーチン) を渡します。

```cpp
VidCapPin -> CaptureFrame (VideoPin, m_Tick);
```

その後、キャプチャルーチンは、KSK PROCESSPIN 構造体の**データ**メンバーとの間でコピーを行うことができます。 また、次の例に示すように、この構造体の**使用される bytesused**更新し、メンバーを**終了**する場合もあります。

```cpp
RtlCopyMemory ( ProcessPin -> Data,
                m_SynthesisBuffer,
                m_VideoInfoHeader -> bmiHeader.biSizeImage
               );
ProcessPin -> BytesUsed = m_VideoInfoHeader -> bmiHeader.biSizeImage;
ProcessPin -> Terminate = TRUE;
```

ミニドライバーは、現在のストリームポインターと pin に対応するストリームヘッダー構造体にもアクセスできます。

```cpp
PKSSTREAM_HEADER StreamHeader = ProcessPin -> StreamPointer -> StreamHeader;
```

フィルター中心の処理を使用するほとんどのミニドライバーでは、ストリームのヘッダーアクセスにのみストリームポインターを使用します。 フィルター中心のモデルでは、AVStream はストリームポインターを内部で操作します。 その結果、フィルター中心のドライバーでストリームポインターを操作する場合、ミニドライバーは注意を払って続行する必要があります。
