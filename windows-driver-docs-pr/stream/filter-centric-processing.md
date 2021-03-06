---
title: フィルター中心の処理
description: フィルター中心の処理
ms.assetid: e56c5102-7ea6-4687-ae5e-1550db9500f0
keywords:
- フィルターを中心としたフィルター WDK AVStream
- フィルターを中心とした AVStream WDK をフィルター処理します。
- WDK AVStream の種類をフィルターします。
- AVStrMiniFilterProcess
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1319eeb257a4cd95a05a4a500b52bc8b6c79ee5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384080"
---
# <a name="filter-centric-processing"></a>フィルター中心の処理





フィルターはフィルターを中心とした処理を使用する場合、既定 AVStream の呼び出しミニドライバーが指定した[ *AVStrMiniFilterProcess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnksfilterprocess)データ フレームは使用可能な各ピンの場合、コールバック ルーチンインスタンス。 ミニドライバーは、設定してこの既定の動作を変更することができます、**フラグ**のメンバー、 [ **KSPIN\_記述子\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex)構造体。

フィルターを中心とした処理を実装するミニドライバーが指定したへのポインターを提供[ *AVStrMiniFilterProcess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnksfilterprocess)コールバック ルーチンで、**プロセス**のメンバー[**KSFILTER\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksfilter_dispatch)構造体。 設定、**プロセス**のメンバー [ **KSPIN\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_dispatch)に**NULL**します。

AVStream 呼び出し[ *AVStrMiniFilterProcess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnksfilterprocess)満たされたはすべて、次の条件のときにのみ。

-   フレームの処理を実行フレームを必要とするピンで利用できます。 ミニドライバーはフラグを設定して処理の動作を変更することができます、**フラグ**のメンバー [ **KSPIN\_記述子\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex)します。 KSPIN 相互に排他的なフラグの組み合わせに特に注意してください\_フラグ\_フレーム\_いない\_REQUIRED\_の\_処理と KSPIN\_フラグ\_いくつか\_フレーム\_REQUIRED\_の\_処理します。 使用してフレームを必要とするピンのセットを変更することも、ミニドライバー、 [ **KsPinAttachAndGate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kspinattachandgate)または[ **KsPinAttachOrGate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kspinattachorgate)ルーチン。

-   暗証番号 (pin) のインスタンスの数以上になるは、 **InstancesNecessary**のメンバー、 [ **KSPIN\_記述子\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex)構造体。 **ClientState**のメンバー、 [ **KSPIN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin)構造体の指定、特に[ **KSSTATE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ne-ks-ksstate)pin の現在のセットを列挙子。 後**InstancesNecessary**のピンを満たす、追加された、 **KSSTATE\_停止**状態はフィルター処理を防ぐことはできません。

-   必要な暗証番号 (pin) のインスタンス数に達した (で指定されたとおり、 **InstancesNecessary**のメンバー、 [ **KSPIN\_記述子\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex)構造体。

-   ミニドライバーを使用して、フィルターのプロセス制御ゲートを終了していない、**KSGATE * * * Xxx*関数。

[ *AVStrMiniFilterProcess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnksfilterprocess)コールバック ルーチンの配列へのポインターを受け取る、ミニドライバー [ **KSPROCESSPIN\_索引**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksprocesspin_indexentry)構造体。 AVStream KSPROCESSPIN の配列を並べ替えます\_暗証番号 (pin) の ID で索引構造体

次のコード例では、ピン留めのプロセス構造体を使用する方法を示します。 コードから取得されますが、 [AVStream フィルターを中心としたシミュレートされたキャプチャ ドライバー (Avssamp)](https://go.microsoft.com/fwlink/p/?linkid=256084)サンプルについては、キャプチャ フィルターを中心としたドライバーを作成する方法を示します。 Windows Driver Kit のサンプルのダウンロードには、ソース コードと、このサンプルの説明が含まれます。

KSPROCESSPIN の配列を受け取るようにミニドライバー\_索引の構造体のフィルターでは、ディスパッチを処理します。 この例で、ミニドライバーは、KSPROCESSPIN から最初の KSPROCESSPIN 構造体を抽出\_インデックス ビデオの索引構造\_PIN\_ID:

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

ミニドライバーは参照しないでください**ProcessPinsIndex** \[ *n*\].**ピン** \[0\]が確認される前に、**カウント**のメンバー **ProcessPinsIndex** \[ *n*\]が 1 つ以上*または*を**InstancesNecessary** 、KSPIN のメンバー\_記述子\_EX内に含まれる構造体**ピン** \[0\]は少なくとも 1 つです。 (後者が true の場合、pin 確実に存在します。)

その、フレームをキャプチャする pin を指定するために、 [ *AVStrMiniFilterProcess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnksfilterprocess)コールバック ルーチン KSPROCESSPIN 構造体へのポインターを渡します*CaptureFrame*、キャプチャのベンダーから提供されたルーチン:

```cpp
VidCapPin -> CaptureFrame (VideoPin, m_Tick);
```

キャプチャ ルーチンをまたはからにコピーしてできます、**データ**KSPROCESSPIN 構造体のメンバー。 可能性がありますが、更新がも、 **BytesUsed**と**Terminate**次の例のように、この構造体のメンバー。

```cpp
RtlCopyMemory ( ProcessPin -> Data,
                m_SynthesisBuffer,
                m_VideoInfoHeader -> bmiHeader.biSizeImage
               );
ProcessPin -> BytesUsed = m_VideoInfoHeader -> bmiHeader.biSizeImage;
ProcessPin -> Terminate = TRUE;
```

ミニドライバーは、現在のストリーム ポインターと暗証番号 (pin) に対応するストリーム ヘッダー構造体をアクセスもできます。

```cpp
PKSSTREAM_HEADER StreamHeader = ProcessPin -> StreamPointer -> StreamHeader;
```

フィルターを中心とした処理を使用するほとんどのミニドライバーは、ヘッダーのストリーム アクセスに対してのみ、ストリーム ポインターを使用します。 フィルターを中心としたモデルでは AVStream ストリーム ポインターを内部的に操作します。 その結果、ミニドライバーは、ドライバーではフィルターを中心としたストリーム ポインターを操作する場合、注意が必要ですを続行する必要があります。
