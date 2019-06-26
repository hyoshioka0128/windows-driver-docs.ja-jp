---
title: 必須コマンド
description: 必須コマンド
ms.assetid: e4a82cc6-8031-4d67-bef8-1d73e2d98b6b
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dac9b0088f727953948194138b529f7e00a7deeb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376502"
---
# <a name="required-commands"></a>必須コマンド


## <span id="ddk_required_commands_si"></span><span id="DDK_REQUIRED_COMMANDS_SI"></span>


次の一連の必要なコマンドは、すべて microdriver で実装する必要があります。

<span id="CMD_GETCAPABILITIES"></span><span id="cmd_getcapabilities"></span>CMD\_GETCAPABILITIES  
ボタンのイベント情報を取得する WIA ベッド ドライバーによって呼び出されます。 3 つのメンバーの渡された[ **VAL** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamicro/ns-wiamicro-val)構造体を入力する必要があります: **lVal**ボタンの数に設定する必要があります**pGuid**イベントです Guid の配列に設定する必要があります。**ppButtonNames**に設定することができます必要に応じて、 **WCHAR** \*のように、ボタンを含む配列が同じ順序で名前**pGuid** (「ボタンのスキャン」または「Fax ボタン」など)。 場合**ppButtonNames**に設定されている**NULL**、WIA ベッドのドライバーが汎用ボタン名を作成します。 CMD への応答では、配列を割り当てることができる\_初期化、および CMD で解放\_非します。

<span id="CMD_INITIALIZE"></span><span id="cmd_initialize"></span>CMD\_初期化  
Microdriver を初期化し、有効な値に設定されたデバイスの I/O ハンドル WIA ベッド ドライバーによって呼び出されます。 このコマンドは、WIA サービス メソッドを呼び出すと、microdriver に送信されます[ **IWiaMiniDrv::drvInitializeWia** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia) WIA ベッド ドライバーにします。

WIA ベッドのドライバーが自動的に 1 つのデバイスの I/O ハンドルを作成し、配置、 **DeviceIOHandles**の渡された配列メンバー [ **SCANINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamicro/ns-wiamicro-_scaninfo)インデックス 0 位置にある構造体。 デバイスと通信する必要があるときに、microdriver はこのハンドルを使用する必要があります。 作成し、に格納されていることができますが、microdriver では、追加のデバイス ハンドル (たとえば、複数の一括 USB パイプを使用する場合など) を必要とする場合、 **DeviceIOHandles**配列の最大数が最大まで\_IO\_ハンドル。 WIA ベッド ドライバーでは、初期化中にそのハンドルが作成されるため、インデックス 0 位置にあるハンドルは自動的に閉じます。 CMD への応答で microdriver によって他のハンドルを閉じる必要があります\_非します。

このコマンドの一部として、microdriver 初期化もすべての値の[ **SCANINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamicro/ns-wiamicro-_scaninfo)構造体。 Microdriver を設定する必要があります、 **SupportedDataTypes**、 **IntensityRange**、 **ContrastRange**、 **BedWidth**、および**BedHeight** WIA ベッドのドライバーがデバイスの有効な範囲に対してこれらの値を自動的に検証できるように、SCANINFO のメンバーが構造体します。

<span id="CMD_RESETSCANNER"></span><span id="cmd_resetscanner"></span>CMD\_RESETSCANNER  
WIA サービス要求への応答でデバイスをリセットする WIA ベッド ドライバーによって呼び出されます。 Microdriver は、電源オンの状態、デバイスを設定する必要があります。 Windows Vista では、WIA ベッド ドライバーはこのコマンドを使用しません。 ただし、microdrivers は、Windows xp の場合と、場合によってはこのコマンドを使用している WIA ベッド ドライバーの将来のバージョンで正常に動作させるのには、このコマンドをサポートするために続行する必要があります。

