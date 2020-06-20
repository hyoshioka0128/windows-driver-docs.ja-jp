---
title: ハードウェア コーデックの検証と認定
description: ハードウェアコーデックの検証と認定
ms.assetid: 8cf96aac-78ba-41f0-b9d0-48948f704262
keywords:
- ハードウェアコーデック WDK AVStream、検証
- ハードウェアコーデック WDK AVStream、認定
- ハードウェアコーデックによる WDK AVStream のサポート、検証と認定
ms.date: 06/19/2020
ms.localizationpriority: medium
ms.openlocfilehash: 2df745926afbe29a8f46f8004b24e35d0d17f9c0
ms.sourcegitcommit: baf3075858705d4c78d4ea4b0869bf6291bcb823
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2020
ms.locfileid: "85112132"
---
# <a name="validating-and-certifying-hardware-codecs"></a>ハードウェアコーデックの検証と認定

ベンダーが提供する AVStream ミニドライバーにハードウェアベースのコーデックサポートが含まれている場合、またはハードウェアをサポートするカスタムの MFT を実装している場合は、x.509 証明書チェーンを指定し、ドライバーの INF ファイルで値を指定して、ドライバーに KSPROPSETID OPMVideoOutput を実装する必要があります \_ 。

## <a name="obtaining-a-x509-certificate"></a>X.509 証明書の取得

ハードウェアによってサポートされるメディアファンデーション変換 (MFT) エンコーダーまたはデコーダーは、CodecMeritCertificationPolicy EKU (拡張キー使用法) 証明書の拡張機能を指定する有効な Microsoft 署名 x.509 証明書を提供する必要があります。 ハードウェアアクセラレータによるコーデックのライセンスを取得するには、PVP-OPM ライセンスプログラムに参加する必要があります。 ライセンス資料を要求するには、 [Windows Media License agreement](mailto://wmla@microsoft.com)エイリアスにお問い合わせください。

## <a name="specifying-merit"></a>指定 (昇給を)

INF ファイルの AddReg セクションで、DWORD 型の MFTMerit レジストリ値を設定します。

```INF
[myVideoDecoder.Reader.AddReg]
HKR,,CLSID,,%Proxy.CLSID%
HKR,,FriendlyName,,%shedVideoDecoder.Reader.FriendlyName%
HKR,,MFTMerit,0x00010001,7
```

## <a name="implementing-kspropsetid_opmvideooutput"></a>KSPROPSETID OPMVideoOutput の実装 \_

KSPROPSETID \_ OPMVideoOutput プロパティセットは、Windows 7 以降の Windows SDK に付属している*Ksopmapi*および*opmapi .h*ヘッダーファイルで公開されています。

プロパティセットとメソッドは、 *Ksopmapi*ファイルから抜粋した次のように定義されています。

```cpp
#ifdef DEFINE_GUIDSTRUCT
#define STATIC_KSPROPSETID_OPMVideoOutput \
0x6f414bb, 0xf43a, 0x4fe2, 0xa5, 0x66, 0x77, 0x4b, 0x4c, 0x81, 0xf0, 0xdb
DEFINE_GUIDSTRUCT("06F414BB-F43A-4fe2-A566-774B4C81F0DB", KSPROPSETID_OPMVideoOutput);
#define KSPROPSETID_OPMVideoOutput DEFINE_GUIDNAMED(KSPROPSETID_OPMVideoOutput)
#endif

typedef enum
{
    //  Output is OPM_RANDOM_NUMBER followed by certificate
    KSMETHOD_OPMVIDEOOUTPUT_STARTINITIALIZATION = 0,

    //  Input OPM_ENCRYPTED_INITIALIZATION_PARAMETERS
    //  Output OPM_STANDARD_INFORMATION
    KSMETHOD_OPMVIDEOOUTPUT_FINISHINITIALIZATION = 1,

    //  Input is OPM_GET_INFO_PARAMETERS, output is OPM_REQUESTED_INFORMATION
    //  Use KsMethod - both input and output in the buffer (not after the KSMETHOD structure)
    KSMETHOD_OPMVIDEOOUTPUT_GETINFORMATION = 2
} KSMETHOD_OPMVIDEOOUTPUT;
```

ユーザーモードコンポーネント \_ は、AVStream プロキシ MFT の**Iksk コントロール**インターフェイスを介して、kspropsetid OPMVideoOutput にアクセスします。 OPMVideoOutput メソッドハンドラールーチンの実装を示すコード例については、「[コーデックの有効性の検証](codec-merit-validation.md)」を参照してください。

OPM に関するドライバー固有の情報については、「 [Output Protection Manager のサポート](https://docs.microsoft.com/windows-hardware/drivers/display/supporting-output-protection-manager)」を参照してください。

OPM のアプリケーション固有の情報については、「 [Output Protection Manager の使用](https://docs.microsoft.com/windows/win32/medfound/using-output-protection-manager)」を参照してください。
