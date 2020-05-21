---
title: ファーストステップガイド-Microsoft Standard Driver for 3D プリンター
description: Microsoft Standard Driver for 3D プリンターを使用すると、開発者は簡単にプリンターを Windows 10 と互換性があります。
ms.assetid: DAFC5B26-09BA-483C-B964-1DA96E77765F
ms.date: 05/18/2020
ms.localizationpriority: medium
ms.openlocfilehash: 1e0daf596f9417895fb604312ab61eea11d04293
ms.sourcegitcommit: 32f42241991d57032e5d39ee9f2a3ab4a66ae396
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/18/2020
ms.locfileid: "83553335"
---
# <a name="getting-started-guide---microsoft-standard-driver-for-3d-printers"></a>ファーストステップガイド-Microsoft Standard Driver for 3D プリンター

Microsoft Standard Driver for 3D プリンターを使用すると、開発者は簡単にプリンターを Windows 10 と互換性があります。 Microsoft OS 記述子を使用するすべてのプリンターは、互換性のある3D プリンターとして認識されます。 この記事では、具体的な例を使用して、デバイスを Windows 10 で3D プリンターとして認識し、印刷機能を通信できるようにするファームウェアを作成する方法について説明します。

## <a name="introduction"></a>はじめに

Microsoft 標準ドライバーは、3D プリンターに Windows 10 との互換性を持たせる独立系ハードウェアベンダー (Ihv) から独自のドライバーを作成する負担を軽減します。 Microsoft OS 記述子を認識している Windows のバージョンでは、制御要求を使用して情報を取得し、それを使用してユーザーの操作を必要とせずにデバイスをインストールおよび構成します。

Windows 10 で動作する3D プリンターを取得する一般的なプロセスには、次の手順が含まれます。

1. **互換性のある ID**。 独立系ハードウェアベンダー (IHV) は、プリンターのファームウェアに "3D 印刷" と互換性のある ID を含める必要があります。 これにより、デバイスを3D プリンターとして認識できるようになります。

2. **標準ドライバー**。 デバイスが接続されると、Windows Update は3D 印刷標準ドライバーをダウンロードし、現在のデバイスを、既定の構成を使用する3D プリンターとして検出します。

3. **拡張プロパティ記述子**。 3D プリンターのいくつかの基本構成は、標準ドライバーの一部として利用可能になります。 そのため、開発者は、3D プリンターに一致する基本構成を選択できます。 基本構成を選択した上で、開発者は、3D プリンターに一致するようにプロパティの一部をオーバーライドし、新しいファームウェアに含めることができます。

4. **プラグアンドプレイ**。 ファームウェアが3D プリンターのフラッシュメモリに書き込まれると、ユーザーが Windows 10 コンピューターに接続するたびに、標準ドライバーが自動的にダウンロードされ、開発者が選択したカスタム印刷機能が使用されます。

以下のセクションでは、具体的な例を使用して、これらの各手順について説明します。

