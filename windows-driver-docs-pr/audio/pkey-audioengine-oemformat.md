---
title: 鍵\_AudioEngine\_OEMFormat
description: 鍵\_AudioEngine\_OEMFormat
ms.assetid: a1587f46-1c21-4419-a1a4-81fe299c6871
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5630075da3329f76ac160e0fce24516755c31f8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572860"
---
# <a name="pkeyaudioengineoemformat"></a>鍵\_AudioEngine\_OEMFormat


Windows Vista 以降では、**鍵\_AudioEngine\_OEMFormat**プロパティのキーは、エンドポイントのオーディオ デバイスの既定のストリームの形式を識別します。 レンダリングとキャプチャの両方のデバイスでは、既定の形式があります。 グローバル オーディオ エンジンでは、デバイスの既定の形式を使用して、共有モードでの操作については、デバイスに接続します。 デバイスをインストールする INF ファイルでは、レジストリにデバイスの既定の形式を読み込みます。 ユーザーは、Windows のマルチ メディア コントロール パネル (Mmsys.cpl) 既定の形式を変更できます。 Windows XP および Windows の以前のバージョンはサポートされず、**鍵\_AudioEngine\_OEMFormat**プロパティのキー。

INF ファイルでは、そのデバイスの追加レジストリ セクションでは、エンドポイントのオーディオ デバイスの既定の形式を指定します。 INF の次の例では、レジストリにデバイスのエンドポイントの既定の形式をロードする追加レジストリ セクションを示します。

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

前の例は、Windows Driver Kit で Sysfx オーディオ サンプルでは、ファイル Sysfx.inf から取得されます。 この INF ファイルの文字列のセクションには、次の定義が含まれています。

```inf
PKEY_AudioEndpoint_ControlPanelProvider = "{1DA5D803-D492-4EDD-8C23-E0C0FFEE7F0E},1"
PKEY_AudioEndpoint_Association          = "{1DA5D803-D492-4EDD-8C23-E0C0FFEE7F0E},2"
PKEY_AudioEngine_OEMFormat              = "{E4870E26-3CC5-4CD2-BA46-CA0A9A70ED04},3"
```

前の例では、OEMSettingsOverride.AddReg の追加レジストリ セクションの名前が定義されている、 [ **AddReg** ](https://msdn.microsoft.com/library/windows/hardware/ff546320) Sysfx.inf でインターフェイスのインストール セクション ディレクティブ。 前の例はエンドポイント数が 0 のいくつかのプロパティを追加します (文字列で識別される"EP\\\\0")、デバイス インターフェイスのレジストリ エントリにします。 (デバイスのインターフェイスを表している場合、 [wave フィルター](https://msdn.microsoft.com/library/windows/hardware/ff538862)追加のエンドポイントは番号付き 1、2、およびでは、複数のエンドポイントを使用します)。インターフェイスのセクションではインストールの詳細については、次を参照してください。 [ **INF AddInterface ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546310)します。

アプリケーションが取得することで、プロパティにアクセスできます INF ファイルは、3 つのプロパティのキーを作成し、関連する値をレジストリに読み込まれるが後、 [IPropertyStore](https://msdn.microsoft.com/library/windows/hardware/ff536954)エンドポイント デバイスのインターフェイス。 ヘッダー ファイル、Windows sdk Mmdeviceapi.h には、次の 3 つのプロパティのキーの C と C++ の定義が含まれています。 IPropertyStore インターフェイスを取得する方法の詳細については、の説明を参照して、 [ **IMMDevice::OpenPropertyStore** ](https://msdn.microsoft.com/library/windows/desktop/dd371412) Windows SDK のドキュメント内のメソッド。

INF の例で、**鍵\_AudioEndpoint\_アソシエーション**プロパティのキーは、エンドポイント デバイス KS pin カテゴリ GUID を識別します。 **鍵\_AudioEndpoint\_ControlPanelProvider** Mmsys.cpl でエンドポイントのプロパティ ページに、プロパティ値を提供する COM インターフェイス オブジェクトのクラス GUID を識別するプロパティのキーデバイスです。 これらのプロパティのキーの詳細については、Windows SDK のドキュメントを参照してください。 KS の詳細については、カテゴリの Guid をピン留めは、「 [Pin Category プロパティ](https://msdn.microsoft.com/library/windows/hardware/ff537742)します。

前の INF 例では、プロパティの値に関連付けられている、**鍵\_AudioEngine\_OEMFormat**プロパティ キーは 48 バイト REG\_を含む、シリアル化されたバイナリ値表現、 [ **WAVEFORMATEX** ](https://msdn.microsoft.com/library/windows/hardware/ff538799)または[ **WAVEFORMATEXTENSIBLE** ](https://msdn.microsoft.com/library/windows/hardware/ff538802)形式を記述する構造体。 登録を計算する\_に関連付けるバイナリ データ値、**鍵\_AudioEngine\_OEMFormat**プロパティ キーを埋め込む、 **WAVEFORMATEX**または**WAVEFORMATEXTENSIBLE**構造体、 **PropVariant**構造体、およびシリアル化、 **PropVariant**構造を呼び出すことによって、 **StgSerializePropVariant**関数。 詳細については、 **PropVariant**構造と**StgSerializePropVariant**関数を Windows SDK のマニュアルを参照してください。

次のコード例は、REG を出力するコンソール アプリケーション\_INF の前の例に表示されるバイナリ データ。

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
    hr = StgSerializePropVariant(&amp;var, &amp;pVal, &amp;cb);
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

    PrintSerializedFormat(&amp;wfx.Format);
}
```

上記のコード サンプルのメイン関数を作成、 [ **WAVEFORMATEXTENSIBLE** ](https://msdn.microsoft.com/library/windows/hardware/ff538802)構造体を既定の形式について説明します。 作成する主な機能を変更することができます、 [ **WAVEFORMATEX** ](https://msdn.microsoft.com/library/windows/hardware/ff538799)または**WAVEFORMATEXTENSIBLE**エンドポイント デバイスの既定の形式を記述する構造体。

上記のコード例で PrintSerializedFormat 関数が形式に関する説明をシリアル化および REG としてシリアル化された形式の説明を出力します\_バイナリ データ。 関数によって生成された印刷出力をコピーして、INF ファイルに貼り付けます。

 

 





