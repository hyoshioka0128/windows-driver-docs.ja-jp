---
title: ファースト ステップ ガイド - Microsoft 標準のドライバーの 3D プリンター
description: Microsoft の標準のドライバーの 3D プリンターでは、Windows 10 と互換性のある自社のプリンターを簡単に作成できます。
ms.assetid: DAFC5B26-09BA-483C-B964-1DA96E77765F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0faefc875791e74ed3e8c8b6498a046a58640d2f
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57463808"
---
# <a name="getting-started-guide---microsoft-standard-driver-for-3d-printers"></a>ファースト ステップ ガイド - Microsoft 標準のドライバーの 3D プリンター


Microsoft の標準のドライバーの 3D プリンターでは、Windows 10 と互換性のある自社のプリンターを簡単に作成できます。 Microsoft OS ディスクリプターを使用するすべてのプリンターは、互換性のある 3D プリンターとして認識できます。 具体的な例を使用して、この記事では、デバイスの Windows 10 での 3D プリンターとして認識され、その印刷機能を通信しているファームウェアを作成する方法を説明します。

## <a name="introduction"></a>概要


Microsoft 標準のドライバーでは、希望する Windows 10 と互換性がある 3D プリンターは、独立系ハードウェア ベンダー (Ihv) から独自のドライバーの書き込みの負担を軽減します。 Microsoft OS ディスクリプターを認識している Windows のバージョンでは、に対する制御要求を使用して、情報を取得し、それを使用して、インストールして、ユーザーの介入を必要とせずにデバイスを構成します。

Windows 10 での作業 3 D プリンターを取得する一般的なプロセスには、次の手順が含まれています。

1.  **互換性のある ID**します。 独立系ハードウェア ベンダー (IHV) は、プリンターのファームウェアで「3D 印刷」互換性 ID を含める必要があります。 これにより、3 D プリンターとして認識されるデバイスです。

2.  **標準のドライバー**します。 は、デバイスが接続されていると Windows 更新プログラムが 3D 印刷標準のドライバーをダウンロードし、既定の構成を使用する 3D プリンターとして現在のデバイスを検出します。

3.  **拡張プロパティの記述子**します。 3D プリンターのいくつかの基本構成が可能な標準のドライバーの一部として。 開発者は自社の 3D プリンターに一致する基本構成を選択したがってできます。 基本構成を選択すると、上に、開発者は自社の 3D プリンターより適切な一致するプロパティの一部をオーバーライドし、新しいファームウェアに含めることがことができます。

4.  **プラグ アンド プレイ**します。 ファームウェアの 3D のプリンターのフラッシュ メモリに書き込み時に、ユーザーは、Windows 10 コンピューターに接続するたびと標準のドライバーが自動的にダウンロードするは、開発者が選択したカスタム印刷機能を使用します。

次のセクションでの具体的な例を使用して各手順を表していますが。

