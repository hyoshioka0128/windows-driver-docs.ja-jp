---
title: ハードウェア コーデックの検証と認定
description: ハードウェア コーデックの検証と認定
ms.assetid: 8cf96aac-78ba-41f0-b9d0-48948f704262
keywords:
- ハードウェア コーデック WDK AVStream、検証しています
- ハードウェア コーデック WDK AVStream、認定
- ハードウェアのコーデック サポート WDK AVStream、検証と認定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 679ba0e2cb5db52f0834cb430bcb1339f0c71c4c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337813"
---
# <a name="validating-and-certifying-hardware-codecs"></a>ハードウェア コーデックの検証と認定


AVStream、ベンダーから提供されたようにミニドライバーには、コーデックのハードウェア ベースのサポートが含まれています。 または、ハードウェアをサポートするカスタム MFT を実装している、する必要があります、X.509 証明書チェーンを指定、ドライバーの INF ファイルで merit 値を指定および実装 KSPROPSETID\_OPMVideoOutput ドライバー。

### <a name="obtaining-an-x509-certificate"></a>**X.509 証明書を取得します。**

Media Foundation の変換 (MFT) エンコーダーまたはデコーダー ハードウェアによってサポートされる必要があります、Microsoft によって署名された有効な X.509 証明書を提供 CodecMeritCertificationPolicy EKU (拡張キー使用法) の証明書の拡張機能を指定します。 ハードウェアの高速化されたコーデックのライセンスを取得するには、PVP OPM ライセンス プログラムに参加する必要があります。 ライセンスの資料を要求するお問い合わせください、 [Windows メディアの使用許諾契約書](mailto://wmla@microsoft.com)エイリアス。

### <a name="specifying-merit"></a>**価値を指定します。**

INF ファイルの [AddReg] セクションでは、MFTMerit を DWORD に型指定されたレジストリ値を設定します。

```INF
[myVideoDecoder.Reader.AddReg]
HKR,,CLSID,,%Proxy.CLSID%
HKR,,FriendlyName,,%shedVideoDecoder.Reader.FriendlyName%
HKR,,MFTMerit,0x00010001,7
```

### <a name="implementing-kspropsetidopmvideooutput"></a>**KSPROPSETID を実装する\_OPMVideoOutput**

KSPROPSETID\_で OPMVideoOutput プロパティ セットが公開される、 *Ksopmapi.h*と*Opmapi.h*ヘッダー ファイルは、Windows 7 用 Windows SDK 以降に付属います。

プロパティ セットとメソッドが次からの抜粋で定義されている、 *Ksopmapi.h*ファイル。

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

ユーザー モード コンポーネント アクセス KSPROPSETID\_を通じて OPMVideoOutput、 **IKsControl** AVStream プロキシ MFT 上のインターフェイス。 ハンドラー ルーチン OPMVideoOutput メソッドの実装を示すコード例では、次を参照してください。[コーデック Merit 検証](codec-merit-validation.md)です。

ドライバー固有 OPM については、次を参照してください。[出力 Protection Manager をサポートしている](https://msdn.microsoft.com/library/windows/hardware/ff569879)します。 OPM の特定のアプリケーションについては、次を参照してください。[出力 Protection Manager を使用した](https://go.microsoft.com/fwlink/p/?linkid=155059)します。
