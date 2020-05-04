---
title: PnP シリアル デバイス用のレジストリ設定
description: PnP シリアル デバイス用のレジストリ設定
ms.assetid: 57bd090a-20fe-41c6-b730-0479f6ae0982
keywords:
- Serial driver WDK、プラグアンドプレイデバイス
- プラグアンドプレイシリアルデバイス WDK
- シリアルデバイス WDK、プラグアンドプレイ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ccaee2b5098c67d149060a57a2d4eeafe1e9d09c
ms.sourcegitcommit: 6b09412f7bf562f7c01ffa94ac44a3d0ea895e3c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "82086722"
---
# <a name="registry-settings-for-a-plug-and-play-serial-device"></a>PnP シリアル デバイス用のレジストリ設定





このトピックでは、シリアルでプラグアンドプレイシリアルデバイスの関数ドライバーとして使用されるレジストリ設定について説明します。 また、シリアルは、16550 UART 互換インターフェイスを必要とするデバイスの下位レベルのデバイスフィルタードライバーとして、これらの設定を使用します。

シリアルは、デバイスを追加するときにこれらのレジストリエントリの値を照会します。 デバイス固有のエントリ値が存在しない場合、Serial はシリアルサービス値を使用します。

次のレジストリ設定は、デバイスのプラグアンドプレイレジストリキーの下にあります。

<a href="" id="portname--reg-sz-"></a>**PortName** (REG\_SZ)  
デバイスの名前を指定します。 通常、デバイスの名前は com<em>&lt;n&gt;</em>です。ここ* &lt;で&gt; 、n*は、インストーラーが[com ポートデータベース](com-port-database.md)から取得する com ポート番号です。 ただし、デバイスを NULL 以外の文字列に設定することはできます。 デバイスが[COM ポート](configuration-of-com-ports.md)として構成されている場合、シリアルはポート名を使用してデバイスのシンボリックリンク名を作成します。 **PortName**の既定値は空の文字列です。

<a href="" id="identifier--reg-sz-"></a>**識別子**(REG\_SZ)  
デバイスの名前を指定します。 **識別子**エントリ値のサポートは、一部のレガシ PCMCIA デバイスとの互換性のために用意されています。 **識別子**の使用は廃止されており、Microsoft Windows 2000 以降のドライバーでは使用できません。 説明については、 **PortName**エントリの値を参照してください。

<a href="" id="multiportdevice--reg-dword-"></a>**Multiportdevice** (REG\_DWORD)  
シリアルポートがマルチポートデバイス上のデバイスであるかどうかを示すブール型フラグを指定します。 **Multiportdevice**が0x00000000 の場合、シリアルポートはスタンドアロンデバイスです。それ以外の場合、シリアルポートはマルチポートデバイス上にあります。 **Multiportdevice**の既定値は0x00000000 です。

<a href="" id="portindex--reg-dword-"></a>**Portindex** (REG\_DWORD)  
マルチポートデバイスのシリアルポートのインデックス番号を指定します。 **インデックス付き**エントリの値は、ポートがビットマップ形式であるか、インデックスが作成されるかを指定します。 **Portindex**の既定値は0x00000000 です。

<a href="" id="clockrate--reg-dword-"></a>**Clockrate** (REG\_DWORD)  
UART のクロックレートを指定します。 **Clockrate**の既定値は1843200ヘルツです。

<a href="" id="indexed--reg-dword-"></a>**インデックス付き**(\_REG DWORD)  
マルチポートデバイスのポートに*ビットマップ*または*インデックス*を作成するかどうかを示すブール値フラグを指定します。 **インデックス**が0以外の場合、ポートのインデックスが作成されます。それ以外の場合、ポートはビットマップになります。 **インデックス**は、 **portindex**エントリ値と組み合わせて使用されます。 **インデックス**の既定値は0x00000000 です。

<a href="" id="disableport--reg-dword-"></a>**Disableport** (REG\_DWORD)  
デバイスを無効にするかどうかを指定するブール型のフラグ。 **Disableport**が0以外の場合、シリアルはデバイスを無効にします。それ以外の場合は、デバイスが有効になります。 **Disableport**エントリ値の使用は廃止されており、Windows 2000 以降のドライバーでは使用できません。 Windows 2000 では、デバイスを有効または無効にするためのデバイスマネージャーの GUI を使用して、汎用的な手動の方法を提供しています。 **Disableport**の既定値は0x00000000 です。 デバイスを無効としてフラグを設定しても、デバイスが存在しないということではないことに注意してください。 シリアルは、無効になっているデバイスの存在を検出しようとします。 デバイスが無効として指定されている\_場合\_、\_シリアルは、 **IRP\_\_\_** が発生したデバイスの開始要求に応答してそのようなデバイスがない状態を返します。 開始要求が失敗すると、プラグアンドプレイマネージャーが削除要求を送信します。

