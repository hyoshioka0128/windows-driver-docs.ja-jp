---
title: ピア サブユニット ドライバー スタック
description: ピア サブユニット ドライバー スタック
ms.assetid: 6ef4b6ae-3802-4ba9-acfa-4b3edba11ba3
keywords:
- ピアサブユニットドライバースタック WDK AV/C
- ドライバースタック WDK AV/C
- スタック WDK AV/C
- サブユニットは WDK AV/C をサポートします
- AV/C WDK、ドライバースタック
- 単体コマンド WDK AV/C
- 組み込みの拡張メカニズム WDK AV/C
- コマンド拡張機能のメカニズム WDK AV/C
- コマンドターゲット WDK AV/C
- Avc 関数ドライバー WDK、ドライバースタック
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19bea615f87d4e6fcd5145c3d898540f395bee51
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823781"
---
# <a name="peer-subunit-driver-stack"></a>ピア サブユニット ドライバー スタック


ピアドライバースタックは、IEEE 1394 バス上でアクティブであり、コンピューターから制御できる AV/C サブユニットを表すために読み込まれたドライバーで構成されます。 外部デバイスコントロールは、AV/C ピアドライバースタックを介して開始する必要があります。 Windows は、デバイスがシステムに接続されている (またはシステムの起動時に存在する) たびに、IEEE 1394 バス上の外部 AV/C デバイスごとに*Avc*のインスタンスを読み込みます。 ピアサブシステムドライバーをサポートするために読み込まれる*avc*の各インスタンスでは、GUID の新しいインスタンス\_AVC\_クラスのデバイスインターフェイスに登録されます。 \_AVC\_クラスデバイスインターフェイスの GUID の詳細については、「avc および[**IOCTL\_avc\_クラス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_class)の[使用](using-avc-sys.md)」を参照してください。

ピアサブシステムドライバーは、サブユニットによってエクスポートされる IOCTL\_AVC\_クラスインターフェイスを介して、それらのデバイスにアクセスして制御*します。* *Avc*は、AV/C コマンドと応答プロトコルを処理します。これには、IEC 61883 関数制御プロトコル (FCP) とのすべてのやり取りが含まれます。 ただし、ピアサブシステムドライバーは、必要に応じて、特定の*61883*の機能と通信したり、直接アクセスしたりすることができないことに注意してください。 サブシステムドライバーが、Microsoft がサポートしていないストリーム形式を使用する AV/C サブユニットを表している場合、サブ*システム*ドライバーは、直接のデバイスとの通信を必要とすることがあります。 サブユニットドライバーは、必要に応じて、 **IOCTL\_61883\_クラス**インターフェイスを使用して、 *61883*と直接通信できます。 Microsoft では、DV および MPEG2 形式のストリーミングをサポートする低フィルタードライバー *Avcstrm .sys*を提供しています。 *Avcstrm .sys*の詳細については、「 [AV/C Streaming の概要](av-c-streaming-overview.md)」を参照してください。

ピアサブユニットドライバーは、外部の AV/C デバイスからの通知を受け取り、AV/C コマンドを受信するように登録できます。 登録するには、ピアサブユニットドライバーが[ **\_内部\_デバイス\_制御**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)i/o 要求パケット (irp) を\_発行します。これには、IOCTL\_AVC\_クラス i/o 制御コードと MJ の**iocontrolcode**メンバーが含まれます。subfunction を AVC\_関数に設定すると、\_要求\_取得されます。 この機能により、ピアサブユニットドライバーはサブユニットから AV/C 要求を受信し、接続と互換性の管理 (CCM) プロトコルやデジタル伝送 Content Protection (DTCP) などの仕様のサポートを有効にすることができます。 CCM の詳細については、「 [IEEE 1394 取引の関連付け](https://go.microsoft.com/fwlink/p/?LinkId=518448)」 web サイトを参照してください。 DTCP の詳細については、[デジタル伝送ライセンス管理者](https://go.microsoft.com/fwlink/p/?linkid=8731)web サイトを参照してください。

この機能は、仮想 AV/c サブシステムドライバーをサポートして、コンピューター (サブシステムドライバーが仮想 AV/C デバイススタックに配置されている) に AV/c コマンドを送信することを目的としています。また、外部デバイスの AV/c サブユニットが av/c コマンドをコンピューターシステム。

### <a href="" id="peer-stack-as-av-c-command-target"></a>**AV/C コマンドターゲットとしてのピアスタック**

ピアサブユニットドライバースタックには、ベンダー固有またはデバイス固有のターゲット AV/C 機能を提供する追加の WDM フィルタードライバーを含めることができます。 このピアサブユニットドライバースタック拡張メカニズムを使用すると、サードパーティベンダーは、5C コピー防止などの付加価値機能、および Microsoft が提供する AV/C 実装の拡張機能を個別に実装できます。

サブユニットドライバーはこの機能を実行できますが、複数のサブユニットを持つデバイスの場合は、WDM フィルタードライバーを使用することをお勧めします。 コンピューターが AV/C ターゲットとして公開されるのは、上位ドライバー (サブユニットまたはフィルタードライバー) が、 [**AVC\_関数**](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-get-request)を使用して受信要求を受信するように登録されている場合\_\_要求を取得する場合のみです。 AV/C ユニットコマンドの詳細については、「 [**AVC\_関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)」を参照してください。

ドライバーの読み込みは、デバイス識別子 (Id) に基づいています。そのため、ユニットの機能は、デバイス固有またはベンダー固有の単位で選択的に読み込むことができます。 仮想サブユニットドライバースタックでは、このメカニズムが一般的にサポートされています (デバイス固有の方法ではありません)。

ピアサブモジュールドライバースタックがデバイス固有のユニット拡張を実装している場合は、すべての未処理のユニットコマンドと、すべての受信サブユニットコマンドが仮想サブモジュール[ドライバースタック](virtual-subunit-driver-stack.md)にルーティングされることに注意してください。

### <a name="unit-command-extension-mechanism"></a>**Unit コマンド拡張機能のメカニズム**

ピアサブユニットドライバースタックのコンテキストでは、ターゲット機能は AV/C ユニットコマンドのサポートに限定されます。 サブシステムドライバー (仮想サブユニットまたはピアサブユニット用) が AV/C 要求を受信するように登録されている場合、 *Avc*は、サブユニット\_情報 (0x31) と UNIT\_INFO (0x30) オペコードのみを直接サポートします。 オペコードの詳細については、「 *AV/C Digital Interface Command Set General Specification, Rev 3.0*」を参照してください。 CCM プロトコルや DTCP などの追加の単位コマンドをサポートするために、 *Avc*はプラグイン拡張機構を提供します。 任意の数のサブユニットまたは WDM フィルタードライバーは、avc\_関数を介して送信された[**avc\_コマンド\_IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_command_irb)構造体の**alternateopcodes**メンバーを介して、サポートする単体オペコードを登録でき[ **\_GET\_REQUEST**](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-get-request)関数。 **Alternateopcodes**は、カウントされたバイト配列です。要素0は、残りのバイトの代替オペコードの数です。 応答の送信時に**Alternateopcodes**は無視されるため、単体要求を処理するときに代替オペコードを非表示にする必要はありません。

組み込みの拡張メカニズムを使用するには、AVC\_\_コマンドの**Subunitaddress**メンバーで、IRB 構造体の単位アドレスを0xff として指定します。 **Subunitaddress**メンバーは、単位コマンドに対してだけで残されています (サブユニットドライバーによって提供されるユニットアドレスはまだ存在しています)。 仮想サブユニットドライバーは、常に**Subunitaddress**メンバーからキーを切ることができます。

 

 




