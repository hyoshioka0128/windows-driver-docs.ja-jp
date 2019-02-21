---
title: プラグ アンド プレイ シリアル デバイス用のレジストリ設定
description: プラグ アンド プレイ シリアル デバイス用のレジストリ設定
ms.assetid: 57bd090a-20fe-41c6-b730-0479f6ae0982
keywords:
- シリアル ドライバー WDK、プラグ アンド プレイ デバイス
- プラグ アンド プレイ シリアル デバイス WDK
- シリアル デバイス WDK、プラグ アンド プレイ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e60723543d8165daf522242b232913250b8ea986
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557052"
---
# <a name="registry-settings-for-a-plug-and-play-serial-device"></a>プラグ アンド プレイ シリアル デバイス用のレジストリ設定





このトピックでは、プラグ アンド プレイ シリアル デバイスのシリアルが関数ドライバーとして使用するレジストリ設定について説明します。 これらの設定は、低レベル デバイス フィルター ドライバーとして 16550 UART と互換性のあるインターフェイスを必要とするデバイスのシリアルによっても使用します。

シリアルは、デバイスを追加するときに、これらのレジストリ エントリ値を照会します。 デバイスに固有のエントリの値が存在しない場合、シリアルはシリアル サービス値を使用します。

次のレジストリ設定は、デバイスのプラグ アンド プレイのレジストリ キーの下です。

<a href="" id="portname--reg-sz-"></a>**PortName** (REG\_SZ)  
デバイスの名前を指定します。 通常、デバイスの名前には COM<em>&lt;n&gt;、</em>場所*&lt;n&gt;* COM ポートの番号からインストーラーを取得するには、 [COMポート データベース](com-port-database.md)します。 ただし、デバイスは、NULL 以外の任意の文字列に設定できます。 として、デバイスが構成されている場合、 [COM ポート](configuration-of-com-ports.md)、シリアル ポート名を使用して、デバイスのシンボリック リンクの名前を作成します。 既定値**PortName**空の文字列します。

<a href="" id="identifier--reg-sz-"></a>**識別子**(REG\_SZ)  
デバイスの名前を指定します。 サポート、**識別子**エントリの値は一部のレガシ PCMCIA デバイスとの互換性を提供します。 使用**識別子**は廃止され、Microsoft Windows 2000 と以降のドライバーでは使用しない必要があります。 詳細については、次を参照してください。、 **PortName**エントリの値。

<a href="" id="multiportdevice--reg-dword-"></a>**MultiportDevice** (REG\_DWORD)  
シリアル ポートがマルチポート デバイス上のデバイスであるかどうかを示すブール型のフラグを指定します。 場合**MultiportDevice** 0x00000000、シリアル ポートがスタンドアロン デバイス; マルチポート デバイスのシリアル ポートは、それ以外の場合、します。 既定値**MultiportDevice** 0x00000000 します。

<a href="" id="portindex--reg-dword-"></a>**PortIndex** (REG\_DWORD)  
マルチポート デバイスのシリアル ポートのインデックス番号を指定します。 **インデックス**エントリの値は、ポートとは、ビットマップ、またはインデックス付きかどうかを指定します。 既定値**PortIndex** 0x00000000 します。

<a href="" id="clockrate--reg-dword-"></a>**ClockRate** (REG\_DWORD)  
UART のクロック速度を指定します。 既定値**ClockRate** 1,843,200 ヘルツです。

<a href="" id="indexed--reg-dword-"></a>**インデックス付き**(REG\_DWORD)  
マルチポート デバイスのポートがあるかどうかを示すブール フラグを指定します*ビットマップ*または*インデックス*します。 場合**インデックス**は、ポートのインデックスが 0 以外。 それ以外のポートはビットマップ。 **インデックス付き**と組み合わせて使用は、 **PortIndex**エントリの値。 既定値**インデックス**0x00000000 します。

<a href="" id="disableport--reg-dword-"></a>**DisablePort** (REG\_DWORD)  
デバイスを無効にするかどうかを指定するブール型のフラグ。 場合**DisablePort**が 0 以外の場合、デバイスはシリアルに無効には、それ以外の場合、デバイスを有効にします。 使用、 **DisablePort**エントリの値は廃止され、Windows 2000 およびそれ以降のドライバーでは使用しない必要があります。 Windows 2000 では、汎用的な手動メソッドを通じて、GUI のデバイス マネージャーを有効にし、デバイスを無効に提供します。 既定値**DisablePort** 0x00000000 します。 無効になっているデバイスにフラグを設定しないわけでは、デバイスが存在しないことに注意してください。 シリアルは、まだ無効になっているデバイスの存在を検出しようとします。 無効になっているように、デバイスが指定されて場合シリアルが状態を返します\_いいえ\_かかる\_デバイスへの応答、 **IRP\_MN\_開始\_デバイス**要求。 開始要求が失敗した後、プラグ アンド プレイ マネージャは、削除要求を送信します。

