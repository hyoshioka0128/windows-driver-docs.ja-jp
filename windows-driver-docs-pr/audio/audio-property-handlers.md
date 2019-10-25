---
title: オーディオのプロパティのハンドラー
description: オーディオのプロパティのハンドラー
ms.assetid: 4bf176ae-b3fd-47e6-9802-a92ef5e9904f
keywords:
- オーディオプロパティ WDK、ハンドラー
- WDM オーディオプロパティ WDK、ハンドラー
- WDK のオーディオをハンドラする
- プロパティハンドラー WDK audio
- set プロパティ WDK audio
- get プロパティ WDK audio
- basic-サポートクエリ WDK オーディオ
- automation テーブル WDK オーディオ
- WDK オーディオ、プロパティハンドラーをフィルター処理します
- WDK オーディオ、プロパティハンドラーをピン留めする
- ノード WDK オーディオ、プロパティハンドラー
ms.date: 08/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: bd5c5ea8c8945f4ef1dd15d2d594ac6b21995c47
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831332"
---
# <a name="audio-property-handlers"></a>オーディオのプロパティのハンドラー


## <span id="audio_property_handlers"></span><span id="AUDIO_PROPERTY_HANDLERS"></span>


ミニポートドライバーは、 [**pcproperty\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcproperty_item)構造体でサポートされている各プロパティに関する情報を格納します。 この構造体には、プロパティに関する次の情報が含まれています。

-   プロパティセット GUID とプロパティ ID (またはインデックス)

-   プロパティのハンドラールーチンへの関数ポインター

-   ハンドラーがサポートするプロパティ操作を指定するフラグ

ミニポートドライバーは、フィルターのために ( [**Pcautomation\_テーブル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcautomation_table)構造によって指定される) オートメーションテーブルを提供します。 ドライバーは、フィルターのピンの種類とノードの種類に対して追加のオートメーションテーブルを提供します。各ピンまたはノードの種類には独自のテーブルがあります。 各オートメーションテーブルには、PCPROPERTY\_項目構造の (空の場合もありますが) 配列が含まれます。これらの各構造体は、フィルター、ピン、またはノードの1つのプロパティを表します。 クライアントがプロパティ要求をフィルター、ピン、またはノードに送信すると、ポートドライバーは、その要求をオートメーションテーブルを介して適切なプロパティハンドラーにルーティングします。

ミニポートドライバーでは、各プロパティに対して一意のプロパティハンドラールーチンを指定できます。 ただし、ドライバーがいくつかの類似したプロパティを処理する場合は、便宜上、1つのハンドラールーチンに統合することもできます。 各プロパティに対して一意のハンドラーを提供するか、複数のプロパティを1つのハンドラーに統合するかは、ドライバーライターによって決定され、プロパティ要求を送信するクライアントに対して透過的である必要があります。

ユーザーモードのクライアントは、 *Dwiocontrolcode*呼び出しパラメーターを IOCTL\_KS\_property に設定して Microsoft Win32 関数[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)を呼び出すことによって、get、set、または basic サポートプロパティ要求を送信できます。 オペレーティングシステムは、この呼び出しを IRP に変換します。この[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)はクラスドライバーにディスパッチされます。 詳細については、「 [KS のプロパティ](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-properties)」を参照してください。

クライアントが KS プロパティ要求 (つまり、IOCTL\_KS\_プロパティ i/o 制御 IRP) をフィルターハンドルまたはピンハンドルに送信すると、KS システムドライバー (Ks) は、フィルターオブジェクトまたはピンオブジェクトのポートドライバーに要求を配信します。 ミニポートドライバーがプロパティのハンドラーを提供する場合、ポートドライバーはハンドラーに要求を転送します。 要求を転送する前に、ポートドライバーは、プロパティ要求の情報を[**pcproperty\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-_pcproperty_request)構造によって指定された形式に変換します。 ポートドライバーは、この構造体をミニポートドライバーのハンドラーに渡します。

PCPROPERTY\_要求の**MajorTarget**メンバーは、オーディオデバイスのプライマリミニポートドライバーインターフェイスをポイントします。 たとえば、WavePci デバイスの場合、これはミニポートドライバーオブジェクトの[IMiniportWavePci](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavepci)インターフェイスへのポインターです。

フィルターハンドルに送信される KS プロパティ要求の場合、PCPROPERTY\_要求の**Minortarget**メンバーは**NULL**になります。 ピンハンドルに要求が送信された場合、 **Minortarget**はピンのストリームインターフェイスをポイントします。 たとえば、WavePci デバイスの場合、これはストリームオブジェクトの[IMiniportWavePciStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavepcistream)インターフェイスへのポインターです。

PCPROPERTY\_の**インスタンス**と**値**のメンバーは、それぞれ KS プロパティ要求の入力バッファーと出力バッファーを参照します。 (バッファーは、 [**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)関数の*lpinbuffer*パラメーターと*lpoutbuffer*パラメーターによって指定されます)。これらのバッファーには、プロパティ記述子 (インスタンスデータ) とプロパティ値 (操作データ) がそれぞれ含まれています。詳細については、「[オーディオドライバーのプロパティセット](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-drivers-property-sets)」を参照してください。 **値**のメンバーは出力バッファーの先頭を指しますが、**インスタンス**ポインターは入力バッファーの先頭からのオフセットです。

