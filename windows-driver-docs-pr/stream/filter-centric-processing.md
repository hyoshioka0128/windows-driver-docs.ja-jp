---
title: フィルター中心の処理
description: フィルター中心の処理
ms.assetid: e56c5102-7ea6-4687-ae5e-1550db9500f0
keywords:
- フィルター中心のフィルター (WDK AVStream)
- AVStream フィルター中心フィルター WDK
- フィルターの種類 WDK AVStream
- AVStrMiniFilterProcess
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 940ba2221c0e175bd4fd2713c25498a8908fc58e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834401"
---
# <a name="filter-centric-processing"></a>フィルター中心の処理





フィルター中心の処理を使用するフィルターでは、各ピンインスタンスで使用できるデータフレームがあるときに、AVStream はミニドライバーが提供する[*Avstrminifilterprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnksfilterprocess)コールバックルーチンを呼び出します。 ミニドライバーは、 [**Kspin\_記述子\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)構造体の**Flags**メンバーを設定することによって、この既定の動作を変更できます。

フィルター中心の処理を実装するには、 [**Ksk フィルター\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_dispatch)構造体の**プロセス**メンバーで、ミニドライバーが提供する[*avstrminifilterprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnksfilterprocess)コールバックルーチンへのポインターを指定します。 [**Kspin\_DISPATCH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_dispatch)の**プロセス**メンバーを**NULL**に設定します。

AVStream は、次のすべての条件が満たされた場合にのみ[*Avstrminifilterprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnksfilterprocess)を呼び出します。

-   フレームは、処理のためにフレームを必要とするピンで使用できます。 ミニドライバーは、 [**Kspin\_記述子\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)の**flags**メンバーにフラグを設定することによって、処理動作を変更できます。 相互排他的なフラグ KSPIN\_\_フラグの組み合わせに特に注意する必要があります。\_の処理と KSPIN\_フラグ\_必要\_\_フレーム\_には\_必要 @no\_ではありません\_の処理には __ を使用します。 ミニドライバーは、 [**KsPinAttachAndGate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspinattachandgate)または[**KsPinAttachOrGate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspinattachorgate)ルーチンを使用してフレームを必要とする pin のセットを変更することもできます。

-   Pin インスタンスの数が、 [**Kspin\_記述子\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)構造体の**InstancesNecessary**メンバー以上です。 [**Kspin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin)構造体の**clientstate**メンバーは、pin が現在設定されている特定の[**ksstate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ne-ks-ksstate)列挙子を指定します。 **InstancesNecessary**が満たされた後は、 **KSK 状態\_停止**状態の追加の pin によってフィルター処理が妨げられることはありません。

-   必要な pin インスタンスの数が満たされています ( [**Kspin\_記述子\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)構造体の**InstancesNecessary**メンバーによって指定されています。

-   ミニドライバーは、**Ksgate * * * Xxx*関数を使用して、フィルターのプロセス制御ゲートを閉じていません。

[*Avstrminifilterprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnksfilterprocess)コールバックルーチンでは、ミニドライバーは、 [**ksprocesspin\_indexentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksprocesspin_indexentry)構造体の配列へのポインターを受け取ります。 AVStream では、KSK の配列をピン ID によって\_INDEXENTRY 構造体の順序で並べ替えます。

次のコード例は、プロセスのピン構造を使用する方法を示しています。 このコードは、フィルター中心のキャプチャドライバーを記述する方法を示す[Avstream フィルター中心のシミュレートされたキャプチャドライバー (Avssamp)](https://go.microsoft.com/fwlink/p/?linkid=256084)サンプルから取得されます。 このサンプルのソースコードと説明は、Windows Driver Kit サンプルのダウンロードに含まれています。

ミニドライバーは、フィルター処理ディスパッチで KSK PROCESSPIN\_INDEXENTRY 構造体の配列を受け取ります。 この例では、ミニドライバーは、index ビデオ\_PIN\_ID の ks\_PROCESSPIN 構造から最初の KSPROCESSPIN 構造体を抽出します。

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

ミニドライバーは、 **ProcessPinsIndex** \[*n*\]を参照することはできません。**ProcessPinsIndex** \[*n*\] の**Count**メンバーが少なくとも1つであること、*または*kspin の**InstancesNecessary**メンバーであることを確認する前に \[0\] を**ピン**留め\_記述子\_EX 構造体は、**ピン**内に含まれています \[0\] は少なくとも1つです。 (後者が true の場合、pin は存在することが保証されます)。

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
