---
title: PKEY\_AudioEngine\_OEMFormat
description: PKEY\_AudioEngine\_OEMFormat
ms.assetid: a1587f46-1c21-4419-a1a4-81fe299c6871
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d20c3384d555edb36f7274663beb2e3cd1e3a8d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832490"
---
# <a name="pkey_audioengine_oemformat"></a>PKEY\_AudioEngine\_OEMFormat


Windows Vista 以降では、 **PKEY\_AudioEngine\_OEMFormat**プロパティキーによって、オーディオエンドポイントデバイスの既定のストリーム形式が識別されます。 レンダリングとキャプチャの両方のデバイスには、既定の形式があります。 グローバルオーディオエンジンは、デバイスの既定の形式を使用して、共有モードの操作でデバイスに接続します。 デバイスをインストールする INF ファイルによって、デバイスの既定の形式がレジストリに読み込まれます。 ユーザーは、Windows のマルチメディアコントロールパネル (Mmsys. cpl) を使用して、既定の形式を変更できます。 Windows XP およびそれ以前のバージョンの Windows では、 **OEMFormat プロパティキー\_PKEY\_AudioEngine**はサポートされていません。

INF ファイルでは、そのデバイスの [レジストリの追加] セクションにオーディオエンドポイントデバイスの既定の形式を指定します。 次の INF の例は、エンドポイントデバイスの既定の形式をレジストリに読み込む、レジストリの追加セクションを示しています。

```inf
;;
;; Identify endpoint device as a set of speakers.
;; Set default format to 48-kHz, 16-bit stereo.
;; Add endpoint extension property page.
;;
[OEMSettingsOverride.AddReg]
HKR,"EP\\0", %PKEY_AudioEndpoint_Association%,,%KSNODETYPE_SPEAKER%
HKR,"EP\\0", %PKEY_AudioEngine_OEMFormat%, %REG_BINARY%, 41,00,00,00,28,00,00,00,
 FE,FF,02,00,80,BB,00,00,00,EE,02,00,04,00,10,00,16,00,10,00,03,00,00,00,01,00,
 00,00,00,00,10,00,80,00,00,AA,00,38,9B,71
HKR,"EP\\0", %PKEY_AudioEndpoint_ControlPanelProvider%,,%AUDIOENDPOINT_EXT_UI_CLSID
```

前の例は、Windows Driver Kit の Sysfx オーディオサンプルにある Sysfx ファイルから取得されています。 この INF ファイルの文字列セクションには、次の定義が含まれています。

```inf
PKEY_AudioEndpoint_ControlPanelProvider = "{1DA5D803-D492-4EDD-8C23-E0C0FFEE7F0E},1"
PKEY_AudioEndpoint_Association          = "{1DA5D803-D492-4EDD-8C23-E0C0FFEE7F0E},2"
PKEY_AudioEngine_OEMFormat              = "{E4870E26-3CC5-4CD2-BA46-CA0A9A70ED04},3"
```

