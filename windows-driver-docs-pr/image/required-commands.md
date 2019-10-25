---
title: 必須コマンド
description: 必須コマンド
ms.assetid: e4a82cc6-8031-4d67-bef8-1d73e2d98b6b
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed52e4eb3779a0336cead613324cbd309cbd1e3a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840752"
---
# <a name="required-commands"></a>必須コマンド


## <span id="ddk_required_commands_si"></span><span id="DDK_REQUIRED_COMMANDS_SI"></span>


次の必要なコマンドセットは、すべてのマイクロドライバで実装する必要があります。

<span id="CMD_GETCAPABILITIES"></span><span id="cmd_getcapabilities"></span>CMD\_GETCAPABILITIES  
ボタンイベント情報を取得するために、WIA フラットドライバーによって呼び出されます。 渡された[**VAL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-val)構造体の3つのメンバーを入力する必要があります。 **lVal**には、ボタンの数を設定する必要があります。**Pguid**は、イベント guid の配列に設定する必要があります。必要に応じて、 **Ppbuttonnames**を、 **pguid**内の順序と同じ順序で、ボタン名を含む**WCHAR**\* 配列に設定できます ("スキャンボタン" や "Fax ボタン" など)。 **Ppbuttonnames**が**NULL**に設定されている場合、WIA フラットドライバーは汎用のボタン名を作成します。 配列は、CMD\_INITIALIZE に応答して割り当てることができ、CMD\_に初期化解除されます。

<span id="CMD_INITIALIZE"></span><span id="cmd_initialize"></span>CMD\_初期化  
マイクロドライバーを初期化し、デバイスの i/o ハンドルを有効な値に設定するために、WIA フラット化ドライバーによって呼び出されます。 このコマンドは、wia サービスが WIA フラットドライバーで[**IWiaMiniDrv::D rvinitializewia**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia)メソッドを呼び出すとマイクロドライバーに送信されます。

WIA フラット化ドライバーは、1つのデバイス i/o ハンドルを自動的に作成し、インデックス0で渡された[**Scaninfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-_scaninfo)構造体の**DeviceIOHandles** array メンバーに格納します。 マイクロドライバは、デバイスと通信する必要がある場合に、このハンドルを使用する必要があります。 マイクロドライバが追加のデバイスハンドルを必要とする場合 (たとえば、複数の一括 USB パイプを使用する場合など) は、 **DeviceIOHandles**配列に作成して格納し、最大\_IO\_ハンドルの最大数まで増やすことができます。 WIA フラット化ドライバーは、初期化中にハンドルを作成したので、インデックス0のハンドルを自動的に閉じます。 他のハンドルは、CMD\_初期化解除に応答して、マイクロドライバーによって閉じられる必要があります。

このコマンドの一部として、microdriver は、 [**Scaninfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-_scaninfo)構造体のすべての値を初期化する必要もあります。 Microdriver は、SCANINFO 構造体の**Supporteddatatypes 型**、 **IntensityRange**、 **ContrastRange**、 **BedWidth**、 **BedHeight**のメンバーを設定する必要があります。これにより、WIA フラット化ドライバーでこれらのメンバーが自動的に検証されるようになります。デバイスの有効範囲に対する値。

<span id="CMD_RESETSCANNER"></span><span id="cmd_resetscanner"></span>CMD\_RESETSCANNER  
Wia フラットドライバーによって呼び出され、WIA サービス要求への応答としてデバイスをリセットします。 マイクロドライバは、デバイスの電源オン状態を設定する必要があります。 Windows Vista では、WIA フラットドライバーはこのコマンドを使用しません。 ただし、このコマンドを使用する可能性のある WIA フラットドライバーの将来のバージョンでは、Windows XP と、場合によっては適切な操作を行うために、マイクロドライバは引き続きこのコマンドをサポートする必要があります。

<span id="CMD_SETDATATYPE"></span><span id="cmd_setdatatype"></span>CMD\_SETDATATYPE  
スキャンのデータ型を設定するために、WIA フラットドライブによって呼び出されます。 次のいずれかの値が渡された[**VAL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-val)構造体の**lVal**メンバーで渡されます。

WIA\_データ\_しきい値−1ビット黒/白

WIA\_データ\_グレースケール-8 ビットグレースケール

WIA\_DATA\_COLOR −24ビットカラー

マイクロドライバは、渡された[**Scaninfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-_scaninfo)構造体の**DataType**メンバーに値を格納する必要があります。

<span id="CMD_SETCONTRAST"></span><span id="cmd_setcontrast"></span>CMD\_SETCONTRAST  
スキャンのコントラスト値を設定するために、WIA フラットドライブによって呼び出されます。 目的のコントラスト値は、渡された[**VAL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-val)構造体の**lVal**メンバーに渡されます。 値−1000は、最も低いコントラスト値、0公称、および1000デバイスの最大コントラストとして解釈される必要があります。 マイクロドライバは、渡された[**Scaninfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-_scaninfo)構造体の**Contrast**メンバーに値を格納する必要があります。

<span id="CMD_SETINTENSITY"></span><span id="cmd_setintensity"></span>CMD\_SETINTENSITY  
スキャンの輝度または明るさの値を設定するために、WIA フラットドライブによって呼び出されます。 必要な輝度値は、渡された[**VAL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-val)構造体の**lVal**メンバーに渡されます。 値−1000は、最低輝度値、0公称、および1000デバイスの最大明度として解釈される必要があります。 マイクロドライバーは、渡された[**Scaninfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-_scaninfo)構造体の**輝度**メンバーに値を格納する必要があります。

<span id="CMD_SETXRESOLUTION"></span><span id="cmd_setxresolution"></span>CMD\_SETXRESOLUTION  
水平スキャン解像度を設定するために、WIA フラットドライブによって呼び出されます。 必要な解像度 (ピクセル単位) は、渡された[**VAL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-val)構造体の**lVal**メンバーに渡されます。 マイクロドライバは、渡された[**Scaninfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-_scaninfo)構造体の**xresolution**メンバに値を格納する必要があります。

<span id="CMD_SETYRESOLUTION"></span><span id="cmd_setyresolution"></span>CMD\_SETYRESOLUTION  
垂直スキャン解像度を設定するために、WIA フラットドライブによって呼び出されます。 必要な解像度 (ピクセル単位) は、渡された VAL 構造体の**lVal**メンバーに渡されます。 マイクロドライバーは、渡された SCANINFO 構造体の**Yresolution**メンバーに値を格納する必要があります。

<span id="CMD_STI_DEVICERESET"></span><span id="cmd_sti_devicereset"></span>CMD\_STI\_DEVICERESET  
静止画像 (STI) 要求に応じてデバイスをリセットするために、WIA フラットドライブによって呼び出されます。 このコマンドは、通常、初期化中に1回だけ呼び出されます。

<span id="CMD_STI_DIAGNOSTIC"></span><span id="cmd_sti_diagnostic"></span>CMD\_の STI\_診断  
ユーザーがデバイスのテストを要求したときに、WIA フラットドライブによって呼び出されます。

<span id="CMD_UNINITIALIZE"></span><span id="cmd_uninitialize"></span>CMD\_初期化解除  
マイクロドライバを初期化解除し、デバイスの i/o ハンドルを閉じます。 WIA フラット化ドライバーは、インデックス0で、 [**Scaninfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-_scaninfo)構造体の**DeviceIOHandles** array メンバー内のデバイスの i/o ハンドルを自動的に閉じます。 このコマンドは、WIA フラットドライバーがアンロードされるときにマイクロドライバーに送信されます。

 

 





