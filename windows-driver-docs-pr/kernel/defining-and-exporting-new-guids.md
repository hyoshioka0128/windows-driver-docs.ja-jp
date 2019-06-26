---
title: 新しい GUID の定義とエクスポート
description: 新しい GUID の定義とエクスポート
ms.assetid: a7deb283-7cab-4f3c-ad96-f8085222456e
keywords:
- WDK のカーネルをグローバルに一意の識別子
- Guid の WDK カーネル
- WDK の Guid 識別子
- Guid をエクスポートします。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c43743ee92cc015deb36be6761ad8bdfad797f54
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377118"
---
# <a name="defining-and-exporting-new-guids"></a>新しい GUID の定義とエクスポート





ドライバーをエクスポートするその他のシステム コンポーネント、ドライバー、またはアプリケーションのアイテムの新しい GUID を定義します。 たとえば、そのデバイスの 1 つのカスタム PnP イベントの新しい GUID を定義します。 定義して、新しい GUID をエクスポートするには、次の操作を行う必要があります。

1.  GUID のシンボリック名を選択します。

    GUID の目的を表す名前を選択します。 GUID として、オペレーティング システムがこのような名前を使用するなど、\_BUS\_型\_PCI と PARPORT\_WMI\_ALLOCATE\_FREE\_カウント\_GUID。

2.  Uuidgen.exe または Guidgen.exe を使用して GUID の値を生成します。 Microsoft Windows SDK をインストールするときに Uuidgen.exe は自動的にインストールします。 Guidgen.exe はから利用可能な[Microsoft Exchange Server GUID ジェネレーター](https://go.microsoft.com/fwlink/p/?linkid=121586)ページをダウンロードします。

    これらのユーティリティは、128 ビット値を表す、書式設定された一意の文字列を生成します。 "-S"、GUID は、C 構造体として書式設定された Uuidgen.exe 出力をオンにします。

3.  適切なヘッダー ファイルで、GUID を定義します。

    使用して、**定義\_GUID**マクロに GUID のシンボリック名をその値に関連付ける (で定義されている Guiddef.h) (例 1 を参照してください)。

    **例 1:Guid を GUID 専用ヘッダー ファイルで定義します。**

    ```cpp
    :
     
    DEFINE_GUID( GUID_BUS_TYPE_PCMCIA, 0x09343630L, 0xaf9f, 0x11d0, 
        0x92,0x9f, 0x00, 0xc0, 0x4f, 0xc3, 0x40, 0xb1 );
    DEFINE_GUID( GUID_BUS_TYPE_PCI, 0xc8ebdfb0L, 0xb510, 0x11d0, 
        0x80,0xE9, 0x00, 0x00, 0xf8, 0x1e, 0x1b, 0x30 );
     
    :
    ```

    GUID は、GUID 定義以外のステートメントを含むヘッダー ファイルで定義されているが、ヘッダー ファイルをインクルードするドライバーに GUID がインスタンス化されることを確認するのには、追加手順が行う必要があります。 **定義\_GUID**以外は、いずれかのステートメントで発生する必要があります **\#ifdef**複数インクルードされないようにするステートメント。 それ以外の場合、ヘッダー ファイルがプリコンパイル済みヘッダーに含まれる場合、この GUID はヘッダー ファイルを使用するドライバー インスタンスされません。 混合ヘッダー ファイルのサンプルの GUID 定義の例 2 を参照してください。

    **例 2:混合ヘッダー ファイルの Guid を定義します。**

    ```cpp
    #ifndef _NTDDSER_    // this ex. is from a serial driver .h file
    #define _NTDDSER_
     
    :
    // Put other header file definitions here.
    :
     
    #endif  // _NTDDSER_
     
    #ifdef DEFINE_GUID   // Do not break compiles of drivers that 
                         // include this header but that do not
                         // want the GUIDs.
    //
    // Put GUID definitions outside of the multiple inclusion 
    // protection.
     
    DEFINE_GUID(GUID_CLASS_COMPORT, 0x86e0d1e0L, 0x8089, 0x11d0, 0x9c,
        0xe4, 0x08, 0x00, 0x3e, 0x30, 0x1f, 0x73);
     
    DEFINE_GUID (GUID_SERENUM_BUS_ENUMERATOR, 0x4D36E978, 0xE325, 
        0x11CE, 0xBF, 0xC1, 0x08, 0x00, 0x2B, 0xE1, 0x03, 0x18);
     
    :
    #endif  // DEFINE_GUID
    ```

    複数インクルードされないようにするステートメントの外側の GUID 定義を配置することは行われません、GUID の複数のインスタンス、ドライバーのため、**定義\_GUID** EXTERN として GUID を定義します。\_C 変数。 型が一致している限り、外部変数の複数の宣言は許可されます。

4.  新しい GUID を作成するときに[デバイス セットアップ クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)または[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)、次の規則が適用されます。
    -   デバイス セットアップ クラスとデバイスのインターフェイス クラスの両方を識別するためには、単一の GUID を使用しません。

    -   GUID に関連付けるシンボリック名を作成する場合は、次の規則を使用します。

        GUID の形式を使用して、デバイス セットアップ クラス\_DEVCLASS\_*XXX*します。

        デバイスのインターフェイス クラスの GUID の形式を使用して、\_DEVINTERFACE\_*XXX*します。

 

 