<span id="CMD_SETDATATYPE"></span><span id="cmd_setdatatype"></span>CMD\_SETDATATYPE  
スキャンのデータ型を設定する WIA ベッド ドライバーによって呼び出されます。 渡される値は次のいずれか、 **lVal**の渡されたメンバー [ **VAL** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamicro/ns-wiamicro-val)構造体。

WIA\_データ\_しきい値 − 1 ビット黒と白

WIA\_データ\_グレースケール − 8 ビットのグレースケール

WIA\_データ\_− 24 ビット カラー

値を格納する必要があります、microdriver、**データ型**の渡されたメンバー [ **SCANINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamicro/ns-wiamicro-_scaninfo)構造体。

<span id="CMD_SETCONTRAST"></span><span id="cmd_setcontrast"></span>CMD\_SETCONTRAST  
スキャンのコントラスト値を設定する WIA ベッド ドライバーによって呼び出されます。 目的のコントラスト値が渡された、 **lVal**の渡されたメンバー [ **VAL** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamicro/ns-wiamicro-val)構造体。 値 −1000 必要があります、デバイスのコントラストが最大最小のコントラスト値、標準、および 1000 0 として解釈されます。 値を格納する必要があります、microdriver、**コントラスト**の渡されたメンバー [ **SCANINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamicro/ns-wiamicro-_scaninfo)構造体。

<span id="CMD_SETINTENSITY"></span><span id="cmd_setintensity"></span>CMD\_SETINTENSITY  
輝度またはスキャンの明るさの値を設定する WIA ベッド ドライバーによって呼び出されます。 目的の輝度値が渡された、 **lVal**の渡されたメンバー [ **VAL** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamicro/ns-wiamicro-val)構造体。 値 −1000 必要があります、デバイスの最大輝度に最も低い明るさの値、標準、および 1000 0 として解釈されます。 値を格納する必要があります、microdriver、**強度**、渡されたのメンバー [ **SCANINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamicro/ns-wiamicro-_scaninfo)構造体。

<span id="CMD_SETXRESOLUTION"></span><span id="cmd_setxresolution"></span>CMD\_SETXRESOLUTION  
スキャンの水平方向の解像度を設定、WIA ベッド ドライバーによって呼び出されます。 ピクセル単位で目的の解像度が渡された、 **lVal**の渡されたメンバー [ **VAL** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamicro/ns-wiamicro-val)構造体。 値を格納する必要があります、microdriver、 **XResolution**の渡されたメンバー [ **SCANINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamicro/ns-wiamicro-_scaninfo)構造体。

<span id="CMD_SETYRESOLUTION"></span><span id="cmd_setyresolution"></span>CMD\_SETYRESOLUTION  
スキャンの垂直方向の解像度を設定、WIA ベッド ドライバーによって呼び出されます。 ピクセル単位で目的の解像度が渡された、 **lVal**渡された VAL 構造体のメンバー。 値を格納する必要があります、microdriver、 **YResolution**渡された SCANINFO 構造体のメンバー。

<span id="CMD_STI_DEVICERESET"></span><span id="cmd_sti_devicereset"></span>CMD\_STI\_DEVICERESET  
まだイメージ (STI) 要求に対する応答でデバイスをリセットする WIA ベッド ドライバーによって呼び出されます。 通常、このコマンドは、初期化中に 1 回だけ呼び出されます。

<span id="CMD_STI_DIAGNOSTIC"></span><span id="cmd_sti_diagnostic"></span>CMD\_STI\_診断  
ユーザーがデバイスのテストを要求したときに、WIA ベッド ドライバーによって呼び出されます。

<span id="CMD_UNINITIALIZE"></span><span id="cmd_uninitialize"></span>CMD\_非  
Microdriver の初期化を解除し、デバイスの I/O ハンドルを閉じます。 デバイス I/O ハンドルを自動的に閉じますが、WIA ベッド ドライバー、 **DeviceIOHandles**の配列のメンバー、 [ **SCANINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamicro/ns-wiamicro-_scaninfo)インデックス 0、構造体。 このコマンドは、WIA ベッド ドライバーをアンロードするときに、microdriver に送信されます。

 

 