詳細については、次を参照してください。 [Microsoft OS ディスクリプター](https://go.microsoft.com/fwlink/p/?LinkId=533944)します。

## <a name="compatible-id"></a>互換性 ID


現在使用されている 3D プリンターを Windows オペレーティング システムを指定するに右互換性 ID を使用する必要は Microsoft 互換性 ID の一覧については、「 [Microsoft OS ディスクリプター](https://go.microsoft.com/fwlink/p/?LinkId=533944)します。

3D プリンターの互換性のある ID が次の表に表示されます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>互換性 ID</th>
<th>下位互換性のある ID</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>"3DPRINT"</p>
<p>(0x33 0x44 0x50 0x52 0x49 0x4E 0x54 0x00)</p></td>
<td><p>不定</p></td>
<td><p>MS3DPRINT G コード プリンター</p></td>
</tr>
</tbody>
</table>

 

3D プリンターのファームウェアに含まれているヘッダー ファイルで次に示すよう、IHV が互換性のある ID を指定する必要があります。

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

上記のコードでは、この行は、3 D プリンターの互換性のある ID を示します。

`'3', 'D', 'P', 'R', 'I', 'N', 'T', 0x00,         // compatibleID ("3DPRINT")`

この特定の構成では、Ihv はファームウェアをコンパイルし、デバイスをフラッシュします。 デバイスが接続された場合、3 D の標準の印刷ドライバーが Windows Update から自動的にダウンロードを取得します。

この段階で、プリンターは標準のドライバーの既定の構成を使用して、既定の構成で使用されるパラメーターは %systemroot% フォルダーでアクセスできる\\System32\\MS3DPrint StandardGCode.xml ファイル。 さらに、開発者が別の基本構成を使用することができます、基本構成の一覧と同じフォルダーの %SYSTEMROOT% で使用できる\\System32\\MS3DPrint します。 この一覧は定期的にこの新しい 3D プリンターが市場に登場にも、新しい構成で格納されます。

## <a name="extended-properties-os-feature-descriptor"></a>OS 機能記述子のプロパティの拡張


前のセクションで説明したように、Ihv はいくつかの基本構成へのアクセスがあります。 これにより、プリンターのフラッシュ メモリに格納される情報の量を最小限に抑えることの利点があります。 開発者は、使用できる基本構成を検査し、自分のプリンターに最も近いものを選択できます。 この例では、SD カードの基本構成を選択し、以下のパラメーターのプロパティの一部をオーバーライドするいきます。

| パラメーター            | 値  |
|-----------------------|--------|
| Job3DOutputAreaWidth  | 250000 |
| Job3DOutputAreaDepth  | 260000 |
| Job3DOutputAreaHeight | 270000 |
| Filamentdiameter      | 2850   |

 

これらのパラメーターの詳細についてを参照してください、 *MS3DPrint Standard G コード Driver.docx*に文書化、 [3D 印刷 SDK](https://go.microsoft.com/fwlink/p/?LinkId=394375)ドキュメント。

基本構成を使用して上書きするパラメーターを指定するには、開発者は、次に示すように拡張プロパティの OS 機能記述子を指定するが。

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

OS の拡張プロパティの機能の記述子に関する情報は、 *OS\_Desc\_Ext\_Prop.doc*ファイル。 参照してください[Microsoft OS ディスクリプター](https://go.microsoft.com/fwlink/p/?LinkId=533944)詳細についてはします。

## <a name="verifying-the-print-capabilities"></a>印刷機能を確認しています


デバイスがファームウェアをフラッシュ メモリに書き込むと、Windows 10 では、デバイスが自動的に検出して、印刷機能は、レジストリに格納されます。

![プレリリースの 3d プリンターをインストールします。 ](images/installing-compatible-3d-printer.png)

IHV が独自にデバイスの VID/PID を変更する非常に重要です。 オペレーティング システムでは、VID と PID よりも優先 OS 記述子とデバイスが正しく検出できません、仕入先 ID (VID) または既存のデバイスを別の製品 ID (PID) を使用しないでください必要があります。

デバイスがで表示される場合は、デバイスが正しくインストールされて**デバイスとプリンター**します。

![「デバイスとプリンター」](images/devices-and-printers-3d.png)

**デバイス マネージャー**、一致するデバイス id と互換性のある id を検証できます。

![デバイス マネージャー](images/device-manager-3d.png)

![デバイス マネージャーの詳細 タブ - デバイス id に一致します。](images/device-manager-details-3d.png)

![デバイス マネージャーの詳細 タブ - 互換性 id](images/device-manager-details2-3d.png)

USB ドライバーのプロパティでレジストリにアクセスして取得できます**HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\Enum\\USB**.

![usb のレジストリでの複数行文字列値を編集します。](images/usb-registry-3d.png)

3D 印刷ドライバーのプロパティでレジストリにアクセスして取得できます**HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\の印刷\\プリンター**します。

![レジストリの 3d 印刷ドライバーのプロパティを表示します。](images/printers-registry-3d.png)

## <a name="additional-resources"></a>その他の技術情報


詳細については、次のドキュメントとリソースを参照してください。

[Windows での 3D 印刷](https://go.microsoft.com/fwlink/p/?LinkId=534206)

[3D 印刷 SDK (MSI のダウンロード)](https://go.microsoft.com/fwlink/p/?LinkId=394375)

[Microsoft OS ディスクリプター](https://go.microsoft.com/fwlink/p/?LinkId=533944)

[USB 2.0 仕様](https://go.microsoft.com/fwlink/p/?linkid=533945)

Microsoft 3D 印刷チームに連絡することもできます[3D 印刷に関する質問をしたり](https://go.microsoft.com/fwlink/p/?LinkId=534751)(ask3dprint@microsoft.com)。

 

 