詳細については、「 [MICROSOFT OS 記述子](https://docs.microsoft.com/previous-versions/gg463179(v=msdn.10))」を参照してください。

## <a name="compatible-id"></a>互換性 ID

現在3D プリンターを使用していることを Windows オペレーティングシステムに指定するには、適切な互換性 ID を使用する必要があります。 Microsoft 互換性 ID の一覧については、「 [MICROSOFT OS 記述子](https://docs.microsoft.com/previous-versions/gg463179(v=msdn.10))」を参照してください。

次の表に、3D プリンターの互換性のある ID を示します。

| 互換性 ID | 下位互換性 ID | Description |
| --- | --- | --- |
| "3DPRINT"<br><br>(0x33 0x44 0x50 0x52 0x44 0X44 0x52 0x00) | 不定 | MS3DPRINT G-コードプリンター |

3D プリンターファームウェアに含まれるヘッダーファイルでは、次に示すように、IHV は互換性のある ID を指定する必要があります。

```cpp
#define MS3DPRINT_CONFIG_SIZE 232

#define MS3DPRINT_OSP_SIZE (4+4+2+0x20+4+MS3DPRINT_CONFIG_SIZE)

#define MS3DPRINT_XPROP_SIZE (4+2+2+2+MS3DPRINT_OSP_SIZE)

#define SIZE_TO_DW(__size)                \
        ((uint32_t)__size) & 0xFF,        \
        (((uint32_t)__size)>>8) & 0xFF,   \
        (((uint32_t)__size)>>16) & 0xFF,  \
        (((uint32_t)__size)>>24) & 0xFF

// CompatibleID and SubCompatibleID
static const uint8_t PROGMEM ms3dprint_descriptor[40] = {
    0x28, 0x00, 0x00, 0x00,                          // dwLength
    0x00, 0x01,                                      // bcdVersion
    0x04, 0x00,                                      // wIndex
    0x01,                                            // bCount
    0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00,        // RESERVED
    0x00,                                            // bFirstInterfaceNumber
    0x01,                                            // RESERVED
    '3', 'D', 'P', 'R', 'I', 'N', 'T', 0x00,         // compatibleID ("3DPRINT")
                                                 // subCompatibleID
    0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00   /*        */  
,
    0x00, 0x00, 0x00, 0x00, 0x00, 0x00               // RESERVED
};
```

上記のコードの次の行は、3D プリンターの互換性のある ID です。

`'3', 'D', 'P', 'R', 'I', 'N', 'T', 0x00,         // compatibleID ("3DPRINT")`

この特定の構成では、Ihv はファームウェアをコンパイルし、デバイスをフラッシュできます。 その後、デバイスが接続されると、3D Print Standard ドライバーが Windows Update から自動的にダウンロードされます。

この段階で、プリンターは標準のドライバーの既定の構成を使用しています。既定の構成で使用されるパラメーターは、 \\ \\ ファイル StandardGCode .xml の% SYSTEMROOT% System32 MS3DPrint フォルダーでアクセスできます。 また、開発者は別の基本構成の使用を選択できます。基本構成の一覧は、同じフォルダー% SYSTEMROOT% \\ System32 \\ MS3DPrint にあります。 この一覧には、新しい3D プリンターが市場で登場すると、新しい構成が定期的に設定されます。

## <a name="extended-properties-os-feature-descriptor"></a>拡張プロパティ OS 機能記述子

前のセクションで説明したように、Ihv はいくつかの基本構成にアクセスできます。 これには、プリンターのフラッシュメモリに格納する必要がある情報の量を最小限に抑えるという利点があります。 開発者は、使用可能な基本構成を調査し、プリンターに最も近い基本構成を選択できます。 この例では、SD カードの基本構成を選択し、次のパラメーターを使用していくつかのプロパティをオーバーライドします。

| パラメーター | 値 |
| --- | --- |
| Job3DOutputAreaWidth | 250000 |
| Job3DOutputAreaDepth | 26万 |
| Job3DOutputAreaHeight | 27万 |
| Filamentdiameter | 2850 |

これらのパラメーターの詳細については、 [3D 印刷 SDK (MSI ダウンロード)](https://go.microsoft.com/fwlink/p/?LinkId=394375)のドキュメントの*MS3DPrint Standard G-コードドライバー .docx*ドキュメントを参照してください。

使用する基本構成とオーバーライドするパラメーターを指定するには、次に示すように、拡張プロパティの OS 機能記述子で開発者が指定する必要があります。

```cpp
// Modifiers to the base configuration
static const uint8_t PROGMEM ms3dprint_properties_descriptor[] = {
    SIZE_TO_DW(MS3DPRINT_XPROP_SIZE),                   // dwLength
    0x00, 0x01,                                         // bcdVersion
    0x05, 0x00,                                         // wIndex
    0x01, 0x00,                                         // wCount

    SIZE_TO_DW(MS3DPRINT_OSP_SIZE),                     // dwSize
    0x07, 0x00, 0x00, 0x00,                             // dwPropertyDataType  (1=REG_SZ, 4=REG_DWORD, 7=REG_MULTI_SZ)

    0x20, 0x00,                                         // wPropertyNameLength
    'M', 0x0, 'S', 0x0, '3', 0x0, 'D', 0x0,             // bPropertyName
    'P', 0x0, 'r', 0x0, 'i', 0x0, 'n', 0x0,
    't', 0x0, 'C', 0x0, 'o', 0x0, 'n', 0x0,
    'f', 0x0, 'i', 0x0, 'g', 0x0, 0x0, 0x0,

    SIZE_TO_DW(MS3DPRINT_CONFIG_SIZE),                  // dwPropertyDataLength

    // Data
    0x42, 0x00, 0x61, 0x00, 0x73, 0x00, 0x65, 0x00, 0x3D, 0x00, 0x53, 0x00, 0x44, 0x00, 0x00, 0x00,  /* Base=SD  */  
    0x4A, 0x00, 0x6F, 0x00, 0x62, 0x00, 0x33, 0x00, 0x44, 0x00, 0x4F, 0x00, 0x75, 0x00, 0x74, 0x00,  /* Job3DOut */  
    0x70, 0x00, 0x75, 0x00, 0x74, 0x00, 0x41, 0x00, 0x72, 0x00, 0x65, 0x00, 0x61, 0x00, 0x57, 0x00,  /* putAreaW */  
    0x69, 0x00, 0x64, 0x00, 0x74, 0x00, 0x68, 0x00, 0x3D, 0x00, 0x32, 0x00, 0x35, 0x00, 0x30, 0x00,  /* idth=250 */  
    0x30, 0x00, 0x30, 0x00, 0x30, 0x00, 0x00, 0x00, 0x4A, 0x00, 0x6F, 0x00, 0x62, 0x00, 0x33, 0x00,  /* 000 Job3 */  
    0x44, 0x00, 0x4F, 0x00, 0x75, 0x00, 0x74, 0x00, 0x70, 0x00, 0x75, 0x00, 0x74, 0x00, 0x41, 0x00,  /* DOutputA */  
    0x72, 0x00, 0x65, 0x00, 0x61, 0x00, 0x44, 0x00, 0x65, 0x00, 0x70, 0x00, 0x74, 0x00, 0x68, 0x00,  /* reaDepth */  
    0x3D, 0x00, 0x32, 0x00, 0x36, 0x00, 0x30, 0x00, 0x30, 0x00, 0x30, 0x00, 0x30, 0x00, 0x00, 0x00,  /* =260000  */  
    0x4A, 0x00, 0x6F, 0x00, 0x62, 0x00, 0x33, 0x00, 0x44, 0x00, 0x4F, 0x00, 0x75, 0x00, 0x74, 0x00,  /* Job3DOut */  
    0x70, 0x00, 0x75, 0x00, 0x74, 0x00, 0x41, 0x00, 0x72, 0x00, 0x65, 0x00, 0x61, 0x00, 0x48, 0x00,  /* putAreaH */  
    0x65, 0x00, 0x69, 0x00, 0x67, 0x00, 0x68, 0x00, 0x74, 0x00, 0x3D, 0x00, 0x32, 0x00, 0x37, 0x00,  /* eight=27 */  
    0x30, 0x00, 0x30, 0x00, 0x30, 0x00, 0x30, 0x00, 0x00, 0x00, 0x66, 0x00, 0x69, 0x00, 0x6C, 0x00,  /* 0000 fil */  
    0x61, 0x00, 0x6D, 0x00, 0x65, 0x00, 0x6E, 0x00, 0x74, 0x00, 0x64, 0x00, 0x69, 0x00, 0x61, 0x00,  /* amentdia */  
    0x6D, 0x00, 0x65, 0x00, 0x74, 0x00, 0x65, 0x00, 0x72, 0x00, 0x3D, 0x00, 0x32, 0x00, 0x38, 0x00,  /* meter=28 */  
    0x35, 0x00, 0x30, 0x00, 0x00, 0x00, 0x00, 0x00                                                   /* 50       */  
};
```

拡張プロパティの OS 機能記述子に関する情報は、 *os \_ Desc \_ Ext \_ Prop. doc*ファイルにあります。 詳細については、「 [MICROSOFT OS 記述子](https://docs.microsoft.com/previous-versions/gg463179(v=msdn.10))」を参照してください。

## <a name="verifying-the-print-capabilities"></a>印刷機能の確認

デバイスのファームウェアがフラッシュメモリに書き込まれると、デバイスは Windows 10 によって自動的に検出され、印刷機能はレジストリに格納されます。

![互換性3d プリンターをインストールしています ](images/installing-compatible-3d-printer.png)

IHV がデバイスの VID/PID を独自のものに変更することは非常に重要です。 オペレーティングシステムは、VID と PID が OS 記述子よりも優先されるため、デバイスを正しく検出できないため、別の既存のデバイスのベンダー ID (VID) または製品 ID (PID) は使用しないでください。

デバイスが正しくインストールされている場合は、[**デバイスとプリンター**] にデバイスが一覧表示されます。

![デバイスとプリンター](images/devices-and-printers-3d.png)

**デバイスマネージャー**では、一致するデバイス id と互換性のある id を確認できます。

![デバイスマネージャー](images/device-manager-3d.png)

![デバイスマネージャーの [詳細] タブ-一致するデバイス id](images/device-manager-details-3d.png)

![デバイスマネージャーの [詳細] タブ互換 id](images/device-manager-details2-3d.png)

USB ドライバーのプロパティを取得するには、 **HKEY \_ LOCAL \_ MACHINE \\ SYSTEM \\ CurrentControlSet \\ Enum \\ USB**でレジストリにアクセスします。

![usb レジストリの複数文字列値の編集](images/usb-registry-3d.png)

3D 印刷ドライバーのプロパティを取得するには、 **HKEY \_ LOCAL \_ MACHINE \\ SYSTEM \\ CurrentControlSet \\ Control \\ Print \\ Printers**でレジストリにアクセスします。

![レジストリで3d 印刷ドライバーのプロパティを表示する](images/printers-registry-3d.png)

## <a name="additional-resources"></a>その他の技術情報

詳細については、次のドキュメントとリソースを参照してください。

[Windows での 3D 印刷](https://www.microsoft.com/3d-print/windows-3d-printing)

[3D 印刷 SDK (MSI ダウンロード)](https://go.microsoft.com/fwlink/p/?LinkId=394375)

[Microsoft OS 記述子](https://docs.microsoft.com/previous-versions/gg463179(v=msdn.10))

[USB 2.0 仕様](https://www.usb.org/documents)

Microsoft 3D 印刷チーム () に問い合わせて、「 [3D 印刷に関する質問](https://go.microsoft.com/fwlink/p/?LinkId=534751)」 () にアクセスすることもでき ask3dprint@microsoft.com ます。