前の例では、OEMSettingsOverride の AddReg セクションの名前は、 [**AddReg**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)ディレクティブによって定義されています。これは、sysfx のインターフェイスインストールセクションにあります。 前の例では、デバイスインターフェイスのレジストリエントリに、エンドポイント番号 0 (文字列 "EP\\\\0" によって識別される) のプロパティをいくつか追加しています。 (デバイスインターフェイスが複数のエンドポイントを持つ[wave フィルター](https://docs.microsoft.com/windows-hardware/drivers/audio/wave-filters)を表している場合、追加のエンドポイントには1、2などの番号が付けられます)。インターフェイスのインストールセクションの詳細については、「 [**INF AddInterface ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addinterface-directive)」を参照してください。

INF ファイルによって3つのプロパティキーが作成され、関連する値がレジストリに読み込まれると、アプリケーションはエンドポイントデバイスの[IPropertyStore](https://docs.microsoft.com/windows/desktop/api/propsys/nn-propsys-ipropertystore)インターフェイスを取得することによってプロパティにアクセスできるようになります。 Windows SDK のヘッダーファイル Mmdeviceapi .h には、3つC++のプロパティキーの C/定義が含まれています。 IPropertyStore インターフェイスの取得の詳細については、Windows SDK のドキュメントの[**IMMDevice:: OpenPropertyStore**](https://docs.microsoft.com/windows/desktop/api/mmdeviceapi/nf-mmdeviceapi-immdevice-openpropertystore)メソッドの説明を参照してください。

前の INF の例では、 **PKEY\_audioendpoint\_アソシエーション**プロパティキーによって、エンドポイントデバイスの KS PIN カテゴリ GUID が識別されます。 **PKEY\_audioendpoint\_controlobwi provider**プロパティキーは、エンドポイントデバイスの mmsys のプロパティページにプロパティ値を提供する COM インターフェイスオブジェクトのクラス GUID を識別します。 これらのプロパティキーの詳細については、Windows SDK のドキュメントを参照してください。 KS pin カテゴリ Guid の詳細については、「[ピンカテゴリのプロパティ](https://docs.microsoft.com/windows-hardware/drivers/audio/pin-category-property)」を参照してください。

前の INF の例では、 **PKEY\_AudioEngine\_OEMFormat**プロパティキーに関連付けられているプロパティ値は、シリアル化された[**WAVEFORMATEX**](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex)の表現を含む48バイトの REG\_バイナリ値です。形式を記述する[**WAVEFORMATEXTENSIBLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible)構造体。 **PKEY\_AudioEngine\_OEMFormat**プロパティキーに関連付ける REG\_バイナリデータ値を計算するには、 **propvariant**構造体に**WAVEFORMATEX**または**WAVEFORMATEXTENSIBLE**構造体を埋め込みます。およびは、 **StgSerializePropVariant**関数を呼び出すことによって、 **propvariant**構造体をシリアル化します。 **Propvariant**構造体と**StgSerializePropVariant**関数の詳細については、Windows SDK のドキュメントを参照してください。

次のコード例は、前の INF の例に示されている REG\_バイナリデータを出力するコンソールアプリケーションです。

```cpp
//
// Embed a WAVEFORMATEXTENSIBLE structure in a PropVariant
// container, and print the PropVariant structure as a
// serialized stream of bytes in REG_BINARY format.
//

#include <stdio.h>
#include <wtypes.h>
#include <propidl.h>
#include <propvarutil.h>
#include <mmreg.h>
#include <ks.h>
#include <ksmedia.h>

void PrintSerializedFormat(WAVEFORMATEX *pWfx)
{
    HRESULT hr;
    PROPVARIANT var;
    SERIALIZEDPROPERTYVALUE* pVal;
    ULONG cb;

    // Create a VT_BLOB from the WAVEFORMATEX structure.
    var.vt = VT_BLOB;
    var.blob.cbSize = sizeof(*pWfx) + pWfx->cbSize;
    var.blob.pBlobData = (BYTE*)pWfx;

    // Serialize the PROPVARIANT structure. The serialized byte stream
    // will eventually be written to the registry as REG_BINARY data.
    hr = StgSerializePropVariant(&var, &pVal, &cb);
    if (SUCCEEDED(hr))
    {
        // Write the binary data to stdout. Format the output so you can
        // copy and paste it directly into the INF file as REG_BINARY data.
        for (UINT i = 0; i < cb; i++)
        {
            BYTE b = ((BYTE*)pVal)[i];
            wprintf(L"%2.2X,", b);
        }

        wprintf(L"\n");
        CoTaskMemFree(pVal);
    }
}

//
// Use a WAVEFORMATEXTENSIBLE structure to specify the format
// for a 48-kHz, 16-bit, (2-channel) stereo audio stream.
//
void main()
{
    WAVEFORMATEXTENSIBLE wfx;

    wfx.Format.wFormatTag = WAVE_FORMAT_EXTENSIBLE;
    wfx.Format.nChannels = 2;
    wfx.Format.nSamplesPerSec = 48000;
    wfx.Format.nAvgBytesPerSec = 4*48000;
    wfx.Format.nBlockAlign = 4;
    wfx.Format.wBitsPerSample = 16;
    wfx.Format.cbSize = sizeof(WAVEFORMATEXTENSIBLE) - sizeof(WAVEFORMATEX);
    wfx.Samples.wValidBitsPerSample = 16;
    wfx.dwChannelMask = 3;
    wfx.SubFormat = KSDATAFORMAT_SUBTYPE_PCM;

    PrintSerializedFormat(&wfx.Format);
}
```

前のコード例の main 関数は、既定の書式を記述する[**WAVEFORMATEXTENSIBLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible)構造体を作成します。 Main 関数を変更して、エンドポイントデバイスの既定の形式を記述する[**WAVEFORMATEX**](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex)または**WAVEFORMATEXTENSIBLE**構造体を作成することができます。

前のコード例の PrintSerializedFormat 関数は、形式の説明をシリアル化し、シリアル化された形式の説明を REG\_バイナリデータとして出力します。 関数によって生成された出力をコピーして、INF ファイルに貼り付けることができます。

 

 