<a href="" id="forcefifoenable--reg-dword-"></a>**ForceFifoEnable** (REG\_DWORD)  
Fifo を使用するシリアルを強制するかどうかを示すブール フラグを指定します。 場合**ForceFifoEnable**が 0 以外の場合、Fifo を使用するシリアルが Fifo の存在を検出するかどうかに関係なく。 それ以外の場合、Fifo は、シリアルが検出できる場合にのみ使用します。 既定値**ForceFifoEnable**シリアル サービスの設定値です。 (シリアル サービスの既定値は、0x00000001 です)。

<a href="" id="rxfifo--reg-dword-"></a>**RxFIFO** (REG\_DWORD)  
シリアル ポートの割り込みをトリガーする FIFO の受信バイト数を指定します。 有効な値は、Serial.h ヘッダー ファイルで定義されている定数を参照してください、[シリアル ドライバーのサンプル](https://go.microsoft.com/fwlink/p/?LinkId=617962)GitHub でします。 既定値**RxFIFO**シリアル サービスの設定値です。 (シリアル サービスの既定値は 8 バイトです)。

<a href="" id="txfifo--reg-dword-"></a>**TxFIFO** (REG\_DWORD)  
シリアル デバイス割り込みをトリガーする FIFO の送信バイト数を指定します。 有効な値は、Serial.h ヘッダー ファイルで定義されている定数を参照してください、[シリアル ドライバーのサンプル](https://go.microsoft.com/fwlink/p/?LinkId=617962)GitHub でします。 既定値**TxFIFO**シリアル サービスの設定値です。 (シリアル サービスの既定値は、14 バイトです)。

<a href="" id="maskinverted--reg-dword-"></a>**MaskInverted** (REG\_DWORD)  
シリアル デバイスのハードウェア割り込み状態のレジスタの内容を反転するかどうかを示すブール フラグを指定します。 場合**MaskInverted** 0 以外の場合、割り込み状態のレジスタが反転されます。 それ以外の場合、割り込み状態レジスタではありませんが反転します。 既定値**MaskInverted** 0x00000000 します。

<a href="" id="serialskipexternalnaming--reg-dword-"></a>**SerialSkipExternalNaming** (REG\_DWORD)  
シリアルとしてデバイスを構成するかどうかを示すブール フラグを指定します、 [COM ポート](configuration-of-com-ports.md)します。 場合**SerialSkipExternalNaming**設定は、0x00000000 に、シリアルは COM ポートとして、デバイスを構成します。 それ以外の場合、シリアルがいないデバイスとして構成する COM ポート。 既定値**SerialSkipExternalNaming** 0x00000000 します。 COM ポートとして、シリアルがデバイスを構成する方法の詳細については、次を参照してください。[外部名前付けの COM ポート](external-naming-of-com-ports.md)します。

<a href="" id="serialrelinquishpowerpolicy--reg-dword-"></a>**SerialRelinquishPowerPolicy** (REG\_DWORD)  
シリアルがシリアル デバイス スタックの電源ポリシーの所有者であるかどうかを示すブール型のフラグを指定します。 場合**SerialRelinquishPowerPolicy**は 0、シリアル電源ポリシー所有者は、シリアルはいない電源ポリシーの所有者。 既定値**SerialRelinquishPowerPolicy** 0x00000000 します。

<a href="" id="share-system-interrupt--reg-dword-"></a>**システムの割り込みを共有**(REG\_DWORD)  
システムをデバイスで使用される割り込みの共有を許可するかどうかを指定するブール型のフラグ。 場合**共有システムの割り込み**が 0 以外の場合、割り込みを共有できます。 それ以外の場合、割り込みを共有することはできません。 既定値**共有システムの割り込み**設定された値には、 **PermitShare**シリアル サービスのエントリの値。 (の既定のサービス値**PermitShare** 0x00000000)。

<a href="" id="serialioresourcesindex--reg-dword-"></a>**SerialIoResourcesIndex** (REG\_DWORD)  
シリアルを使用してデバイスのシリアル レジスタの I/O のアドレスを決定するリソースの部分的な記述子のインデックスを指定します。 既定値**SerialIoResourceIndex** 0x00000000 します。

 

 