入力バッファーは、 [**Ksk プロパティ**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))または[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)構造体のいずれかで始まります。 ポートドライバーは、この構造の情報を PCPROPERTY\_要求構造体の**Node**、 **propertyitem**、および**Verb**メンバーにコピーします。 データが、バッファー内の KSK プロパティまたは KSNODEPROPERTY 構造体の後に続く場合、ポートドライバーは、このデータへのポインターを使用して**インスタンス**メンバーを読み込みます。 それ以外の場合は、**インスタンス**を**NULL**に設定します。

入力バッファーが、ノード情報を含まない KSK プロパティ構造で始まる場合、ポートドライバーは PCPROPERTY\_要求構造の**ノード**メンバーを ULONG (-1) に設定します。 この場合、ポートドライバーは、プロパティ要求のターゲットがフィルターハンドルまたはピンハンドルによって指定されているかどうかに応じて、フィルターまたはピンのミニポートドライバーのオートメーションテーブルから適切なハンドラーを呼び出します。 (テーブルでプロパティのハンドラーが指定されていない場合、ポートドライバーは代わりに要求を処理します)。

入力バッファーが KSNODEPROPERTY 構造体で始まる場合、ポートドライバーは、この構造体から PCPROPERTY\_要求構造体の**ノード**メンバーにノード ID をコピーし、ミニポートドライバーのオートメーションから適切なハンドラーを呼び出します。ノードのテーブルです。 (この場合も、テーブルでプロパティのハンドラーが指定されていない場合は、ポートドライバーによって要求が処理されます)。

ポートドライバーは、プロパティ要求の操作フラグに\_トポロジビット\_型を確認し、次の2つの構造体 (KSK プロパティまたは KSNODEPROPERTY) が入力バッファーの先頭に存在するかどうかを判断します。

-   このビットが設定されている場合、要求はノードプロパティ用であり、入力バッファーは KSNODEPROPERTY 構造体で始まります。

-   それ以外の場合、入力バッファーは KSK プロパティ構造で始まります。

KSK プロパティ\_型\_トポロジの詳細については、「 [**Ksk プロパティ**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))」を参照してください。

PCPROPERTY\_要求構造体の**InstanceSize**および**valuesize**メンバーは、**インスタンス**と**値**のメンバーが指すバッファーのサイズを指定します。 **Valuesize**は、プロパティ要求の出力バッファーのサイズと同じですが、 **InstanceSize**は、入力バッファーの KSK プロパティまたは KSNODEPROPERTY 構造に従うデータのサイズです。 つまり、 **InstanceSize**は、入力バッファーのサイズから ksk プロパティまたは KSNODEPROPERTY 構造体のサイズを差し引いたものです。 この構造体の後にデータが追加されていない場合、ポートドライバーは**InstanceSize**をゼロ (および**インスタンス**から**NULL**) に設定します。

たとえば、クライアントが[**KSNODEPROPERTY\_AUDIO\_CHANNEL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)構造体を入力バッファーのインスタンスデータとして指定した場合、ポートドライバーは、その**インスタンス**メンバーを持つ pcproperty\_要求構造体を渡します。KSNODEPROPERTY\_AUDIO\_CHANNEL 構造体の**チャネル**メンバーを指し、その**InstanceSize**メンバーに値が含まれています。

**sizeof**(KSNODEPROPERTY\_AUDIO\_CHANNEL)- **sizeof**(KSNODEPROPERTY)

プロパティ値を取得するために get property 要求を送信する前に、クライアントは、ミニポートドライバーのプロパティハンドラーがプロパティ値を書き込むことができる出力バッファーを割り当てる必要があります。 一部のプロパティでは、出力バッファーのサイズはデバイスに依存し、クライアントはプロパティハンドラーに必要なバッファーサイズを照会する必要があります。 このような場合、クライアントは、出力バッファーポインターが nullptr で出力バッファーの長さが0である初期プロパティ要求を送信します。 ハンドラーは、必要なバッファーサイズと状態コード STATUS_BUFFER_OVERFLOW を返すことによって応答します。 次に、クライアントは、指定されたサイズの出力バッファーを割り当て、2番目の get プロパティ要求でこのバッファーを送信することによって、プロパティ値を取得します。
 
指定されたバッファーサイズが小さすぎて要求された情報を取得できない場合、メソッドは STATUS_BUFFER_TOO_SMALL を返します。 
 
場合によっては、PortCls port ドライバーが、出力バッファーのアドレスとサイズが0以外のプロパティ要求に応答して、STATUS_BUFFER_OVERFLOW ではなく STATUS_BUFFER_TOO_SMALL を返します。 このような場合、必要なバッファーサイズは返されません。 
 
詳細については、次を参照してください。 NTSTATUS 値とこれらのブログ投稿[を使用](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-ntstatus-values)します。

- [後続の操作に必要なバイト数を返す方法](https://blogs.msdn.microsoft.com/doronh/2006/12/12/how-to-return-the-number-of-bytes-required-for-a-subsequent-operation/)

- [STATUS_BUFFER_OVERFLOW は、STATUS_BUFFER_OVERFLOW_PREVENTED という名前にする必要があります。](https://devblogs.microsoft.com/oldnewthing/?p=22863)




 

 