<a href="" id="forcefifoenable--reg-dword-"></a>**Forcefion enable** (REG\_DWORD)  
直列が Fifo を使用するように強制するかどうかを示すブール型のフラグを指定します。 **Forcefiが enable**が0以外の場合、直列が fifo の存在を検出できるかどうかに関係なく、fifo が使用されます。 それ以外の場合、Fifo は直列が検出できる場合にのみ使用されます。 **Forcefia enable**の既定値は、シリアルサービスに対して設定された値です。 (シリアルサービスの既定値は0x00000001 です)。

<a href="" id="rxfifo--reg-dword-"></a>**RxFIFO** (REG\_DWORD)  
シリアルポートの割り込みをトリガーする receive FIFO のバイト数を指定します。 有効な値については、GitHub の[シリアルドライバーサンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/serial/serial)で、serial .h ヘッダーファイルで定義されている定数を参照してください。 **RxFIFO**の既定値は、シリアルサービスに対して設定された値です。 (シリアルサービスの既定値は8バイトです)。

<a href="" id="txfifo--reg-dword-"></a>**Txfifo** (REG\_DWORD)  
シリアルデバイスの割り込みをトリガーする、転送 FIFO のバイト数を指定します。 有効な値については、GitHub の[シリアルドライバーサンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/serial/serial)で、serial .h ヘッダーファイルで定義されている定数を参照してください。 既定値の**Txfifo**は、シリアルサービスに対して設定された値です。 (シリアルサービスの既定値は14バイトです)。

<a href="" id="maskinverted--reg-dword-"></a>**MaskInverted** (REG\_DWORD)  
シリアルデバイスハードウェアが割り込みステータスレジスタの内容を反転するかどうかを示すブールフラグを指定します。 **MaskInverted**が0以外の場合、割り込みステータスレジスタは反転されます。それ以外の場合、割り込みステータスレジスタは反転されません。 **MaskInverted**の既定値は0x00000000 です。

<a href="" id="serialskipexternalnaming--reg-dword-"></a>**SerialSkipExternalNaming** (REG\_DWORD)  
シリアルによってデバイスが[COM ポート](configuration-of-com-ports.md)として構成されるかどうかを示すブール型のフラグを指定します。 **SerialSkipExternalNaming**が0x00000000 に設定されている場合、シリアルはデバイスを COM ポートとして構成します。それ以外の場合、シリアルはデバイスを COM ポートとして構成しません。 **SerialSkipExternalNaming**の既定値は0x00000000 です。 シリアルによってデバイスが COM ポートとして構成される方法の詳細については、「 [Com ポートの外部名前付け](external-naming-of-com-ports.md)」を参照してください。

<a href="" id="serialrelinquishpowerpolicy--reg-dword-"></a>**SerialRelinquishPowerPolicy** (REG\_DWORD)  
シリアルがシリアルデバイススタックの電源ポリシーの所有者であるかどうかを示すブール型のフラグを指定します。 **SerialRelinquishPowerPolicy**が0の場合、Serial は電源ポリシーの所有者です。それ以外の場合、Serial は電源ポリシーの所有者ではありません。 **SerialRelinquishPowerPolicy**の既定値は0x00000000 です。

<a href="" id="share-system-interrupt--reg-dword-"></a>**共有システム割り込み**(REG\_DWORD)  
デバイスが使用する割り込みをシステムが共有することを許可するかどうかを指定するブール型のフラグです。 **共有システムの割り込み**が0以外の場合は、割り込みを共有できます。それ以外の場合は、割り込みを共有できません。 **共有システム割り込み**の既定値は、シリアルサービスの**PermitShare**エントリ値に設定された値です。 ( **PermitShare**の既定のサービス値は0x00000000 です)。

<a href="" id="serialioresourcesindex--reg-dword-"></a>**SerialIoResourcesIndex** (REG\_DWORD)  
シリアル化によってデバイスのシリアルレジスタセットの i/o アドレスを決定するために使用される部分的なリソース記述子のインデックスを指定します。 **系列**の既定値は0x00000000 です。

 

 




